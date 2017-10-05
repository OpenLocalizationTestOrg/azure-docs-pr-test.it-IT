---
title: Personalizzare cluster HDInsight usando Bootstrap - Azure | Microsoft Docs
description: Informazioni su come personalizzare cluster HDInsight tramite Bootstrap.
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
ms.openlocfilehash: c7a6fafa90eac66774d564c82c926c662baf784c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a><span data-ttu-id="40ae1-103">Personalizzare cluster HDInsight tramite Bootstrap</span><span class="sxs-lookup"><span data-stu-id="40ae1-103">Customize HDInsight clusters using Bootstrap</span></span>

<span data-ttu-id="40ae1-104">A volte può essere necessario modificare i file di configurazione che includono:</span><span class="sxs-lookup"><span data-stu-id="40ae1-104">Sometimes, you want to configure the configuration files, which include:</span></span>

* <span data-ttu-id="40ae1-105">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-105">clusterIdentity.xml</span></span>
* <span data-ttu-id="40ae1-106">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-106">core-site.xml</span></span>
* <span data-ttu-id="40ae1-107">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-107">gateway.xml</span></span>
* <span data-ttu-id="40ae1-108">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-108">hbase-env.xml</span></span>
* <span data-ttu-id="40ae1-109">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-109">hbase-site.xml</span></span>
* <span data-ttu-id="40ae1-110">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-110">hdfs-site.xml</span></span>
* <span data-ttu-id="40ae1-111">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-111">hive-env.xml</span></span>
* <span data-ttu-id="40ae1-112">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-112">hive-site.xml</span></span>
* <span data-ttu-id="40ae1-113">mapred-site</span><span class="sxs-lookup"><span data-stu-id="40ae1-113">mapred-site</span></span>
* <span data-ttu-id="40ae1-114">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-114">oozie-site.xml</span></span>
* <span data-ttu-id="40ae1-115">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-115">oozie-env.xml</span></span>
* <span data-ttu-id="40ae1-116">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-116">storm-site.xml</span></span>
* <span data-ttu-id="40ae1-117">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-117">tez-site.xml</span></span>
* <span data-ttu-id="40ae1-118">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-118">webhcat-site.xml</span></span>
* <span data-ttu-id="40ae1-119">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="40ae1-119">yarn-site.xml</span></span>

<span data-ttu-id="40ae1-120">Sono disponibili tre metodi per usare Bootstrap:</span><span class="sxs-lookup"><span data-stu-id="40ae1-120">There are three methods to use bootstrap:</span></span>

* <span data-ttu-id="40ae1-121">Usare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="40ae1-121">Use Azure PowerShell</span></span>
* <span data-ttu-id="40ae1-122">Usare .NET SDK</span><span class="sxs-lookup"><span data-stu-id="40ae1-122">Use .NET SDK</span></span>
* <span data-ttu-id="40ae1-123">Usare un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="40ae1-123">Use Azure Resource Manager template</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="40ae1-124">Per informazioni sull'installazione di componenti aggiuntivi nel cluster HDInsight durante la creazione, vedere:</span><span class="sxs-lookup"><span data-stu-id="40ae1-124">For information on installing additional components on HDInsight cluster during the creation time, see:</span></span>

* [<span data-ttu-id="40ae1-125">Personalizzare cluster HDInsight mediante Azione di script (Linux)</span><span class="sxs-lookup"><span data-stu-id="40ae1-125">Customize HDInsight clusters using Script Action (Linux)</span></span>](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a><span data-ttu-id="40ae1-126">Usare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="40ae1-126">Use Azure PowerShell</span></span>
<span data-ttu-id="40ae1-127">Il codice PowerShell seguente personalizza una configurazione Hive:</span><span class="sxs-lookup"><span data-stu-id="40ae1-127">The following PowerShell code customizes a Hive configuration:</span></span>

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

<span data-ttu-id="40ae1-128">Uno script di PowerShell completo funzionante è disponibile nell' [appendice A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="40ae1-128">A complete working PowerShell script can be found in [Appendix-A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span></span>

<span data-ttu-id="40ae1-129">**Per verificare la modifica:**</span><span class="sxs-lookup"><span data-stu-id="40ae1-129">**To verify the change:**</span></span>

1. <span data-ttu-id="40ae1-130">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40ae1-130">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40ae1-131">Scegliere **Cluster HDInsight** dal menu di sinistra.</span><span class="sxs-lookup"><span data-stu-id="40ae1-131">From the left menu, click **HDInsight clusters**.</span></span> <span data-ttu-id="40ae1-132">Se non viene visualizzato, prima fare clic su **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="40ae1-132">If you don't see it, click **More services** first.</span></span>
3. <span data-ttu-id="40ae1-133">Fare clic sul cluster appena creato usando lo script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40ae1-133">Click the cluster you just created using the PowerShell script.</span></span>
4. <span data-ttu-id="40ae1-134">Fare clic su **Dashboard** nella parte superiore del pannello per aprire l'interfaccia utente di Ambari.</span><span class="sxs-lookup"><span data-stu-id="40ae1-134">Click **Dashboard** from the top of the blade to open the Ambari UI.</span></span>
5. <span data-ttu-id="40ae1-135">Fare clic su **Hive** nel menu di sinistra.</span><span class="sxs-lookup"><span data-stu-id="40ae1-135">Click **Hive** from the left menu.</span></span>
6. <span data-ttu-id="40ae1-136">Fare clic su **HiveServer2** da **Riepilogo**.</span><span class="sxs-lookup"><span data-stu-id="40ae1-136">Click **HiveServer2** from **Summary**.</span></span>
7. <span data-ttu-id="40ae1-137">Fare clic sulla scheda **Configurazioni** .</span><span class="sxs-lookup"><span data-stu-id="40ae1-137">Click the **Configs** tab.</span></span>
8. <span data-ttu-id="40ae1-138">Fare clic su **Hive** nel menu di sinistra.</span><span class="sxs-lookup"><span data-stu-id="40ae1-138">Click **Hive** from the left menu.</span></span>
9. <span data-ttu-id="40ae1-139">Fare clic sulla scheda **Avanzate** .</span><span class="sxs-lookup"><span data-stu-id="40ae1-139">Click the **Advanced** tab.</span></span>
10. <span data-ttu-id="40ae1-140">Scorrere verso il basso e quindi espandere le **impostazioni avanzate hive-site**.</span><span class="sxs-lookup"><span data-stu-id="40ae1-140">Scroll down and then expand **Advanced hive-site**.</span></span>
11. <span data-ttu-id="40ae1-141">Cercare **hive.metastore.client.socket.timeout** nella sezione.</span><span class="sxs-lookup"><span data-stu-id="40ae1-141">Look for **hive.metastore.client.socket.timeout** in the section.</span></span>

<span data-ttu-id="40ae1-142">Ecco altri esempi relativi alla personalizzazione di altri file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="40ae1-142">Some more samples on customizing other configuration files:</span></span>

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

<span data-ttu-id="40ae1-143">Per altre informazioni, vedere il blog di Azim Uddin relativo alla [personalizzazione della creazione di cluster HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="40ae1-143">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span></span>

## <a name="use-net-sdk"></a><span data-ttu-id="40ae1-144">Usare .NET SDK</span><span class="sxs-lookup"><span data-stu-id="40ae1-144">Use .NET SDK</span></span>
<span data-ttu-id="40ae1-145">Vedere [Creare cluster basati su Linux in HDInsight tramite .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span><span class="sxs-lookup"><span data-stu-id="40ae1-145">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span></span>

## <a name="use-resource-manager-template"></a><span data-ttu-id="40ae1-146">Usare i modelli di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="40ae1-146">Use Resource Manager template</span></span>
<span data-ttu-id="40ae1-147">È possibile usare bootstrap in un modello di Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="40ae1-147">You can use bootstrap in Resource Manager template:</span></span>

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![HDInsight Hadoop personalizzare cluster bootstrap modello di Azure Resource Manager](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a><span data-ttu-id="40ae1-149">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="40ae1-149">See also</span></span>
* <span data-ttu-id="40ae1-150">[Creare cluster Hadoop in HDInsight][hdinsight-provision-cluster] contiene istruzioni relative alla creazione di un cluster HDInsight con altre opzioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="40ae1-150">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="40ae1-151">[Sviluppare script di Azione script per HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="40ae1-151">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="40ae1-152">[Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="40ae1-152">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="40ae1-153">[Installare e usare R nei cluster HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="40ae1-153">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="40ae1-154">[Installare e usare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="40ae1-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="40ae1-155">[Installare e usare Giraph nei cluster HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="40ae1-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


<span data-ttu-id="40ae1-156">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fasi durante la creazione di un cluster"</span><span class="sxs-lookup"><span data-stu-id="40ae1-156">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"</span></span>

## <a name="appx-a-powershell-sample"></a><span data-ttu-id="40ae1-157">Appendice A: Esempio di PowerShell</span><span class="sxs-lookup"><span data-stu-id="40ae1-157">Appx-A: PowerShell sample</span></span>
<span data-ttu-id="40ae1-158">Questo script di PowerShell crea un cluster HDInsight e personalizza un'impostazione Hive:</span><span class="sxs-lookup"><span data-stu-id="40ae1-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span></span>

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
    # Connect to Azure
    ####################################
    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

    Write-Host "Creating the default storage account and default blob container ..."  -ForegroundColor Green
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
        -Context $defaultStorageContext #use the cluster name as the container name

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
    # Verify the cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
