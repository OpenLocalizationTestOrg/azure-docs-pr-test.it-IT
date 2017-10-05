---
title: Monitorare i cluster Hadoop in HDInsight con l'API Ambari - Azure | Microsoft Docs
description: "Usare le API Apache Ambari per la creazione, la gestione e il monitoraggio di cluster Hadoop. Gli intuitivi strumenti operatore e le API nascondono la complessità di Hadoop."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: b6fc2098027690eb76b69b1427f0e9541b8a7a69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-the-ambari-api"></a><span data-ttu-id="412f9-104">Monitorare i cluster Hadoop in HDInsight tramite l'API Ambari</span><span class="sxs-lookup"><span data-stu-id="412f9-104">Monitor Hadoop clusters in HDInsight using the Ambari API</span></span>
<span data-ttu-id="412f9-105">Informazioni sul monitoraggio di cluster HDInsight con API Ambari.</span><span class="sxs-lookup"><span data-stu-id="412f9-105">Learn how to monitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="412f9-106">Le informazioni contenute in questo articolo sono relative principalmente ai cluster HDInsight basati su Windows, che forniscono una versione in sola lettura dell’API REST Ambari.</span><span class="sxs-lookup"><span data-stu-id="412f9-106">The information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of the Ambari REST API.</span></span> <span data-ttu-id="412f9-107">Per i cluster basati su Linux, vedere [Gestire i cluster Hadoop tramite Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="412f9-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="412f9-108">Informazioni su Ambari</span><span class="sxs-lookup"><span data-stu-id="412f9-108">What is Ambari?</span></span>
<span data-ttu-id="412f9-109">[Apache Ambari][ambari-home] viene usato per il provisioning, la gestione e il monitoraggio di cluster Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="412f9-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="412f9-110">Comprende una raccolta di strumenti operatore intuitivi e un set affidabile di API che nascondono la complessità di Hadoop, semplificando le operazioni sui cluster.</span><span class="sxs-lookup"><span data-stu-id="412f9-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide the complexity of Hadoop, simplifying the operation of clusters.</span></span> <span data-ttu-id="412f9-111">Per altre informazioni, vedere le [informazioni di riferimento dell'API Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="412f9-111">For more information about the APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="412f9-112">Attualmente HDInsight supporta solo la funzione di monitoraggio di Ambari.</span><span class="sxs-lookup"><span data-stu-id="412f9-112">HDInsight currently supports only the Ambari monitoring feature.</span></span> <span data-ttu-id="412f9-113">L'API Ambari 1.0 è supportata dai cluster HDInsight versioni 3.0 e 2.1.</span><span class="sxs-lookup"><span data-stu-id="412f9-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="412f9-114">Questo articolo descrive l'accesso alle API Ambari su cluster HDInsight versioni 3.1 e 2.1.</span><span class="sxs-lookup"><span data-stu-id="412f9-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="412f9-115">La differenza principale tra i due è che alcuni componenti sono cambiati con l'introduzione di nuove funzionalità (ad esempio, il server della cronologia dei processi).</span><span class="sxs-lookup"><span data-stu-id="412f9-115">The key difference between the two is that some of the components have changed with the introduction of new capabilities (such as the Job History Server).</span></span> 

<span data-ttu-id="412f9-116">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="412f9-116">**Prerequisites**</span></span>

<span data-ttu-id="412f9-117">Prima di iniziare questa esercitazione sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="412f9-117">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="412f9-118">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="412f9-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="412f9-119">(Facoltativo) [cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="412f9-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="412f9-120">Per installarlo, vedere [cURL Releases and Downloads][curl-download] (Versioni e download di cURL).</span><span class="sxs-lookup"><span data-stu-id="412f9-120">To install it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="412f9-121">Quando si usa il comando cURL in Windows, per i valori delle opzioni usare le virgolette doppie invece di quelle singole.</span><span class="sxs-lookup"><span data-stu-id="412f9-121">When use the cURL command in Windows, use double-quotation marks instead of single-quotation marks for the option values.</span></span>
  > 
  > 
* <span data-ttu-id="412f9-122">**Un cluster HDInsight di Azure**.</span><span class="sxs-lookup"><span data-stu-id="412f9-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="412f9-123">Per istruzioni sul provisioning dei cluster, vedere [Introduzione a HDInsight][hdinsight-get-started] o [Effettuare il provisioning di cluster HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="412f9-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="412f9-124">Per completare l'esercitazione sono necessari i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="412f9-124">You need the following data to go through the tutorial:</span></span>
  
  | <span data-ttu-id="412f9-125">Proprietà del cluster</span><span class="sxs-lookup"><span data-stu-id="412f9-125">Cluster property</span></span> | <span data-ttu-id="412f9-126">Nome variabile di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="412f9-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="412f9-127">Valore</span><span class="sxs-lookup"><span data-stu-id="412f9-127">Value</span></span> | <span data-ttu-id="412f9-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="412f9-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="412f9-129">Nome del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="412f9-129">HDInsight cluster name</span></span> |<span data-ttu-id="412f9-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="412f9-130">$clusterName</span></span> | |<span data-ttu-id="412f9-131">Il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="412f9-131">The name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="412f9-132">Nome utente cluster</span><span class="sxs-lookup"><span data-stu-id="412f9-132">Cluster username</span></span> |<span data-ttu-id="412f9-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="412f9-133">$clusterUsername</span></span> | |<span data-ttu-id="412f9-134">Nome utente del cluster specificato al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="412f9-134">Cluster user name specified when the cluster was created.</span></span> |
  |   <span data-ttu-id="412f9-135">Password cluster</span><span class="sxs-lookup"><span data-stu-id="412f9-135">Cluster password</span></span> |<span data-ttu-id="412f9-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="412f9-136">$clusterPassword</span></span> | |<span data-ttu-id="412f9-137">Password dell'utente del cluster.</span><span class="sxs-lookup"><span data-stu-id="412f9-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="412f9-138">Avvio rapido</span><span class="sxs-lookup"><span data-stu-id="412f9-138">Jump-start</span></span>
<span data-ttu-id="412f9-139">È possibile usare Ambari per monitorare cluster HDInsight in vari modi.</span><span class="sxs-lookup"><span data-stu-id="412f9-139">There are several ways to use Ambari to monitor HDInsight clusters.</span></span>

<span data-ttu-id="412f9-140">**Usare Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="412f9-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="412f9-141">Lo script di Azure PowerShell seguente ottiene le informazioni di analisi del processo MapReduce *in un cluster HDInsight 3.5*.</span><span class="sxs-lookup"><span data-stu-id="412f9-141">The following Azure PowerShell script gets the MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="412f9-142">La differenza principale consiste nel fatto che queste informazioni vengono estratte dal servizio YARN (anziché da MapReduce).</span><span class="sxs-lookup"><span data-stu-id="412f9-142">The key difference is that we pull these details from the YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="412f9-143">Lo script di PowerShell seguente ottiene le informazioni di analisi del processo MapReduce *in un cluster HDInsight 2.1*.</span><span class="sxs-lookup"><span data-stu-id="412f9-143">The following PowerShell script gets the MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="412f9-144">L'output è:</span><span class="sxs-lookup"><span data-stu-id="412f9-144">The output is:</span></span>

![Output di jobtracker][img-jobtracker-output]

<span data-ttu-id="412f9-146">**Usare cURL**</span><span class="sxs-lookup"><span data-stu-id="412f9-146">**Use cURL**</span></span>

<span data-ttu-id="412f9-147">L'esempio seguente ottiene informazioni sul cluster usando cURL:</span><span class="sxs-lookup"><span data-stu-id="412f9-147">The following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="412f9-148">L'output è:</span><span class="sxs-lookup"><span data-stu-id="412f9-148">The output is:</span></span>

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

<span data-ttu-id="412f9-149">**Note per la versione rilasciata in data 08/10/2014**:</span><span class="sxs-lookup"><span data-stu-id="412f9-149">**For the 10/8/2014 release**:</span></span>

<span data-ttu-id="412f9-150">Quando si usa l'endpoint Ambari, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", il campo *host_name* restituisce il nome di dominio completo (FQDN) del nodo anziché il nome host.</span><span class="sxs-lookup"><span data-stu-id="412f9-150">When using the Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", the *host_name* field returns the fully qualified domain name (FQDN) of the node instead of the host name.</span></span> <span data-ttu-id="412f9-151">Prima della versione rilasciata l'10/8/2014, questo esempio restituiva semplicemente "**headnode0**".</span><span class="sxs-lookup"><span data-stu-id="412f9-151">Before the 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="412f9-152">Dopo la versione dell'10/8/2014, si ottiene il nome FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", come nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="412f9-152">After the 10/8/2014 release, you get the FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in the previous example.</span></span> <span data-ttu-id="412f9-153">Questa modifica si è resa necessaria per facilitare scenari in cui sia possibile implementare più tipi di cluster, come HBase e Hadoop, in un'unica rete virtuale (VNET).</span><span class="sxs-lookup"><span data-stu-id="412f9-153">This change was required to facilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="412f9-154">Ciò accade, ad esempio, quando si usa HBase come piattaforma back-end per Hadoop.</span><span class="sxs-lookup"><span data-stu-id="412f9-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="412f9-155">API Ambari di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="412f9-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="412f9-156">La tabella seguente riporta alcune delle chiamate API Ambari di monitoraggio più comuni.</span><span class="sxs-lookup"><span data-stu-id="412f9-156">The following table lists some of the most common Ambari monitoring API calls.</span></span> <span data-ttu-id="412f9-157">Per altre informazioni, vedere le [informazioni di riferimento dell'API Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="412f9-157">For more information about the API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="412f9-158">Chiamata API di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="412f9-158">Monitor API call</span></span> | <span data-ttu-id="412f9-159">URI</span><span class="sxs-lookup"><span data-stu-id="412f9-159">URI</span></span> | <span data-ttu-id="412f9-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="412f9-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="412f9-161">Get clusters</span><span class="sxs-lookup"><span data-stu-id="412f9-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="412f9-162">Get cluster info.</span><span class="sxs-lookup"><span data-stu-id="412f9-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="412f9-163">cluster, servizi, hosts</span><span class="sxs-lookup"><span data-stu-id="412f9-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="412f9-164">Get services</span><span class="sxs-lookup"><span data-stu-id="412f9-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="412f9-165">Services include: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="412f9-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="412f9-166">Get services info.</span><span class="sxs-lookup"><span data-stu-id="412f9-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="412f9-167">Get service components</span><span class="sxs-lookup"><span data-stu-id="412f9-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="412f9-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="412f9-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="412f9-169">Get component info.</span><span class="sxs-lookup"><span data-stu-id="412f9-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="412f9-170">ServiceComponentInfo, componenti host, metriche</span><span class="sxs-lookup"><span data-stu-id="412f9-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="412f9-171">Get hosts</span><span class="sxs-lookup"><span data-stu-id="412f9-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="412f9-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="412f9-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="412f9-173">Get host info.</span><span class="sxs-lookup"><span data-stu-id="412f9-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="412f9-174">Get host components</span><span class="sxs-lookup"><span data-stu-id="412f9-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="412f9-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="412f9-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="412f9-176">Get host component info.</span><span class="sxs-lookup"><span data-stu-id="412f9-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="412f9-177">HostRoles, componente, host, metriche</span><span class="sxs-lookup"><span data-stu-id="412f9-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="412f9-178">Get configurations</span><span class="sxs-lookup"><span data-stu-id="412f9-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="412f9-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="412f9-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="412f9-180">Get configuration info.</span><span class="sxs-lookup"><span data-stu-id="412f9-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="412f9-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="412f9-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="412f9-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="412f9-182">Next Steps</span></span>
<span data-ttu-id="412f9-183">In questa esercitazione si è appreso come utilizzare le chiamate API Ambari di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="412f9-183">Now you have learned how to use Ambari monitoring API calls.</span></span> <span data-ttu-id="412f9-184">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="412f9-184">To learn more, see:</span></span>

* <span data-ttu-id="412f9-185">[Gestire cluster HDInsight tramite il portale di Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="412f9-185">[Manage HDInsight clusters using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="412f9-186">[Gestire cluster HDInsight tramite Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="412f9-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="412f9-187">[Gestire cluster HDInsight tramite l'interfaccia della riga di comando][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="412f9-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="412f9-188">[Documentazione relativa a HDInsight][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="412f9-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="412f9-189">[Introduzione a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="412f9-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[img-jobtracker-output]: ./media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png
