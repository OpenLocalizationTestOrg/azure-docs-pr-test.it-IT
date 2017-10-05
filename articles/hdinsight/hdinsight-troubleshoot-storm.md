---
title: Risolvere i problemi di Storm usando Azure HDInsight | Microsoft Docs
description: Risposte alle domande frequenti sull'uso di Apache Storm con Azure HDInsight.
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
ms.openlocfilehash: 70a3d762431d90acdd6ed2a432a569f34d0ce447
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="dbe30-104">Risolvere i problemi di Storm usando Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="dbe30-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="dbe30-105">Informazioni sui problemi principali che possono verificarsi quando si usano i payload di Apache Storm in Apache Ambari unitamente alle risoluzioni.</span><span class="sxs-lookup"><span data-stu-id="dbe30-105">Learn about the top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-the-storm-ui-on-a-cluster"></a><span data-ttu-id="dbe30-106">Come accedere all'interfaccia utente di Storm in un cluster</span><span class="sxs-lookup"><span data-stu-id="dbe30-106">How do I access the Storm UI on a cluster</span></span>
<span data-ttu-id="dbe30-107">Per accedere all'interfaccia utente di Storm da un browser, è possibile procedere in due modi:</span><span class="sxs-lookup"><span data-stu-id="dbe30-107">You have two options for accessing the Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="dbe30-108">Tramite l'interfaccia utente di Ambari</span><span class="sxs-lookup"><span data-stu-id="dbe30-108">Ambari UI</span></span>
1. <span data-ttu-id="dbe30-109">Andare al dashboard di Ambari.</span><span class="sxs-lookup"><span data-stu-id="dbe30-109">Go to the Ambari dashboard.</span></span>
2. <span data-ttu-id="dbe30-110">Nell'elenco dei servizi selezionare **Storm**.</span><span class="sxs-lookup"><span data-stu-id="dbe30-110">In the list of services, select **Storm**.</span></span>
3. <span data-ttu-id="dbe30-111">Scegliere **Storm UI** (Interfaccia utente di Storm) dal menu **Quick Links** (Collegamenti rapidi).</span><span class="sxs-lookup"><span data-stu-id="dbe30-111">In the **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="dbe30-112">Collegamento diretto</span><span class="sxs-lookup"><span data-stu-id="dbe30-112">Direct link</span></span>
<span data-ttu-id="dbe30-113">È possibile accedere all'interfaccia utente di Storm all'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="dbe30-113">You can access the Storm UI at the following URL:</span></span>

<span data-ttu-id="dbe30-114">https://\<nome DNS del cluster\>/stormui</span><span class="sxs-lookup"><span data-stu-id="dbe30-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="dbe30-115">Esempio:</span><span class="sxs-lookup"><span data-stu-id="dbe30-115">Example:</span></span>

 <span data-ttu-id="dbe30-116">https://stormcluster.azurehdinsight.net/stormui</span><span class="sxs-lookup"><span data-stu-id="dbe30-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-to-another"></a><span data-ttu-id="dbe30-117">Come trasferire informazioni di checkpoint dello spout dell'hub eventi di Storm da una topologia all'altra</span><span class="sxs-lookup"><span data-stu-id="dbe30-117">How do I transfer Storm event hub spout checkpoint information from one topology to another</span></span>

<span data-ttu-id="dbe30-118">Quando si sviluppano topologie che leggono da Hub eventi di Azure usando il file JAR dello spout dell'hub eventi di HDInsight Storm, è necessario distribuire una topologia con lo stesso nome in un nuovo cluster.</span><span class="sxs-lookup"><span data-stu-id="dbe30-118">When you develop topologies that read from Azure Event Hubs by using the HDInsight Storm event hub spout .jar file, you must deploy a topology that has the same name on a new cluster.</span></span> <span data-ttu-id="dbe30-119">È tuttavia necessario conservare i dati dei checkpoint di cui è stato eseguito il commit ad Apache ZooKeeper sul vecchio cluster.</span><span class="sxs-lookup"><span data-stu-id="dbe30-119">However, you must retain the checkpoint data that was committed to Apache ZooKeeper on the old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="dbe30-120">Dove vengono archiviati i dati dei checkpoint</span><span class="sxs-lookup"><span data-stu-id="dbe30-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="dbe30-121">I dati dei checkpoint per gli offset vengono archiviati dallo spout dell'hub eventi in due percorsi radice di ZooKeeper:</span><span class="sxs-lookup"><span data-stu-id="dbe30-121">Checkpoint data for offsets is stored by the event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="dbe30-122">I checkpoint dello spout non transazionali vengono archiviati in /eventhubspout.</span><span class="sxs-lookup"><span data-stu-id="dbe30-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="dbe30-123">I dati dei checkpoint dello spout transazionali vengono archiviati in /transactional.</span><span class="sxs-lookup"><span data-stu-id="dbe30-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-to-restore"></a><span data-ttu-id="dbe30-124">Come eseguire il ripristino</span><span class="sxs-lookup"><span data-stu-id="dbe30-124">How to restore</span></span>
<span data-ttu-id="dbe30-125">Per ottenere gli script e le librerie usati per esportare i dati da ZooKeeper e quindi importarli nuovamente in ZooKeeper con un nuovo nome, vedere gli [esempi di HDInsight Storm](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="dbe30-125">To get the scripts and libraries that you use to export data out of ZooKeeper and then import the data back to ZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="dbe30-126">La cartella lib ha file JAR che contengono l'implementazione per l'operazione di esportazione/importazione.</span><span class="sxs-lookup"><span data-stu-id="dbe30-126">The lib folder has .jar files that contain the implementation for the export/import operation.</span></span> <span data-ttu-id="dbe30-127">La cartella bash contiene uno script di esempio che mostra come esportare i dati dal server ZooKeeper sul vecchio cluster e quindi reimportarli nel nuovo cluster del server ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="dbe30-127">The bash folder has an example script that demonstrates how to export data from the ZooKeeper server on the old cluster, and then import it back to the ZooKeeper server on the new cluster.</span></span>

<span data-ttu-id="dbe30-128">Eseguire lo script [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) dai nodi ZooKeeper per esportare e quindi importare i dati.</span><span class="sxs-lookup"><span data-stu-id="dbe30-128">Run the [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from the ZooKeeper nodes to export and then import data.</span></span> <span data-ttu-id="dbe30-129">Aggiornare lo script alla versione corretta di Hortonworks Data Platform (HDP).</span><span class="sxs-lookup"><span data-stu-id="dbe30-129">Update the script to the correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="dbe30-130">A breve questi script saranno generici in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dbe30-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="dbe30-131">Gli script generici possono essere eseguiti da qualsiasi nodo del cluster senza modifiche da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="dbe30-131">Generic scripts can run from any node on the cluster without modifications by the user.)</span></span>

<span data-ttu-id="dbe30-132">Il comando di esportazione scrive i metadati in un percorso Apache Hadoop Distributed File System (HDFS) (in un archivio BLOB di Azure o in un archivio di Azure Data Lake Store) nella posizione impostata.</span><span class="sxs-lookup"><span data-stu-id="dbe30-132">The export command writes the metadata to an Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="dbe30-133">esempi</span><span class="sxs-lookup"><span data-stu-id="dbe30-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="dbe30-134">Esportare i metadati dell'offset</span><span class="sxs-lookup"><span data-stu-id="dbe30-134">Export offset metadata</span></span>
1. <span data-ttu-id="dbe30-135">Usare SSH per andare al cluster ZooKeeper del vecchio cluster da cui è necessario esportare l'offset dei checkpoint.</span><span class="sxs-lookup"><span data-stu-id="dbe30-135">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="dbe30-136">Usare il comando seguente (dopo avere aggiornato la stringa della versione HDP) per esportare i dati dell'offset ZooKeeper nel percorso HDFS /stormmetadta/zkdata:</span><span class="sxs-lookup"><span data-stu-id="dbe30-136">Run the following command (after you update the HDP version string) to export ZooKeeper offset data to the /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="dbe30-137">Importare i metadati dell'offset</span><span class="sxs-lookup"><span data-stu-id="dbe30-137">Import offset metadata</span></span>
1. <span data-ttu-id="dbe30-138">Usare SSH per andare al cluster ZooKeeper del vecchio cluster da cui è necessario esportare l'offset dei checkpoint.</span><span class="sxs-lookup"><span data-stu-id="dbe30-138">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="dbe30-139">Usare il comando seguente (dopo avere aggiornato la stringa della versione HDP) per importare i dati dell'offset ZooKeeper dal percorso HDFS /stormmetadta/zkdata al cluster di destinazione del server ZooKeeper:</span><span class="sxs-lookup"><span data-stu-id="dbe30-139">Run the following command (after you update the HDP version string) to import ZooKeeper offset data from the HDFS path /stormmetadata/zkdata to the ZooKeeper server on the target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-the-beginning-or-from-a-timestamp-that-the-user-chooses"></a><span data-ttu-id="dbe30-140">Eliminare i metadati dell'offset per permettere alle topologie di avviare l'elaborazione dei dati dall'inizio o da un timestamp scelto dall'utente</span><span class="sxs-lookup"><span data-stu-id="dbe30-140">Delete offset metadata so that topologies can start processing data from the beginning, or from a timestamp that the user chooses</span></span>
1. <span data-ttu-id="dbe30-141">Usare SSH per andare al cluster ZooKeeper del vecchio cluster da cui è necessario esportare l'offset dei checkpoint.</span><span class="sxs-lookup"><span data-stu-id="dbe30-141">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="dbe30-142">Usare il comando seguente (dopo avere aggiornato la stringa della versione HDP) per eliminare tutti i dati dell'offset ZooKeeper nel cluster corrente:</span><span class="sxs-lookup"><span data-stu-id="dbe30-142">Run the following command (after you update the HDP version string) to delete all ZooKeeper offset data in the current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="dbe30-143">Individuare i binari Storm in un cluster</span><span class="sxs-lookup"><span data-stu-id="dbe30-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="dbe30-144">La posizione dei file binari Storm per lo stack HDP corrente è /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="dbe30-144">Storm binaries for the current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="dbe30-145">Il percorso è lo stesso sia per i nodi head che per i nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="dbe30-145">The location is the same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="dbe30-146">Potrebbero essere presenti più file binari per versioni HDP specifiche in /usr/hdp (ad esempio, /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="dbe30-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="dbe30-147">La cartella /usr/hdp/current/storm-client è collegata alla versione più recente in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="dbe30-147">The /usr/hdp/current/storm-client folder is symlinked to the latest version that is running on the cluster.</span></span>

<span data-ttu-id="dbe30-148">Per altre informazioni, vedere [Connettersi a un cluster HDInsight con SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="dbe30-148">For more information, see [Connect to an HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-the-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="dbe30-149">Procedura per determinare la topologia di distribuzione di un cluster Storm</span><span class="sxs-lookup"><span data-stu-id="dbe30-149">How do I determine the deployment topology of a Storm cluster</span></span>
<span data-ttu-id="dbe30-150">Identificare prima tutti i componenti installati in HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="dbe30-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="dbe30-151">Un cluster Storm è costituito da quattro categorie di nodi:</span><span class="sxs-lookup"><span data-stu-id="dbe30-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="dbe30-152">Nodi gateway</span><span class="sxs-lookup"><span data-stu-id="dbe30-152">Gateway nodes</span></span>
* <span data-ttu-id="dbe30-153">Nodi head</span><span class="sxs-lookup"><span data-stu-id="dbe30-153">Head nodes</span></span>
* <span data-ttu-id="dbe30-154">Nodi ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="dbe30-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="dbe30-155">Nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="dbe30-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="dbe30-156">Nodi gateway</span><span class="sxs-lookup"><span data-stu-id="dbe30-156">Gateway nodes</span></span>
<span data-ttu-id="dbe30-157">Un nodo del gateway è un servizio gateway e proxy inverso che consente il pubblico accesso a un servizio di gestione Ambari attivo.</span><span class="sxs-lookup"><span data-stu-id="dbe30-157">A gateway node is a gateway and reverse proxy service that enables public access to an active Ambari management service.</span></span> <span data-ttu-id="dbe30-158">Gestisce anche l'algoritmo di elezione di Ambari.</span><span class="sxs-lookup"><span data-stu-id="dbe30-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="dbe30-159">Nodi head</span><span class="sxs-lookup"><span data-stu-id="dbe30-159">Head nodes</span></span>
<span data-ttu-id="dbe30-160">I nodi head di Storm eseguono i seguenti servizi:</span><span class="sxs-lookup"><span data-stu-id="dbe30-160">Storm head nodes run the following services:</span></span>
* <span data-ttu-id="dbe30-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="dbe30-161">Nimbus</span></span>
* <span data-ttu-id="dbe30-162">Server Ambari</span><span class="sxs-lookup"><span data-stu-id="dbe30-162">Ambari server</span></span>
* <span data-ttu-id="dbe30-163">Server delle metriche Ambari</span><span class="sxs-lookup"><span data-stu-id="dbe30-163">Ambari Metrics server</span></span>
* <span data-ttu-id="dbe30-164">Agente di raccolta delle metriche Ambari</span><span class="sxs-lookup"><span data-stu-id="dbe30-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="dbe30-165">Nodi ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="dbe30-165">ZooKeeper nodes</span></span>
<span data-ttu-id="dbe30-166">HDInsight viene offerto con un quorum ZooKeeper di tre nodi.</span><span class="sxs-lookup"><span data-stu-id="dbe30-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="dbe30-167">La dimensione del quorum è fissa e non può essere riconfigurata.</span><span class="sxs-lookup"><span data-stu-id="dbe30-167">The quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="dbe30-168">I servizi Storm nel cluster sono configurati per usare automaticamente il quorum ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="dbe30-168">Storm services in the cluster are configured to automatically use the ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="dbe30-169">Nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="dbe30-169">Worker nodes</span></span>
<span data-ttu-id="dbe30-170">I nodi di lavoro di Storm eseguono i seguenti servizi:</span><span class="sxs-lookup"><span data-stu-id="dbe30-170">Storm worker nodes run the following services:</span></span>
* <span data-ttu-id="dbe30-171">Supervisore</span><span class="sxs-lookup"><span data-stu-id="dbe30-171">Supervisor</span></span>
* <span data-ttu-id="dbe30-172">Java Virtual Machine (JVM) di lavoro, per le topologie in esecuzione</span><span class="sxs-lookup"><span data-stu-id="dbe30-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="dbe30-173">Agente Ambari</span><span class="sxs-lookup"><span data-stu-id="dbe30-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="dbe30-174">Come individuare i file binari dello spout dell'hub eventi di Storm per lo sviluppo</span><span class="sxs-lookup"><span data-stu-id="dbe30-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="dbe30-175">Per altre informazioni sull'uso dei file JAR dello spout dell'hub eventi di Storm con la topologia, vedere le risorse seguenti.</span><span class="sxs-lookup"><span data-stu-id="dbe30-175">For more information about using Storm event hub spout .jar files with your topology, see the following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="dbe30-176">Topologia basata su Java</span><span class="sxs-lookup"><span data-stu-id="dbe30-176">Java-based topology</span></span>
[<span data-ttu-id="dbe30-177">Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="dbe30-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="dbe30-178">Topologia basata su C# (Mono in cluster HDInsight 3.4+ Linux Storm)</span><span class="sxs-lookup"><span data-stu-id="dbe30-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="dbe30-179">Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="dbe30-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="dbe30-180">File binari dello spout dell'hub eventi di Storm più recenti per cluster HDInsight 3.5+ Linux Storm</span><span class="sxs-lookup"><span data-stu-id="dbe30-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="dbe30-181">Per informazioni su come usare lo spout dell'hub eventi di Storm più recente che utilizza i cluster HDInsight 3.5+ Linux Storm, vedere il [mvn-repo](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="dbe30-181">To learn how to use the latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see the mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="dbe30-182">Esempi di codice sorgente</span><span class="sxs-lookup"><span data-stu-id="dbe30-182">Source code examples</span></span>
<span data-ttu-id="dbe30-183">Vedere gli [esempi](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) su come leggere e scrivere da Hub eventi di Azure usando una topologia di Apache Storm (scritta in Java) in un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dbe30-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how to read and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="dbe30-184">Individuare i file di configurazione Storm Log4J nei cluster</span><span class="sxs-lookup"><span data-stu-id="dbe30-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="dbe30-185">Per identificare i file di configurazione di Apache Log4J per i servizi Storm.</span><span class="sxs-lookup"><span data-stu-id="dbe30-185">To identify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="dbe30-186">Nei nodi head</span><span class="sxs-lookup"><span data-stu-id="dbe30-186">On head nodes</span></span>
<span data-ttu-id="dbe30-187">La configurazione Log4J di Nimbus viene letta da /usr/hdp/\<versione HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="dbe30-187">The Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="dbe30-188">Nei nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="dbe30-188">On worker nodes</span></span>
<span data-ttu-id="dbe30-189">La configurazione Log4J del supervisore viene letta da /usr/hdp/\<versione HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="dbe30-189">The supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="dbe30-190">Il file di configurazione Log4J di lavoro viene letto da /usr/hdp/\<versione HDP\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="dbe30-190">The worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="dbe30-191">Esempi: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="dbe30-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

