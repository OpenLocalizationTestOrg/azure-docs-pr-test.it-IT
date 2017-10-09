---
title: aaaTroubleshoot Hive tramite Azure HDInsight | Documenti Microsoft
description: Ottenere risposte toocommon domande sull'uso di Apache Hive e Azure HDInsight.
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
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="59e91-104">Risolvere i problemi di Hive tramite Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="59e91-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="59e91-105">Informazioni sulle domande hello e le relative soluzioni quando si lavora con Apache Hive payload in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="59e91-105">Learn about hello top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="59e91-106">Come esportare un metastore Hive e importarlo in un altro cluster</span><span class="sxs-lookup"><span data-stu-id="59e91-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="59e91-107">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="59e91-107">Resolution steps</span></span>

1. <span data-ttu-id="59e91-108">Connettere il cluster di HDInsight toohello tramite un client Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="59e91-108">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="59e91-109">Per altre informazioni, vedere [Informazioni aggiuntive](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="59e91-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="59e91-110">Eseguire i comando seguente nel cluster HDInsight hello da cui si desidera tooexport hello metastore hello:</span><span class="sxs-lookup"><span data-stu-id="59e91-110">Run hello following command on hello HDInsight cluster from which you want tooexport hello metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="59e91-111">Questo comando genera un file denominato alltables.sql.</span><span class="sxs-lookup"><span data-stu-id="59e91-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="59e91-112">Copiare hello file alltables.sql toohello nuovo cluster HDInsight e quindi eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="59e91-112">Copy hello file alltables.sql toohello new HDInsight cluster, and then run hello following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="59e91-113">codice Hello nei passaggi di risoluzione hello si presuppone che i dati vengono tracciati nel nuovo cluster hello hello stesso come percorsi di dati hello vecchio cluster hello.</span><span class="sxs-lookup"><span data-stu-id="59e91-113">hello code in hello resolution steps assumes that data paths on hello new cluster are hello same as hello data paths on hello old cluster.</span></span> <span data-ttu-id="59e91-114">Se i percorsi dati hello sono diversi, è possibile modificare manualmente hello generato alltables.sql file tooreflect tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="59e91-114">If hello data paths are different, you can manually edit hello generated alltables.sql file tooreflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="59e91-115">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="59e91-115">Additional reading</span></span>

- [<span data-ttu-id="59e91-116">Connettere il cluster di HDInsight tooan tramite SSH</span><span class="sxs-lookup"><span data-stu-id="59e91-116">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="59e91-117">Come individuare i log di Hive in un cluster</span><span class="sxs-lookup"><span data-stu-id="59e91-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="59e91-118">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="59e91-118">Resolution steps</span></span>

1. <span data-ttu-id="59e91-119">Connettere il cluster di HDInsight toohello utilizzando SSH.</span><span class="sxs-lookup"><span data-stu-id="59e91-119">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="59e91-120">Per altre informazioni, vedere **Informazioni aggiuntive**.</span><span class="sxs-lookup"><span data-stu-id="59e91-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="59e91-121">i registri del client tooview Hive, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="59e91-121">tooview Hive client logs, use hello following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="59e91-122">i log metastore Hive tooview, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="59e91-122">tooview Hive metastore logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="59e91-123">tooview Hiveserver log, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="59e91-123">tooview Hiveserver logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="59e91-124">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="59e91-124">Additional reading</span></span>

- [<span data-ttu-id="59e91-125">Connettere il cluster di HDInsight tooan tramite SSH</span><span class="sxs-lookup"><span data-stu-id="59e91-125">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="59e91-126">Modalità avvio hello shell Hive con configurazioni specifiche in un cluster</span><span class="sxs-lookup"><span data-stu-id="59e91-126">How do I launch hello Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="59e91-127">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="59e91-127">Resolution steps</span></span>

1. <span data-ttu-id="59e91-128">Specificare una coppia chiave-valore di configurazione quando si avvia hello Hive shell.</span><span class="sxs-lookup"><span data-stu-id="59e91-128">Specify a configuration key-value pair when you start hello Hive shell.</span></span> <span data-ttu-id="59e91-129">Per altre informazioni, vedere [Informazioni aggiuntive](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="59e91-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="59e91-130">toolist tutte le configurazioni valide nel Hive shell, utilizzare hello seguente comando:</span><span class="sxs-lookup"><span data-stu-id="59e91-130">toolist all effective configurations on Hive shell, use hello following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="59e91-131">Ad esempio, utilizzare hello seguente toostart Hive shell dei comandi con la registrazione di debug abilitata nella console di hello:</span><span class="sxs-lookup"><span data-stu-id="59e91-131">For example, use hello following command toostart Hive shell with debug logging enabled on hello console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="59e91-132">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="59e91-132">Additional reading</span></span>

- <span data-ttu-id="59e91-133">[Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties) (Proprietà di configurazione di Hive)</span><span class="sxs-lookup"><span data-stu-id="59e91-133">[Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)</span></span>


## <span data-ttu-id="59e91-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Come analizzare i dati di un grafo aciclico diretto di Tez in un percorso critico del cluster</span><span class="sxs-lookup"><span data-stu-id="59e91-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="59e91-135">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="59e91-135">Resolution steps</span></span>
 
1. <span data-ttu-id="59e91-136">tooanalyze un Tez Apache indirizzare grafico aciclico diretto (DAG) in un grafico critici del cluster, connettere il cluster di HDInsight toohello utilizzando SSH.</span><span class="sxs-lookup"><span data-stu-id="59e91-136">tooanalyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="59e91-137">Per altre informazioni, vedere [Informazioni aggiuntive](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="59e91-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="59e91-138">Al prompt dei comandi eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="59e91-138">At a command prompt, run hello following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="59e91-139">toolist altri analizzatori che possono essere utilizzati tooanalyze Tez DAG, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="59e91-139">toolist other analyzers that can be used tooanalyze Tez DAG, use hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="59e91-140">È necessario fornire un programma di esempio come primo argomento hello.</span><span class="sxs-lookup"><span data-stu-id="59e91-140">You must provide an example program as hello first argument.</span></span>

  <span data-ttu-id="59e91-141">I nomi di programma validi includono:</span><span class="sxs-lookup"><span data-stu-id="59e91-141">Valid program names include:</span></span>
    - <span data-ttu-id="59e91-142">**ContainerReuseAnalyzer**: stampare i dettagli di riutilizzo dei contenitori in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="59e91-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="59e91-143">**CriticalPath**: percorso critico hello di ricerca di un DAG</span><span class="sxs-lookup"><span data-stu-id="59e91-143">**CriticalPath**: Find hello critical path of a DAG</span></span>
    - <span data-ttu-id="59e91-144">**LocalityAnalyzer**: stampare i dettagli della località in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="59e91-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="59e91-145">**ShuffleTimeAnalyzer**: analizzare i dettagli di tempo casuale di hello in un DAG</span><span class="sxs-lookup"><span data-stu-id="59e91-145">**ShuffleTimeAnalyzer**: Analyze hello shuffle time details in a DAG</span></span>
    - <span data-ttu-id="59e91-146">**SkewAnalyzer**: analizzare i dettagli di inclinazione hello in un DAG</span><span class="sxs-lookup"><span data-stu-id="59e91-146">**SkewAnalyzer**: Analyze hello skew details in a DAG</span></span>
    - <span data-ttu-id="59e91-147">**SlowNodeAnalyzer**: stampare i dettagli del nodo in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="59e91-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="59e91-148">**SlowTaskIdentifier**: stampare i dettagli sulle attività lente in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="59e91-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="59e91-149">**SlowestVertexAnalyzer**: stampare i dettagli relativi ai vertici più lenti in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="59e91-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="59e91-150">**SpillAnalyzer**: stampare i dettagli relativi all'espansione in un grafo aciclico diretto</span><span class="sxs-lookup"><span data-stu-id="59e91-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="59e91-151">**TaskConcurrencyAnalyzer**: stampare i dettagli di concorrenza hello attività in un DAG</span><span class="sxs-lookup"><span data-stu-id="59e91-151">**TaskConcurrencyAnalyzer**: Print hello task concurrency details in a DAG</span></span>
    - <span data-ttu-id="59e91-152">**VertexLevelCriticalPathAnalyzer**: percorso critico hello di ricerca a livello di vertici in un DAG</span><span class="sxs-lookup"><span data-stu-id="59e91-152">**VertexLevelCriticalPathAnalyzer**: Find hello critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="59e91-153">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="59e91-153">Additional reading</span></span>

- [<span data-ttu-id="59e91-154">Connettere il cluster di HDInsight tooan tramite SSH</span><span class="sxs-lookup"><span data-stu-id="59e91-154">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="59e91-155">Come scaricare i dati DAG di Tez da un cluster</span><span class="sxs-lookup"><span data-stu-id="59e91-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="59e91-156">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="59e91-156">Resolution steps</span></span>

<span data-ttu-id="59e91-157">Non esistono due modi toocollect hello DAG Tez dati:</span><span class="sxs-lookup"><span data-stu-id="59e91-157">There are two ways toocollect hello Tez DAG data:</span></span>

- <span data-ttu-id="59e91-158">Dalla riga di comando hello:</span><span class="sxs-lookup"><span data-stu-id="59e91-158">From hello command line:</span></span>
 
    <span data-ttu-id="59e91-159">Connettere il cluster di HDInsight toohello utilizzando SSH.</span><span class="sxs-lookup"><span data-stu-id="59e91-159">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="59e91-160">Al prompt dei comandi di hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="59e91-160">At hello command prompt, run hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="59e91-161">Utilizzare hello Ambari Tez Vista:</span><span class="sxs-lookup"><span data-stu-id="59e91-161">Use hello Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="59e91-162">Passare tooAmbari.</span><span class="sxs-lookup"><span data-stu-id="59e91-162">Go tooAmbari.</span></span> 
  2. <span data-ttu-id="59e91-163">Visualizzazione di passare tooTez (sotto l'icona di riquadri hello nell'angolo superiore destro hello).</span><span class="sxs-lookup"><span data-stu-id="59e91-163">Go tooTez view (under hello tiles icon in hello upper-right corner).</span></span> 
  3. <span data-ttu-id="59e91-164">Selezionare hello desiderato tooview DAG.</span><span class="sxs-lookup"><span data-stu-id="59e91-164">Select hello DAG you want tooview.</span></span>
  4. <span data-ttu-id="59e91-165">Selezionare **Download data** (Scarica dati).</span><span class="sxs-lookup"><span data-stu-id="59e91-165">Select **Download data**.</span></span>

### <span data-ttu-id="59e91-166"><a name="additional-reading-end"></a>Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="59e91-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="59e91-167">Connettere il cluster di HDInsight tooan tramite SSH</span><span class="sxs-lookup"><span data-stu-id="59e91-167">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






