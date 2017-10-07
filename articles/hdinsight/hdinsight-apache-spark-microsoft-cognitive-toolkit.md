---
title: aaaMicrosoft cognitivi Toolkit con Azure HDInsight Spark per deep learning | Documenti Microsoft
description: "Informazioni su come un training Microsoft cognitivi Toolkit completa modello di apprendimento può essere applicato tooa set di dati utilizzando hello Spark Python API in un cluster Azure HDInsight Spark."
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
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="6a9c4-103">Usare il modello di apprendimento approfondito Microsoft Cognitive Toolkit con un cluster Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="6a9c4-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="6a9c4-104">In questo articolo, hello i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-104">In this article, you do hello following steps.</span></span>

1. <span data-ttu-id="6a9c4-105">Eseguire un tooinstall script personalizzato Microsoft cognitivi Toolkit in un cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-105">Run a custom script tooinstall Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="6a9c4-106">Caricare un toosee cluster Spark di Jupyter notebook toohello come tooapply con training Microsoft cognitivi Toolkit deep learning toofiles modello in un Account di archiviazione Blob di Azure utilizzando hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="6a9c4-106">Upload a Jupyter notebook toohello Spark cluster toosee how tooapply a trained Microsoft Cognitive Toolkit deep learning model toofiles in an Azure Blob Storage Account using hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a9c4-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6a9c4-107">Prerequisites</span></span>

* <span data-ttu-id="6a9c4-108">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-108">**An Azure subscription**.</span></span> <span data-ttu-id="6a9c4-109">Prima di iniziare questa esercitazione, è necessario disporre di un abbonamento ad Azure.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="6a9c4-110">Vedere [Crea subito il tuo account Azure gratuito](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="6a9c4-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="6a9c4-111">**Cluster Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="6a9c4-112">Per eseguire la procedura dell'articolo, creare un cluster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="6a9c4-113">Per le istruzioni, vedere [Creare un cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="6a9c4-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="6a9c4-114">Svolgimento della soluzione</span><span class="sxs-lookup"><span data-stu-id="6a9c4-114">How does this solution flow?</span></span>

<span data-ttu-id="6a9c4-115">Questa soluzione è suddivisa tra questo articolo e un notebook di Jupyter che deve essere caricato come parte di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="6a9c4-116">In questo articolo è completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6a9c4-116">In this article, you complete hello following steps:</span></span>

* <span data-ttu-id="6a9c4-117">Eseguire un'azione di script in un cluster di HDInsight Spark tooinstall Microsoft cognitivi Toolkit e Python pacchetti.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-117">Run a script action on an HDInsight Spark cluster tooinstall Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="6a9c4-118">Caricare notebook Jupyter hello che esegue hello soluzione toohello cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-118">Upload hello Jupyter notebook that runs hello solution toohello HDInsight Spark cluster.</span></span>

<span data-ttu-id="6a9c4-119">Hello seguenti passaggi rimanenti vengono trattati in notebook Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-119">hello following remaining steps are covered in hello Jupyter notebook.</span></span>

- <span data-ttu-id="6a9c4-120">Caricare immagini di esempio in un set di dati resilienti distribuito di Spark o RDD</span><span class="sxs-lookup"><span data-stu-id="6a9c4-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="6a9c4-121">Caricare i moduli e definire i set di impostazioni</span><span class="sxs-lookup"><span data-stu-id="6a9c4-121">Load modules and define presets</span></span>
   - <span data-ttu-id="6a9c4-122">Scaricare hello set di dati in locale nel cluster Spark hello</span><span class="sxs-lookup"><span data-stu-id="6a9c4-122">Download hello dataset locally on hello Spark cluster</span></span>
   - <span data-ttu-id="6a9c4-123">Convertire i set di dati hello in un RDD</span><span class="sxs-lookup"><span data-stu-id="6a9c4-123">Convert hello dataset into an RDD</span></span>
- <span data-ttu-id="6a9c4-124">Immagini di hello punteggio usando un modello del Toolkit cognitivi con training</span><span class="sxs-lookup"><span data-stu-id="6a9c4-124">Score hello images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="6a9c4-125">Scaricare il cluster Spark toohello di hello training Toolkit cognitivi modello</span><span class="sxs-lookup"><span data-stu-id="6a9c4-125">Download hello trained Cognitive Toolkit model toohello Spark cluster</span></span>
   - <span data-ttu-id="6a9c4-126">Definire le funzioni toobe usata dai nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="6a9c4-126">Define functions toobe used by worker nodes</span></span>
   - <span data-ttu-id="6a9c4-127">Immagini di punteggio hello nei nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="6a9c4-127">Score hello images on worker nodes</span></span>
   - <span data-ttu-id="6a9c4-128">Valutare l'accuratezza del modello</span><span class="sxs-lookup"><span data-stu-id="6a9c4-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="6a9c4-129">Installare Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="6a9c4-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="6a9c4-130">È possibile installare Microsoft Cognitive Toolkit in un cluster Spark tramite l'azione script.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="6a9c4-131">Genera script azione utilizza componenti tooinstall script personalizzati nel cluster hello che non sono disponibili per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-131">Script action uses custom scripts tooinstall components on hello cluster that are not available by default.</span></span> <span data-ttu-id="6a9c4-132">È possibile utilizzare uno script personalizzato hello da hello del portale di Azure tramite HDInsight .NET SDK oppure tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-132">You can use hello custom script from hello Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="6a9c4-133">È inoltre possibile utilizzare hello script tooinstall hello toolkit come parte della creazione del cluster, o dopo i cluster di hello sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-133">You can also use hello script tooinstall hello toolkit either as part of cluster creation, or after hello cluster is up and running.</span></span> 

<span data-ttu-id="6a9c4-134">In questo articolo, utilizziamo hello tooinstall portale hello toolkit, dopo aver creato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-134">In this article, we use hello portal tooinstall hello toolkit, after hello cluster has been created.</span></span> <span data-ttu-id="6a9c4-135">Per altri modi toorun hello uno script personalizzato, vedere [HDInsight personalizzare cluster tramite Script azione](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6a9c4-135">For other ways toorun hello custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="6a9c4-136">Utilizzo di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6a9c4-136">Using hello Azure Portal</span></span>

<span data-ttu-id="6a9c4-137">Per istruzioni su come toouse hello Azure Portal toorun eseguito uno script di azione, vedere [HDInsight personalizzare cluster tramite Script azione](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="6a9c4-137">For instructions on how toouse hello Azure Portal toorun script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="6a9c4-138">Assicurarsi di fornire hello seguente input tooinstall Microsoft cognitivi Toolkit.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-138">Make sure you provide hello following inputs tooinstall Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="6a9c4-139">Specificare un valore per nome dell'azione script hello.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-139">Provide a value for hello script action name.</span></span>

* <span data-ttu-id="6a9c4-140">Per **URI script Bash**, immettere `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="6a9c4-141">Verificare che si esegue uno script hello solo in hello nodi head e di lavoro e deselezionare tutti hello altre caselle di controllo.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-141">Make sure you run hello script only on hello head and worker nodes and clear all hello other checkboxes.</span></span>

* <span data-ttu-id="6a9c4-142">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-142">Click **Create**.</span></span>

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a><span data-ttu-id="6a9c4-143">Caricare hello Jupyter notebook tooAzure cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="6a9c4-143">Upload hello Jupyter notebook tooAzure HDInsight Spark cluster</span></span>

<span data-ttu-id="6a9c4-144">hello toouse Microsoft cognitivi Toolkit con cluster Azure HDInsight Spark hello, è necessario caricare notebook Jupyter hello **CNTK_model_scoring_on_Spark_walkthrough.ipynb** cluster Azure HDInsight Spark toohello.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-144">toouse hello Microsoft Cognitive Toolkit with hello Azure HDInsight Spark cluster, you must load hello Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="6a9c4-145">Il notebook è disponibile in GitHub all'indirizzo [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="6a9c4-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="6a9c4-146">Repository di GitHub hello clone [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="6a9c4-146">Clone hello GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="6a9c4-147">Per istruzioni tooclone, vedere [clonazione di un repository](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="6a9c4-147">For instructions tooclone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="6a9c4-148">Hello portale di Azure, aprire Pannello cluster Spark hello in cui è già stato eseguito il provisioning, fare clic su **Dashboard Cluster**, quindi fare clic su **server Jupyter notebook**.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-148">From hello Azure Portal, open hello Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="6a9c4-149">È anche possibile avviare notebook Jupyter hello passando toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-149">You can also launch hello Jupyter notebook by going toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="6a9c4-150">Sostituire \<clustername > con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-150">Replace \<clustername> with hello name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="6a9c4-151">Notebook Jupyter hello, fare clic su **caricare** in hello nell'angolo superiore destro e quindi passare toohello percorso in cui è stato clonato repository GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-151">From hello Jupyter notebook, click **Upload** in hello top-right corner and then navigate toohello location where you cloned hello GitHub repository.</span></span>

    <span data-ttu-id="6a9c4-152">![Caricare Jupyter notebook tooAzure cluster HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "caricare Jupyter notebook tooAzure cluster HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="6a9c4-152">![Upload Jupyter notebook tooAzure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook tooAzure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="6a9c4-153">Fare ancora clic su **Carica**.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="6a9c4-154">Dopo aver caricato notebook hello, fare clic sul nome del blocco appunti hello hello e segui le istruzioni di hello in blocco per Appunti hello stesso come tooload hello set di dati e come eseguire l'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="6a9c4-154">After hello notebook is uploaded, click hello name of hello notebook and then follow hello instructions in hello notebook itself on how tooload hello data set and perform hello tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="6a9c4-155">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="6a9c4-155">See also</span></span>
* [<span data-ttu-id="6a9c4-156">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6a9c4-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="6a9c4-157">Scenari</span><span class="sxs-lookup"><span data-stu-id="6a9c4-157">Scenarios</span></span>
* [<span data-ttu-id="6a9c4-158">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6a9c4-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="6a9c4-159">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="6a9c4-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="6a9c4-160">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="6a9c4-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="6a9c4-161">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="6a9c4-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="6a9c4-162">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6a9c4-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="6a9c4-163">Application Insight telemetry data analysis using Spark in HDInsight (Analisi dei dati di telemetria di Application Insights con Spark in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="6a9c4-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="6a9c4-164">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="6a9c4-164">Create and run applications</span></span>
* [<span data-ttu-id="6a9c4-165">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="6a9c4-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="6a9c4-166">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="6a9c4-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="6a9c4-167">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="6a9c4-167">Tools and extensions</span></span>
* [<span data-ttu-id="6a9c4-168">Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="6a9c4-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="6a9c4-169">Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota</span><span class="sxs-lookup"><span data-stu-id="6a9c4-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="6a9c4-170">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6a9c4-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="6a9c4-171">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="6a9c4-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="6a9c4-172">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="6a9c4-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="6a9c4-173">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="6a9c4-173">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="6a9c4-174">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="6a9c4-174">Manage resources</span></span>
* [<span data-ttu-id="6a9c4-175">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="6a9c4-175">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="6a9c4-176">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6a9c4-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
