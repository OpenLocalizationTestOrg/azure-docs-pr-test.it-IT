---
title: Cluster HDInsight con bootstrap - Azure aaaCustomize | Documenti Microsoft
description: Informazioni su come toocustomize HDInsight cluster utilizzando bootstrap.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ab2ebf0c-e961-4e95-8151-9724ee22d769
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0029680fd1aa0e9e6aa9cdf667256c31b7ddc565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a><span data-ttu-id="52808-103">Personalizzare cluster HDInsight tramite Bootstrap</span><span class="sxs-lookup"><span data-stu-id="52808-103">Customize HDInsight clusters using Bootstrap</span></span>

<span data-ttu-id="52808-104">In alcuni casi, si desidera tooconfigure hello i file di configurazione, tra cui:</span><span class="sxs-lookup"><span data-stu-id="52808-104">Sometimes, you want tooconfigure hello configuration files, which include:</span></span>

* <span data-ttu-id="52808-105">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="52808-105">clusterIdentity.xml</span></span>
* <span data-ttu-id="52808-106">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="52808-106">core-site.xml</span></span>
* <span data-ttu-id="52808-107">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="52808-107">gateway.xml</span></span>
* <span data-ttu-id="52808-108">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="52808-108">hbase-env.xml</span></span>
* <span data-ttu-id="52808-109">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="52808-109">hbase-site.xml</span></span>
* <span data-ttu-id="52808-110">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="52808-110">hdfs-site.xml</span></span>
* <span data-ttu-id="52808-111">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="52808-111">hive-env.xml</span></span>
* <span data-ttu-id="52808-112">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="52808-112">hive-site.xml</span></span>
* <span data-ttu-id="52808-113">mapred-site</span><span class="sxs-lookup"><span data-stu-id="52808-113">mapred-site</span></span>
* <span data-ttu-id="52808-114">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="52808-114">oozie-site.xml</span></span>
* <span data-ttu-id="52808-115">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="52808-115">oozie-env.xml</span></span>
* <span data-ttu-id="52808-116">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="52808-116">storm-site.xml</span></span>
* <span data-ttu-id="52808-117">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="52808-117">tez-site.xml</span></span>
* <span data-ttu-id="52808-118">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="52808-118">webhcat-site.xml</span></span>
* <span data-ttu-id="52808-119">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="52808-119">yarn-site.xml</span></span>

<span data-ttu-id="52808-120">Esistono tre metodi toouse bootstrap:</span><span class="sxs-lookup"><span data-stu-id="52808-120">There are three methods toouse bootstrap:</span></span>

* <span data-ttu-id="52808-121">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="52808-121">Use Azure PowerShell</span></span>
* <span data-ttu-id="52808-122">Usare .NET SDK</span><span class="sxs-lookup"><span data-stu-id="52808-122">Use .NET SDK</span></span>
* <span data-ttu-id="52808-123">Usare un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="52808-123">Use Azure Resource Manager template</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="52808-124">Per informazioni sull'installazione di componenti aggiuntivi nel cluster HDInsight durante la fase di creazione di hello, vedere:</span><span class="sxs-lookup"><span data-stu-id="52808-124">For information on installing additional components on HDInsight cluster during hello creation time, see:</span></span>

* [<span data-ttu-id="52808-125">Personalizzare cluster HDInsight mediante Azione di script (Linux)</span><span class="sxs-lookup"><span data-stu-id="52808-125">Customize HDInsight clusters using Script Action (Linux)</span></span>](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a><span data-ttu-id="52808-126">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="52808-126">Use Azure PowerShell</span></span>
<span data-ttu-id="52808-127">Hello seguente codice di PowerShell consente di personalizzare una configurazione di Hive:</span><span class="sxs-lookup"><span data-stu-id="52808-127">hello following PowerShell code customizes a Hive configuration:</span></span>

    # hive-site.xml configuration
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $existingResourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $clusterSizeInNodes `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -Config $config 

<span data-ttu-id="52808-128">Uno script di PowerShell completo funzionante è disponibile nell' [appendice A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="52808-128">A complete working PowerShell script can be found in [Appendix-A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span></span>

<span data-ttu-id="52808-129">**modifica di hello tooverify:**</span><span class="sxs-lookup"><span data-stu-id="52808-129">**tooverify hello change:**</span></span>

1. <span data-ttu-id="52808-130">Accesso toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="52808-130">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="52808-131">Scegliere dal menu a sinistra hello **cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="52808-131">From hello left menu, click **HDInsight clusters**.</span></span> <span data-ttu-id="52808-132">Se non viene visualizzato, prima fare clic su **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="52808-132">If you don't see it, click **More services** first.</span></span>
3. <span data-ttu-id="52808-133">Fare clic su cluster hello che appena creata mediante uno script di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="52808-133">Click hello cluster you just created using hello PowerShell script.</span></span>
4. <span data-ttu-id="52808-134">Fare clic su **Dashboard** dall'alto hello di hello pannello tooopen hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="52808-134">Click **Dashboard** from hello top of hello blade tooopen hello Ambari UI.</span></span>
5. <span data-ttu-id="52808-135">Fare clic su **Hive** dal menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="52808-135">Click **Hive** from hello left menu.</span></span>
6. <span data-ttu-id="52808-136">Fare clic su **HiveServer2** da **Riepilogo**.</span><span class="sxs-lookup"><span data-stu-id="52808-136">Click **HiveServer2** from **Summary**.</span></span>
7. <span data-ttu-id="52808-137">Fare clic su hello **configurazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="52808-137">Click hello **Configs** tab.</span></span>
8. <span data-ttu-id="52808-138">Fare clic su **Hive** dal menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="52808-138">Click **Hive** from hello left menu.</span></span>
9. <span data-ttu-id="52808-139">Fare clic su hello **avanzate** scheda.</span><span class="sxs-lookup"><span data-stu-id="52808-139">Click hello **Advanced** tab.</span></span>
10. <span data-ttu-id="52808-140">Scorrere verso il basso e quindi espandere le **impostazioni avanzate hive-site**.</span><span class="sxs-lookup"><span data-stu-id="52808-140">Scroll down and then expand **Advanced hive-site**.</span></span>
11. <span data-ttu-id="52808-141">Cercare **hive.metastore.client.socket.timeout** nella sezione hello.</span><span class="sxs-lookup"><span data-stu-id="52808-141">Look for **hive.metastore.client.socket.timeout** in hello section.</span></span>

<span data-ttu-id="52808-142">Ecco altri esempi relativi alla personalizzazione di altri file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="52808-142">Some more samples on customizing other configuration files:</span></span>

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

<span data-ttu-id="52808-143">Per altre informazioni, vedere il blog di Azim Uddin relativo alla [personalizzazione della creazione di cluster HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="52808-143">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span></span>

## <a name="use-net-sdk"></a><span data-ttu-id="52808-144">Usare .NET SDK</span><span class="sxs-lookup"><span data-stu-id="52808-144">Use .NET SDK</span></span>
<span data-ttu-id="52808-145">Vedere [basati su Linux creare cluster HDInsight con hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span><span class="sxs-lookup"><span data-stu-id="52808-145">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span></span>

## <a name="use-resource-manager-template"></a><span data-ttu-id="52808-146">Usare i modelli di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="52808-146">Use Resource Manager template</span></span>
<span data-ttu-id="52808-147">È possibile usare bootstrap in un modello di Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="52808-147">You can use bootstrap in Resource Manager template:</span></span>

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![HDInsight Hadoop personalizzare cluster bootstrap modello di Azure Resource Manager](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a><span data-ttu-id="52808-149">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="52808-149">See also</span></span>
* <span data-ttu-id="52808-150">[Creare i cluster Hadoop in HDInsight] [ hdinsight-provision-cluster] vengono fornite istruzioni su come toocreate un HDInsight cluster tramite altre opzioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="52808-150">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="52808-151">[Sviluppare script di Azione script per HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="52808-151">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="52808-152">[Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="52808-152">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="52808-153">[Installare e usare R nei cluster HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="52808-153">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="52808-154">[Installare e usare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="52808-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="52808-155">[Installare e usare Giraph nei cluster HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="52808-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fasi durante la creazione di un cluster"

## <a name="appx-a-powershell-sample"></a><span data-ttu-id="52808-157">Appendice A: Esempio di PowerShell</span><span class="sxs-lookup"><span data-stu-id="52808-157">Appx-A: PowerShell sample</span></span>
<span data-ttu-id="52808-158">Questo script di PowerShell crea un cluster HDInsight e personalizza un'impostazione Hive:</span><span class="sxs-lookup"><span data-stu-id="52808-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span></span>

    ####################################
    # Set these variables
    ####################################
    #region - used for creating Azure service names
    $nameToken = "<ENTER AN ALIAS>" 
    #endregion

    #region - cluster user accounts
    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"

    $sshUserName = "sshuser" #HDInsight ssh user name
    $sshPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"
    #endregion

    ####################################
    # Service names and varialbes
    ####################################
    #region - service names
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    $location = "East US 2"
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    ####################################
    # Connect tooAzure
    ####################################
    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create an HDInsight cluster
    ####################################
    # Create dependent components
    ####################################
    Write-Host "Creating a resource group ..." -ForegroundColor Green
    New-AzureRmResourceGroup `
        -Name  $resourceGroupName `
        -Location $location

    Write-Host "Creating hello default storage account and default blob container ..."  -ForegroundColor Green
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS

    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageContext #use hello cluster name as hello container name

    ####################################
    # Create a configuration object
    ####################################
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    ####################################
    # Create an HDInsight cluster
    ####################################
    $httpPW = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$httpPW)

    $sshPW = ConvertTo-SecureString -String $sshPassword -AsPlainText -Force
    $sshCredential = New-Object System.Management.Automation.PSCredential($sshUserName,$sshPW)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -Location $location `
        -ClusterSizeInNodes 1 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -SshCredential $sshCredential `
        -Config $config

    ####################################
    # Verify hello cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
