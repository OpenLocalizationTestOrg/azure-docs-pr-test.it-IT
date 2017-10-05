---
title: Installare e usare Giraph nei cluster Hadoop in HDInsight - Azure | Documentazione Microsoft
description: Informazioni su come personalizzare un cluster HDInsight con Giraph e su come usare Giraph.
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
ms.openlocfilehash: f0eb5c1f457380600463a370043f03e6d655a02c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="1293e-103">Installare e usare Giraph nei cluster HDInsight basati su Windows</span><span class="sxs-lookup"><span data-stu-id="1293e-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="1293e-104">Informazioni su come personalizzare i cluster HDInsight basati su Windows con Giraph usando Script azione e su come utilizzare Giraph per elaborare grafici su vasta scala.</span><span class="sxs-lookup"><span data-stu-id="1293e-104">Learn how to customize Windows based HDInsight cluster with Giraph using Script Action, and how to use Giraph to process large-scale graphs.</span></span> <span data-ttu-id="1293e-105">Per informazioni sull'uso di Giraph con un cluster basato su Linux, vedere [Installare Giraph nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1293e-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1293e-106">I passaggi descritti in questo documento funzionano solo con i cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="1293e-106">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1293e-107">HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="1293e-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="1293e-108">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="1293e-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1293e-109">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1293e-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="1293e-110">Per informazioni su come installare Giraph in un cluster HDInsight basato su Linux, vedere [Installare Giraph nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1293e-110">For information on how to install Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="1293e-111">È possibile installare Giraph in qualsiasi tipo di cluster (Hadoop, Storm, HBase, Spark) su Azure HDInsight usando *Azione di script*.</span><span class="sxs-lookup"><span data-stu-id="1293e-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="1293e-112">Uno script di esempio per l'installazione di Giraph in un cluster HDInsight è disponibile in un BLOB di archiviazione di sola lettura di Azure all'indirizzo [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="1293e-112">A sample script to install Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="1293e-113">Lo script di esempio funziona solo con cluster HDInsight versione 3.1.</span><span class="sxs-lookup"><span data-stu-id="1293e-113">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="1293e-114">Per altre informazioni sulle versioni dei cluster HDInsight, vedere [Versioni cluster HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="1293e-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="1293e-115">**Articoli correlati**</span><span class="sxs-lookup"><span data-stu-id="1293e-115">**Related articles**</span></span>

* [<span data-ttu-id="1293e-116">Installare Giraph nei cluster Hadoop di HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="1293e-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="1293e-117">[Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="1293e-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="1293e-118">[Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.</span><span class="sxs-lookup"><span data-stu-id="1293e-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="1293e-119">[Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="1293e-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="1293e-120">Che cos'è Giraph?</span><span class="sxs-lookup"><span data-stu-id="1293e-120">What is Giraph?</span></span>
<span data-ttu-id="1293e-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> consente di elaborare grafici con Hadoop e può essere usato con Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1293e-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="1293e-122">È possibile usare i grafici per modellare le relazioni tra gli oggetti, ad esempio le connessioni tra router in una rete di grandi dimensioni, come Internet, oppure le relazioni tra persone iscritte a social network, come nel cosiddetto grafico dei social network.</span><span class="sxs-lookup"><span data-stu-id="1293e-122">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span></span> <span data-ttu-id="1293e-123">Grazie all'elaborazione del grafico è possibile ottenere informazioni dettagliate sulle relazioni tra gli oggetti in un grafico e in particolare di:</span><span class="sxs-lookup"><span data-stu-id="1293e-123">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="1293e-124">Identificare possibili amici sulla base delle relazioni correnti.</span><span class="sxs-lookup"><span data-stu-id="1293e-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="1293e-125">Identificare la route più breve tra due computer di una rete.</span><span class="sxs-lookup"><span data-stu-id="1293e-125">Identifying the shortest route between two computers in a network.</span></span>
* <span data-ttu-id="1293e-126">Calcolare la posizione in classifica di pagine Web.</span><span class="sxs-lookup"><span data-stu-id="1293e-126">Calculating the page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="1293e-127">Installare Giraph tramite il portale</span><span class="sxs-lookup"><span data-stu-id="1293e-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="1293e-128">Avviare la creazione di un cluster usando l'opzione **CREAZIONE PERSONALIZZATA**, come descritto in [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1293e-128">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="1293e-129">Nella pagina **Azioni script** della procedura guidata fare clic su **aggiungi azione script** per specificare i dettagli relativi all'azione script, come descritto di seguito:</span><span class="sxs-lookup"><span data-stu-id="1293e-129">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="1293e-130">![Usare l'azione script per personalizzare un cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Usare l'azione script per personalizzare un cluster")</span><span class="sxs-lookup"><span data-stu-id="1293e-130">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="1293e-131">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1293e-131">Property</span></span></th><th><span data-ttu-id="1293e-132">Valore</span><span class="sxs-lookup"><span data-stu-id="1293e-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="1293e-133">Nome</span><span class="sxs-lookup"><span data-stu-id="1293e-133">Name</span></span></td>
            <td><span data-ttu-id="1293e-134">Specificare un nome per l'azione script.</span><span class="sxs-lookup"><span data-stu-id="1293e-134">Specify a name for the script action.</span></span> <span data-ttu-id="1293e-135">Ad esempio, <b>Installare Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="1293e-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="1293e-136">URI script</span><span class="sxs-lookup"><span data-stu-id="1293e-136">Script URI</span></span></td>
            <td><span data-ttu-id="1293e-137">Specificare l'URI (Uniform Resource Identifier) dello script da richiamare per personalizzare il cluster.</span><span class="sxs-lookup"><span data-stu-id="1293e-137">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="1293e-138">Ad esempio, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="1293e-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="1293e-139">Tipo di nodo</span><span class="sxs-lookup"><span data-stu-id="1293e-139">Node Type</span></span></td>
            <td><span data-ttu-id="1293e-140">Specificare i nodi in cui viene eseguito lo script di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="1293e-140">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="1293e-141">È possibile scegliere <b>Tutti i nodi</b>, <b>Solo nodi head</b> o <b>Solo nodi di lavoro</b>.</span><span class="sxs-lookup"><span data-stu-id="1293e-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="1293e-142">Parametri</span><span class="sxs-lookup"><span data-stu-id="1293e-142">Parameters</span></span></td>
            <td><span data-ttu-id="1293e-143">Specificare i parametri, se richiesti dallo script.</span><span class="sxs-lookup"><span data-stu-id="1293e-143">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="1293e-144">Lo script per installare Giraph non richiede alcun parametro, di conseguenza è possibile lasciare vuoto questo campo.</span><span class="sxs-lookup"><span data-stu-id="1293e-144">The script to install Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="1293e-145">È possibile aggiungere altre azioni script per installare più componenti nel cluster.</span><span class="sxs-lookup"><span data-stu-id="1293e-145">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="1293e-146">Dopo aver aggiunto gli script, fare clic sul segno di spunta per avviare la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="1293e-146">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="1293e-147">Usare Giraph</span><span class="sxs-lookup"><span data-stu-id="1293e-147">Use Giraph</span></span>
<span data-ttu-id="1293e-148">L'esempio SimpleShortestPathsComputation viene usato per illustrare l'implementazione di base di <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> per trovare il percorso più breve tra oggetti di un grafico.</span><span class="sxs-lookup"><span data-stu-id="1293e-148">We use the SimpleShortestPathsComputation example to demonstrate the basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding the shortest path between objects in a graph.</span></span> <span data-ttu-id="1293e-149">Usare la procedura seguente per caricare i dati e il file JAR di esempio, eseguire un processo con l'esempio SimpleShortestPathsComputation e quindi visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="1293e-149">Use the following steps to upload the sample data and the sample jar, run a job by using the SimpleShortestPathsComputation example, and then view the results.</span></span>

1. <span data-ttu-id="1293e-150">Caricare un file di dati di esempio nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="1293e-150">Upload a sample data file to Azure Blob storage.</span></span> <span data-ttu-id="1293e-151">Nella workstation locale creare un nuovo file denominato **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="1293e-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="1293e-152">Questo file deve contenere le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="1293e-152">It should contain the following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="1293e-153">Caricare il file tiny_graph.txt nella risorsa di archiviazione primaria per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1293e-153">Upload the tiny_graph.txt file to the primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="1293e-154">Per istruzioni su come caricare i dati, vedere [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="1293e-154">For instructions on how to upload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="1293e-155">Questi dati descrivono una relazione tra gli oggetti in un grafico diretto, usando il formato [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span><span class="sxs-lookup"><span data-stu-id="1293e-155">This data describes a relationship between objects in a directed graph, by using the format [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span></span> <span data-ttu-id="1293e-156">Ogni riga rappresenta una relazione tra un oggetto **source\_id** e uno o più oggetti **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="1293e-156">Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="1293e-157">Il valore **edge\_value** (o peso) costituisce la potenza o la distanza della connessione tra **source_id** e **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="1293e-157">The **edge\_value** (or weight) can be thought of as the strength or distance of the connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="1293e-158">I dati disegnati usando il valore (o peso) come distanza tra gli oggetti sono simili a quelli raffigurati di seguito:</span><span class="sxs-lookup"><span data-stu-id="1293e-158">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="1293e-160">Eseguire l'esempio SimpleShortestPathsComputation.</span><span class="sxs-lookup"><span data-stu-id="1293e-160">Run the SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="1293e-161">Usare i cmdlet di Azure PowerShell seguenti per eseguire l'esempio specificando come input il file tiny_graph.txt.</span><span class="sxs-lookup"><span data-stu-id="1293e-161">Use the following Azure PowerShell cmdlets to run the example by using the tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1293e-162">Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** ed è stato rimosso dal 1° gennaio 2017.</span><span class="sxs-lookup"><span data-stu-id="1293e-162">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="1293e-163">La procedura descritta in questo documento usa i nuovi cmdlet HDInsight, compatibili con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1293e-163">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="1293e-164">Per installare la versione più recente, seguire la procedura descritta in [Come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) .</span><span class="sxs-lookup"><span data-stu-id="1293e-164">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="1293e-165">Se sono presenti script che devono essere modificati per l'uso dei nuovi cmdlet compatibili con Azure Resource Manager, per altre informazioni vedere [Migrazione a strumenti di sviluppo basati su Azure Resource Manager per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) .</span><span class="sxs-lookup"><span data-stu-id="1293e-165">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

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
    # Create the definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run the job, write output to the Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="1293e-166">Nell'esempio precedente sostituire **clustername** con il nome del cluster HDInsight in cui è installato Giraph.</span><span class="sxs-lookup"><span data-stu-id="1293e-166">In the above example, replace **clustername** with the name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="1293e-167">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="1293e-167">View the results.</span></span> <span data-ttu-id="1293e-168">Al termine del processo, i risultati verranno archiviati in due file di output nella cartella **wasb:///example/out/shotestpaths**.</span><span class="sxs-lookup"><span data-stu-id="1293e-168">Once the job has finished, the results will be stored in two output files in the **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="1293e-169">I file sono denominati **part-m-00001** e **part-m-00002**.</span><span class="sxs-lookup"><span data-stu-id="1293e-169">The files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="1293e-170">Eseguire la procedura seguente per scaricare e visualizzare l'output:</span><span class="sxs-lookup"><span data-stu-id="1293e-170">Perform the following steps to download and view the output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select the current subscription
    Select-AzureSubscription $subscriptionName

    # Create the Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download the job output to the workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="1293e-171">Nella directory attuale della workstation verrà creata la struttura di directory **example/output/shortestpaths** e i due file di output verranno scaricati in questo percorso.</span><span class="sxs-lookup"><span data-stu-id="1293e-171">This will create the **example/output/shortestpaths** directory structure in the current directory on your workstation, and download the two output files to that location.</span></span>

    <span data-ttu-id="1293e-172">Usare il cmdlet **Cat** per visualizzare i contenuti dei file:</span><span class="sxs-lookup"><span data-stu-id="1293e-172">Use the **Cat** cmdlet to display the contents of the files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="1293e-173">L'output sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="1293e-173">The output should appear similar to the following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="1293e-174">L'esempio SimpleShortestPathComputation è hardcoded in modo da essere avviato con l'ID oggetto 1 e individuare il percorso più breve ad altri oggetti.</span><span class="sxs-lookup"><span data-stu-id="1293e-174">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="1293e-175">L'output dovrebbe quindi essere `destination_id distance`, in cui distance è il valore (o il peso) dei confini attraversati tra l'ID oggetto 1 e l'ID di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1293e-175">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="1293e-176">Con questa visualizzazione è possibile verificare i risultati attraversando i percorsi più brevi tra l'ID 1 e tutti gli altri oggetti.</span><span class="sxs-lookup"><span data-stu-id="1293e-176">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="1293e-177">Notare che il percorso più breve tra l'ID 1 e l'ID 4 è 5,</span><span class="sxs-lookup"><span data-stu-id="1293e-177">Note that the shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="1293e-178">che corrisponde alla distanza totale tra <span style="color:orange">ID 1 e 3</span> e quindi tra <span style="color:red">ID 3 e 4</span>.</span><span class="sxs-lookup"><span data-stu-id="1293e-178">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="1293e-180">Installare Giraph tramite Aure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1293e-180">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="1293e-181">Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="1293e-181">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="1293e-182">L'esempio illustra come installare Spark tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1293e-182">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="1293e-183">È necessario personalizzare lo script da usare [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="1293e-183">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="1293e-184">Installare Giraph tramite .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1293e-184">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="1293e-185">Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="1293e-185">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="1293e-186">L'esempio illustra come installare Spark tramite .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="1293e-186">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="1293e-187">È necessario personalizzare lo script da usare [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="1293e-187">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="1293e-188">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1293e-188">See also</span></span>
* [<span data-ttu-id="1293e-189">Installare Giraph nei cluster Hadoop di HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="1293e-189">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="1293e-190">[Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="1293e-190">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="1293e-191">[Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.</span><span class="sxs-lookup"><span data-stu-id="1293e-191">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="1293e-192">[Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="1293e-192">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="1293e-193">[Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]: esempio di azione script sull'installazione di Spark.</span><span class="sxs-lookup"><span data-stu-id="1293e-193">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="1293e-194">[Installare R nei cluster HDInsight][hdinsight-install-r]: esempio di azione script sull'installazione di R.</span><span class="sxs-lookup"><span data-stu-id="1293e-194">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="1293e-195">[Installare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install.md): esempio di Azione di script sull'installazione di Solr.</span><span class="sxs-lookup"><span data-stu-id="1293e-195">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
