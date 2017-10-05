---
title: 'Gestire cluster Hadoop in HDInsight con PowerShell: Azure | Microsoft Docs'
description: "Informazioni su come eseguire attività amministrative per i cluster Hadoop in HDInsight tramite Azure PowerShell."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c47dabd7c4aa4ba0be08c419989e536711f03677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="d48f0-103">Gestire cluster Hadoop in HDInsight tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d48f0-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="d48f0-104">Azure PowerShell è un ambiente di scripting potente che può essere usato per controllare e automatizzare la distribuzione e la gestione dei carichi di lavoro in Azure.</span><span class="sxs-lookup"><span data-stu-id="d48f0-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="d48f0-105">In questo articolo verrà illustrato come gestire cluster Hadoop in Azure HDInsight usando una console di Azure PowerShell locale tramite Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d48f0-105">In this article, you will learn how to manage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through the use of Windows PowerShell.</span></span> <span data-ttu-id="d48f0-106">Per l'elenco dei cmdlet PowerShell per HDInsight, vedere [Documentazione di riferimento di cmdlet di HDInsight][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="d48f0-106">For the list of the HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="d48f0-107">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="d48f0-107">**Prerequisites**</span></span>

<span data-ttu-id="d48f0-108">Per eseguire le procedure descritte nell'articolo è necessario:</span><span class="sxs-lookup"><span data-stu-id="d48f0-108">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="d48f0-109">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d48f0-109">**An Azure subscription**.</span></span> <span data-ttu-id="d48f0-110">Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d48f0-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="d48f0-111">Installare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d48f0-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="d48f0-112">Se è installato Azure PowerShell versione 0.9x, è necessario disinstallarlo prima di installare una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="d48f0-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="d48f0-113">Per controllare la versione di PowerShell installata:</span><span class="sxs-lookup"><span data-stu-id="d48f0-113">To check the version of the installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="d48f0-114">Per disinstallare la versione precedente, eseguire Programmi e Funzionalità nel Pannello di controllo.</span><span class="sxs-lookup"><span data-stu-id="d48f0-114">To uninstall the older version, run Programs and Features in the control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="d48f0-115">Creare i cluster</span><span class="sxs-lookup"><span data-stu-id="d48f0-115">Create clusters</span></span>
<span data-ttu-id="d48f0-116">Vedere [Creare cluster basati su Linux in HDInsight tramite Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="d48f0-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="d48f0-117">Elencare cluster</span><span class="sxs-lookup"><span data-stu-id="d48f0-117">List clusters</span></span>
<span data-ttu-id="d48f0-118">Usare il comando seguente per visualizzare l'elenco di tutti i cluster nella sottoscrizione corrente:</span><span class="sxs-lookup"><span data-stu-id="d48f0-118">Use the following command to list all clusters in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="d48f0-119">Mostrare cluster</span><span class="sxs-lookup"><span data-stu-id="d48f0-119">Show cluster</span></span>
<span data-ttu-id="d48f0-120">Usare il comando seguente per visualizzare i dettagli di un cluster specifico nella sottoscrizione corrente:</span><span class="sxs-lookup"><span data-stu-id="d48f0-120">Use the following command to show details of a specific cluster in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="d48f0-121">Eliminare cluster</span><span class="sxs-lookup"><span data-stu-id="d48f0-121">Delete clusters</span></span>
<span data-ttu-id="d48f0-122">Utilizzare il comando seguente per eliminare un cluster:</span><span class="sxs-lookup"><span data-stu-id="d48f0-122">Use the following command to delete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="d48f0-123">È inoltre possibile eliminare un cluster rimuovendo il gruppo di risorse che lo contiene.</span><span class="sxs-lookup"><span data-stu-id="d48f0-123">You can also delete a cluster by removing the resource group that contains the cluster.</span></span> <span data-ttu-id="d48f0-124">Tenere presente che questa operazione eliminerà tutte le risorse nel gruppo, compreso l’account di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="d48f0-124">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="d48f0-125">Ridimensionare i cluster</span><span class="sxs-lookup"><span data-stu-id="d48f0-125">Scale clusters</span></span>
<span data-ttu-id="d48f0-126">La funzionalità di scalabilità del cluster consente di modificare il numero di nodi del ruolo di lavoro usati da un cluster in esecuzione in Azure HDInsight senza dover ricreare il cluster.</span><span class="sxs-lookup"><span data-stu-id="d48f0-126">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="d48f0-127">Sono supportati solo i cluster con HDInsight versione 3.1.3 o successive.</span><span class="sxs-lookup"><span data-stu-id="d48f0-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="d48f0-128">Se non si è certi della versione del cluster, è possibile controllare la pagina delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="d48f0-128">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="d48f0-129">Vedere [Elencare e visualizzare i cluster](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="d48f0-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="d48f0-130">Questa sezione descrive l'impatto della modifica del numero di nodi dati per ogni tipo di cluster supportato da HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d48f0-130">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="d48f0-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="d48f0-131">Hadoop</span></span>

    <span data-ttu-id="d48f0-132">È possibile aumentare facilmente il numero di nodi del ruolo di lavoro in un cluster Hadoop in esecuzione senza conseguenze per eventuali processi in sospeso o in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d48f0-132">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="d48f0-133">È inoltre possibile inviare nuovi processi mentre è in corso l'operazione.</span><span class="sxs-lookup"><span data-stu-id="d48f0-133">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="d48f0-134">Gli errori in un'operazione di scalabilità vengono gestiti in modo che il cluster rimanga sempre in uno stato funzionale.</span><span class="sxs-lookup"><span data-stu-id="d48f0-134">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="d48f0-135">Quando un cluster Hadoop viene ridimensionato riducendo il numero di nodi dati, alcuni dei servizi del cluster vengono riavviati.</span><span class="sxs-lookup"><span data-stu-id="d48f0-135">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="d48f0-136">In questo modo, tutti i processi in esecuzione e in attesa daranno esito negativo dopo il completamento dell'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="d48f0-136">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="d48f0-137">È tuttavia possibile inviare nuovamente i processi una volta completata l'operazione.</span><span class="sxs-lookup"><span data-stu-id="d48f0-137">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="d48f0-138">HBase</span><span class="sxs-lookup"><span data-stu-id="d48f0-138">HBase</span></span>

    <span data-ttu-id="d48f0-139">È possibile aggiungere o rimuovere facilmente nodi nel cluster HBase mentre è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d48f0-139">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="d48f0-140">I server a livello di area vengono bilanciati automaticamente entro pochi minuti dal completamento dell'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="d48f0-140">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="d48f0-141">È tuttavia possibile anche bilanciare manualmente i server a livello di area accedendo al nodo head del cluster ed eseguendo i comandi seguenti da una finestra del prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="d48f0-141">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="d48f0-142">Storm</span><span class="sxs-lookup"><span data-stu-id="d48f0-142">Storm</span></span>

    <span data-ttu-id="d48f0-143">È possibile aggiungere o rimuovere facilmente nodi dati dal cluster Storm mentre è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d48f0-143">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="d48f0-144">Tuttavia, dopo il completamento dell'operazione di ridimensionamento, è necessario bilanciare nuovamente la topologia.</span><span class="sxs-lookup"><span data-stu-id="d48f0-144">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="d48f0-145">A tale scopo, è possibile scegliere tra due opzioni:</span><span class="sxs-lookup"><span data-stu-id="d48f0-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="d48f0-146">Interfaccia utente Web di Storm</span><span class="sxs-lookup"><span data-stu-id="d48f0-146">Storm web UI</span></span>
  * <span data-ttu-id="d48f0-147">Interfaccia della riga di comando (CLI)</span><span class="sxs-lookup"><span data-stu-id="d48f0-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="d48f0-148">Per altre informazioni, fare riferimento alla [documentazione su Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) .</span><span class="sxs-lookup"><span data-stu-id="d48f0-148">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="d48f0-149">L'interfaccia utente Web di Storm è disponibile nel cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d48f0-149">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![Ribilanciamento scala di HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="d48f0-151">Di seguito viene fornito un esempio d'uso del comando CLI per ribilanciare la topologia di Storm:</span><span class="sxs-lookup"><span data-stu-id="d48f0-151">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="d48f0-152">Per modificare le dimensioni del cluster Hadoop mediante Azure PowerShell, eseguire il comando seguente da un computer client:</span><span class="sxs-lookup"><span data-stu-id="d48f0-152">To change the Hadoop cluster size by using Azure PowerShell, run the following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="d48f0-153">Concedere/Revocare l'accesso</span><span class="sxs-lookup"><span data-stu-id="d48f0-153">Grant/revoke access</span></span>
<span data-ttu-id="d48f0-154">Per i cluster HDInsight sono disponibili i servizi Web HTTP seguenti (tutti con endpoint RESTful):</span><span class="sxs-lookup"><span data-stu-id="d48f0-154">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="d48f0-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="d48f0-155">ODBC</span></span>
* <span data-ttu-id="d48f0-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="d48f0-156">JDBC</span></span>
* <span data-ttu-id="d48f0-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="d48f0-157">Ambari</span></span>
* <span data-ttu-id="d48f0-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="d48f0-158">Oozie</span></span>
* <span data-ttu-id="d48f0-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="d48f0-159">Templeton</span></span>

<span data-ttu-id="d48f0-160">Per impostazione predefinita, a questi servizi è concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="d48f0-160">By default, these services are granted for access.</span></span> <span data-ttu-id="d48f0-161">L'accesso può essere revocato/concesso,</span><span class="sxs-lookup"><span data-stu-id="d48f0-161">You can revoke/grant the access.</span></span> <span data-ttu-id="d48f0-162">Per revocare:</span><span class="sxs-lookup"><span data-stu-id="d48f0-162">To revoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="d48f0-163">Per concedere:</span><span class="sxs-lookup"><span data-stu-id="d48f0-163">To grant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter the Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter the HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="d48f0-164">La concessione/revoca dell'accesso implica la reimpostazione del nome utente e della password del cluster.</span><span class="sxs-lookup"><span data-stu-id="d48f0-164">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
>
>

<span data-ttu-id="d48f0-165">Questa operazione può essere eseguita anche tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="d48f0-165">This can also be done via the Portal.</span></span> <span data-ttu-id="d48f0-166">Vedere l'articolo su come [amministrare HDInsight con il portale di Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="d48f0-166">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="d48f0-167">Aggiornare le credenziali utente HTTP</span><span class="sxs-lookup"><span data-stu-id="d48f0-167">Update HTTP user credentials</span></span>
<span data-ttu-id="d48f0-168">È la stessa procedura di [Concedere/revocare l'accesso HTTP](#grant/revoke-access). Se al cluster è stato concesso l'accesso HTTP, è necessario prima revocarlo.</span><span class="sxs-lookup"><span data-stu-id="d48f0-168">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="d48f0-169">E quindi concedere l'accesso con le nuove credenziali utente HTTP.</span><span class="sxs-lookup"><span data-stu-id="d48f0-169">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="d48f0-170">Trovare l'account di archiviazione predefinito</span><span class="sxs-lookup"><span data-stu-id="d48f0-170">Find the default storage account</span></span>
<span data-ttu-id="d48f0-171">Il seguente script di Powershell dimostra come ottenere il nome dell’account di archiviazione predefinito e la chiave dell’account di archiviazione predefinita per un cluster.</span><span class="sxs-lookup"><span data-stu-id="d48f0-171">The following Powershell script demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-the-resource-group"></a><span data-ttu-id="d48f0-172">Trovare il gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="d48f0-172">Find the resource group</span></span>
<span data-ttu-id="d48f0-173">Nella modalità Resource Manager ogni cluster HDInsight appartiene a un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d48f0-173">In the Resource Manager mode, each HDInsight cluster belongs to an Azure resource group.</span></span>  <span data-ttu-id="d48f0-174">Trovare il gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="d48f0-174">To find the resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="d48f0-175">Inviare i processi</span><span class="sxs-lookup"><span data-stu-id="d48f0-175">Submit jobs</span></span>
<span data-ttu-id="d48f0-176">**Inviare processi MapReduce**</span><span class="sxs-lookup"><span data-stu-id="d48f0-176">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="d48f0-177">Vedere [esempi di MapReduce di Hadoop in HDInsight basato su Windows](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d48f0-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="d48f0-178">**Inviare processi Hive**</span><span class="sxs-lookup"><span data-stu-id="d48f0-178">**To submit Hive jobs**</span></span>

<span data-ttu-id="d48f0-179">Vedere [Esecuzione di query Hive tramite PowerShell](hdinsight-hadoop-use-hive-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="d48f0-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="d48f0-180">**Inviare processi Pig**</span><span class="sxs-lookup"><span data-stu-id="d48f0-180">**To submit Pig jobs**</span></span>

<span data-ttu-id="d48f0-181">Vedere [Eseguire processi Pig mediante PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d48f0-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="d48f0-182">**Inviare processi Sqoop**</span><span class="sxs-lookup"><span data-stu-id="d48f0-182">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="d48f0-183">Vedere [Usare Sqoop con Hadoop in HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="d48f0-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="d48f0-184">**Inviare processi Oozie**</span><span class="sxs-lookup"><span data-stu-id="d48f0-184">**To submit Oozie jobs**</span></span>

<span data-ttu-id="d48f0-185">Vedere [Usare Oozie con Hadoop per definire ed eseguire un flusso di lavoro in HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="d48f0-185">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="d48f0-186">Caricare dati nell'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="d48f0-186">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="d48f0-187">Vedere[Caricare dati in HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="d48f0-187">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="d48f0-188">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d48f0-188">See Also</span></span>
* <span data-ttu-id="d48f0-189">[Documentazione di riferimento dei cmdlet di HDInsight][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="d48f0-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="d48f0-190">[Amministrare HDInsight con il portale di Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="d48f0-190">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="d48f0-191">[Amministrare HDInsight con l'interfaccia della riga di comando][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="d48f0-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="d48f0-192">[Creare cluster HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="d48f0-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="d48f0-193">[Caricare dati in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="d48f0-193">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="d48f0-194">[Inviare processi Hadoop a livello di codice][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="d48f0-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="d48f0-195">[Introduzione ad Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d48f0-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
