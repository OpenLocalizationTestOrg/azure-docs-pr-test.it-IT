---
title: Monitorare e gestire Hadoop con l'API REST Ambari - Azure HDInsight | Microsoft Docs
description: "Informazioni sull'uso di Ambari per monitorare e gestire i cluster Hadoop in Azure HDInsight. In questo documento si apprenderà come usare l'API REST Ambari inclusa nei cluster HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 7960d83bce22d4f671d61e9aaf55561bc24308f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-rest-api"></a><span data-ttu-id="c8398-104">Gestire i cluster HDInsight mediante l'API REST Ambari</span><span class="sxs-lookup"><span data-stu-id="c8398-104">Manage HDInsight clusters by using the Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="c8398-105">Informazioni sull'uso dell'API REST per gestire e monitorare i cluster Hadoop in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c8398-105">Learn how to use the Ambari REST API to manage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="c8398-106">Apache Ambari semplifica la gestione e il monitoraggio di un cluster Hadoop grazie a un'interfaccia utente Web facile da usare e alle API REST.</span><span class="sxs-lookup"><span data-stu-id="c8398-106">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="c8398-107">Ambari è incluso nei cluster HDInsight che usano il sistema operativo Linux.</span><span class="sxs-lookup"><span data-stu-id="c8398-107">Ambari is included on HDInsight clusters that use the Linux operating system.</span></span> <span data-ttu-id="c8398-108">È possibile usare Ambari per monitorare il cluster e apportare modifiche alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="c8398-108">You can use Ambari to monitor the cluster and make configuration changes.</span></span>

## <span data-ttu-id="c8398-109"><a id="whatis"></a>Informazioni su Ambari</span><span class="sxs-lookup"><span data-stu-id="c8398-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="c8398-110">[Apache Ambari](http://ambari.apache.org) fornisce l'interfaccia utente Web che può essere utilizzata per il provisioning, la gestione e il monitoraggio dei cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c8398-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used to provision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="c8398-111">Gli sviluppatori possono integrare queste funzionalità nelle applicazioni usando le [API REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="c8398-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="c8398-112">Ambari viene fornito per impostazione predefinita con i cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="c8398-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-to-use-the-ambari-rest-api"></a><span data-ttu-id="c8398-113">Come usare l'API REST Ambari</span><span class="sxs-lookup"><span data-stu-id="c8398-113">How to use the Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8398-114">Le informazioni e gli esempi descritti in questo documento richiedono un cluster HDInsight che usa il sistema operativo Linux.</span><span class="sxs-lookup"><span data-stu-id="c8398-114">The information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="c8398-115">Per altre informazioni, vedere [Guida introduttiva di HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c8398-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="c8398-116">In questo documento vengono descritti gli esempi per Bourne shell (bash) e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8398-116">The examples in this document are provided for both the Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="c8398-117">Gli esempi bash sono stati testati con GNU bash 4.3.11 ma dovrebbero funzionare anche con altre shell Unix.</span><span class="sxs-lookup"><span data-stu-id="c8398-117">The bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="c8398-118">Gli esempi PowerShell sono stati testati con PowerShell 5.0 ma dovrebbero funzionare anche con PowerShell 3.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="c8398-118">The PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="c8398-119">Se si usa __Bourne shell__ (bash) è necessario disporre di:</span><span class="sxs-lookup"><span data-stu-id="c8398-119">If using the __Bourne shell__ (Bash), you must have the following installed:</span></span>

* <span data-ttu-id="c8398-120">[cURL](http://curl.haxx.se/): cURL è un'utilità che può essere usata per lavorare con le API REST dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="c8398-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used to work with REST APIs from the command line.</span></span> <span data-ttu-id="c8398-121">In questo documento viene usata per comunicare con l'API REST Ambari.</span><span class="sxs-lookup"><span data-stu-id="c8398-121">In this document, it is used to communicate with the Ambari REST API.</span></span>

<span data-ttu-id="c8398-122">Sia con bash che con PowerShell è necessario che sia installato anche [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="c8398-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="c8398-123">Jq è un'utilità per lavorare con documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="c8398-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="c8398-124">Viene usata in **tutti** gli esempi bash e in **uno** degli esempi PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8398-124">It is used in **all** the Bash examples, and **one** of the PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="c8398-125">URI di base per l'API REST Ambari</span><span class="sxs-lookup"><span data-stu-id="c8398-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="c8398-126">L'URI di base per l'API REST Ambari in HDInsight è https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, dove **CLUSTERNAME** è il nome del cluster in uso.</span><span class="sxs-lookup"><span data-stu-id="c8398-126">The base URI for the Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8398-127">A differenza delle altre occorrenze nell'URI, nel nome del cluster nella parte del nome di dominio completo (FQDN) dell'URI (CLUSTERNAME.azurehdinsight.net) non viene fatta distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="c8398-127">While the cluster name in the fully qualified domain name (FQDN) part of the URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in the URI are case-sensitive.</span></span> <span data-ttu-id="c8398-128">Ad esempio, se il cluster è denominato `MyCluster`, son validi gli URI seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8398-128">For example, if your cluster is named `MyCluster`, the following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="c8398-129">Gli URI seguenti restituiscono un errore perché nella seconda occorrenza del nome non vengono usate le maiuscole/minuscole corrette.</span><span class="sxs-lookup"><span data-stu-id="c8398-129">The following URIs return an error because the second occurrence of the name is not the correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="c8398-130">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="c8398-130">Authentication</span></span>

<span data-ttu-id="c8398-131">La connessione ad Ambari su HDInsight richiede HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c8398-131">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="c8398-132">Usare il nome dell'account amministratore (il valore predefinito è **admin**) e la password forniti durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-132">Use the admin account name (the default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="c8398-133">Esempi: autenticazione e analisi di JSON</span><span class="sxs-lookup"><span data-stu-id="c8398-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="c8398-134">Gli esempi seguenti illustrano come effettuare una richiesta GET all'API REST Ambari di base:</span><span class="sxs-lookup"><span data-stu-id="c8398-134">The following examples demonstrate how to make a GET request against the base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="c8398-135">Gli esempi bash in questo documento partono dai presupposti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8398-135">The Bash examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="c8398-136">Il nome di accesso per il cluster è il valore predefinito di `admin`.</span><span class="sxs-lookup"><span data-stu-id="c8398-136">The login name for the cluster is the default value of `admin`.</span></span>
> * <span data-ttu-id="c8398-137">`$PASSWORD` contiene la password per il comando di accesso di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c8398-137">`$PASSWORD` contains the password for the HDInsight login command.</span></span> <span data-ttu-id="c8398-138">È possibile impostare questo valore usando `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="c8398-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="c8398-139">`$CLUSTERNAME` contiene il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-139">`$CLUSTERNAME` contains the name of the cluster.</span></span> <span data-ttu-id="c8398-140">È possibile impostare questo valore usando `set CLUSTERNAME='clustername'`</span><span class="sxs-lookup"><span data-stu-id="c8398-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="c8398-141">Gli esempi PowerShell in questo documento partono dai presupposti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8398-141">The PowerShell examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="c8398-142">`$creds` è un oggetto credenziale che contiene la password e l'accesso dell'amministratore per il cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-142">`$creds` is a credential object that contains the admin login and password for the cluster.</span></span> <span data-ttu-id="c8398-143">È possibile impostare questo valore usando `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` e specificando le credenziali quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="c8398-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` and providing the credentials when prompted.</span></span>
> * <span data-ttu-id="c8398-144">`$clusterName` è una stringa che contiene il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-144">`$clusterName` is a string that contains the name of the cluster.</span></span> <span data-ttu-id="c8398-145">È possibile impostare questo valore usando `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="c8398-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="c8398-146">Entrambi gli esempi restituiscono un documento JSON che inizia con informazioni simili a quelle nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c8398-146">Both examples return a JSON document that begins with information similar to the following example:</span></span>

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a><span data-ttu-id="c8398-147">Analisi dei dati JSON</span><span class="sxs-lookup"><span data-stu-id="c8398-147">Parsing JSON data</span></span>

<span data-ttu-id="c8398-148">L'esempio seguente usa `jq` per analizzare il documento di risposta JSON e visualizzare solo le informazioni `health_report` dai risultati.</span><span class="sxs-lookup"><span data-stu-id="c8398-148">The following example uses `jq` to parse the JSON response document and display only the `health_report` information from the results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="c8398-149">PowerShell 3.0 e versioni successive mette a disposizione il cmdlet `ConvertFrom-Json`, che converte il documento JSON in un oggetto più facile da usare da PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8398-149">PowerShell 3.0 and higher provides the `ConvertFrom-Json` cmdlet, which converts the JSON document into an object that is easier to work with from PowerShell.</span></span> <span data-ttu-id="c8398-150">L'esempio seguente usa `ConvertFrom-Json` per visualizzare solo le informazioni `health_report` dai risultati.</span><span class="sxs-lookup"><span data-stu-id="c8398-150">The following example uses `ConvertFrom-Json` to display only the `health_report` information from the results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="c8398-151">Anche se nella maggior parte degli esempi in questo documento viene usato `ConvertFrom-Json` per visualizzare gli elementi del documento di risposta, l'esempio sull'[aggiornamento della configurazione di Ambari](#example-update-ambari-configuration) usa jq.</span><span class="sxs-lookup"><span data-stu-id="c8398-151">While most examples in this document use `ConvertFrom-Json` to display elements from the response document, the [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="c8398-152">Jq viene usato in questo esempio per creare un nuovo modello dal documento di risposta JSON.</span><span class="sxs-lookup"><span data-stu-id="c8398-152">Jq is used in this example to construct a new template from the JSON response document.</span></span>

<span data-ttu-id="c8398-153">Per informazioni tecniche complete sull'API REST, vedere la pagina relativa alle [informazioni di riferimento per l'API Ambari V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="c8398-153">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-the-fqdn-of-cluster-nodes"></a><span data-ttu-id="c8398-154">Esempio: Ottenere il nome di dominio completo dei nodi del cluster</span><span class="sxs-lookup"><span data-stu-id="c8398-154">Example: Get the FQDN of cluster nodes</span></span>

<span data-ttu-id="c8398-155">Quando si usa HDInsight, potrebbe essere necessario conoscere il nome di dominio completo di un nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-155">When working with HDInsight, you may need to know the fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="c8398-156">È possibile recuperare con facilità l'FQDN per i diversi nodi del cluster usando gli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8398-156">You can easily retrieve the FQDN for the various nodes in the cluster using the following examples:</span></span>

* <span data-ttu-id="c8398-157">**Tutti i nodi**</span><span class="sxs-lookup"><span data-stu-id="c8398-157">**All nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* <span data-ttu-id="c8398-158">**Nodi head**</span><span class="sxs-lookup"><span data-stu-id="c8398-158">**Head nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="c8398-159">**Nodi di lavoro**</span><span class="sxs-lookup"><span data-stu-id="c8398-159">**Worker nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="c8398-160">**Nodi Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="c8398-160">**Zookeeper nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-the-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="c8398-161">Esempio: ottenere l'indirizzo IP interno dei nodi del cluster</span><span class="sxs-lookup"><span data-stu-id="c8398-161">Example: Get the internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8398-162">Gli indirizzi IP restituiti dagli esempi in questa sezione non sono direttamente accessibili tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="c8398-162">The IP addresses returned by the examples in this section are not directly accessible over the internet.</span></span> <span data-ttu-id="c8398-163">Sono accessibili solo all'interno della rete virtuale di Azure che contiene il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c8398-163">They are only accessible within the Azure Virtual Network that contains the HDInsight cluster.</span></span>
>
> <span data-ttu-id="c8398-164">Per altre informazioni sull'uso di HDInsight e delle reti virtuali vedere [Estendere le funzionalità di HDInsight usando una rete virtuale di Azure personalizzata](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="c8398-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="c8398-165">Per trovare l'indirizzo IP, è necessario conoscere il nome di dominio completo (FQDN) interno dei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-165">To find the IP address, you must know the internal fully qualified domain name (FQDN) of the cluster nodes.</span></span> <span data-ttu-id="c8398-166">Quando è stato ottenuto l'FQDN è possibile ottenere l'indirizzo IP dell'host.</span><span class="sxs-lookup"><span data-stu-id="c8398-166">Once you have the FQDN, you can then get the IP address of the host.</span></span> <span data-ttu-id="c8398-167">Negli esempi seguenti per prima cosa viene effettuata una query in Ambari per ottenere l'FQDN di tutti i nodi host, poi viene effettuata un'altra query in Ambari per ottenere l'indirizzo IP di ogni host.</span><span class="sxs-lookup"><span data-stu-id="c8398-167">The following examples first query Ambari for the FQDN of all the host nodes, then query Ambari for the IP address of each host.</span></span>

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-the-default-storage"></a><span data-ttu-id="c8398-168">Esempio: ottenere la risorsa di archiviazione predefinita</span><span class="sxs-lookup"><span data-stu-id="c8398-168">Example: Get the default storage</span></span>

<span data-ttu-id="c8398-169">Quando si crea un cluster HDInsight è necessario usare un account di archiviazione di Azure oppure Data Lake Store come risorsa di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as the default storage for the cluster.</span></span> <span data-ttu-id="c8398-170">È possibile usare Ambari per recuperare queste informazioni dopo la creazione del cluster,</span><span class="sxs-lookup"><span data-stu-id="c8398-170">You can use Ambari to retrieve this information after the cluster has been created.</span></span> <span data-ttu-id="c8398-171">ad esempio se si desidera leggere o scrivere dati nel contenitore all'esterno di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c8398-171">For example, if you want to read/write data to the container outside HDInsight.</span></span>

<span data-ttu-id="c8398-172">Negli esempi seguenti viene recuperata la configurazione di archiviazione predefinita dal cluster:</span><span class="sxs-lookup"><span data-stu-id="c8398-172">The following examples retrieve the default storage configuration from the cluster:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> <span data-ttu-id="c8398-173">Questi esempi restituiscono la prima configurazione applicata al server (`service_config_version=1`) che contiene queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="c8398-173">These examples return the first configuration applied to the server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="c8398-174">Se si recupera un valore che è stato modificato dopo la creazione del cluster, potrebbe essere necessario elencare le versioni della configurazione e recuperare la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="c8398-174">If you retrieve a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span></span>

<span data-ttu-id="c8398-175">Il valore restituito è simile a uno degli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8398-175">The return value is similar to one of the following examples:</span></span>

* <span data-ttu-id="c8398-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - Questo valore indica che il cluster usa un account di archiviazione di Azure come risorsa di archiviazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c8398-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that the cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="c8398-177">Il valore `ACCOUNTNAME` è il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c8398-177">The `ACCOUNTNAME` value is the name of the storage account.</span></span> <span data-ttu-id="c8398-178">La porzione `CONTAINER` corrisponde al nome del contenitore BLOB nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c8398-178">The `CONTAINER` portion is the name of the blob container in the storage account.</span></span> <span data-ttu-id="c8398-179">Il contenitore è la radice della risorsa di archiviazione compatibile con HDFS per il cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-179">The container is the root of the HDFS compatible storage for the cluster.</span></span>

* <span data-ttu-id="c8398-180">`adl://home` - Questo valore indica che il cluster usa Azure Data Lake Store come risorsa di archiviazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c8398-180">`adl://home` - This value indicates that the cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="c8398-181">Per trovare il nome dell'account Data Lake Store, usare gli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8398-181">To find the Data Lake Store account name, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    <span data-ttu-id="c8398-182">Il valore restituito è simile a `ACCOUNTNAME.azuredatalakestore.net`, dove `ACCOUNTNAME` è il nome dell'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c8398-182">The return value is similar to `ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is the name of the Data Lake Store account.</span></span>

    <span data-ttu-id="c8398-183">Per trovare la directory all'interno di Data Lake Store contenente la risorsa di archiviazione per il cluster, usare gli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8398-183">To find the directory within Data Lake Store that contains the storage for the cluster, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    <span data-ttu-id="c8398-184">Il valore restituito è simile a `/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="c8398-184">The return value is similar to `/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="c8398-185">Questo valore è un percorso all'interno dell'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c8398-185">This value is a path within the Data Lake Store account.</span></span> <span data-ttu-id="c8398-186">Questo percorso è la radice del file system compatibile con HDFS per il cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-186">This path is the root of the HDFS compatible file system for the cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="c8398-187">Il cmdlet `Get-AzureRmHDInsightCluster` messo a disposizione da [Azure PowerShell](/powershell/azure/overview) restituisce anche le informazioni di archiviazione per il cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-187">The `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns the storage information for the cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="c8398-188">Esempio: ottenere una configurazione</span><span class="sxs-lookup"><span data-stu-id="c8398-188">Example: Get configuration</span></span>

1. <span data-ttu-id="c8398-189">Consente di ottenere le configurazioni disponibili per il cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-189">Get the configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="c8398-190">L'esempio restituisce un documento JSON contenente la configurazione corrente, identificata dal valore *tag*, per i componenti installati nel cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-190">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="c8398-191">L'esempio di seguito rappresenta un estratto dei dati restituiti da un tipo di cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="c8398-191">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. <span data-ttu-id="c8398-192">Consente di ottenere la configurazione del componente a cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="c8398-192">Get the configuration for the component that you are interested in.</span></span> <span data-ttu-id="c8398-193">Nell'esempio seguente, sostituire `INITIAL` con il valore del tag restituito dalla richiesta precedente.</span><span class="sxs-lookup"><span data-stu-id="c8398-193">In the following example, replace `INITIAL` with the tag value returned from the previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="c8398-194">Questo esempio restituisce un documento JSON che contiene la configurazione corrente del componente `core-site`.</span><span class="sxs-lookup"><span data-stu-id="c8398-194">This example returns a JSON document containing the current configuration for the `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="c8398-195">Esempio: aggiornare la configurazione</span><span class="sxs-lookup"><span data-stu-id="c8398-195">Example: Update configuration</span></span>

1. <span data-ttu-id="c8398-196">Ottenere la configurazione corrente, archiviata da Ambari come "configurazione desiderata":</span><span class="sxs-lookup"><span data-stu-id="c8398-196">Get the current configuration, which Ambari stores as the "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="c8398-197">L'esempio restituisce un documento JSON contenente la configurazione corrente, identificata dal valore *tag*, per i componenti installati nel cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-197">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="c8398-198">L'esempio di seguito rappresenta un estratto dei dati restituiti da un tipo di cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="c8398-198">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    <span data-ttu-id="c8398-199">È necessario copiare il nome del componente, ad esempio **spark\_thrift\_sparkconf**, e il valore **tag** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="c8398-199">From this list, you need to copy the name of the component (for example, **spark\_thrift\_sparkconf** and the **tag** value.</span></span>

2. <span data-ttu-id="c8398-200">Recuperare la configurazione del componente e del tag usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8398-200">Retrieve the configuration for the component and tag by using the following commands:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > <span data-ttu-id="c8398-201">Sostituire **spark-thrift-sparkconf** e **INITIAL** con il componente e il tag di cui si vuole recuperare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="c8398-201">Replace **spark-thrift-sparkconf** and **INITIAL** with the component and tag that you want to retrieve the configuration for.</span></span>
   
    <span data-ttu-id="c8398-202">Jq viene usato per trasformare i dati recuperati da HDInsight in un nuovo modello di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c8398-202">Jq is used to turn the data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="c8398-203">In particolare, questi esempi eseguono le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8398-203">Specifically, these examples perform the following actions:</span></span>
   
    * <span data-ttu-id="c8398-204">Crea un valore univoco contenente la stringa "version" e la data, che viene archiviato in `newtag`.</span><span class="sxs-lookup"><span data-stu-id="c8398-204">Creates a unique value containing the string "version" and the date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="c8398-205">Crea un documento radice per la nuova configurazione desiderata.</span><span class="sxs-lookup"><span data-stu-id="c8398-205">Creates a root document for the new desired configuration.</span></span>

    * <span data-ttu-id="c8398-206">Ottiene i contenuti della matrice `.items[]` e li aggiunge sotto l'elemento **desired_config**.</span><span class="sxs-lookup"><span data-stu-id="c8398-206">Gets the contents of the `.items[]` array and adds it under the **desired_config** element.</span></span>

    * <span data-ttu-id="c8398-207">Elimina gli elementi `href`, `version` e `Config` perché non sono necessari per l'invio di una nuova configurazione.</span><span class="sxs-lookup"><span data-stu-id="c8398-207">Deletes the `href`, `version`, and `Config` elements, as these elements aren't needed to submit a new configuration.</span></span>

    * <span data-ttu-id="c8398-208">Aggiunge un elemento `tag` con un valore di `version#################`.</span><span class="sxs-lookup"><span data-stu-id="c8398-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="c8398-209">La parte numerica si basa sulla data corrente.</span><span class="sxs-lookup"><span data-stu-id="c8398-209">The numeric portion is based on the current date.</span></span> <span data-ttu-id="c8398-210">Ogni configurazione deve avere un tag univoco.</span><span class="sxs-lookup"><span data-stu-id="c8398-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="c8398-211">Infine i dati vengono salvati nel documento `newconfig.json`.</span><span class="sxs-lookup"><span data-stu-id="c8398-211">Finally, the data is saved to the `newconfig.json` document.</span></span> <span data-ttu-id="c8398-212">La struttura del documento deve essere simile all'esempio di seguito:</span><span class="sxs-lookup"><span data-stu-id="c8398-212">The document structure should appear similar to the following example:</span></span>
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. <span data-ttu-id="c8398-213">Aprire il documento `newconfig.json` e modificare o aggiungere i valori nell'oggetto `properties`.</span><span class="sxs-lookup"><span data-stu-id="c8398-213">Open the `newconfig.json` document and modify/add values in the `properties` object.</span></span> <span data-ttu-id="c8398-214">L'esempio seguente modifica il valore di `"spark.yarn.am.memory"` da `"1g"` a `"3g"`.</span><span class="sxs-lookup"><span data-stu-id="c8398-214">The following example changes the value of `"spark.yarn.am.memory"` from `"1g"` to `"3g"`.</span></span> <span data-ttu-id="c8398-215">Aggiunge anche `"spark.kryoserializer.buffer.max"` con un valore di `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="c8398-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="c8398-216">Al termine delle modifiche, salvare il file.</span><span class="sxs-lookup"><span data-stu-id="c8398-216">Save the file once you are done making modifications.</span></span>

4. <span data-ttu-id="c8398-217">Usare i comandi seguenti per inviare la configurazione aggiornata ad Ambari.</span><span class="sxs-lookup"><span data-stu-id="c8398-217">Use the following commands to submit the updated configuration to Ambari.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    <span data-ttu-id="c8398-218">Questi comandi inviano il contenuto del file **newconfig.json** al cluster come nuova configurazione desiderata.</span><span class="sxs-lookup"><span data-stu-id="c8398-218">These commands submit the contents of the **newconfig.json** file to the cluster as the new desired configuration.</span></span> <span data-ttu-id="c8398-219">La richiesta restituisce un documento JSON.</span><span class="sxs-lookup"><span data-stu-id="c8398-219">The request returns a JSON document.</span></span> <span data-ttu-id="c8398-220">L'elemento **versionTag** di questo documento deve corrispondere alla versione inviata, mentre l'oggetto **configs** conterrà le modifiche di configurazione richieste.</span><span class="sxs-lookup"><span data-stu-id="c8398-220">The **versionTag** element in this document should match the version you submitted, and the **configs** object contains the configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="c8398-221">Esempio: Riavviare un componente del servizio</span><span class="sxs-lookup"><span data-stu-id="c8398-221">Example: Restart a service component</span></span>

<span data-ttu-id="c8398-222">A questo punto, se si osserva l'interfaccia utente di Ambari Web, il servizio Spark indicherà che è necessario il riavvio per rendere effettiva la nuova configurazione.</span><span class="sxs-lookup"><span data-stu-id="c8398-222">At this point, if you look at the Ambari web UI, the Spark service indicates that it needs to be restarted before the new configuration can take effect.</span></span> <span data-ttu-id="c8398-223">Usare la procedura seguente per riavviare il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8398-223">Use the following steps to restart the service.</span></span>

1. <span data-ttu-id="c8398-224">Usare il codice seguente per attivare la modalità di manutenzione del servizio Spark:</span><span class="sxs-lookup"><span data-stu-id="c8398-224">Use the following to enable maintenance mode for the Spark service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    <span data-ttu-id="c8398-225">Questi comandi inviano un documento JSON al server che attiva la modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="c8398-225">These commands send a JSON document to the server that turns on maintenance mode.</span></span> <span data-ttu-id="c8398-226">È possibile verificare che il servizio sia in modalità di manutenzione usando la richiesta seguente:</span><span class="sxs-lookup"><span data-stu-id="c8398-226">You can verify that the service is now in maintenance mode using the following request:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    <span data-ttu-id="c8398-227">Viene restituito il valore `ON`.</span><span class="sxs-lookup"><span data-stu-id="c8398-227">The return value is `ON`.</span></span>

2. <span data-ttu-id="c8398-228">Successivamente usare il codice seguente per disattivare il servizio:</span><span class="sxs-lookup"><span data-stu-id="c8398-228">Next, use the following to turn off the service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    <span data-ttu-id="c8398-229">La risposta restituita è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c8398-229">The response is similar to the following example:</span></span>
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > <span data-ttu-id="c8398-230">Il valore `href` restituito dall'URI usa l'indirizzo IP interno del nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-230">The `href` value returned by this URI is using the internal IP address of the cluster node.</span></span> <span data-ttu-id="c8398-231">Per usarlo dall'esterno del cluster, sostituire la parte '10.0.0.18:8080' con il nome FQDN del cluster.</span><span class="sxs-lookup"><span data-stu-id="c8398-231">To use it from outside the cluster, replace the \`10.0.0.18:8080' portion with the FQDN of the cluster.</span></span> 
    
    <span data-ttu-id="c8398-232">Il comando seguente recupera lo stato della richiesta:</span><span class="sxs-lookup"><span data-stu-id="c8398-232">The following commands retrieve the status of the request:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    <span data-ttu-id="c8398-233">La risposta `COMPLETED` indica che la richiesta è stata completata.</span><span class="sxs-lookup"><span data-stu-id="c8398-233">A response of `COMPLETED` indicates that the request has finished.</span></span>

3. <span data-ttu-id="c8398-234">Dopo aver completato la richiesta precedente, usare il codice seguente per avviare il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8398-234">Once the previous request completes, use the following to start the service.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    <span data-ttu-id="c8398-235">Il servizio ora usa la nuova configurazione.</span><span class="sxs-lookup"><span data-stu-id="c8398-235">The service is now using the new configuration.</span></span>

4. <span data-ttu-id="c8398-236">Infine, usare il codice seguente per disattivare la modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="c8398-236">Finally, use the following to turn off maintenance mode.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a><span data-ttu-id="c8398-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8398-237">Next steps</span></span>

<span data-ttu-id="c8398-238">Per informazioni tecniche complete sull'API REST, vedere la pagina relativa alle [informazioni di riferimento per l'API Ambari V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="c8398-238">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

