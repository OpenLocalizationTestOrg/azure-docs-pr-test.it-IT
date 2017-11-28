---
title: cluster aaaInstall e utilizzare Giraph in Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come cluster di HDInsight toocustomize con Giraph e come toouse Giraph.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="70c1d-103">Installare e usare Giraph nei cluster HDInsight basati su Windows</span><span class="sxs-lookup"><span data-stu-id="70c1d-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="70c1d-104">Informazioni su come toocustomize Windows basato su cluster HDInsight con Giraph mediante l'azione di Script e come toouse Giraph tooprocess su larga scala grafici.</span><span class="sxs-lookup"><span data-stu-id="70c1d-104">Learn how toocustomize Windows based HDInsight cluster with Giraph using Script Action, and how toouse Giraph tooprocess large-scale graphs.</span></span> <span data-ttu-id="70c1d-105">Per informazioni sull'uso di Giraph con un cluster basato su Linux, vedere [Installare Giraph nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="70c1d-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70c1d-106">Hello passaggi di questa operazione solo documenti con i cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="70c1d-106">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="70c1d-107">HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="70c1d-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="70c1d-108">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="70c1d-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="70c1d-109">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="70c1d-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="70c1d-110">Per informazioni su come tooinstall Giraph in un cluster HDInsight basati su Linux, vedere [Giraph installare nei cluster HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="70c1d-110">For information on how tooinstall Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="70c1d-111">È possibile installare Giraph in qualsiasi tipo di cluster (Hadoop, Storm, HBase, Spark) su Azure HDInsight usando *Azione di script*.</span><span class="sxs-lookup"><span data-stu-id="70c1d-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="70c1d-112">Un tooinstall di script di esempio Giraph in un cluster HDInsight è disponibile da un blob di archiviazione di Azure di sola lettura in [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="70c1d-112">A sample script tooinstall Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="70c1d-113">script di esempio Hello funziona solo con versione 3.1 del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="70c1d-113">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="70c1d-114">Per altre informazioni sulle versioni dei cluster HDInsight, vedere [Versioni cluster HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="70c1d-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="70c1d-115">**Articoli correlati**</span><span class="sxs-lookup"><span data-stu-id="70c1d-115">**Related articles**</span></span>

* [<span data-ttu-id="70c1d-116">Installare Giraph nei cluster Hadoop di HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="70c1d-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="70c1d-117">[Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="70c1d-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="70c1d-118">[Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.</span><span class="sxs-lookup"><span data-stu-id="70c1d-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="70c1d-119">[Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="70c1d-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="70c1d-120">Che cos'è Giraph?</span><span class="sxs-lookup"><span data-stu-id="70c1d-120">What is Giraph?</span></span>
<span data-ttu-id="70c1d-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> consente grafico tooperform elaborazione tramite Hadoop e può essere utilizzato con Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="70c1d-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="70c1d-122">Grafici modellare relazioni tra oggetti, ad esempio le connessioni hello tra i router in una rete di grandi dimensioni come hello Internet, o relazioni tra gli utenti nel social network (talvolta definito tooas un grafico di social networking).</span><span class="sxs-lookup"><span data-stu-id="70c1d-122">Graphs model relationships between objects, such as hello connections between routers on a large network like hello Internet, or relationships between people on social networks (sometimes referred tooas a social graph).</span></span> <span data-ttu-id="70c1d-123">Elaborazione Graph consente tooreason sulle relazioni hello tra gli oggetti in un grafico, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="70c1d-123">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="70c1d-124">Identificare possibili amici sulla base delle relazioni correnti.</span><span class="sxs-lookup"><span data-stu-id="70c1d-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="70c1d-125">Identificazione hello itinerario più breve tra due computer in una rete.</span><span class="sxs-lookup"><span data-stu-id="70c1d-125">Identifying hello shortest route between two computers in a network.</span></span>
* <span data-ttu-id="70c1d-126">Calcolare il numero di dimensioni di hello pagina delle pagine Web.</span><span class="sxs-lookup"><span data-stu-id="70c1d-126">Calculating hello page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="70c1d-127">Installare Giraph tramite il portale</span><span class="sxs-lookup"><span data-stu-id="70c1d-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="70c1d-128">Avviare la creazione di un cluster tramite hello **creazione personalizzata** opzione, come descritto in [cluster creare Hadoop in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="70c1d-128">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="70c1d-129">In hello **azioni Script** pagina della procedura guidata hello, fare clic su **aggiungere script azione** tooprovide i dettagli sulla azione script hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="70c1d-129">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="70c1d-130">![Utilizzare l'azione Script toocustomize un cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize azione Script Usa un cluster")</span><span class="sxs-lookup"><span data-stu-id="70c1d-130">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="70c1d-131">Proprietà</span><span class="sxs-lookup"><span data-stu-id="70c1d-131">Property</span></span></th><th><span data-ttu-id="70c1d-132">Valore</span><span class="sxs-lookup"><span data-stu-id="70c1d-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="70c1d-133">Nome</span><span class="sxs-lookup"><span data-stu-id="70c1d-133">Name</span></span></td>
            <td><span data-ttu-id="70c1d-134">Specificare un nome per l'azione script hello.</span><span class="sxs-lookup"><span data-stu-id="70c1d-134">Specify a name for hello script action.</span></span> <span data-ttu-id="70c1d-135">Ad esempio, <b>Installare Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="70c1d-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="70c1d-136">URI script</span><span class="sxs-lookup"><span data-stu-id="70c1d-136">Script URI</span></span></td>
            <td><span data-ttu-id="70c1d-137">Specificare hello Uniform Resource Identifier (URI) toohello script che è richiamato toocustomize hello cluster.</span><span class="sxs-lookup"><span data-stu-id="70c1d-137">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="70c1d-138">Ad esempio, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="70c1d-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="70c1d-139">Tipo di nodo</span><span class="sxs-lookup"><span data-stu-id="70c1d-139">Node Type</span></span></td>
            <td><span data-ttu-id="70c1d-140">Specificare i nodi di hello in cui viene eseguito uno script di personalizzazione di hello.</span><span class="sxs-lookup"><span data-stu-id="70c1d-140">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="70c1d-141">È possibile scegliere <b>Tutti i nodi</b>, <b>Solo nodi head</b> o <b>Solo nodi di lavoro</b>.</span><span class="sxs-lookup"><span data-stu-id="70c1d-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="70c1d-142">parameters</span><span class="sxs-lookup"><span data-stu-id="70c1d-142">Parameters</span></span></td>
            <td><span data-ttu-id="70c1d-143">Specificare i parametri di hello, se richiesti dallo script hello.</span><span class="sxs-lookup"><span data-stu-id="70c1d-143">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="70c1d-144">Hello script tooinstall Giraph non richiede alcun parametro, pertanto è possibile lasciare vuoto questo.</span><span class="sxs-lookup"><span data-stu-id="70c1d-144">hello script tooinstall Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="70c1d-145">È possibile aggiungere più di uno script azione tooinstall più componenti nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="70c1d-145">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="70c1d-146">Dopo aver aggiunto gli script hello, fare clic su hello segno di spunta toostart la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="70c1d-146">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="70c1d-147">Usare Giraph</span><span class="sxs-lookup"><span data-stu-id="70c1d-147">Use Giraph</span></span>
<span data-ttu-id="70c1d-148">Utilizziamo hello SimpleShortestPathsComputation esempio toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementazione per trovare il percorso più breve di hello tra gli oggetti in un grafico.</span><span class="sxs-lookup"><span data-stu-id="70c1d-148">We use hello SimpleShortestPathsComputation example toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding hello shortest path between objects in a graph.</span></span> <span data-ttu-id="70c1d-149">Utilizzare hello seguendo i passaggi tooupload hello esempio hello e dati esempio jar, eseguire un processo utilizzando l'esempio SimpleShortestPathsComputation hello e quindi visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="70c1d-149">Use hello following steps tooupload hello sample data and hello sample jar, run a job by using hello SimpleShortestPathsComputation example, and then view hello results.</span></span>

1. <span data-ttu-id="70c1d-150">Caricare un tooAzure di file di dati di esempio nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="70c1d-150">Upload a sample data file tooAzure Blob storage.</span></span> <span data-ttu-id="70c1d-151">Nella workstation locale creare un nuovo file denominato **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="70c1d-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="70c1d-152">Deve contenere hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="70c1d-152">It should contain hello following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="70c1d-153">Caricare hello tiny_graph.txt file toohello archiviazione primaria per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="70c1d-153">Upload hello tiny_graph.txt file toohello primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="70c1d-154">Per istruzioni su come visualizzare dati tooupload, [caricare dati per i processi di Hadoop in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="70c1d-154">For instructions on how tooupload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="70c1d-155">Questi dati descrivono una relazione tra gli oggetti in un grafico diretto, utilizzando il formato di hello [origine\_id, origine\_valore, [[dest\_id], [edge\_valore],...]]. Ogni riga rappresenta una relazione tra un oggetto **source\_id** e uno o più oggetti **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="70c1d-155">This data describes a relationship between objects in a directed graph, by using hello format [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="70c1d-156">Hello **bordo\_valore** (o peso) può essere considerato come livello di attendibilità hello o una distanza di connessione hello tra **source_id** e **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="70c1d-156">hello **edge\_value** (or weight) can be thought of as hello strength or distance of hello connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="70c1d-157">Disegnare out, e utilizza il valore di hello (o peso) come distanza hello tra oggetti, hello di sopra dei dati può essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="70c1d-157">Drawn out, and using hello value (or weight) as hello distance between objects, hello above data might look like this:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="70c1d-159">Eseguire l'esempio SimpleShortestPathsComputation hello.</span><span class="sxs-lookup"><span data-stu-id="70c1d-159">Run hello SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="70c1d-160">Utilizzare hello seguendo l'esempio hello toorun i cmdlet di Azure PowerShell utilizzando file tiny_graph.txt hello come input.</span><span class="sxs-lookup"><span data-stu-id="70c1d-160">Use hello following Azure PowerShell cmdlets toorun hello example by using hello tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="70c1d-161">Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** ed è stato rimosso dal 1° gennaio 2017.</span><span class="sxs-lookup"><span data-stu-id="70c1d-161">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="70c1d-162">Hello passaggi in questo documento usa hello nuovi cmdlet di HDInsight che funzionano con Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="70c1d-162">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="70c1d-163">Eseguire le operazioni di hello in [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70c1d-163">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="70c1d-164">Se si dispone di script che toobe necessità modificato toouse hello nuovi cmdlet che funzionano con Gestione risorse di Azure, vedere [di strumenti di migrazione tooAzure sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="70c1d-164">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="70c1d-165">In hello esempio precedente, sostituire **clustername** con nome hello del cluster HDInsight con Giraph installato.</span><span class="sxs-lookup"><span data-stu-id="70c1d-165">In hello above example, replace **clustername** with hello name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="70c1d-166">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="70c1d-166">View hello results.</span></span> <span data-ttu-id="70c1d-167">Al termine dell'operazione processo hello hello risultati verranno archiviati in due file di output di hello **wasb: / / / esempio/out/shotestpaths** cartella.</span><span class="sxs-lookup"><span data-stu-id="70c1d-167">Once hello job has finished, hello results will be stored in two output files in hello **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="70c1d-168">file Hello sono denominati **parte-m-00001** e **parte-m-00002**.</span><span class="sxs-lookup"><span data-stu-id="70c1d-168">hello files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="70c1d-169">Eseguire hello output di hello toodownload e visualizzare i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="70c1d-169">Perform hello following steps toodownload and view hello output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="70c1d-170">Verrà creata hello **output/esempio/shortestpaths** struttura di directory nella directory corrente di hello nelle workstation e i file toothat percorso di download hello due output.</span><span class="sxs-lookup"><span data-stu-id="70c1d-170">This will create hello **example/output/shortestpaths** directory structure in hello current directory on your workstation, and download hello two output files toothat location.</span></span>

    <span data-ttu-id="70c1d-171">Hello utilizzare **Cat** cmdlet toodisplay hello contenuto file hello:</span><span class="sxs-lookup"><span data-stu-id="70c1d-171">Use hello **Cat** cmdlet toodisplay hello contents of hello files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="70c1d-172">output di Hello risulterà simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="70c1d-172">hello output should appear similar toohello following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="70c1d-173">esempio SimpleShortestPathComputation Hello è hardcoded toostart con ID 1 oggetto e trovare gli oggetti tooother percorso più brevi hello.</span><span class="sxs-lookup"><span data-stu-id="70c1d-173">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="70c1d-174">Pertanto l'output di hello deve essere letto come `destination_id distance`, dove distanza è hello valore (o peso), dei bordi hello percorsi tra l'oggetto ID 1 e ID di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="70c1d-174">So hello output should be read as `destination_id distance`, where distance is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="70c1d-175">Questa visualizzazione, è possibile verificare i risultati di hello viaggiando percorsi più brevi hello tra ID 1 e tutti gli altri oggetti.</span><span class="sxs-lookup"><span data-stu-id="70c1d-175">Visualizing this, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="70c1d-176">Si noti che il percorso più breve tra ID 1 e ID 4 hello sono 5.</span><span class="sxs-lookup"><span data-stu-id="70c1d-176">Note that hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="70c1d-177">Si tratta di hello distanza totale tra <span style="color:orange">ID 1 e 3</span>e quindi <span style="color:red">ID 3 e 4</span>.</span><span class="sxs-lookup"><span data-stu-id="70c1d-177">This is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="70c1d-179">Installare Giraph tramite Aure PowerShell</span><span class="sxs-lookup"><span data-stu-id="70c1d-179">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="70c1d-180">Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="70c1d-180">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="70c1d-181">esempio Hello viene illustrato come tooinstall Spark con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70c1d-181">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="70c1d-182">È necessario toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="70c1d-182">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="70c1d-183">Installare Giraph tramite .NET SDK</span><span class="sxs-lookup"><span data-stu-id="70c1d-183">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="70c1d-184">Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="70c1d-184">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="70c1d-185">esempio Hello viene illustrato come tooinstall Spark usando hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="70c1d-185">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="70c1d-186">È necessario toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="70c1d-186">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="70c1d-187">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="70c1d-187">See also</span></span>
* [<span data-ttu-id="70c1d-188">Installare Giraph nei cluster Hadoop di HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="70c1d-188">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="70c1d-189">[Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="70c1d-189">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="70c1d-190">[Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.</span><span class="sxs-lookup"><span data-stu-id="70c1d-190">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="70c1d-191">[Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="70c1d-191">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="70c1d-192">[Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]: esempio di azione script sull'installazione di Spark.</span><span class="sxs-lookup"><span data-stu-id="70c1d-192">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="70c1d-193">[Installare R nei cluster HDInsight][hdinsight-install-r]: esempio di azione script sull'installazione di R.</span><span class="sxs-lookup"><span data-stu-id="70c1d-193">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="70c1d-194">[Installare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install.md): esempio di Azione di script sull'installazione di Solr.</span><span class="sxs-lookup"><span data-stu-id="70c1d-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
