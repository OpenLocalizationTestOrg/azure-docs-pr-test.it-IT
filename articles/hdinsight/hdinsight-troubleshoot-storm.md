---
title: aaaTroubleshoot Storm tramite Azure HDInsight | Documenti Microsoft
description: Ottenere risposte toocommon domande sull'uso di Apache Storm con Azure HDInsight.
keywords: Azure HDInsight, Storm, domande frequenti, guida alla risoluzione dei problemi, problemi comuni
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="5d3dc-104">Risolvere i problemi di Storm usando Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5d3dc-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="5d3dc-105">Informazioni sui problemi principali hello e le relative soluzioni per l'utilizzo di payload Apache Storm in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-105">Learn about hello top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a><span data-ttu-id="5d3dc-106">La modalità di accesso di hello Storm UI in un cluster</span><span class="sxs-lookup"><span data-stu-id="5d3dc-106">How do I access hello Storm UI on a cluster</span></span>
<span data-ttu-id="5d3dc-107">Sono disponibili due opzioni per l'accesso a hello Storm UI da un browser:</span><span class="sxs-lookup"><span data-stu-id="5d3dc-107">You have two options for accessing hello Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="5d3dc-108">Tramite l'interfaccia utente di Ambari</span><span class="sxs-lookup"><span data-stu-id="5d3dc-108">Ambari UI</span></span>
1. <span data-ttu-id="5d3dc-109">Passare toohello Ambari dashboard.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-109">Go toohello Ambari dashboard.</span></span>
2. <span data-ttu-id="5d3dc-110">Nell'elenco di hello dei servizi, selezionare **Storm**.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-110">In hello list of services, select **Storm**.</span></span>
3. <span data-ttu-id="5d3dc-111">In hello **collegamenti rapidi** dal menu **dell'interfaccia utente Storm**.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-111">In hello **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="5d3dc-112">Collegamento diretto</span><span class="sxs-lookup"><span data-stu-id="5d3dc-112">Direct link</span></span>
<span data-ttu-id="5d3dc-113">È possibile accedere hello Storm UI in hello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="5d3dc-113">You can access hello Storm UI at hello following URL:</span></span>

<span data-ttu-id="5d3dc-114">https://\<nome DNS del cluster\>/stormui</span><span class="sxs-lookup"><span data-stu-id="5d3dc-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="5d3dc-115">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5d3dc-115">Example:</span></span>

 <span data-ttu-id="5d3dc-116">https://stormcluster.azurehdinsight.net/stormui</span><span class="sxs-lookup"><span data-stu-id="5d3dc-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a><span data-ttu-id="5d3dc-117">Come è possibile trasferire informazioni di checkpoint beccuccio hub eventi Storm da una topologia tooanother</span><span class="sxs-lookup"><span data-stu-id="5d3dc-117">How do I transfer Storm event hub spout checkpoint information from one topology tooanother</span></span>

<span data-ttu-id="5d3dc-118">Quando si sviluppano le topologie di lettura dagli hub di eventi di Azure tramite hello JAR beccuccio hub eventi di HDInsight Storm, è necessario distribuire una topologia con hello stesso nome in un nuovo cluster.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-118">When you develop topologies that read from Azure Event Hubs by using hello HDInsight Storm event hub spout .jar file, you must deploy a topology that has hello same name on a new cluster.</span></span> <span data-ttu-id="5d3dc-119">Tuttavia, è necessario conservare i dati di checkpoint hello che è stato eseguito il commit tooApache ZooKeeper nel vecchio cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-119">However, you must retain hello checkpoint data that was committed tooApache ZooKeeper on hello old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="5d3dc-120">Dove vengono archiviati i dati dei checkpoint</span><span class="sxs-lookup"><span data-stu-id="5d3dc-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="5d3dc-121">I dati di checkpoint per l'offset sono archiviati da hello evento hub beccuccio in ZooKeeper in due percorsi principali:</span><span class="sxs-lookup"><span data-stu-id="5d3dc-121">Checkpoint data for offsets is stored by hello event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="5d3dc-122">I checkpoint dello spout non transazionali vengono archiviati in /eventhubspout.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="5d3dc-123">I dati dei checkpoint dello spout transazionali vengono archiviati in /transactional.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-toorestore"></a><span data-ttu-id="5d3dc-124">Come toorestore</span><span class="sxs-lookup"><span data-stu-id="5d3dc-124">How toorestore</span></span>
<span data-ttu-id="5d3dc-125">gli script hello tooget e raccolte che si utilizzano dati di tooexport fuori ZooKeeper e quindi importare hello tooZooKeeper indietro di dati con un nuovo nome, vedere [esempi HDInsight Storm](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="5d3dc-125">tooget hello scripts and libraries that you use tooexport data out of ZooKeeper and then import hello data back tooZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="5d3dc-126">cartella lib Hello è file JAR che contengono l'implementazione di hello per l'operazione di esportazione/importazione hello.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-126">hello lib folder has .jar files that contain hello implementation for hello export/import operation.</span></span> <span data-ttu-id="5d3dc-127">cartella bash Hello è uno script di esempio che illustra come dati tooexport hello server ZooKeeper nel vecchio cluster hello e quindi importarlo server ZooKeeper toohello indietro nel nuovo cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-127">hello bash folder has an example script that demonstrates how tooexport data from hello ZooKeeper server on hello old cluster, and then import it back toohello ZooKeeper server on hello new cluster.</span></span>

<span data-ttu-id="5d3dc-128">Eseguire hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) generare uno script da hello ZooKeeper nodi tooexport e quindi importare i dati.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-128">Run hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from hello ZooKeeper nodes tooexport and then import data.</span></span> <span data-ttu-id="5d3dc-129">Aggiornamento hello script toohello Hortonworks Data Platform (HDP) versione corretta.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-129">Update hello script toohello correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="5d3dc-130">A breve questi script saranno generici in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="5d3dc-131">Script generico può eseguire da qualsiasi nodo nel cluster hello senza modifiche dall'utente hello.)</span><span class="sxs-lookup"><span data-stu-id="5d3dc-131">Generic scripts can run from any node on hello cluster without modifications by hello user.)</span></span>

<span data-ttu-id="5d3dc-132">comando Esporta Hello scrive hello percorso dei metadati tooan Apache Hadoop Distributed File System (HDFS) (in un archivio di archiviazione Blob di Azure o archivio Azure Data Lake) in una posizione che è impostato.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-132">hello export command writes hello metadata tooan Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="5d3dc-133">esempi</span><span class="sxs-lookup"><span data-stu-id="5d3dc-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="5d3dc-134">Esportare i metadati dell'offset</span><span class="sxs-lookup"><span data-stu-id="5d3dc-134">Export offset metadata</span></span>
1. <span data-ttu-id="5d3dc-135">Usare SSH toogo toohello ZooKeeper cluster nel cluster hello dal quale checkpoint hello offset deve toobe esportato.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-135">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="5d3dc-136">Hello esecuzione comando che segue (dopo l'aggiornamento hello stringa di versione HDP) tooexport ZooKeeper offset dati toohello /stormmetadta/zkdata HDFS percorso:</span><span class="sxs-lookup"><span data-stu-id="5d3dc-136">Run hello following command (after you update hello HDP version string) tooexport ZooKeeper offset data toohello /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="5d3dc-137">Importare i metadati dell'offset</span><span class="sxs-lookup"><span data-stu-id="5d3dc-137">Import offset metadata</span></span>
1. <span data-ttu-id="5d3dc-138">Usare SSH toogo toohello ZooKeeper cluster nel cluster hello dal quale checkpoint hello offset deve toobe esportato.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-138">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="5d3dc-139">Esecuzione hello il seguente comando (dopo l'aggiornamento di stringa di versione di hello HDP) tooimport ZooKeeper offset dati hello HDFS percorso stormmetadata/zkdata toohello ZooKeeper server nel cluster di destinazione hello:</span><span class="sxs-lookup"><span data-stu-id="5d3dc-139">Run hello following command (after you update hello HDP version string) tooimport ZooKeeper offset data from hello HDFS path /stormmetadata/zkdata toohello ZooKeeper server on hello target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a><span data-ttu-id="5d3dc-140">Eliminare i metadati di offset, in modo che topologie è possono avviare l'elaborazione dei dati dall'inizio hello o da un timestamp sceglie tale utente hello</span><span class="sxs-lookup"><span data-stu-id="5d3dc-140">Delete offset metadata so that topologies can start processing data from hello beginning, or from a timestamp that hello user chooses</span></span>
1. <span data-ttu-id="5d3dc-141">Usare SSH toogo toohello ZooKeeper cluster nel cluster hello dal quale checkpoint hello offset deve toobe esportato.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-141">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="5d3dc-142">Esecuzione hello il seguente comando (dopo l'aggiornamento di stringa di versione di hello HDP) toodelete tutti ZooKeeper offset dati in cluster corrente hello:</span><span class="sxs-lookup"><span data-stu-id="5d3dc-142">Run hello following command (after you update hello HDP version string) toodelete all ZooKeeper offset data in hello current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="5d3dc-143">Individuare i binari Storm in un cluster</span><span class="sxs-lookup"><span data-stu-id="5d3dc-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="5d3dc-144">File binari di Storm per stack HDP corrente hello sono /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-144">Storm binaries for hello current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="5d3dc-145">percorso Hello è hello stesso sia per i nodi head e per i nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-145">hello location is hello same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="5d3dc-146">Potrebbero essere presenti più file binari per versioni HDP specifiche in /usr/hdp (ad esempio, /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="5d3dc-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="5d3dc-147">cartella /usr/hdp/current/storm-client hello è symlinked toohello versione più recente che è in esecuzione nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-147">hello /usr/hdp/current/storm-client folder is symlinked toohello latest version that is running on hello cluster.</span></span>

<span data-ttu-id="5d3dc-148">Per ulteriori informazioni, vedere [cluster HDInsight tooan di connettersi tramite SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="5d3dc-148">For more information, see [Connect tooan HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="5d3dc-149">Come è possibile determinare la topologia di distribuzione hello di un cluster Storm</span><span class="sxs-lookup"><span data-stu-id="5d3dc-149">How do I determine hello deployment topology of a Storm cluster</span></span>
<span data-ttu-id="5d3dc-150">Identificare prima tutti i componenti installati in HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="5d3dc-151">Un cluster Storm è costituito da quattro categorie di nodi:</span><span class="sxs-lookup"><span data-stu-id="5d3dc-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="5d3dc-152">Nodi gateway</span><span class="sxs-lookup"><span data-stu-id="5d3dc-152">Gateway nodes</span></span>
* <span data-ttu-id="5d3dc-153">Nodi head</span><span class="sxs-lookup"><span data-stu-id="5d3dc-153">Head nodes</span></span>
* <span data-ttu-id="5d3dc-154">Nodi ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="5d3dc-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="5d3dc-155">Nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="5d3dc-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="5d3dc-156">Nodi gateway</span><span class="sxs-lookup"><span data-stu-id="5d3dc-156">Gateway nodes</span></span>
<span data-ttu-id="5d3dc-157">Un nodo di gateway è un gateway e un servizio di proxy inverso che consente di servizio di gestione di accesso pubblico tooan active Ambari.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-157">A gateway node is a gateway and reverse proxy service that enables public access tooan active Ambari management service.</span></span> <span data-ttu-id="5d3dc-158">Gestisce anche l'algoritmo di elezione di Ambari.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="5d3dc-159">Nodi head</span><span class="sxs-lookup"><span data-stu-id="5d3dc-159">Head nodes</span></span>
<span data-ttu-id="5d3dc-160">I nodi head Storm eseguire hello seguenti servizi:</span><span class="sxs-lookup"><span data-stu-id="5d3dc-160">Storm head nodes run hello following services:</span></span>
* <span data-ttu-id="5d3dc-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="5d3dc-161">Nimbus</span></span>
* <span data-ttu-id="5d3dc-162">Server Ambari</span><span class="sxs-lookup"><span data-stu-id="5d3dc-162">Ambari server</span></span>
* <span data-ttu-id="5d3dc-163">Server delle metriche Ambari</span><span class="sxs-lookup"><span data-stu-id="5d3dc-163">Ambari Metrics server</span></span>
* <span data-ttu-id="5d3dc-164">Agente di raccolta delle metriche Ambari</span><span class="sxs-lookup"><span data-stu-id="5d3dc-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="5d3dc-165">Nodi ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="5d3dc-165">ZooKeeper nodes</span></span>
<span data-ttu-id="5d3dc-166">HDInsight viene offerto con un quorum ZooKeeper di tre nodi.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="5d3dc-167">dimensione di Hello quorum è fissa e non può essere riconfigurati.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-167">hello quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="5d3dc-168">Servizi di Storm cluster hello sono quorum di ZooKeeper hello utilizzare tooautomatically configurato.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-168">Storm services in hello cluster are configured tooautomatically use hello ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="5d3dc-169">Nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="5d3dc-169">Worker nodes</span></span>
<span data-ttu-id="5d3dc-170">Nodi di lavoro Storm eseguire hello seguenti servizi:</span><span class="sxs-lookup"><span data-stu-id="5d3dc-170">Storm worker nodes run hello following services:</span></span>
* <span data-ttu-id="5d3dc-171">Supervisore</span><span class="sxs-lookup"><span data-stu-id="5d3dc-171">Supervisor</span></span>
* <span data-ttu-id="5d3dc-172">Java Virtual Machine (JVM) di lavoro, per le topologie in esecuzione</span><span class="sxs-lookup"><span data-stu-id="5d3dc-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="5d3dc-173">Agente Ambari</span><span class="sxs-lookup"><span data-stu-id="5d3dc-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="5d3dc-174">Come individuare i file binari dello spout dell'hub eventi di Storm per lo sviluppo</span><span class="sxs-lookup"><span data-stu-id="5d3dc-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="5d3dc-175">Per ulteriori informazioni sull'utilizzo dei file JAR di Storm evento hub beccuccio con la topologia, vedere hello seguenti risorse.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-175">For more information about using Storm event hub spout .jar files with your topology, see hello following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="5d3dc-176">Topologia basata su Java</span><span class="sxs-lookup"><span data-stu-id="5d3dc-176">Java-based topology</span></span>
[<span data-ttu-id="5d3dc-177">Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="5d3dc-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="5d3dc-178">Topologia basata su C# (Mono in cluster HDInsight 3.4+ Linux Storm)</span><span class="sxs-lookup"><span data-stu-id="5d3dc-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="5d3dc-179">Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="5d3dc-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="5d3dc-180">File binari dello spout dell'hub eventi di Storm più recenti per cluster HDInsight 3.5+ Linux Storm</span><span class="sxs-lookup"><span data-stu-id="5d3dc-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="5d3dc-181">toolearn come toouse hello più recente Storm evento hub beccuccio che funziona con HDInsight 3.5 + cluster Linux Storm, vedere hello mvn-repo [file readme](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="5d3dc-181">toolearn how toouse hello latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see hello mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="5d3dc-182">Esempi di codice sorgente</span><span class="sxs-lookup"><span data-stu-id="5d3dc-182">Source code examples</span></span>
<span data-ttu-id="5d3dc-183">Vedere [esempi](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) come tooread e scrivere da Hub di eventi di Azure usando una topologia di Apache Storm (scritta in linguaggio) in un cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how tooread and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="5d3dc-184">Individuare i file di configurazione Storm Log4J nei cluster</span><span class="sxs-lookup"><span data-stu-id="5d3dc-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="5d3dc-185">file di configurazione tooidentify Apache Log4J per i servizi di Storm.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-185">tooidentify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="5d3dc-186">Nei nodi head</span><span class="sxs-lookup"><span data-stu-id="5d3dc-186">On head nodes</span></span>
<span data-ttu-id="5d3dc-187">configurazione di Hello Nimbus Log4J viene letta in /usr. hdp/\<versione HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-187">hello Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="5d3dc-188">Nei nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="5d3dc-188">On worker nodes</span></span>
<span data-ttu-id="5d3dc-189">configurazione del Supervisore Log4J Hello viene letto in /usr. hdp/\<versione HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-189">hello supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="5d3dc-190">file di configurazione di lavoro Log4J Hello viene letto in /usr. hdp/\<versione HDP\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="5d3dc-190">hello worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="5d3dc-191">Esempi: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="5d3dc-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

