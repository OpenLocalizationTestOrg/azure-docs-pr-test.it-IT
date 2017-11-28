---
title: cluster aaaManage Hadoop in HDInsight con PowerShell - Azure | Documenti Microsoft
description: "Informazioni su come attività amministrative tooperform per hello cluster Hadoop in HDInsight con Azure PowerShell."
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
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="b2a5d-103">Gestire cluster Hadoop in HDInsight tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2a5d-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="b2a5d-104">Azure PowerShell è un ambiente di scripting potente che è possibile utilizzare toocontrol e automatizzare la distribuzione di hello e la gestione dei carichi di lavoro in Azure.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="b2a5d-105">In questo articolo si apprenderà come toomanage di cluster Hadoop in HDInsight di Azure tramite una console di Azure PowerShell locale tramite hello utilizzato Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-105">In this article, you will learn how toomanage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through hello use of Windows PowerShell.</span></span> <span data-ttu-id="b2a5d-106">Per hello l'elenco dei cmdlet HDInsight PowerShell hello, vedere [riferimento ai cmdlet di HDInsight][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="b2a5d-106">For hello list of hello HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="b2a5d-107">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="b2a5d-107">**Prerequisites**</span></span>

<span data-ttu-id="b2a5d-108">Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-108">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="b2a5d-109">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-109">**An Azure subscription**.</span></span> <span data-ttu-id="b2a5d-110">Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b2a5d-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="b2a5d-111">Installare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2a5d-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="b2a5d-112">Se è installato Azure PowerShell versione 0.9x, è necessario disinstallarlo prima di installare una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="b2a5d-113">versione di hello toocheck di hello installato PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-113">toocheck hello version of hello installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="b2a5d-114">toouninstall hello versione meno recente, eseguire programmi e funzionalità nel Pannello di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-114">toouninstall hello older version, run Programs and Features in hello control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="b2a5d-115">Creare i cluster</span><span class="sxs-lookup"><span data-stu-id="b2a5d-115">Create clusters</span></span>
<span data-ttu-id="b2a5d-116">Vedere [Creare cluster basati su Linux in HDInsight tramite Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="b2a5d-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="b2a5d-117">Elencare cluster</span><span class="sxs-lookup"><span data-stu-id="b2a5d-117">List clusters</span></span>
<span data-ttu-id="b2a5d-118">Utilizzare hello seguente toolist comando tutti i cluster nella sottoscrizione corrente hello:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-118">Use hello following command toolist all clusters in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="b2a5d-119">Mostrare cluster</span><span class="sxs-lookup"><span data-stu-id="b2a5d-119">Show cluster</span></span>
<span data-ttu-id="b2a5d-120">Utilizzare i seguenti comandi tooshow dettagli di un cluster specifico nella sottoscrizione corrente hello hello:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-120">Use hello following command tooshow details of a specific cluster in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="b2a5d-121">Eliminare cluster</span><span class="sxs-lookup"><span data-stu-id="b2a5d-121">Delete clusters</span></span>
<span data-ttu-id="b2a5d-122">Utilizzare hello successivo comando toodelete un cluster:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-122">Use hello following command toodelete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="b2a5d-123">Inoltre, è possibile eliminare un cluster tramite la rimozione di gruppo di risorse hello contenente cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-123">You can also delete a cluster by removing hello resource group that contains hello cluster.</span></span> <span data-ttu-id="b2a5d-124">Si noti, questa operazione eliminerà tutte le risorse di hello gruppo hello inclusi account di archiviazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-124">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="b2a5d-125">Ridimensionare i cluster</span><span class="sxs-lookup"><span data-stu-id="b2a5d-125">Scale clusters</span></span>
<span data-ttu-id="b2a5d-126">scalabilità funzionalità cluster di Hello consente numero hello toochange di nodi di lavoro utilizzato da un cluster che è in esecuzione in Azure HDInsight senza toore-creare cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-126">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b2a5d-127">Sono supportati solo i cluster con HDInsight versione 3.1.3 o successive.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="b2a5d-128">Se si è certi della versione di hello del cluster, è possibile controllare una pagina delle proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-128">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="b2a5d-129">Vedere [Elencare e visualizzare i cluster](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="b2a5d-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="b2a5d-130">impatto di Hello di modifica del numero di hello di nodi di dati per ogni tipo di cluster supportato da HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-130">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="b2a5d-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="b2a5d-131">Hadoop</span></span>

    <span data-ttu-id="b2a5d-132">È possibile aumentare facilmente numero hello di nodi di lavoro in un cluster Hadoop che è in esecuzione senza conseguenze per tutti i processi in sospeso o in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-132">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="b2a5d-133">È inoltre possibile avviare nuovi processi mentre è in corso hello operazione.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-133">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="b2a5d-134">Gli errori in un'operazione di ridimensionamento normalmente vengono gestiti in modo che hello cluster rimanga sempre in uno stato funzionale.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-134">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="b2a5d-135">Quando un cluster Hadoop è ridotta, riducendo il numero di hello di nodi di dati, alcuni dei servizi di hello cluster hello vengono riavviati.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-135">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="b2a5d-136">In questo modo tutti in esecuzione e in sospeso toofail processi al completamento di hello di hello l'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-136">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="b2a5d-137">È tuttavia possibile inviare di nuovo i processi di hello al termine dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-137">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="b2a5d-138">HBase</span><span class="sxs-lookup"><span data-stu-id="b2a5d-138">HBase</span></span>

    <span data-ttu-id="b2a5d-139">Senza problemi, è possibile aggiungere o rimuovere cluster HBase di nodi tooyour mentre è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-139">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="b2a5d-140">Server locali sono bilanciati automaticamente entro pochi minuti di completare l'operazione di ridimensionamento hello.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-140">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="b2a5d-141">Tuttavia, è possibile bilanciare manualmente server regionali hello accedendo toohello nodo head del cluster e in esecuzione hello seguendo i comandi da una finestra del prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-141">However, you can also manually balance hello regional servers by logging in toohello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="b2a5d-142">Storm</span><span class="sxs-lookup"><span data-stu-id="b2a5d-142">Storm</span></span>

    <span data-ttu-id="b2a5d-143">Senza problemi, è possibile aggiungere o rimuovere cluster Storm tooyour nodi di dati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-143">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="b2a5d-144">Tuttavia, dopo il completamento dell'operazione di ridimensionamento hello, sarà necessario topologia hello toorebalance.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-144">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="b2a5d-145">A tale scopo, è possibile scegliere tra due opzioni:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="b2a5d-146">Interfaccia utente Web di Storm</span><span class="sxs-lookup"><span data-stu-id="b2a5d-146">Storm web UI</span></span>
  * <span data-ttu-id="b2a5d-147">Interfaccia della riga di comando (CLI)</span><span class="sxs-lookup"><span data-stu-id="b2a5d-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="b2a5d-148">Consultare toohello [documentazione di Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-148">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="b2a5d-149">interfaccia utente web di Storm Hello è disponibile nel cluster HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-149">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![Ribilanciamento scala di HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="b2a5d-151">Di seguito è riportato un esempio come toouse hello CLI comando topologia di Storm toorebalance hello:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-151">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="b2a5d-152">hello toochange dimensioni del cluster Hadoop usando Azure PowerShell, eseguire hello comando seguente da un computer client:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-152">toochange hello Hadoop cluster size by using Azure PowerShell, run hello following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="b2a5d-153">Concedere/Revocare l'accesso</span><span class="sxs-lookup"><span data-stu-id="b2a5d-153">Grant/revoke access</span></span>
<span data-ttu-id="b2a5d-154">Cluster HDInsight sono hello (tutti questi servizi hanno endpoint REST) i servizi HTTP web seguente:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-154">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="b2a5d-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="b2a5d-155">ODBC</span></span>
* <span data-ttu-id="b2a5d-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="b2a5d-156">JDBC</span></span>
* <span data-ttu-id="b2a5d-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="b2a5d-157">Ambari</span></span>
* <span data-ttu-id="b2a5d-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="b2a5d-158">Oozie</span></span>
* <span data-ttu-id="b2a5d-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="b2a5d-159">Templeton</span></span>

<span data-ttu-id="b2a5d-160">Per impostazione predefinita, a questi servizi è concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-160">By default, these services are granted for access.</span></span> <span data-ttu-id="b2a5d-161">È possibile revocare o concedere l'accesso hello.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-161">You can revoke/grant hello access.</span></span> <span data-ttu-id="b2a5d-162">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-162">toorevoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="b2a5d-163">toogrant:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-163">toogrant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="b2a5d-164">Per concedere o revocare l'accesso hello, sarà necessario reimpostare la password e nome utente di hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-164">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="b2a5d-165">Questa operazione può anche essere eseguita tramite hello portale.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-165">This can also be done via hello Portal.</span></span> <span data-ttu-id="b2a5d-166">Vedere [HDInsight amministrare tramite hello Azure portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="b2a5d-166">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="b2a5d-167">Aggiornare le credenziali utente HTTP</span><span class="sxs-lookup"><span data-stu-id="b2a5d-167">Update HTTP user credentials</span></span>
<span data-ttu-id="b2a5d-168">È hello stessa stored procedure come [accesso Grant/revoke HTTP](#grant/revoke-access). Se il cluster hello è stata concessa hello accesso HTTP, è necessario revocare.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-168">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="b2a5d-169">E quindi concedere l'accesso di hello con nuove credenziali utente HTTP.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-169">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="b2a5d-170">Trovare l'account di archiviazione predefinito hello</span><span class="sxs-lookup"><span data-stu-id="b2a5d-170">Find hello default storage account</span></span>
<span data-ttu-id="b2a5d-171">Hello lo script di Powershell seguente viene illustrato come tooget hello Nome account di archiviazione predefinito e hello chiave account di archiviazione predefinito per un cluster.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-171">hello following Powershell script demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a><span data-ttu-id="b2a5d-172">Trovare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="b2a5d-172">Find hello resource group</span></span>
<span data-ttu-id="b2a5d-173">In modalità di gestione risorse di hello, ogni cluster HDInsight appartiene tooan gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2a5d-173">In hello Resource Manager mode, each HDInsight cluster belongs tooan Azure resource group.</span></span>  <span data-ttu-id="b2a5d-174">gruppo di risorse toofind hello:</span><span class="sxs-lookup"><span data-stu-id="b2a5d-174">toofind hello resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="b2a5d-175">Inviare i processi</span><span class="sxs-lookup"><span data-stu-id="b2a5d-175">Submit jobs</span></span>
<span data-ttu-id="b2a5d-176">**processi MapReduce toosubmit**</span><span class="sxs-lookup"><span data-stu-id="b2a5d-176">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="b2a5d-177">Vedere [esempi di MapReduce di Hadoop in HDInsight basato su Windows](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b2a5d-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="b2a5d-178">**processi Hive toosubmit**</span><span class="sxs-lookup"><span data-stu-id="b2a5d-178">**toosubmit Hive jobs**</span></span>

<span data-ttu-id="b2a5d-179">Vedere [Esecuzione di query Hive tramite PowerShell](hdinsight-hadoop-use-hive-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="b2a5d-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="b2a5d-180">**processi Pig toosubmit**</span><span class="sxs-lookup"><span data-stu-id="b2a5d-180">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="b2a5d-181">Vedere [Eseguire processi Pig mediante PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b2a5d-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="b2a5d-182">**toosubmit Sqoop processi**</span><span class="sxs-lookup"><span data-stu-id="b2a5d-182">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="b2a5d-183">Vedere [Usare Sqoop con Hadoop in HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="b2a5d-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="b2a5d-184">**processi di Oozie toosubmit**</span><span class="sxs-lookup"><span data-stu-id="b2a5d-184">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="b2a5d-185">Vedere [utilizzare Oozie con Hadoop toodefine ed eseguire un flusso di lavoro in HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="b2a5d-185">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="b2a5d-186">Carica l'archiviazione Blob di dati tooAzure</span><span class="sxs-lookup"><span data-stu-id="b2a5d-186">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="b2a5d-187">Vedere [caricare dati tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="b2a5d-187">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="b2a5d-188">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b2a5d-188">See Also</span></span>
* <span data-ttu-id="b2a5d-189">[Documentazione di riferimento dei cmdlet di HDInsight][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="b2a5d-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="b2a5d-190">[Amministrazione di HDInsight tramite hello portale di Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="b2a5d-190">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="b2a5d-191">[Amministrare HDInsight con l'interfaccia della riga di comando][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="b2a5d-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="b2a5d-192">[Creare cluster HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="b2a5d-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="b2a5d-193">[Caricare dati tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="b2a5d-193">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="b2a5d-194">[Inviare processi Hadoop a livello di codice][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="b2a5d-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="b2a5d-195">[Introduzione ad Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="b2a5d-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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
