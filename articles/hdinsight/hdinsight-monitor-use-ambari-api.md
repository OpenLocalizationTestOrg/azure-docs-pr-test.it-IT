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
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a>Monitorare i cluster Hadoop in HDInsight con Ambari API hello
Informazioni su come cluster di toomonitor HDInsight con Ambari APIs.

> [!NOTE]
> informazioni di Hello in questo articolo vengono utilizzato principalmente per i cluster HDInsight basati su Windows, che forniscono una versione di sola lettura di hello Ambari REST API. Per i cluster basati su Linux, vedere [Gestire i cluster Hadoop tramite Ambari](hdinsight-hadoop-manage-ambari.md).
> 
> 

## <a name="what-is-ambari"></a>Informazioni su Ambari
[Apache Ambari][ambari-home] viene usato per il provisioning, la gestione e il monitoraggio di cluster Apache Hadoop. Include un insieme di strumenti di operatore intuitivo e un set affidabile di API che nascondono la complessità hello di Hadoop, semplificando l'operazione di hello dei cluster. Per ulteriori informazioni su hello API, vedere [riferimento all'API Ambari][ambari-api-reference]. 

HDInsight supporta attualmente solo hello Ambari funzionalità di monitoraggio. L'API Ambari 1.0 è supportata dai cluster HDInsight versioni 3.0 e 2.1. Questo articolo descrive l'accesso alle API Ambari su cluster HDInsight versioni 3.1 e 2.1. Hello chiave differenza hello due è che alcuni dei componenti di hello sono stati modificati con l'introduzione di hello le nuove funzionalità (ad esempio hello Server cronologia dei processi). 

**Prerequisiti**

Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti elementi:

* **Workstation con Azure PowerShell**.
* (Facoltativo) [cURL][curl]. tooinstall, vedere [cURL versioni e i download][curl-download].
  
  > [!NOTE]
  > Quando utilizzare comando cURL hello in Windows, utilizzare virgolette doppie anziché virgolette singole per i valori di opzione hello.
  > 
  > 
* **Un cluster HDInsight di Azure**. Per istruzioni sul provisioning dei cluster, vedere [Introduzione a HDInsight][hdinsight-get-started] o [Effettuare il provisioning di cluster HDInsight][hdinsight-provision]. È necessario hello toogo dati esercitazione hello seguenti:
  
  | Proprietà del cluster | Nome variabile di Azure PowerShell | Valore | Descrizione |
  | --- | --- | --- | --- |
  |   Nome del cluster HDInsight |$clusterName | |nome Hello del cluster HDInsight. |
  |   Nome utente cluster |$clusterUsername | |Nome utente del cluster specificato quando hello cluster è stato creato. |
  |   Password cluster |$clusterPassword | |Password dell'utente del cluster. |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a>Avvio rapido
Esistono diversi modi i cluster di HDInsight toouse Ambari toomonitor.

**Usare Azure PowerShell**

lo script di PowerShell di Azure seguente Hello Ottiene le informazioni di individuazione processo MapReduce hello *in un cluster HDInsight 3.5.*  la differenza principale Hello è che è pull questi dettagli servizio YARN hello (anziché MapReduce).

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

lo script di PowerShell seguente Hello Ottiene le informazioni di individuazione processo MapReduce hello *in un cluster HDInsight 2.1*:

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

output di Hello è:

![Output di jobtracker][img-jobtracker-output]

**Usare cURL**

Hello seguente esempio mostra come ottenere informazioni del cluster tramite cURL:

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

output di Hello è:

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

**Versione 8/10/2014 hello**:

Quando tramite hello Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* campo Restituisce il nome di dominio completo hello (FQDN) del nodo hello anziché il nome host hello. Prima versione di hello 8/10/2014, in questo esempio viene restituito semplicemente "**headnode0**". Dopo il rilascio di 8/10/2014 hello, si ottiene hello FQDN "**headnode0. { ClusterDNS} .azurehdinsight .net**", come illustrato nell'esempio precedente hello. Questa modifica è stato richiesto toofacilitate scenari in cui più tipi di cluster (ad esempio HBase e Hadoop) possono essere distribuiti in una rete virtuale (VNET). Ciò accade, ad esempio, quando si usa HBase come piattaforma back-end per Hadoop.

## <a name="ambari-monitoring-apis"></a>API Ambari di monitoraggio
Hello nella tabella seguente sono elencate alcune hello più comuni Ambari monitoraggio chiamate API. Per ulteriori informazioni su hello API, vedere [riferimento all'API Ambari][ambari-api-reference].

| Chiamata API di monitoraggio | URI | Descrizione |
| --- | --- | --- |
| Get clusters |`/api/v1/clusters` | |
| Get cluster info. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |cluster, servizi, hosts |
| Get services |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |Services include: hdfs, mapreduce |
| Get services info. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| Get service components |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker |
| Get component info. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |ServiceComponentInfo, componenti host, metriche |
| Get hosts |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |headnode0, workernode0 |
| Get host info. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| Get host components |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |namenode, resourcemanager |
| Get host component info. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |HostRoles, componente, host, metriche |
| Get configurations |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |Config types: core-site, hdfs-site, mapred-site, hive-site |
| Get configuration info. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |Config types: core-site, hdfs-site, mapred-site, hive-site |

## <a name="next-steps"></a>Passaggi successivi
Ora si è appreso come toouse Ambari API di monitoraggio delle chiamate. toolearn informazioni, vedere:

* [Gestire i cluster HDInsight tramite hello portale di Azure][hdinsight-admin-portal]
* [Gestire cluster HDInsight tramite Azure PowerShell][hdinsight-admin-powershell]
* [Gestire cluster HDInsight tramite l'interfaccia della riga di comando][hdinsight-admin-cli]
* [Documentazione relativa a HDInsight][hdinsight-documentation]
* [Introduzione a HDInsight][hdinsight-get-started]

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
