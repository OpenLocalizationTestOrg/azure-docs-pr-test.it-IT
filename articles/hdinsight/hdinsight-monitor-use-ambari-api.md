---
title: aaaMonitor di cluster Hadoop in HDInsight mediante hello API Ambari - Azure | Documenti Microsoft
description: "Utilizzare hello Apache Ambari APIs per la creazione, gestione e monitoraggio dei cluster Hadoop. API e strumenti operatore intuitiva nascondono la complessità di hello di Hadoop."
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
ms.openlocfilehash: d61a8aae5ddfcd7d44f2e4cc899e0a4da5e5fdcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a><span data-ttu-id="61357-104">Monitorare i cluster Hadoop in HDInsight con Ambari API hello</span><span class="sxs-lookup"><span data-stu-id="61357-104">Monitor Hadoop clusters in HDInsight using hello Ambari API</span></span>
<span data-ttu-id="61357-105">Informazioni su come cluster di toomonitor HDInsight con Ambari APIs.</span><span class="sxs-lookup"><span data-stu-id="61357-105">Learn how toomonitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="61357-106">informazioni di Hello in questo articolo vengono utilizzato principalmente per i cluster HDInsight basati su Windows, che forniscono una versione di sola lettura di hello Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="61357-106">hello information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of hello Ambari REST API.</span></span> <span data-ttu-id="61357-107">Per i cluster basati su Linux, vedere [Gestire i cluster Hadoop tramite Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="61357-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="61357-108">Informazioni su Ambari</span><span class="sxs-lookup"><span data-stu-id="61357-108">What is Ambari?</span></span>
<span data-ttu-id="61357-109">[Apache Ambari][ambari-home] viene usato per il provisioning, la gestione e il monitoraggio di cluster Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="61357-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="61357-110">Include un insieme di strumenti di operatore intuitivo e un set affidabile di API che nascondono la complessità hello di Hadoop, semplificando l'operazione di hello dei cluster.</span><span class="sxs-lookup"><span data-stu-id="61357-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide hello complexity of Hadoop, simplifying hello operation of clusters.</span></span> <span data-ttu-id="61357-111">Per ulteriori informazioni su hello API, vedere [riferimento all'API Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="61357-111">For more information about hello APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="61357-112">HDInsight supporta attualmente solo hello Ambari funzionalità di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="61357-112">HDInsight currently supports only hello Ambari monitoring feature.</span></span> <span data-ttu-id="61357-113">L'API Ambari 1.0 è supportata dai cluster HDInsight versioni 3.0 e 2.1.</span><span class="sxs-lookup"><span data-stu-id="61357-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="61357-114">Questo articolo descrive l'accesso alle API Ambari su cluster HDInsight versioni 3.1 e 2.1.</span><span class="sxs-lookup"><span data-stu-id="61357-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="61357-115">Hello chiave differenza hello due è che alcuni dei componenti di hello sono stati modificati con l'introduzione di hello le nuove funzionalità (ad esempio hello Server cronologia dei processi).</span><span class="sxs-lookup"><span data-stu-id="61357-115">hello key difference between hello two is that some of hello components have changed with hello introduction of new capabilities (such as hello Job History Server).</span></span> 

<span data-ttu-id="61357-116">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="61357-116">**Prerequisites**</span></span>

<span data-ttu-id="61357-117">Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="61357-117">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="61357-118">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="61357-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="61357-119">(Facoltativo) [cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="61357-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="61357-120">tooinstall, vedere [cURL versioni e i download][curl-download].</span><span class="sxs-lookup"><span data-stu-id="61357-120">tooinstall it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="61357-121">Quando utilizzare comando cURL hello in Windows, utilizzare virgolette doppie anziché virgolette singole per i valori di opzione hello.</span><span class="sxs-lookup"><span data-stu-id="61357-121">When use hello cURL command in Windows, use double-quotation marks instead of single-quotation marks for hello option values.</span></span>
  > 
  > 
* <span data-ttu-id="61357-122">**Un cluster HDInsight di Azure**.</span><span class="sxs-lookup"><span data-stu-id="61357-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="61357-123">Per istruzioni sul provisioning dei cluster, vedere [Introduzione a HDInsight][hdinsight-get-started] o [Effettuare il provisioning di cluster HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="61357-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="61357-124">È necessario hello toogo dati esercitazione hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="61357-124">You need hello following data toogo through hello tutorial:</span></span>
  
  | <span data-ttu-id="61357-125">Proprietà del cluster</span><span class="sxs-lookup"><span data-stu-id="61357-125">Cluster property</span></span> | <span data-ttu-id="61357-126">Nome variabile di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61357-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="61357-127">Valore</span><span class="sxs-lookup"><span data-stu-id="61357-127">Value</span></span> | <span data-ttu-id="61357-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="61357-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="61357-129">Nome del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="61357-129">HDInsight cluster name</span></span> |<span data-ttu-id="61357-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="61357-130">$clusterName</span></span> | |<span data-ttu-id="61357-131">nome Hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61357-131">hello name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="61357-132">Nome utente cluster</span><span class="sxs-lookup"><span data-stu-id="61357-132">Cluster username</span></span> |<span data-ttu-id="61357-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="61357-133">$clusterUsername</span></span> | |<span data-ttu-id="61357-134">Nome utente del cluster specificato quando hello cluster è stato creato.</span><span class="sxs-lookup"><span data-stu-id="61357-134">Cluster user name specified when hello cluster was created.</span></span> |
  |   <span data-ttu-id="61357-135">Password cluster</span><span class="sxs-lookup"><span data-stu-id="61357-135">Cluster password</span></span> |<span data-ttu-id="61357-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="61357-136">$clusterPassword</span></span> | |<span data-ttu-id="61357-137">Password dell'utente del cluster.</span><span class="sxs-lookup"><span data-stu-id="61357-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="61357-138">Avvio rapido</span><span class="sxs-lookup"><span data-stu-id="61357-138">Jump-start</span></span>
<span data-ttu-id="61357-139">Esistono diversi modi i cluster di HDInsight toouse Ambari toomonitor.</span><span class="sxs-lookup"><span data-stu-id="61357-139">There are several ways toouse Ambari toomonitor HDInsight clusters.</span></span>

<span data-ttu-id="61357-140">**Usare Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="61357-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="61357-141">lo script di PowerShell di Azure seguente Hello Ottiene le informazioni di individuazione processo MapReduce hello *in un cluster HDInsight 3.5.*</span><span class="sxs-lookup"><span data-stu-id="61357-141">hello following Azure PowerShell script gets hello MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="61357-142">la differenza principale Hello è che è pull questi dettagli servizio YARN hello (anziché MapReduce).</span><span class="sxs-lookup"><span data-stu-id="61357-142">hello key difference is that we pull these details from hello YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="61357-143">lo script di PowerShell seguente Hello Ottiene le informazioni di individuazione processo MapReduce hello *in un cluster HDInsight 2.1*:</span><span class="sxs-lookup"><span data-stu-id="61357-143">hello following PowerShell script gets hello MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="61357-144">output di Hello è:</span><span class="sxs-lookup"><span data-stu-id="61357-144">hello output is:</span></span>

![Output di jobtracker][img-jobtracker-output]

<span data-ttu-id="61357-146">**Usare cURL**</span><span class="sxs-lookup"><span data-stu-id="61357-146">**Use cURL**</span></span>

<span data-ttu-id="61357-147">Hello seguente esempio mostra come ottenere informazioni del cluster tramite cURL:</span><span class="sxs-lookup"><span data-stu-id="61357-147">hello following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="61357-148">output di Hello è:</span><span class="sxs-lookup"><span data-stu-id="61357-148">hello output is:</span></span>

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

<span data-ttu-id="61357-149">**Versione 8/10/2014 hello**:</span><span class="sxs-lookup"><span data-stu-id="61357-149">**For hello 10/8/2014 release**:</span></span>

<span data-ttu-id="61357-150">Quando tramite hello Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* campo Restituisce il nome di dominio completo hello (FQDN) del nodo hello anziché il nome host hello.</span><span class="sxs-lookup"><span data-stu-id="61357-150">When using hello Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* field returns hello fully qualified domain name (FQDN) of hello node instead of hello host name.</span></span> <span data-ttu-id="61357-151">Prima versione di hello 8/10/2014, in questo esempio viene restituito semplicemente "**headnode0**".</span><span class="sxs-lookup"><span data-stu-id="61357-151">Before hello 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="61357-152">Dopo il rilascio di 8/10/2014 hello, si ottiene hello FQDN "**headnode0. { ClusterDNS} .azurehdinsight .net**", come illustrato nell'esempio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="61357-152">After hello 10/8/2014 release, you get hello FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in hello previous example.</span></span> <span data-ttu-id="61357-153">Questa modifica è stato richiesto toofacilitate scenari in cui più tipi di cluster (ad esempio HBase e Hadoop) possono essere distribuiti in una rete virtuale (VNET).</span><span class="sxs-lookup"><span data-stu-id="61357-153">This change was required toofacilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="61357-154">Ciò accade, ad esempio, quando si usa HBase come piattaforma back-end per Hadoop.</span><span class="sxs-lookup"><span data-stu-id="61357-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="61357-155">API Ambari di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="61357-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="61357-156">Hello nella tabella seguente sono elencate alcune hello più comuni Ambari monitoraggio chiamate API.</span><span class="sxs-lookup"><span data-stu-id="61357-156">hello following table lists some of hello most common Ambari monitoring API calls.</span></span> <span data-ttu-id="61357-157">Per ulteriori informazioni su hello API, vedere [riferimento all'API Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="61357-157">For more information about hello API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="61357-158">Chiamata API di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="61357-158">Monitor API call</span></span> | <span data-ttu-id="61357-159">URI</span><span class="sxs-lookup"><span data-stu-id="61357-159">URI</span></span> | <span data-ttu-id="61357-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="61357-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61357-161">Get clusters</span><span class="sxs-lookup"><span data-stu-id="61357-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="61357-162">Get cluster info.</span><span class="sxs-lookup"><span data-stu-id="61357-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="61357-163">cluster, servizi, hosts</span><span class="sxs-lookup"><span data-stu-id="61357-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="61357-164">Get services</span><span class="sxs-lookup"><span data-stu-id="61357-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="61357-165">Services include: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="61357-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="61357-166">Get services info.</span><span class="sxs-lookup"><span data-stu-id="61357-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="61357-167">Get service components</span><span class="sxs-lookup"><span data-stu-id="61357-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="61357-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="61357-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="61357-169">Get component info.</span><span class="sxs-lookup"><span data-stu-id="61357-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="61357-170">ServiceComponentInfo, componenti host, metriche</span><span class="sxs-lookup"><span data-stu-id="61357-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="61357-171">Get hosts</span><span class="sxs-lookup"><span data-stu-id="61357-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="61357-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="61357-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="61357-173">Get host info.</span><span class="sxs-lookup"><span data-stu-id="61357-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="61357-174">Get host components</span><span class="sxs-lookup"><span data-stu-id="61357-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="61357-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="61357-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="61357-176">Get host component info.</span><span class="sxs-lookup"><span data-stu-id="61357-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="61357-177">HostRoles, componente, host, metriche</span><span class="sxs-lookup"><span data-stu-id="61357-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="61357-178">Get configurations</span><span class="sxs-lookup"><span data-stu-id="61357-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="61357-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="61357-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="61357-180">Get configuration info.</span><span class="sxs-lookup"><span data-stu-id="61357-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="61357-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="61357-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="61357-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61357-182">Next Steps</span></span>
<span data-ttu-id="61357-183">Ora si è appreso come toouse Ambari API di monitoraggio delle chiamate.</span><span class="sxs-lookup"><span data-stu-id="61357-183">Now you have learned how toouse Ambari monitoring API calls.</span></span> <span data-ttu-id="61357-184">toolearn informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="61357-184">toolearn more, see:</span></span>

* <span data-ttu-id="61357-185">[Gestire i cluster HDInsight tramite hello portale di Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="61357-185">[Manage HDInsight clusters using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="61357-186">[Gestire cluster HDInsight tramite Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="61357-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="61357-187">[Gestire cluster HDInsight tramite l'interfaccia della riga di comando][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="61357-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="61357-188">[Documentazione relativa a HDInsight][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="61357-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="61357-189">[Introduzione a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="61357-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

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
