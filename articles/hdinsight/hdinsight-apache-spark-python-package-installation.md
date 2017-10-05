---
title: 'Azione script: installare pacchetti Python con Jupyter in Azure HDInsight | Documentazione Microsoft'
description: "Istruzioni dettagliate su come usare l’azione script e configurare notebook di Jupyter disponibili con cluster HDInsight Spark per l'uso di pacchetti Python esterni."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 20cf384c96d4ff4eaf064c8880ad128d521fb9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-script-action-to-install-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="e6b5c-103">Usare Azioni script per installare pacchetti Python esterni per notebook di Jupyter in cluster Apache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6b5c-103">Use Script Action to install external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6b5c-104">Uso di comandi Magic nelle celle</span><span class="sxs-lookup"><span data-stu-id="e6b5c-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="e6b5c-105">Uso di azioni script</span><span class="sxs-lookup"><span data-stu-id="e6b5c-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="e6b5c-106">Vengono fornite informazioni su come usare le azioni script per configurare un cluster Apache Spark in HDInsight (Linux) per l'uso di pacchetti **python** esterni creati dalla community non inclusi e non immediatamente disponibili nel cluster.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-106">Learn how to use Script Actions to configure an Apache Spark cluster on HDInsight (Linux) to use external, community-contributed **python** packages that are not included out-of-the-box in the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="e6b5c-107">È anche possibile configurare un notebook di Jupyter con il comando Magic `%%configure` per usare pacchetti esterni.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-107">You can also configure a Jupyter notebook by using `%%configure` magic to use external packages.</span></span> <span data-ttu-id="e6b5c-108">Per istruzioni, vedere [Usare pacchetti esterni con notebook di Jupyter nei cluster Apache Spark in HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e6b5c-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="e6b5c-109">Per un elenco completo dei pacchetti disponibili, è possibile eseguire una ricerca nell'[indice di pacchetto](https://pypi.python.org/pypi).</span><span class="sxs-lookup"><span data-stu-id="e6b5c-109">You can search the [package index](https://pypi.python.org/pypi) for the complete list of packages that are available.</span></span> <span data-ttu-id="e6b5c-110">È anche possibile ottenere un elenco dei pacchetti disponibili da altre origini.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="e6b5c-111">È possibile ad esempio installare pacchetti resi disponibili tramite [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) o [conda-forge](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="e6b5c-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="e6b5c-112">Questo articolo descrive come installare il pacchetto [TensorFlow](https://www.tensorflow.org/) usando azioni script nel cluster e come usarlo tramite notebook di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-112">In this article, you will learn how to install the [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via the Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6b5c-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e6b5c-113">Prerequisites</span></span>
<span data-ttu-id="e6b5c-114">È necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="e6b5c-114">You must have the following:</span></span>

* <span data-ttu-id="e6b5c-115">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-115">An Azure subscription.</span></span> <span data-ttu-id="e6b5c-116">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e6b5c-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e6b5c-117">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e6b5c-118">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e6b5c-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="e6b5c-119">Se non dispone di un cluster Spark in HDInsight Linux, è possibile eseguire le azioni script durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="e6b5c-120">Vedere la documentazione su [come usare azioni script personalizzate](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="e6b5c-120">Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="e6b5c-121">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="e6b5c-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="e6b5c-122">Dalla Schermata iniziale del [portale di Azure](https://portal.azure.com/)fare clic sul riquadro del cluster Spark (se è stato aggiunto sulla Schermata iniziale).</span><span class="sxs-lookup"><span data-stu-id="e6b5c-122">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="e6b5c-123">È anche possibile passare al cluster da **Esplora tutto** > **Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-123">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="e6b5c-124">Nel pannello del cluster Spark fare clic su **Azioni script** in **Utilizzo**.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-124">From the Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="e6b5c-125">Eseguire l'azione personalizzata per installare TensorFlow nei nodi head e nei nodi del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-125">Run the custom action that installs TensorFlow in the head nodes and the worker nodes.</span></span> <span data-ttu-id="e6b5c-126">Per informazioni sullo script Bash, fare riferimento al sito https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh. Vedere la documentazione su [come usare le azioni script personalizzate](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="e6b5c-126">The bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="e6b5c-127">Nel cluster sono presenti due installazioni di Python.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-127">There are two python installations in the cluster.</span></span> <span data-ttu-id="e6b5c-128">Spark userà l'installazione Anaconda Python che si trova in `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-128">Spark will use the Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="e6b5c-129">Fare riferimento a tale installazione nelle azioni personalizzate tramite `/usr/bin/anaconda/bin/pip` e `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="e6b5c-130">Aprire un notebook PySpark Jupyter</span><span class="sxs-lookup"><span data-stu-id="e6b5c-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="e6b5c-131">![Creare un nuovo notebook Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Creare un nuovo notebook Jupyter")</span><span class="sxs-lookup"><span data-stu-id="e6b5c-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="e6b5c-132">Un nuovo notebook verrà creato e aperto con il nome Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-132">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="e6b5c-133">Fare clic sul nome del notebook nella parte superiore e immettere un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-133">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="e6b5c-134">![Specificare un nome per il notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Specificare un nome per il notebook")</span><span class="sxs-lookup"><span data-stu-id="e6b5c-134">![Provide a name for the notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="e6b5c-135">A questo punto verranno eseguiti il codice relativo a `import tensorflow` e l'esempio di tipo hello world.</span><span class="sxs-lookup"><span data-stu-id="e6b5c-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="e6b5c-136">Codice da copiare:</span><span class="sxs-lookup"><span data-stu-id="e6b5c-136">Code to copy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="e6b5c-137">Il risultato avrà l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="e6b5c-137">The result will look like this:</span></span>
    
    <span data-ttu-id="e6b5c-138">![Esecuzione del codice TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Esecuzione del codice TensorFlow")</span><span class="sxs-lookup"><span data-stu-id="e6b5c-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="e6b5c-139"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e6b5c-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="e6b5c-140">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6b5c-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="e6b5c-141">Scenari</span><span class="sxs-lookup"><span data-stu-id="e6b5c-141">Scenarios</span></span>
* [<span data-ttu-id="e6b5c-142">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6b5c-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e6b5c-143">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="e6b5c-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="e6b5c-144">Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="e6b5c-144">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e6b5c-145">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="e6b5c-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="e6b5c-146">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6b5c-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="e6b5c-147">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="e6b5c-147">Create and run applications</span></span>
* [<span data-ttu-id="e6b5c-148">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="e6b5c-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e6b5c-149">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="e6b5c-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="e6b5c-150">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="e6b5c-150">Tools and extensions</span></span>
* [<span data-ttu-id="e6b5c-151">Usare pacchetti esterni con notebook di Jupyter nei cluster Apache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6b5c-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="e6b5c-152">Usare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="e6b5c-152">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e6b5c-153">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Usare il plug-in Strumenti HDInsight per IntelliJ IDEA per eseguire il debug di applicazioni Spark in remoto)</span><span class="sxs-lookup"><span data-stu-id="e6b5c-153">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="e6b5c-154">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6b5c-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="e6b5c-155">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6b5c-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e6b5c-156">Installare Jupyter nel computer e connetterlo a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="e6b5c-156">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="e6b5c-157">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="e6b5c-157">Manage resources</span></span>
* [<span data-ttu-id="e6b5c-158">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6b5c-158">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e6b5c-159">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6b5c-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
