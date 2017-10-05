---
title: Usare R in HDInsight per la personalizzazione dei cluster - Azure | Documentazione Microsoft
description: Informazioni su come installare R tramite Azione di script e su come usare R nei cluster HDInsight.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 5b9b793d49217acd9f0c6c518596a7afb5600d69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="2c4bf-103">Installare e usare R nei cluster Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c4bf-103">Install and use R on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="2c4bf-104">Informazioni su come personalizzare i cluster HDInsight basati su Windows con R usando Azione di script e su come usare R nei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-104">Learn how to customize Windows based HDInsight cluster with R using Script Action, and how to use R on HDInsight clusters.</span></span> <span data-ttu-id="2c4bf-105">L'[offerta per HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) include R Server come parte del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-105">The [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="2c4bf-106">In questo modo gli script R possono usare MapReduce e Spark per eseguire i calcoli distribuiti.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-106">This allows R scripts to use MapReduce and Spark to run distributed computations.</span></span> <span data-ttu-id="2c4bf-107">Per altre informazioni, vedere [Introduzione all'uso di R Server in HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2c4bf-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="2c4bf-108">Per informazioni sull'uso di R con un cluster basato su Linux, vedere [Installare e usare R nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2c4bf-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="2c4bf-109">È possibile installare R in qualsiasi tipo di cluster (Hadoop, Storm, HBase, Spark) su Azure HDInsight usando *Azione di script*.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="2c4bf-110">Uno script di esempio per l'installazione di R in un cluster HDInsight è disponibile in un BLOB di archiviazione di sola lettura di Azure all'indirizzo [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="2c4bf-110">A sample script to install R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="2c4bf-111">**Articoli correlati**</span><span class="sxs-lookup"><span data-stu-id="2c4bf-111">**Related articles**</span></span>

* [<span data-ttu-id="2c4bf-112">Installare e usare R nei cluster Hadoop di HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="2c4bf-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="2c4bf-113">[Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informazioni generali sulla creazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c4bf-113">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="2c4bf-114">[Personalizzare cluster HDInsight mediante l'azione script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="2c4bf-115">Sviluppare script di Azione script per HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c4bf-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="2c4bf-116">Che cos'è R?</span><span class="sxs-lookup"><span data-stu-id="2c4bf-116">What is R?</span></span>
<span data-ttu-id="2c4bf-117"><a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> è un linguaggio open source e un ambiente per l'elaborazione statistica.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-117">The <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="2c4bf-118">R fornisce centinaia di funzioni statistiche integrate e un proprio linguaggio che combina aspetti di programmazione funzionale con aspetti di programmazione orientata agli oggetti.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="2c4bf-119">Offre inoltre funzionalità complete di grafica.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="2c4bf-120">R è l'ambiente di programmazione preferito da numerosi statistici e scienziati professionisti attivi in un'ampia gamma di campi.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-120">R is the preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="2c4bf-121">R è compatibile con WASB (Azure Blob Storage), consentendo di elaborare i dati archiviati usando R in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="2c4bf-122">Installare R</span><span class="sxs-lookup"><span data-stu-id="2c4bf-122">Install R</span></span>
<span data-ttu-id="2c4bf-123">Per installare R in un cluster HDInsight è disponibile uno [script di esempio](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) da un BLOB di sola lettura in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) to install R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="2c4bf-124">Questa sezione contiene istruzioni su come usare lo script di esempio quando si creano cluster usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-124">This section provides instructions about how to use the sample script while creating the cluster using the Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="2c4bf-125">Lo script di esempio è stato introdotto con il cluster HDInsight versione 3.1.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-125">The sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="2c4bf-126">Per altre informazioni sulle versioni dei cluster HDInsight, vedere [Versioni cluster HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="2c4bf-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="2c4bf-127">Durante la creazione di un cluster HDInsight dal portale, fare clic su **Configurazione facoltativa** e quindi fare clic su **Azioni script**.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-127">When you create an HDInsight cluster from the Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="2c4bf-128">Nella pagina **Azioni di script** immettere i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="2c4bf-128">On the **Script Actions** page, enter the following values:</span></span>

    <span data-ttu-id="2c4bf-129">![Usare l'azione script per personalizzare un cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Usare l'azione script per personalizzare un cluster")</span><span class="sxs-lookup"><span data-stu-id="2c4bf-129">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="2c4bf-130">Proprietà</span><span class="sxs-lookup"><span data-stu-id="2c4bf-130">Property</span></span></th><th><span data-ttu-id="2c4bf-131">Valore</span><span class="sxs-lookup"><span data-stu-id="2c4bf-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="2c4bf-132">Nome</span><span class="sxs-lookup"><span data-stu-id="2c4bf-132">Name</span></span></td>
            <td><span data-ttu-id="2c4bf-133">Specificare un nome per l'azione script, ad esempio <b>Installa R</b>.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-133">Specify a name for the script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="2c4bf-134">URI script</span><span class="sxs-lookup"><span data-stu-id="2c4bf-134">Script URI</span></span></td>
            <td><span data-ttu-id="2c4bf-135">Specificare l'URI per lo script che viene richiamato per personalizzare il cluster, ad esempio <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span><span class="sxs-lookup"><span data-stu-id="2c4bf-135">Specify the URI to the script that is invoked to customize the cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="2c4bf-136">Tipo di nodo</span><span class="sxs-lookup"><span data-stu-id="2c4bf-136">Node Type</span></span></td>
            <td><span data-ttu-id="2c4bf-137">Specificare i nodi in cui viene eseguito lo script di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="2c4bf-138">È possibile scegliere <b>Tutti i nodi</b>, <b>Solo nodi head</b> o <b>Solo nodi di lavoro</b>.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="2c4bf-139">Parametri</span><span class="sxs-lookup"><span data-stu-id="2c4bf-139">Parameters</span></span></td>
            <td><span data-ttu-id="2c4bf-140">Specificare i parametri, se richiesti dallo script.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="2c4bf-141">Tuttavia, lo script per installare R non richiede alcun parametro, di conseguenza è possibile lasciare vuoto questo campo.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-141">However, the script to install R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="2c4bf-142">È possibile aggiungere altre azioni di script per installare più componenti nel cluster.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="2c4bf-143">Dopo aver aggiunto gli script, fare clic sul segno di spunta per avviare la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-143">After you have added the scripts, click the check mark to start crating the cluster.</span></span>

<span data-ttu-id="2c4bf-144">È inoltre possibile usare lo script per installare R in HDInsight usando Azure PowerShell o HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-144">You can also use the script to install R on HDInsight by using Azure PowerShell or the HDInsight .NET SDK.</span></span> <span data-ttu-id="2c4bf-145">Le istruzioni relative a queste procedure vengono fornite più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="2c4bf-146">Eseguire gli script R</span><span class="sxs-lookup"><span data-stu-id="2c4bf-146">Run R scripts</span></span>
<span data-ttu-id="2c4bf-147">Questa sezione descrive come eseguire uno script R nel cluster Hadoop con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-147">This section describes how to run an R script on the Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="2c4bf-148">**Stabilire una connessione desktop remoto al cluster**: dal portale, abilitare il desktop remoto per il cluster creato con R installato, quindi connettersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-148">**Establish a Remote Desktop connection to the cluster**: From the Portal, enable Remote Desktop for the cluster you created with R installed, and then connect to the cluster.</span></span> <span data-ttu-id="2c4bf-149">Per istruzioni, vedere [Connettersi a cluster HDInsight tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="2c4bf-149">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="2c4bf-150">**Aprire la console di R**: l'installazione di R inserisce un collegamento alla console di R sul desktop del nodo head.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-150">**Open the R console**: The R installation puts a link to the R console on the desktop of the head node.</span></span> <span data-ttu-id="2c4bf-151">Fare clic su di esso per aprire la console di R.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-151">Click on it to open the R console.</span></span>
3. <span data-ttu-id="2c4bf-152">**Eseguire lo script R**: lo script R può essere eseguito direttamente dalla console di R incollandolo in essa, selezionandolo e premendo Invio.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-152">**Run the R script**: The R script can be run directly from the R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="2c4bf-153">Di seguito è riportato un semplice script di esempio che genera i numeri da 1 a 100 e li moltiplica per 2.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-153">Here is a simple example script that generates the numbers 1 to 100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="2c4bf-154">Le prime due righe chiamano le librerie RHadoop che vengono installate con R. La riga finale stampa i risultati nella console.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-154">The first two lines call the RHadoop libraries that are installed with R. The final line prints the results to the console.</span></span> <span data-ttu-id="2c4bf-155">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2c4bf-155">The output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="2c4bf-156">Installare R usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c4bf-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="2c4bf-157">Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="2c4bf-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="2c4bf-158">L'esempio illustra come installare Spark tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-158">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="2c4bf-159">È necessario personalizzare lo script da usare [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="2c4bf-159">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="2c4bf-160">Installare R usando .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2c4bf-160">Install R using .NET SDK</span></span>
<span data-ttu-id="2c4bf-161">Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="2c4bf-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="2c4bf-162">L'esempio illustra come installare Spark tramite .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-162">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="2c4bf-163">È necessario personalizzare lo script da usare [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span><span class="sxs-lookup"><span data-stu-id="2c4bf-163">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="2c4bf-164">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2c4bf-164">See also</span></span>
* [<span data-ttu-id="2c4bf-165">Installare e usare R nei cluster Hadoop di HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="2c4bf-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="2c4bf-166">[Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informazioni generali sulla creazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c4bf-166">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="2c4bf-167">[Personalizzare cluster HDInsight mediante l'azione script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="2c4bf-168">Sviluppare script di Azione script per HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c4bf-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="2c4bf-169">[Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]: esempio di Azione script sull'installazione di Spark</span><span class="sxs-lookup"><span data-stu-id="2c4bf-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="2c4bf-170">[Installare e usare Spark nei cluster HDInsight](hdinsight-hadoop-giraph-install.md): esempio di Script azione sull'installazione di Giraph</span><span class="sxs-lookup"><span data-stu-id="2c4bf-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="2c4bf-171">[Installare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install-linux.md): esempio di Azione di script sull'installazione di Solr.</span><span class="sxs-lookup"><span data-stu-id="2c4bf-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
