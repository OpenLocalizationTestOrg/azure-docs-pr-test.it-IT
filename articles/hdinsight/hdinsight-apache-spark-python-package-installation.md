---
title: azione aaaScript - i pacchetti di installazione di Python con Jupyter in Azure HDInsight | Documenti Microsoft
description: Istruzioni dettagliate su come i cluster di pacchetti python esterno toouse notebook Jupyter delle tooconfigure di azione script toouse disponibili con HDInsight Spark.
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
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="b670a-103">Utilizzare i pacchetti genera Script azione tooinstall esterni Python per notebook Jupyter cluster Apache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b670a-103">Use Script Action tooinstall external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b670a-104">Uso di comandi Magic nelle celle</span><span class="sxs-lookup"><span data-stu-id="b670a-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="b670a-105">Uso di azioni script</span><span class="sxs-lookup"><span data-stu-id="b670a-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="b670a-106">Informazioni su come toouse azioni Script tooconfigure un cluster di Apache Spark in HDInsight (Linux) toouse esterno,-il contributo della community **python** di casella pacchetti che non sono presenti cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b670a-106">Learn how toouse Script Actions tooconfigure an Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed **python** packages that are not included out-of-the-box in hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b670a-107">È inoltre possibile configurare un server Jupyter notebook tramite `%%configure` particolare toouse i pacchetti esterni.</span><span class="sxs-lookup"><span data-stu-id="b670a-107">You can also configure a Jupyter notebook by using `%%configure` magic toouse external packages.</span></span> <span data-ttu-id="b670a-108">Per istruzioni, vedere [Usare pacchetti esterni con notebook di Jupyter nei cluster Apache Spark in HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b670a-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="b670a-109">È possibile cercare hello [indice del pacchetto](https://pypi.python.org/pypi) per l'elenco completo di hello dei pacchetti disponibili.</span><span class="sxs-lookup"><span data-stu-id="b670a-109">You can search hello [package index](https://pypi.python.org/pypi) for hello complete list of packages that are available.</span></span> <span data-ttu-id="b670a-110">È anche possibile ottenere un elenco dei pacchetti disponibili da altre origini.</span><span class="sxs-lookup"><span data-stu-id="b670a-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="b670a-111">È possibile ad esempio installare pacchetti resi disponibili tramite [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) o [conda-forge](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="b670a-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="b670a-112">In questo articolo si apprenderà come hello tooinstall [TensorFlow](https://www.tensorflow.org/) pacchetto tramite Script Actoin sul cluster e utilizzarlo tramite notebook Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="b670a-112">In this article, you will learn how tooinstall hello [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via hello Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b670a-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b670a-113">Prerequisites</span></span>
<span data-ttu-id="b670a-114">È necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="b670a-114">You must have hello following:</span></span>

* <span data-ttu-id="b670a-115">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b670a-115">An Azure subscription.</span></span> <span data-ttu-id="b670a-116">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b670a-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b670a-117">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b670a-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b670a-118">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b670a-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="b670a-119">Se non dispone di un cluster Spark in HDInsight Linux, è possibile eseguire le azioni script durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="b670a-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="b670a-120">Visitare documentazione hello [come toouse custom script azioni](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="b670a-120">Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="b670a-121">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="b670a-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="b670a-122">Da hello [portale Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello).</span><span class="sxs-lookup"><span data-stu-id="b670a-122">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="b670a-123">È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b670a-123">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="b670a-124">Dal Pannello di cluster Spark hello, fare clic su **azioni Script** in **utilizzo**.</span><span class="sxs-lookup"><span data-stu-id="b670a-124">From hello Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="b670a-125">Eseguire l'azione personalizzata hello che installa TensorFlow nei nodi head di hello e nodi di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="b670a-125">Run hello custom action that installs TensorFlow in hello head nodes and hello worker nodes.</span></span> <span data-ttu-id="b670a-126">script bash Hello possibile fare riferimento da: documentazione di hello visita https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh su [come toouse custom script azioni](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="b670a-126">hello bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="b670a-127">Esistono due python installazioni cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b670a-127">There are two python installations in hello cluster.</span></span> <span data-ttu-id="b670a-128">Spark utilizzerà l'installazione di python Anaconda hello in `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="b670a-128">Spark will use hello Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="b670a-129">Fare riferimento a tale installazione nelle azioni personalizzate tramite `/usr/bin/anaconda/bin/pip` e `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="b670a-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="b670a-130">Aprire un notebook PySpark Jupyter</span><span class="sxs-lookup"><span data-stu-id="b670a-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="b670a-131">![Creare un nuovo notebook Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Creare un nuovo notebook Jupyter")</span><span class="sxs-lookup"><span data-stu-id="b670a-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="b670a-132">Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="b670a-132">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="b670a-133">Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="b670a-133">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="b670a-134">![Specificare un nome per notebook hello](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "specificare un nome per notebook hello")</span><span class="sxs-lookup"><span data-stu-id="b670a-134">![Provide a name for hello notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="b670a-135">A questo punto verranno eseguiti il codice relativo a `import tensorflow` e l'esempio di tipo hello world.</span><span class="sxs-lookup"><span data-stu-id="b670a-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="b670a-136">Codice toocopy:</span><span class="sxs-lookup"><span data-stu-id="b670a-136">Code toocopy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="b670a-137">risultato Hello sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b670a-137">hello result will look like this:</span></span>
    
    <span data-ttu-id="b670a-138">![Esecuzione del codice TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Esecuzione del codice TensorFlow")</span><span class="sxs-lookup"><span data-stu-id="b670a-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="b670a-139"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b670a-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="b670a-140">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b670a-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="b670a-141">Scenari</span><span class="sxs-lookup"><span data-stu-id="b670a-141">Scenarios</span></span>
* [<span data-ttu-id="b670a-142">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b670a-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b670a-143">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="b670a-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b670a-144">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="b670a-144">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b670a-145">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="b670a-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b670a-146">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b670a-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b670a-147">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="b670a-147">Create and run applications</span></span>
* [<span data-ttu-id="b670a-148">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="b670a-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b670a-149">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="b670a-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b670a-150">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="b670a-150">Tools and extensions</span></span>
* [<span data-ttu-id="b670a-151">Usare pacchetti esterni con notebook di Jupyter nei cluster Apache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b670a-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b670a-152">Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="b670a-152">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b670a-153">Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota</span><span class="sxs-lookup"><span data-stu-id="b670a-153">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b670a-154">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b670a-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b670a-155">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="b670a-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b670a-156">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="b670a-156">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b670a-157">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="b670a-157">Manage resources</span></span>
* [<span data-ttu-id="b670a-158">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="b670a-158">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b670a-159">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b670a-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
