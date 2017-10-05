---
title: Personalizzare cluster HDInsight tramite l'azione script - Azure | Microsoft Docs
description: Informazioni su come personalizzare cluster HDInsight mediante Azione di script.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: ec95b6d66c71b4278dd1e16807fcc75f5e8b1c36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="c15a9-103">Personalizzare cluster HDInsight basati su Windows tramite Azione script</span><span class="sxs-lookup"><span data-stu-id="c15a9-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="c15a9-104">**Azione script** può essere utilizzato per richiamare [gli script personalizzati](hdinsight-hadoop-script-actions.md) durante il processo di creazione di cluster per l'installazione del software aggiuntivo in un cluster.</span><span class="sxs-lookup"><span data-stu-id="c15a9-104">**Script Action** can be used to invoke [custom scripts](hdinsight-hadoop-script-actions.md) during the cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="c15a9-105">Le informazioni contenute in questo articolo sono specifiche per i cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="c15a9-105">The information in this article is specific to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="c15a9-106">Per i cluster basati su Linux, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c15a9-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c15a9-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="c15a9-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c15a9-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c15a9-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="c15a9-109">I cluster HDInsight possono essere personalizzati in molti modi diversi, ad esempio includendo account di archiviazione di Azure aggiuntivi, modificando i file di configurazione Hadoop (core-site.xml, hive-site.xml e così via) o aggiungendo librerie condivise (ad esempio Hive e Oozie) in posizioni comuni nel cluster.</span><span class="sxs-lookup"><span data-stu-id="c15a9-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing the Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in the cluster.</span></span> <span data-ttu-id="c15a9-110">Queste personalizzazioni possono essere apportate tramite Azure PowerShell, Azure HDInsight .NET SDK o il Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c15a9-110">These customizations can be done through Azure PowerShell, the Azure HDInsight .NET SDK, or the Azure portal.</span></span> <span data-ttu-id="c15a9-111">Per altre informazioni, vedere [Creare cluster Hadoop basati su Windows in HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="c15a9-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="c15a9-112">Azione di script nel processo di creazione di cluster</span><span class="sxs-lookup"><span data-stu-id="c15a9-112">Script Action in the cluster creation process</span></span>
<span data-ttu-id="c15a9-113">L'opzione Azione di script viene usata solo mentre è in corso il processo di creazione di un cluster.</span><span class="sxs-lookup"><span data-stu-id="c15a9-113">Script Action is only used while a cluster is in the process of being created.</span></span> <span data-ttu-id="c15a9-114">Il diagramma seguente illustra quando l'opzione Azione di script viene eseguita durante il processo di creazione:</span><span class="sxs-lookup"><span data-stu-id="c15a9-114">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="c15a9-115">![Personalizzazione di cluster HDInsight e fasi durante la creazione di un cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="c15a9-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="c15a9-116">Quando lo script è in esecuzione, il cluster entra nella fase **ClusterCustomization** .</span><span class="sxs-lookup"><span data-stu-id="c15a9-116">When the script is running, the cluster enters the **ClusterCustomization** stage.</span></span> <span data-ttu-id="c15a9-117">In questa fase, lo script viene eseguito con l'account di amministratore di sistema in parallelo su tutti i nodi specificati nel cluster e fornisce privilegi di amministratore completi sui nodi.</span><span class="sxs-lookup"><span data-stu-id="c15a9-117">At this stage, the script is run under the system admin account, in parallel on all the specified nodes in the cluster, and provides full admin privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="c15a9-118">Perché durante la fase **ClusterCustomization** si dispone dei privilegi di amministratore sui nodi del cluster, è possibile usare lo script per eseguire operazioni come arresto e avvio dei servizi, inclusi quelli correlati a Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c15a9-118">Because you have admin privileges on the cluster nodes during the **ClusterCustomization** stage, you can use the script to perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="c15a9-119">Pertanto, come parte dello script, è necessario assicurarsi che i servizi di Ambari e altri servizi correlati a Hadoop siano attivi prima che lo script termini l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c15a9-119">So, as part of the script, you must ensure that the Ambari services and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="c15a9-120">Questi servizi sono necessari per verificare correttamente l'integrità e lo stato del cluster durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="c15a9-120">These services are required to successfully ascertain the health and state of the cluster while it is being created.</span></span> <span data-ttu-id="c15a9-121">Se si modifica qualsiasi configurazione del cluster che influisce su questi servizi, è necessario usare le funzioni di supporto fornite.</span><span class="sxs-lookup"><span data-stu-id="c15a9-121">If you change any configuration on the cluster that affects these services, you must use the helper functions that are provided.</span></span> <span data-ttu-id="c15a9-122">Per altre informazioni sulle funzioni di supporto, vedere [Sviluppare script di Azione script per HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="c15a9-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="c15a9-123">L'output e i log degli errori dello script vengono archiviati nell'account di archiviazione predefinito specificato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="c15a9-123">The output and the error logs for the script are stored in the default Storage account you specified for the cluster.</span></span> <span data-ttu-id="c15a9-124">I log vengono archiviati in una tabella con il nome **u<\frammento-nome-cluster><\timestamp>setuplog**.</span><span class="sxs-lookup"><span data-stu-id="c15a9-124">The logs are stored in a table with the name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="c15a9-125">Si tratta di log aggregati dello script eseguito su tutti i nodi (nodo head e nodi di lavoro) del cluster.</span><span class="sxs-lookup"><span data-stu-id="c15a9-125">These are aggregate logs from the script run on all the nodes (head node and worker nodes) in the cluster.</span></span>

<span data-ttu-id="c15a9-126">Ogni cluster può accettare più azioni di script che vengono richiamate nell'ordine in cui sono specificate.</span><span class="sxs-lookup"><span data-stu-id="c15a9-126">Each cluster can accept multiple script actions that are invoked in the order in which they are specified.</span></span> <span data-ttu-id="c15a9-127">Uno script può essere eseguito nel nodo head, nei nodi di lavoro o in entrambi.</span><span class="sxs-lookup"><span data-stu-id="c15a9-127">A script can be ran on the head node, the worker nodes, or both.</span></span>

<span data-ttu-id="c15a9-128">HDInsight fornisce diversi script di esempio per installare i componenti seguenti nei cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c15a9-128">HDInsight provides several scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="c15a9-129">Nome</span><span class="sxs-lookup"><span data-stu-id="c15a9-129">Name</span></span> | <span data-ttu-id="c15a9-130">Script</span><span class="sxs-lookup"><span data-stu-id="c15a9-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="c15a9-131">**Installare Spark**</span><span class="sxs-lookup"><span data-stu-id="c15a9-131">**Install Spark**</span></span> |<span data-ttu-id="c15a9-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="c15a9-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="c15a9-133">Vedere [Installare e usare Spark in cluster Hadoop di HDInsight][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="c15a9-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="c15a9-134">**Installare R**</span><span class="sxs-lookup"><span data-stu-id="c15a9-134">**Install R**</span></span> |<span data-ttu-id="c15a9-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="c15a9-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="c15a9-136">Vedere [Installare e usare R nei cluster HDInsight][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="c15a9-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="c15a9-137">**Installare Solr**</span><span class="sxs-lookup"><span data-stu-id="c15a9-137">**Install Solr**</span></span> |<span data-ttu-id="c15a9-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="c15a9-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="c15a9-139">Vedere [Installare e usare Solr nei cluster Hadoop di HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="c15a9-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="c15a9-140">- **Installare Giraph**</span><span class="sxs-lookup"><span data-stu-id="c15a9-140">- **Install Giraph**</span></span> |<span data-ttu-id="c15a9-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="c15a9-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="c15a9-142">Vedere [Installare Giraph nei cluster HDInsight Hadoop](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="c15a9-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="c15a9-143">**Precaricare le librerie Hive**</span><span class="sxs-lookup"><span data-stu-id="c15a9-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="c15a9-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="c15a9-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="c15a9-145">Vedere l'articolo relativo all' [aggiunta di librerie Hive in cluster HDInsight](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="c15a9-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-the-azure-portal"></a><span data-ttu-id="c15a9-146">Chiamare script tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c15a9-146">Call scripts using the Azure portal</span></span>
<span data-ttu-id="c15a9-147">**Nel portale di Azure**</span><span class="sxs-lookup"><span data-stu-id="c15a9-147">**From the Azure portal**</span></span>

1. <span data-ttu-id="c15a9-148">Avviare la creazione di un cluster come descritto in [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c15a9-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="c15a9-149">In Configurazione facoltativa fare clic su **aggiungi azione script** nel pannello **Azioni script** per specificare i dettagli relativi all'azione script, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c15a9-149">Under Optional Configuration, for the **Script Actions** blade, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="c15a9-150">![Usare l'azione script per personalizzare un cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Usare l'azione script per personalizzare un cluster")</span><span class="sxs-lookup"><span data-stu-id="c15a9-150">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="c15a9-151">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c15a9-151">Property</span></span></th><th><span data-ttu-id="c15a9-152">Valore</span><span class="sxs-lookup"><span data-stu-id="c15a9-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="c15a9-153">Nome</span><span class="sxs-lookup"><span data-stu-id="c15a9-153">Name</span></span></td>
            <td><span data-ttu-id="c15a9-154">Specificare un nome per l'azione script.</span><span class="sxs-lookup"><span data-stu-id="c15a9-154">Specify a name for the script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="c15a9-155">URI script</span><span class="sxs-lookup"><span data-stu-id="c15a9-155">Script URI</span></span></td>
            <td><span data-ttu-id="c15a9-156">Specificare l'URI dello script da richiamare per personalizzare il cluster.</span><span class="sxs-lookup"><span data-stu-id="c15a9-156">Specify the URI to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="c15a9-157">s</span><span class="sxs-lookup"><span data-stu-id="c15a9-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="c15a9-158">Head/Lavoro</span><span class="sxs-lookup"><span data-stu-id="c15a9-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="c15a9-159">Specificare i nodi **head** o **ruolo di lavoro** in cui viene eseguito lo script di personalizzazione</b>.</span><span class="sxs-lookup"><span data-stu-id="c15a9-159">Specify the nodes (**Head** or **Worker**) on which the customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="c15a9-160">Parametri</span><span class="sxs-lookup"><span data-stu-id="c15a9-160">Parameters</span></span></td>
            <td><span data-ttu-id="c15a9-161">Specificare i parametri, se richiesti dallo script.</span><span class="sxs-lookup"><span data-stu-id="c15a9-161">Specify the parameters, if required by the script.</span></span></td></tr>
    </table>

    <span data-ttu-id="c15a9-162">È possibile aggiungere altre azioni di script per installare più componenti nel cluster.</span><span class="sxs-lookup"><span data-stu-id="c15a9-162">Press ENTER to add more than one script action to install multiple components on the cluster.</span></span>
3. <span data-ttu-id="c15a9-163">Fare clic su **Seleziona** per salvare la configurazione dell'azione di script e continuare con la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="c15a9-163">Click **Select** to save the script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="c15a9-164">Chiamare script con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c15a9-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="c15a9-165">Lo script di PowerShell seguente dimostra come installare Spark nel cluster HDInsight basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="c15a9-165">This following PowerShell script demonstrates how to install Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" to list IDs.

    $nameToken = "<Enter A Name Token>"  # The token is use to create Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect to Azure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare the dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify the configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action to the cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


<span data-ttu-id="c15a9-166">Per installare altri software, è necessario sostituire il file script nello script:</span><span class="sxs-lookup"><span data-stu-id="c15a9-166">To install other software, you will need to replace the script file in the script:</span></span>

<span data-ttu-id="c15a9-167">Quando richiesto, immettere le credenziali per il cluster.</span><span class="sxs-lookup"><span data-stu-id="c15a9-167">When prompted, enter the credentials for the cluster.</span></span> <span data-ttu-id="c15a9-168">La creazione del cluster può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="c15a9-168">It can take several minutes before the cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="c15a9-169">Chiamare script con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c15a9-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="c15a9-170">L'esempio seguente dimostra come installare Spark nel cluster HDInsight basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="c15a9-170">The following sample demonstrates how to install Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="c15a9-171">Per installare altri software, è necessario sostituire il file script nel codice.</span><span class="sxs-lookup"><span data-stu-id="c15a9-171">To install other software, you will need to replace the script file in the code.</span></span>

<span data-ttu-id="c15a9-172">**Per creare un cluster HDInsight con Spark**</span><span class="sxs-lookup"><span data-stu-id="c15a9-172">**To create an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="c15a9-173">Creare un'applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c15a9-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="c15a9-174">Eseguire il comando seguente dalla console di Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="c15a9-174">From the Nuget Package Manager Console, run the following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="c15a9-175">Nel file Program.cs usare le istruzioni using seguenti:</span><span class="sxs-lookup"><span data-stu-id="c15a9-175">Use the following using statements in the Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="c15a9-176">Sostituire il codice nella classe con il seguente:</span><span class="sxs-lookup"><span data-stu-id="c15a9-176">Place the code in the class with the following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is the GUID for the PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate to an Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">The AAD tenant ID</param>
        /// <param name="ClientId">The AAD client ID</param>
        /// <param name="SubscriptionId">The Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for the Resource manager and set the subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register the HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="c15a9-177">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c15a9-177">Press **F5** to run the application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="c15a9-178">Supporto per software open source usato nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="c15a9-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="c15a9-179">Il servizio Microsoft Azure HDInsight è una piattaforma flessibile che permette di creare applicazioni Big Data nel cloud usando un ecosistema di tecnologie open source basate su Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c15a9-179">The Microsoft Azure HDInsight service is a flexible platform that enables you to build big-data applications in the cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="c15a9-180">Microsoft Azure fornisce un livello di supporto generale per le tecnologie open source, come illustrato nella sezione relativa all' **ambito del supporto** del <a href="http://azure.microsoft.com/support/faq/" target="_blank">sito Web Domande frequenti sul supporto di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="c15a9-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in the **Support Scope** section of the <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="c15a9-181">Il servizio HDInsight fornisce un livello di supporto aggiuntivo per alcuni componenti, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c15a9-181">The HDInsight service provides an additional level of support for some of the components, as described below.</span></span>

<span data-ttu-id="c15a9-182">Nel servizio HDInsight sono disponibili due tipi di componenti open source:</span><span class="sxs-lookup"><span data-stu-id="c15a9-182">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="c15a9-183">**Componenti predefiniti** - Questi componenti sono preinstallati nei cluster HDInsight e forniscono la funzionalità di base del cluster.</span><span class="sxs-lookup"><span data-stu-id="c15a9-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="c15a9-184">Questa categoria include ad esempio il gestore risorse YARN, il linguaggio di query Hive (HiveQL) e la libreria Mahout.</span><span class="sxs-lookup"><span data-stu-id="c15a9-184">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="c15a9-185">L'elenco completo dei componenti del cluster è disponibile in [Novità delle versioni cluster di Hadoop incluse in HDInsight](hdinsight-component-versioning.md)</a>.</span><span class="sxs-lookup"><span data-stu-id="c15a9-185">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="c15a9-186">**Componenti personalizzati** - Un utente del cluster può installare o usare nel carico di lavoro qualsiasi componente disponibile nella community o creato da lui stesso.</span><span class="sxs-lookup"><span data-stu-id="c15a9-186">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

<span data-ttu-id="c15a9-187">I componenti predefiniti sono supportati in modo completo e il Supporto Microsoft contribuirà a isolare e risolvere i problemi correlati a questi componenti.</span><span class="sxs-lookup"><span data-stu-id="c15a9-187">Built-in components are fully supported, and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>

> [!WARNING]
> <span data-ttu-id="c15a9-188">I componenti forniti con il cluster HDInsight sono supportati in modo completo e il Supporto Microsoft contribuirà a isolare e risolvere i problemi correlati a questi componenti.</span><span class="sxs-lookup"><span data-stu-id="c15a9-188">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="c15a9-189">I componenti personalizzati ricevono supporto commercialmente ragionevole per semplificare la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="c15a9-189">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="c15a9-190">È possibile che si ottenga la risoluzione dei problemi o che venga richiesto di usare i canali disponibili per le tecnologie open source, in cui è possibile ottenere supporto approfondito per la tecnologia specifica.</span><span class="sxs-lookup"><span data-stu-id="c15a9-190">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="c15a9-191">È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="c15a9-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="c15a9-192">Per i progetti Apache sono anche disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/) e [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="c15a9-192">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="c15a9-193">Il servizio HDInsight permette di usare i componenti personalizzati in molti modi.</span><span class="sxs-lookup"><span data-stu-id="c15a9-193">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="c15a9-194">Indipendentemente dal modo in cui un componente viene usato o installato nel cluster, verrà applicato lo stesso livello di supporto.</span><span class="sxs-lookup"><span data-stu-id="c15a9-194">Regardless of how a component is used or installed on the cluster, the same level of support applies.</span></span> <span data-ttu-id="c15a9-195">L'elenco seguente illustra i modi più comuni per usare i componenti personalizzati nei cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c15a9-195">Below is a list of the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="c15a9-196">Invio di processi - È possibile inviare al cluster processi Hadoop o di altro tipo che eseguono o usano componenti personalizzati.</span><span class="sxs-lookup"><span data-stu-id="c15a9-196">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>
2. <span data-ttu-id="c15a9-197">Personalizzazione del cluster - Durante la creazione di un cluster, è possibile specificare impostazioni aggiuntive e componenti personalizzati, che verranno installati nei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="c15a9-197">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on the cluster nodes.</span></span>
3. <span data-ttu-id="c15a9-198">Esempi - Microsoft e altri utenti possono fornire esempi relativi all'uso dei componenti personalizzati più diffusi nei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c15a9-198">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="c15a9-199">Questi esempi vengono forniti senza supporto.</span><span class="sxs-lookup"><span data-stu-id="c15a9-199">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="c15a9-200">Sviluppare script di Azione di script</span><span class="sxs-lookup"><span data-stu-id="c15a9-200">Develop Script Action scripts</span></span>
<span data-ttu-id="c15a9-201">Vedere [Sviluppare script di Azione script per HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="c15a9-201">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="c15a9-202">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c15a9-202">See also</span></span>
* <span data-ttu-id="c15a9-203">[Creare cluster Hadoop in HDInsight][hdinsight-provision-cluster] contiene istruzioni relative alla creazione di un cluster HDInsight con altre opzioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="c15a9-203">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="c15a9-204">[Sviluppare script di Azione script per HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="c15a9-204">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="c15a9-205">[Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="c15a9-205">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="c15a9-206">[Installare e usare R nei cluster HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="c15a9-206">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="c15a9-207">[Installare e usare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="c15a9-207">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="c15a9-208">[Installare e usare Giraph nei cluster HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="c15a9-208">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


<span data-ttu-id="c15a9-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fasi durante la creazione di un cluster"</span><span class="sxs-lookup"><span data-stu-id="c15a9-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"</span></span>
