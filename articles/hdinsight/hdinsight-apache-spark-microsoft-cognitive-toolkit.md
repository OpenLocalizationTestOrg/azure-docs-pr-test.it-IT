---
title: Microsoft Cognitive Toolkit in Azure HDInsight Spark per l'apprendimento approfondito | Microsoft Docs
description: Informazioni su come un modello con training per l'apprendimento approfondito Microsoft Cognitive Toolkit possa essere applicato a un set di dati tramite l'API Python Spark in un cluster Azure HDInsight Spark.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: fafd738f782660b824732bab8cc3bec8405947e7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="07008-103">Usare il modello di apprendimento approfondito Microsoft Cognitive Toolkit con un cluster Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="07008-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="07008-104">In questo articolo viene illustrata la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="07008-104">In this article, you do the following steps.</span></span>

1. <span data-ttu-id="07008-105">Eseguire uno script personalizzato per installare Microsoft Cognitive Toolkit in un cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="07008-105">Run a custom script to install Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="07008-106">Caricare un notebook di Jupyter nel cluster Spark per vedere come applicare ai file un modello con training di apprendimento approfondito di Microsoft Cognitive Toolkit in un account di archiviazione BLOB di Azure tramite l'[API Python Spark (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="07008-106">Upload a Jupyter notebook to the Spark cluster to see how to apply a trained Microsoft Cognitive Toolkit deep learning model to files in an Azure Blob Storage Account using the [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07008-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="07008-107">Prerequisites</span></span>

* <span data-ttu-id="07008-108">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="07008-108">**An Azure subscription**.</span></span> <span data-ttu-id="07008-109">Prima di iniziare questa esercitazione, è necessario disporre di un abbonamento ad Azure.</span><span class="sxs-lookup"><span data-stu-id="07008-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="07008-110">Vedere [Crea subito il tuo account Azure gratuito](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="07008-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="07008-111">**Cluster Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="07008-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="07008-112">Per eseguire la procedura dell'articolo, creare un cluster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="07008-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="07008-113">Per le istruzioni, vedere [Creare un cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="07008-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="07008-114">Svolgimento della soluzione</span><span class="sxs-lookup"><span data-stu-id="07008-114">How does this solution flow?</span></span>

<span data-ttu-id="07008-115">Questa soluzione è suddivisa tra questo articolo e un notebook di Jupyter che deve essere caricato come parte di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="07008-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="07008-116">In questo articolo verrà completata la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="07008-116">In this article, you complete the following steps:</span></span>

* <span data-ttu-id="07008-117">Eseguire un'azione script in un cluster HDInsight Spark per installare i pacchetti Microsoft Cognitive Toolkit e Python.</span><span class="sxs-lookup"><span data-stu-id="07008-117">Run a script action on an HDInsight Spark cluster to install Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="07008-118">Caricare il notebook di Jupyter che esegue la soluzione nel cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="07008-118">Upload the Jupyter notebook that runs the solution to the HDInsight Spark cluster.</span></span>

<span data-ttu-id="07008-119">I passaggi rimanenti elencati sotto vengono trattati nel notebook di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="07008-119">The following remaining steps are covered in the Jupyter notebook.</span></span>

- <span data-ttu-id="07008-120">Caricare immagini di esempio in un set di dati resilienti distribuito di Spark o RDD</span><span class="sxs-lookup"><span data-stu-id="07008-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="07008-121">Caricare i moduli e definire i set di impostazioni</span><span class="sxs-lookup"><span data-stu-id="07008-121">Load modules and define presets</span></span>
   - <span data-ttu-id="07008-122">Scaricare il set di dati in locale nel cluster Spark</span><span class="sxs-lookup"><span data-stu-id="07008-122">Download the dataset locally on the Spark cluster</span></span>
   - <span data-ttu-id="07008-123">Convertire il set di dati in RDD</span><span class="sxs-lookup"><span data-stu-id="07008-123">Convert the dataset into an RDD</span></span>
- <span data-ttu-id="07008-124">Classificare le immagini tramite un modello con training Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="07008-124">Score the images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="07008-125">Scaricare il modello con training Cognitive Toolkit nel cluster Spark</span><span class="sxs-lookup"><span data-stu-id="07008-125">Download the trained Cognitive Toolkit model to the Spark cluster</span></span>
   - <span data-ttu-id="07008-126">Definire le funzioni usate dai nodi del ruolo di lavoro</span><span class="sxs-lookup"><span data-stu-id="07008-126">Define functions to be used by worker nodes</span></span>
   - <span data-ttu-id="07008-127">Classificare le immagini nei nodi del ruolo di lavoro</span><span class="sxs-lookup"><span data-stu-id="07008-127">Score the images on worker nodes</span></span>
   - <span data-ttu-id="07008-128">Valutare l'accuratezza del modello</span><span class="sxs-lookup"><span data-stu-id="07008-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="07008-129">Installare Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="07008-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="07008-130">È possibile installare Microsoft Cognitive Toolkit in un cluster Spark tramite l'azione script.</span><span class="sxs-lookup"><span data-stu-id="07008-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="07008-131">L'azione script usa script personalizzati per installare nel cluster i componenti che non sono disponibili per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="07008-131">Script action uses custom scripts to install components on the cluster that are not available by default.</span></span> <span data-ttu-id="07008-132">È possibile usare lo script personalizzato dal portale di Azure tramite HDInsight .NET SDK o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="07008-132">You can use the custom script from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="07008-133">È possibile usare lo script anche per installare il toolkit sia nell’ambito della creazione del cluster sia quando il cluster è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="07008-133">You can also use the script to install the toolkit either as part of cluster creation, or after the cluster is up and running.</span></span> 

<span data-ttu-id="07008-134">In questo articolo il toolkit verrà installato dal portale, dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="07008-134">In this article, we use the portal to install the toolkit, after the cluster has been created.</span></span> <span data-ttu-id="07008-135">Per altri modi di eseguire lo script personalizzato, vedere [Personalizzare cluster HDInsight tramite azione script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="07008-135">For other ways to run the custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="07008-136">Uso del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="07008-136">Using the Azure Portal</span></span>

<span data-ttu-id="07008-137">Per istruzioni su come usare il portale di Azure per eseguire azioni di script, vedere [Personalizzare cluster HDInsight tramite azione script](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="07008-137">For instructions on how to use the Azure Portal to run script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="07008-138">Assicurarsi di specificare i dati seguenti per installare Microsoft Cognitive Toolkit.</span><span class="sxs-lookup"><span data-stu-id="07008-138">Make sure you provide the following inputs to install Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="07008-139">Specificare un valore per il nome dell'azione script.</span><span class="sxs-lookup"><span data-stu-id="07008-139">Provide a value for the script action name.</span></span>

* <span data-ttu-id="07008-140">Per **URI script Bash**, immettere `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="07008-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="07008-141">Assicurarsi di eseguire lo script solo nei nodi head e del ruolo di lavoro e deselezionare tutte le altre caselle di controllo.</span><span class="sxs-lookup"><span data-stu-id="07008-141">Make sure you run the script only on the head and worker nodes and clear all the other checkboxes.</span></span>

* <span data-ttu-id="07008-142">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="07008-142">Click **Create**.</span></span>

## <a name="upload-the-jupyter-notebook-to-azure-hdinsight-spark-cluster"></a><span data-ttu-id="07008-143">Caricare il notebook di Jupyter nel cluster Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="07008-143">Upload the Jupyter notebook to Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="07008-144">Per usare Microsoft Cognitive Toolkit con il cluster Azure HDInsight Spark, è necessario caricare il notebook di Jupyter **CNTK_model_scoring_on_Spark_walkthrough.ipynb** nel cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="07008-144">To use the Microsoft Cognitive Toolkit with the Azure HDInsight Spark cluster, you must load the Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** to the Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="07008-145">Il notebook è disponibile in GitHub all'indirizzo [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="07008-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="07008-146">Clonare il repository di GitHub all'indirizzo [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="07008-146">Clone the GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="07008-147">Per istruzioni su come eseguire la clonazione, vedere [Cloning a repository](https://help.github.com/articles/cloning-a-repository/) (Clonazione di un repository).</span><span class="sxs-lookup"><span data-stu-id="07008-147">For instructions to clone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="07008-148">Dal portale di Azure, aprire il pannello del cluster Spark di cui è già stato eseguito il provisioning, fare clic su **Dashboard cluster** e quindi su **Notebook di Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="07008-148">From the Azure Portal, open the Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="07008-149">È anche possibile avviare il notebook di Jupyter accedendo all'URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="07008-149">You can also launch the Jupyter notebook by going to the URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="07008-150">Sostituire \<clustername> con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="07008-150">Replace \<clustername> with the name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="07008-151">Dal notebook di Jupyter, fare clic su **Carica** nell'angolo in alto a destra e passare al percorso in cui è stato clonato il repository di GitHub.</span><span class="sxs-lookup"><span data-stu-id="07008-151">From the Jupyter notebook, click **Upload** in the top-right corner and then navigate to the location where you cloned the GitHub repository.</span></span>

    <span data-ttu-id="07008-152">![Caricare il notebook di Jupyter nel cluster Azure HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Caricare il notebook di Jupyter nel cluster Azure HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="07008-152">![Upload Jupyter notebook to Azure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="07008-153">Fare ancora clic su **Carica**.</span><span class="sxs-lookup"><span data-stu-id="07008-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="07008-154">Dopo averlo caricato, fare clic sul nome del notebook e seguire le istruzioni nel notebook stesso su come caricare il set di dati ed eseguire l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="07008-154">After the notebook is uploaded, click the name of the notebook and then follow the instructions in the notebook itself on how to load the data set and perform the tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="07008-155">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="07008-155">See also</span></span>
* [<span data-ttu-id="07008-156">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="07008-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="07008-157">Scenari</span><span class="sxs-lookup"><span data-stu-id="07008-157">Scenarios</span></span>
* [<span data-ttu-id="07008-158">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="07008-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="07008-159">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="07008-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="07008-160">Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="07008-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="07008-161">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="07008-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="07008-162">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="07008-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="07008-163">Application Insight telemetry data analysis using Spark in HDInsight (Analisi dei dati di telemetria di Application Insights con Spark in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="07008-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="07008-164">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="07008-164">Create and run applications</span></span>
* [<span data-ttu-id="07008-165">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="07008-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="07008-166">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="07008-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="07008-167">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="07008-167">Tools and extensions</span></span>
* [<span data-ttu-id="07008-168">Usare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="07008-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="07008-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Usare il plug-in Strumenti HDInsight per IntelliJ IDEA per eseguire il debug di applicazioni Spark in remoto)</span><span class="sxs-lookup"><span data-stu-id="07008-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="07008-170">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="07008-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="07008-171">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="07008-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="07008-172">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="07008-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="07008-173">Installare Jupyter Notebook nel computer e connetterlo a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="07008-173">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="07008-174">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="07008-174">Manage resources</span></span>
* [<span data-ttu-id="07008-175">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="07008-175">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="07008-176">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="07008-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
