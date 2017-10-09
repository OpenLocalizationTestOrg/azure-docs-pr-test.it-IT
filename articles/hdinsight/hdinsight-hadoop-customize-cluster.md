---
title: aaaCustomize cluster HDInsight tramite script azioni - Azure | Documenti Microsoft
description: Informazioni su come cluster di HDInsight toocustomize mediante l'azione di Script.
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
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="23ae0-103">Personalizzare cluster HDInsight basati su Windows tramite Azione script</span><span class="sxs-lookup"><span data-stu-id="23ae0-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="23ae0-104">**Azione di script** può essere utilizzato tooinvoke [script personalizzati](hdinsight-hadoop-script-actions.md) durante il processo di creazione di cluster hello per l'installazione di software aggiuntivi in un cluster.</span><span class="sxs-lookup"><span data-stu-id="23ae0-104">**Script Action** can be used tooinvoke [custom scripts](hdinsight-hadoop-script-actions.md) during hello cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="23ae0-105">informazioni di Hello in questo articolo sono di tipo cluster HDInsight basati su tooWindows specifici.</span><span class="sxs-lookup"><span data-stu-id="23ae0-105">hello information in this article is specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="23ae0-106">Per i cluster basati su Linux, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="23ae0-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23ae0-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="23ae0-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="23ae0-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="23ae0-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="23ae0-109">Cluster HDInsight possono essere personalizzati in una vasta gamma di altri modi, ad esempio l'utilizzo di altri account di archiviazione di Azure, la modifica hello Hadoop file di configurazione (hive-Site.XML Core-Site.XML, e così via) o aggiunta di raccolte (ad esempio, Hive e Oozie) condivise in percorsi comuni in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing hello Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in hello cluster.</span></span> <span data-ttu-id="23ae0-110">Queste personalizzazioni possono essere eseguite tramite Azure PowerShell, hello Azure HDInsight .NET SDK o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="23ae0-110">These customizations can be done through Azure PowerShell, hello Azure HDInsight .NET SDK, or hello Azure portal.</span></span> <span data-ttu-id="23ae0-111">Per altre informazioni, vedere [Creare cluster Hadoop basati su Windows in HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="23ae0-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="23ae0-112">Genera script azione nel processo di creazione di cluster hello</span><span class="sxs-lookup"><span data-stu-id="23ae0-112">Script Action in hello cluster creation process</span></span>
<span data-ttu-id="23ae0-113">Genera script azione viene utilizzato solo durante un cluster è in corso di hello corso di creazione.</span><span class="sxs-lookup"><span data-stu-id="23ae0-113">Script Action is only used while a cluster is in hello process of being created.</span></span> <span data-ttu-id="23ae0-114">Hello diagramma seguente illustra quando viene eseguita l'azione di Script durante il processo di creazione di hello:</span><span class="sxs-lookup"><span data-stu-id="23ae0-114">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="23ae0-115">![Personalizzazione di cluster HDInsight e fasi durante la creazione di un cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="23ae0-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="23ae0-116">Durante l'esecuzione di script hello, cluster hello immette hello **ClusterCustomization** fase.</span><span class="sxs-lookup"><span data-stu-id="23ae0-116">When hello script is running, hello cluster enters hello **ClusterCustomization** stage.</span></span> <span data-ttu-id="23ae0-117">In questa fase, hello script viene eseguito con l'account amministratore di sistema hello, in parallelo in tutte hello specificato nodi cluster hello e fornisce i privilegi di amministratore completi nei nodi hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-117">At this stage, hello script is run under hello system admin account, in parallel on all hello specified nodes in hello cluster, and provides full admin privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="23ae0-118">Poiché si dispone dei privilegi di amministratore nei nodi del cluster hello durante il **ClusterCustomization** fase, è possibile utilizzare le operazioni di tooperform script hello come arrestare e avviare servizi, inclusi quelli correlati Hadoop.</span><span class="sxs-lookup"><span data-stu-id="23ae0-118">Because you have admin privileges on hello cluster nodes during the **ClusterCustomization** stage, you can use hello script tooperform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="23ae0-119">Pertanto, come parte dello script hello, è necessario assicurarsi che i servizi Ambari hello e altri servizi correlati a Hadoop siano in esecuzione prima di script hello al termine dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="23ae0-119">So, as part of hello script, you must ensure that hello Ambari services and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="23ae0-120">Questi servizi sono necessari toosuccessfully verificare hello integrità e dello stato del cluster hello durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="23ae0-120">These services are required toosuccessfully ascertain hello health and state of hello cluster while it is being created.</span></span> <span data-ttu-id="23ae0-121">Se si modifica qualsiasi configurazione in cluster che influisce su questi servizi, è necessario utilizzare funzioni di supporto hello forniti.</span><span class="sxs-lookup"><span data-stu-id="23ae0-121">If you change any configuration on the cluster that affects these services, you must use hello helper functions that are provided.</span></span> <span data-ttu-id="23ae0-122">Per altre informazioni sulle funzioni di supporto, vedere [Sviluppare script di Azione script per HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="23ae0-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="23ae0-123">output di Hello e di log degli errori di hello per script hello vengono archiviati nell'account di archiviazione predefinito hello specificato per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-123">hello output and hello error logs for hello script are stored in hello default Storage account you specified for hello cluster.</span></span> <span data-ttu-id="23ae0-124">Hello i log vengono archiviati in una tabella con nome hello **u < \cluster-name-fragment >< \time-stamp > setuplog**.</span><span class="sxs-lookup"><span data-stu-id="23ae0-124">hello logs are stored in a table with hello name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="23ae0-125">Questi sono registri di aggregazione da eseguire in tutti i nodi di hello (nodo head e i nodi di lavoro) cluster hello uno script di hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-125">These are aggregate logs from hello script run on all hello nodes (head node and worker nodes) in hello cluster.</span></span>

<span data-ttu-id="23ae0-126">Ogni cluster possono accettare più azioni di script che vengono richiamate nell'ordine di hello in cui sono state specificate.</span><span class="sxs-lookup"><span data-stu-id="23ae0-126">Each cluster can accept multiple script actions that are invoked in hello order in which they are specified.</span></span> <span data-ttu-id="23ae0-127">Uno script può essere eseguito nel nodo head hello, nodi di lavoro hello o entrambi.</span><span class="sxs-lookup"><span data-stu-id="23ae0-127">A script can be ran on hello head node, hello worker nodes, or both.</span></span>

<span data-ttu-id="23ae0-128">HDInsight offre diversi hello tooinstall di script seguenti componenti nei cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="23ae0-128">HDInsight provides several scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="23ae0-129">Nome</span><span class="sxs-lookup"><span data-stu-id="23ae0-129">Name</span></span> | <span data-ttu-id="23ae0-130">Script</span><span class="sxs-lookup"><span data-stu-id="23ae0-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="23ae0-131">**Installare Spark**</span><span class="sxs-lookup"><span data-stu-id="23ae0-131">**Install Spark**</span></span> |<span data-ttu-id="23ae0-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="23ae0-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="23ae0-133">Vedere [Installare e usare Spark in cluster Hadoop di HDInsight][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="23ae0-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="23ae0-134">**Installare R**</span><span class="sxs-lookup"><span data-stu-id="23ae0-134">**Install R**</span></span> |<span data-ttu-id="23ae0-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="23ae0-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="23ae0-136">Vedere [Installare e usare R nei cluster HDInsight][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="23ae0-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="23ae0-137">**Installare Solr**</span><span class="sxs-lookup"><span data-stu-id="23ae0-137">**Install Solr**</span></span> |<span data-ttu-id="23ae0-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="23ae0-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="23ae0-139">Vedere [Installare e usare Solr nei cluster Hadoop di HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="23ae0-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="23ae0-140">- **Installare Giraph**</span><span class="sxs-lookup"><span data-stu-id="23ae0-140">- **Install Giraph**</span></span> |<span data-ttu-id="23ae0-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="23ae0-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="23ae0-142">Vedere [Installare Giraph nei cluster HDInsight Hadoop](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="23ae0-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="23ae0-143">**Precaricare le librerie Hive**</span><span class="sxs-lookup"><span data-stu-id="23ae0-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="23ae0-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="23ae0-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="23ae0-145">Vedere l'articolo relativo all' [aggiunta di librerie Hive in cluster HDInsight](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="23ae0-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-hello-azure-portal"></a><span data-ttu-id="23ae0-146">Script di chiamata utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="23ae0-146">Call scripts using hello Azure portal</span></span>
<span data-ttu-id="23ae0-147">**Dal portale di Azure hello**</span><span class="sxs-lookup"><span data-stu-id="23ae0-147">**From hello Azure portal**</span></span>

1. <span data-ttu-id="23ae0-148">Avviare la creazione di un cluster come descritto in [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="23ae0-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="23ae0-149">Nella sezione Configurazione facoltativi per hello **azioni Script** pannello, fare clic su **aggiungere script azione** tooprovide i dettagli sulla azione script hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="23ae0-149">Under Optional Configuration, for hello **Script Actions** blade, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="23ae0-150">![Utilizzare l'azione Script toocustomize un cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize azione Script Usa un cluster")</span><span class="sxs-lookup"><span data-stu-id="23ae0-150">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="23ae0-151">Proprietà</span><span class="sxs-lookup"><span data-stu-id="23ae0-151">Property</span></span></th><th><span data-ttu-id="23ae0-152">Valore</span><span class="sxs-lookup"><span data-stu-id="23ae0-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="23ae0-153">Nome</span><span class="sxs-lookup"><span data-stu-id="23ae0-153">Name</span></span></td>
            <td><span data-ttu-id="23ae0-154">Specificare un nome per l'azione script hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-154">Specify a name for hello script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="23ae0-155">URI script</span><span class="sxs-lookup"><span data-stu-id="23ae0-155">Script URI</span></span></td>
            <td><span data-ttu-id="23ae0-156">Specificare hello URI toohello script che è richiamato toocustomize hello cluster.</span><span class="sxs-lookup"><span data-stu-id="23ae0-156">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="23ae0-157">s</span><span class="sxs-lookup"><span data-stu-id="23ae0-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="23ae0-158">Head/Lavoro</span><span class="sxs-lookup"><span data-stu-id="23ae0-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="23ae0-159">Specificare i nodi di hello (**Head** o **lavoro**) in cui personalizzazione hello script viene eseguito.</b>.</span><span class="sxs-lookup"><span data-stu-id="23ae0-159">Specify hello nodes (**Head** or **Worker**) on which hello customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="23ae0-160">parameters</span><span class="sxs-lookup"><span data-stu-id="23ae0-160">Parameters</span></span></td>
            <td><span data-ttu-id="23ae0-161">Specificare i parametri di hello, se richiesti dallo script hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-161">Specify hello parameters, if required by hello script.</span></span></td></tr>
    </table>

    <span data-ttu-id="23ae0-162">Premere INVIO tooadd più di uno script azione tooinstall più componenti cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-162">Press ENTER tooadd more than one script action tooinstall multiple components on hello cluster.</span></span>
3. <span data-ttu-id="23ae0-163">Fare clic su **selezionare** toosave hello configurazione script dell'azione e continuare con la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="23ae0-163">Click **Select** toosave hello script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="23ae0-164">Chiamare script con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="23ae0-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="23ae0-165">Questo script di PowerShell seguente viene illustrato come tooinstall Spark in Windows basato su cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23ae0-165">This following PowerShell script demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
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

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
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


<span data-ttu-id="23ae0-166">tooinstall altro software, sono necessari file di script hello tooreplace nello script hello:</span><span class="sxs-lookup"><span data-stu-id="23ae0-166">tooinstall other software, you will need tooreplace hello script file in hello script:</span></span>

<span data-ttu-id="23ae0-167">Quando richiesto, immettere le credenziali di hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-167">When prompted, enter hello credentials for hello cluster.</span></span> <span data-ttu-id="23ae0-168">Può richiedere alcuni minuti prima che venga creato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-168">It can take several minutes before hello cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="23ae0-169">Chiamare script con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="23ae0-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="23ae0-170">Hello seguente esempio viene illustrato come tooinstall Spark in Windows basato su cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23ae0-170">hello following sample demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="23ae0-171">tooinstall altro software, sono necessari file di script hello tooreplace nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-171">tooinstall other software, you will need tooreplace hello script file in hello code.</span></span>

<span data-ttu-id="23ae0-172">**un cluster di HDInsight con Spark toocreate**</span><span class="sxs-lookup"><span data-stu-id="23ae0-172">**toocreate an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="23ae0-173">Creare un'applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="23ae0-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="23ae0-174">Dalla Console di gestione pacchetti Nuget hello, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="23ae0-174">From hello Nuget Package Manager Console, run hello following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="23ae0-175">Dopo l'utilizzo di istruzioni nel file Program.cs hello hello di utilizzo:</span><span class="sxs-lookup"><span data-stu-id="23ae0-175">Use hello following using statements in hello Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="23ae0-176">Inserire codice hello nella classe hello con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="23ae0-176">Place hello code in hello class with hello following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
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
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
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
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="23ae0-177">Premere **F5** toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-177">Press **F5** toorun hello application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="23ae0-178">Supporto per software open source usato nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="23ae0-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="23ae0-179">servizio Microsoft Azure HDInsight Hello è una piattaforma flessibile che consente applicazioni big data toobuild nel cloud hello utilizzando un ecosistema di tecnologie open source in corrispondenza di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="23ae0-179">hello Microsoft Azure HDInsight service is a flexible platform that enables you toobuild big-data applications in hello cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="23ae0-180">Microsoft Azure offre un livello di supporto generale per le tecnologie open source, come descritto in hello **supportano ambito** sezione di hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">sito Web di domande frequenti su Azure supporta</a>.</span><span class="sxs-lookup"><span data-stu-id="23ae0-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in hello **Support Scope** section of hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="23ae0-181">servizio HDInsight Hello fornisce un ulteriore livello di supporto per alcuni dei componenti di hello, come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="23ae0-181">hello HDInsight service provides an additional level of support for some of hello components, as described below.</span></span>

<span data-ttu-id="23ae0-182">Esistono due tipi di componenti open source che sono disponibili nel servizio HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="23ae0-182">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="23ae0-183">**I componenti predefiniti** -questi componenti sono pre-installati nei cluster HDInsight e forniscono funzionalità di base del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="23ae0-184">Ad esempio, ResourceManager YARN, linguaggio di query Hive hello (HiveQL) e libreria Mahout hello appartenere toothis categoria.</span><span class="sxs-lookup"><span data-stu-id="23ae0-184">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="23ae0-185">È disponibile in un elenco completo dei componenti cluster [novità introdotta nelle versioni di cluster Hadoop hello fornite da HDInsight?](hdinsight-component-versioning.md) </a>.</span><span class="sxs-lookup"><span data-stu-id="23ae0-185">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="23ae0-186">**I componenti personalizzati** -, come un utente del cluster di hello, puoi installare o utilizzare nel carico di lavoro qualsiasi componente disponibile nella community hello o creato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="23ae0-186">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

<span data-ttu-id="23ae0-187">I componenti predefiniti sono completamente supportati e il supporto Microsoft verrà Guida tooisolate e risolvere i problemi correlati toothese componenti.</span><span class="sxs-lookup"><span data-stu-id="23ae0-187">Built-in components are fully supported, and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>

> [!WARNING]
> <span data-ttu-id="23ae0-188">I componenti forniti con i cluster di HDInsight hello sono completamente supportati e il supporto Microsoft verrà Guida tooisolate e risolvere i problemi correlati toothese componenti.</span><span class="sxs-lookup"><span data-stu-id="23ae0-188">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="23ae0-189">I componenti personalizzati ricevano supporto commercialmente ragionevole toohelp toofurther per risolvere il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-189">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="23ae0-190">Ciò potrebbe comportare la risoluzione problema hello o chiedere che tooengage i canali disponibili per hello apertura di tecnologie di origine in cui si trova esperienza completa per tale tecnologia.</span><span class="sxs-lookup"><span data-stu-id="23ae0-190">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="23ae0-191">È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Per i progetti Apache sono anche disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/) e [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="23ae0-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="23ae0-192">servizio HDInsight Hello modi diversi componenti personalizzati toouse.</span><span class="sxs-lookup"><span data-stu-id="23ae0-192">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="23ae0-193">Indipendentemente dalla modalità un componente viene utilizzato o installato nel cluster hello, hello stesso livello di supporto si applica.</span><span class="sxs-lookup"><span data-stu-id="23ae0-193">Regardless of how a component is used or installed on hello cluster, hello same level of support applies.</span></span> <span data-ttu-id="23ae0-194">Di seguito è riportato un elenco dei modi più comuni di hello componenti personalizzati possono essere utilizzati nei cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="23ae0-194">Below is a list of hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="23ae0-195">Invio di processi - Hadoop o altri tipi di processi che utilizzano componenti personalizzati di esecuzione può essere inviato toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="23ae0-195">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>
2. <span data-ttu-id="23ae0-196">Personalizzazione del cluster - durante la creazione del cluster, è possibile specificare impostazioni aggiuntive e i componenti personalizzati che verranno installati nei nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-196">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on hello cluster nodes.</span></span>
3. <span data-ttu-id="23ae0-197">Esempi - per componenti personalizzati più diffusi, Microsoft e altri utenti possono fornire esempi di come utilizzare questi componenti nei cluster di HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-197">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="23ae0-198">Questi esempi vengono forniti senza supporto.</span><span class="sxs-lookup"><span data-stu-id="23ae0-198">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="23ae0-199">Sviluppare script di Azione di script</span><span class="sxs-lookup"><span data-stu-id="23ae0-199">Develop Script Action scripts</span></span>
<span data-ttu-id="23ae0-200">Vedere [Sviluppare script di Azione script per HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="23ae0-200">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="23ae0-201">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="23ae0-201">See also</span></span>
* <span data-ttu-id="23ae0-202">[Creare i cluster Hadoop in HDInsight] [ hdinsight-provision-cluster] vengono fornite istruzioni su come toocreate un HDInsight cluster tramite altre opzioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="23ae0-202">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="23ae0-203">[Sviluppare script di Azione script per HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="23ae0-203">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="23ae0-204">[Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="23ae0-204">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="23ae0-205">[Installare e usare R nei cluster HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="23ae0-205">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="23ae0-206">[Installare e usare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="23ae0-206">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="23ae0-207">[Installare e usare Giraph nei cluster HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="23ae0-207">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fasi durante la creazione di un cluster"
