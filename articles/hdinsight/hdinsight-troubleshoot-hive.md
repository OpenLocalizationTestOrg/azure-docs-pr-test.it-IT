---
title: Risolvere i problemi di Hive tramite Azure HDInsight | Microsoft Docs
description: Risposte alle domande frequenti sull'uso di Apache Hive e Azure HDInsight.
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
ms.openlocfilehash: 53e9685458190efe6a586504721b8e7baadaed60
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="d8a06-104">Risolvere i problemi di Hive tramite Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8a06-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="d8a06-105">Informazioni sui problemi principali che possono verificarsi quando si usano i payload di Apache Hive in Apache Ambari unitamente alle risoluzioni.</span><span class="sxs-lookup"><span data-stu-id="d8a06-105">Learn about the top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="d8a06-106">Come esportare un metastore Hive e importarlo in un altro cluster</span><span class="sxs-lookup"><span data-stu-id="d8a06-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="d8a06-107">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="d8a06-107">Resolution steps</span></span>

1. <span data-ttu-id="d8a06-108">Connettersi al cluster HDInsight con un client Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="d8a06-108">Connect to the HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="d8a06-109">Per altre informazioni, vedere [Informazioni aggiuntive](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="d8a06-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="d8a06-110">Eseguire il comando seguente nel cluster HDInsight da cui si vuole esportare il metastore:</span><span class="sxs-lookup"><span data-stu-id="d8a06-110">Run the following command on the HDInsight cluster from which you want to export the metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="d8a06-111">Questo comando genera un file denominato alltables.sql.</span><span class="sxs-lookup"><span data-stu-id="d8a06-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="d8a06-112">Copiare il file alltables.sql nel nuovo cluster HDInsight e quindi eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d8a06-112">Copy the file alltables.sql to the new HDInsight cluster, and then run the following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="d8a06-113">Il codice nella procedura di risoluzione presuppone che i percorsi di dati nel nuovo cluster siano uguali ai percorsi di dati nel cluster precedente.</span><span class="sxs-lookup"><span data-stu-id="d8a06-113">The code in the resolution steps assumes that data paths on the new cluster are the same as the data paths on the old cluster.</span></span> <span data-ttu-id="d8a06-114">Se i percorsi di dati sono diversi, è possibile modificare manualmente il file alltables.sql generato per rispecchiare eventuali modifiche.</span><span class="sxs-lookup"><span data-stu-id="d8a06-114">If the data paths are different, you can manually edit the generated alltables.sql file to reflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="d8a06-115">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d8a06-115">Additional reading</span></span>

- [<span data-ttu-id="d8a06-116">Connettersi a un cluster HDInsight usando SSH</span><span class="sxs-lookup"><span data-stu-id="d8a06-116">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="d8a06-117">Come individuare i log di Hive in un cluster</span><span class="sxs-lookup"><span data-stu-id="d8a06-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="d8a06-118">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="d8a06-118">Resolution steps</span></span>

1. <span data-ttu-id="d8a06-119">Connettersi al cluster HDInsight usando SSH.</span><span class="sxs-lookup"><span data-stu-id="d8a06-119">Connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="d8a06-120">Per altre informazioni, vedere **Informazioni aggiuntive**.</span><span class="sxs-lookup"><span data-stu-id="d8a06-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="d8a06-121">Per visualizzare i log del client Hive, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d8a06-121">To view Hive client logs, use the following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="d8a06-122">Per visualizzare i log del metastore Hive, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d8a06-122">To view Hive metastore logs, use the following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="d8a06-123">Per visualizzare i log di Hiveserver, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d8a06-123">To view Hiveserver logs, use the following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="d8a06-124">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d8a06-124">Additional reading</span></span>

- [<span data-ttu-id="d8a06-125">Connettersi a un cluster HDInsight usando SSH</span><span class="sxs-lookup"><span data-stu-id="d8a06-125">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-the-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="d8a06-126">Come avviare la shell di Hive con configurazioni specifiche in un cluster</span><span class="sxs-lookup"><span data-stu-id="d8a06-126">How do I launch the Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="d8a06-127">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="d8a06-127">Resolution steps</span></span>

1. <span data-ttu-id="d8a06-128">Specificare una coppia chiave-valore di configurazione all'avvio della shell di Hive.</span><span class="sxs-lookup"><span data-stu-id="d8a06-128">Specify a configuration key-value pair when you start the Hive shell.</span></span> <span data-ttu-id="d8a06-129">Per altre informazioni, vedere [Informazioni aggiuntive](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="d8a06-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="d8a06-130">Per elencare tutte le configurazioni valide nella shell di Hive, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d8a06-130">To list all effective configurations on Hive shell, use the following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="d8a06-131">Ad esempio, usare il comando seguente per avviare la shell di Hive con la registrazione debug abilitata nella console:</span><span class="sxs-lookup"><span data-stu-id="d8a06-131">For example, use the following command to start Hive shell with debug logging enabled on the console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="d8a06-132">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d8a06-132">Additional reading</span></span>

- <span data-ttu-id="d8a06-133">[Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties) (Proprietà di configurazione di Hive)</span><span class="sxs-lookup"><span data-stu-id="d8a06-133">[Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)</span></span>


## <span data-ttu-id="d8a06-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Come analizzare i dati di un grafo aciclico diretto di Tez in un percorso critico del cluster</span><span class="sxs-lookup"><span data-stu-id="d8a06-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="d8a06-135">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="d8a06-135">Resolution steps</span></span>
 
1. <span data-ttu-id="d8a06-136">Per analizzare i dati di un grafo aciclico diretto di Apache Tez in un grafo critico del cluster, connettersi al cluster HDInsight usando SSH.</span><span class="sxs-lookup"><span data-stu-id="d8a06-136">To analyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="d8a06-137">Per altre informazioni, vedere [Informazioni aggiuntive](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="d8a06-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="d8a06-138">Al prompt dei comandi, eseguire il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="d8a06-138">At a command prompt, run the following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="d8a06-139">Per elencare altri analizzatori che possono essere usati per analizzare i dati DAG di Tez, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d8a06-139">To list other analyzers that can be used to analyze Tez DAG, use the following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="d8a06-140">È necessario fornire un programma di esempio come primo argomento.</span><span class="sxs-lookup"><span data-stu-id="d8a06-140">You must provide an example program as the first argument.</span></span>

  <span data-ttu-id="d8a06-141">I nomi di programma validi includono:</span><span class="sxs-lookup"><span data-stu-id="d8a06-141">Valid program names include:</span></span>
    - <span data-ttu-id="d8a06-142">**ContainerReuseAnalyzer**: stampare i dettagli di riutilizzo dei contenitori in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="d8a06-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="d8a06-143">**CriticalPath**: trovare il percorso critico di un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="d8a06-143">**CriticalPath**: Find the critical path of a DAG</span></span>
    - <span data-ttu-id="d8a06-144">**LocalityAnalyzer**: stampare i dettagli della località in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="d8a06-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="d8a06-145">**ShuffleTimeAnalyzer**: analizzare i dettagli degli orari di riproduzione casuale in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="d8a06-145">**ShuffleTimeAnalyzer**: Analyze the shuffle time details in a DAG</span></span>
    - <span data-ttu-id="d8a06-146">**SkewAnalyzer**: analizzare i dettagli dell'asimmetria in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="d8a06-146">**SkewAnalyzer**: Analyze the skew details in a DAG</span></span>
    - <span data-ttu-id="d8a06-147">**SlowNodeAnalyzer**: stampare i dettagli del nodo in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="d8a06-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="d8a06-148">**SlowTaskIdentifier**: stampare i dettagli sulle attività lente in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="d8a06-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="d8a06-149">**SlowestVertexAnalyzer**: stampare i dettagli relativi ai vertici più lenti in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="d8a06-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="d8a06-150">**SpillAnalyzer**: stampare i dettagli relativi all'espansione in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="d8a06-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="d8a06-151">**TaskConcurrencyAnalyzer**: stampare i dettagli relativi alla concorrenza delle attività in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="d8a06-151">**TaskConcurrencyAnalyzer**: Print the task concurrency details in a DAG</span></span>
    - <span data-ttu-id="d8a06-152">**VertexLevelCriticalPathAnalyzer**: trovare il percorso critico a livello di vertice in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="d8a06-152">**VertexLevelCriticalPathAnalyzer**: Find the critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="d8a06-153">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d8a06-153">Additional reading</span></span>

- [<span data-ttu-id="d8a06-154">Connettersi a un cluster HDInsight usando SSH</span><span class="sxs-lookup"><span data-stu-id="d8a06-154">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="d8a06-155">Come scaricare i dati DAG di Tez da un cluster</span><span class="sxs-lookup"><span data-stu-id="d8a06-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="d8a06-156">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="d8a06-156">Resolution steps</span></span>

<span data-ttu-id="d8a06-157">Esistono due modi per raccogliere i dati di un grafo aciclico diretto di Tez:</span><span class="sxs-lookup"><span data-stu-id="d8a06-157">There are two ways to collect the Tez DAG data:</span></span>

- <span data-ttu-id="d8a06-158">Dalla riga di comando:</span><span class="sxs-lookup"><span data-stu-id="d8a06-158">From the command line:</span></span>
 
    <span data-ttu-id="d8a06-159">Connettersi al cluster HDInsight usando SSH.</span><span class="sxs-lookup"><span data-stu-id="d8a06-159">Connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="d8a06-160">Nel prompt dei comandi eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d8a06-160">At the command prompt, run the following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="d8a06-161">Usare la visualizzazione Tez di Ambari:</span><span class="sxs-lookup"><span data-stu-id="d8a06-161">Use the Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="d8a06-162">Passare ad Ambari.</span><span class="sxs-lookup"><span data-stu-id="d8a06-162">Go to Ambari.</span></span> 
  2. <span data-ttu-id="d8a06-163">Passare alla visualizzazione Tez, disponibile sotto l'icona dei riquadri, nell'angolo superiore destro.</span><span class="sxs-lookup"><span data-stu-id="d8a06-163">Go to Tez view (under the tiles icon in the upper-right corner).</span></span> 
  3. <span data-ttu-id="d8a06-164">Selezionare il grafo aciclico diretto da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="d8a06-164">Select the DAG you want to view.</span></span>
  4. <span data-ttu-id="d8a06-165">Selezionare **Download data** (Scarica dati).</span><span class="sxs-lookup"><span data-stu-id="d8a06-165">Select **Download data**.</span></span>

### <span data-ttu-id="d8a06-166"><a name="additional-reading-end"></a>Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d8a06-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="d8a06-167">Connettersi a un cluster HDInsight usando SSH</span><span class="sxs-lookup"><span data-stu-id="d8a06-167">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






