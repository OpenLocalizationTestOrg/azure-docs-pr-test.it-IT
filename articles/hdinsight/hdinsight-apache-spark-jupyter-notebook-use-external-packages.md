---
title: Usare i pacchetti Maven personalizzati con Jupyter in Spark in Azure HDInsight | Microsoft Docs
description: Istruzioni dettagliate su come configurare i notebook di Jupyter disponibili con i cluster HDInsight Spark per l'uso di pacchetti Maven personalizzati.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 0bcfe220e60e34937c667c7b416065d5f3dc8d63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="163e9-103">Usare pacchetti esterni con notebook di Jupyter nei cluster Apache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="163e9-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="163e9-104">Uso di comandi Magic nelle celle</span><span class="sxs-lookup"><span data-stu-id="163e9-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="163e9-105">Uso di azioni script</span><span class="sxs-lookup"><span data-stu-id="163e9-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="163e9-106">Informazioni su come configurare un notebook di Jupyter in un cluster Apache Spark in HDInsight per l'uso di pacchetti **maven** esterni creati dalla community e non inclusi per impostazione predefinita nel cluster.</span><span class="sxs-lookup"><span data-stu-id="163e9-106">Learn how to configure a Jupyter notebook in Apache Spark cluster on HDInsight to use external, community-contributed **maven** packages that are not included out-of-the-box in the cluster.</span></span> 

<span data-ttu-id="163e9-107">Per un elenco completo dei pacchetti disponibili, è possibile eseguire ricerche nel [repository Maven](http://search.maven.org/) .</span><span class="sxs-lookup"><span data-stu-id="163e9-107">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="163e9-108">È anche possibile ottenere un elenco dei pacchetti disponibili da altre origini.</span><span class="sxs-lookup"><span data-stu-id="163e9-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="163e9-109">Ad esempio, un elenco completo dei pacchetti creati dalla community è disponibile nel sito Web [spark-packages.org](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="163e9-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="163e9-110">In questo articolo si apprenderà a usare il pacchetto [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) con Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="163e9-110">In this article, you will learn how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="163e9-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="163e9-111">Prerequisites</span></span>
<span data-ttu-id="163e9-112">È necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="163e9-112">You must have the following:</span></span>

* <span data-ttu-id="163e9-113">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="163e9-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="163e9-114">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="163e9-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="163e9-115">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="163e9-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="163e9-116">Dalla Schermata iniziale del [portale di Azure](https://portal.azure.com/)fare clic sul riquadro del cluster Spark (se è stato aggiunto sulla Schermata iniziale).</span><span class="sxs-lookup"><span data-stu-id="163e9-116">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="163e9-117">È anche possibile passare al cluster da **Esplora tutto** > **Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="163e9-117">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="163e9-118">Dal pannello del cluster Spark fare clic su **Collegamenti rapidi** e dal pannello **Dashboard cluster** fare clic su **Notebook di Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="163e9-118">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="163e9-119">Se richiesto, immettere le credenziali per il cluster.</span><span class="sxs-lookup"><span data-stu-id="163e9-119">If prompted, enter the admin credentials for the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="163e9-120">È anche possibile raggiungere il notebook di Jupyter per il cluster aprendo l'URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="163e9-120">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="163e9-121">Sostituire **CLUSTERNAME** con il nome del cluster:</span><span class="sxs-lookup"><span data-stu-id="163e9-121">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="163e9-122">Creare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="163e9-122">Create a new notebook.</span></span> <span data-ttu-id="163e9-123">Fare clic su **New** (Nuovo) e quindi su **Spark**.</span><span class="sxs-lookup"><span data-stu-id="163e9-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="163e9-124">![Creare un nuovo notebook Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Creare un nuovo notebook Jupyter")</span><span class="sxs-lookup"><span data-stu-id="163e9-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="163e9-125">Un nuovo notebook verrà creato e aperto con il nome Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="163e9-125">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="163e9-126">Fare clic sul nome del notebook nella parte superiore e immettere un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="163e9-126">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="163e9-127">![Specificare un nome per il notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Specificare un nome per il notebook")</span><span class="sxs-lookup"><span data-stu-id="163e9-127">![Provide a name for the notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="163e9-128">Si userà `%%configure` magic verrà usato per configurare il notebook per l'uso di un pacchetto esterno.</span><span class="sxs-lookup"><span data-stu-id="163e9-128">You will use the `%%configure` magic to configure the notebook to use an external package.</span></span> <span data-ttu-id="163e9-129">Nei notebook che usano pacchetti esterni assicurarsi di richiamare `%%configure` magic nella prima cella del codice.</span><span class="sxs-lookup"><span data-stu-id="163e9-129">In notebooks that use external packages, make sure you call the `%%configure` magic in the first code cell.</span></span> <span data-ttu-id="163e9-130">Questo accorgimento garantisce che il kernel sia configurato per l'uso del pacchetto prima dell'avvio della sessione.</span><span class="sxs-lookup"><span data-stu-id="163e9-130">This ensures that the kernel is configured to use the package before the session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="163e9-131">Se si dimentica di configurare il kernel nella prima cella, è possibile usare `%%configure` magic con il parametro `-f`. In questo modo, tuttavia, la sessione verrà riavviata e le operazioni eseguite andranno perse.</span><span class="sxs-lookup"><span data-stu-id="163e9-131">If you forget to configure the kernel in the first cell, you can use the `%%configure` with the `-f` parameter, but that will restart the session and all progress will be lost.</span></span>

    | <span data-ttu-id="163e9-132">Versione HDInsight</span><span class="sxs-lookup"><span data-stu-id="163e9-132">HDInsight version</span></span> | <span data-ttu-id="163e9-133">Comando</span><span class="sxs-lookup"><span data-stu-id="163e9-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="163e9-134">Per HDInsight 3.3 e HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="163e9-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="163e9-135">Per HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="163e9-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="163e9-136">Il frammento di codice riportato sopra attende le coordinate Maven per il pacchetto esterno nel repository centrale Maven.</span><span class="sxs-lookup"><span data-stu-id="163e9-136">The snippet above expects the maven coordinates for the external package in Maven Central Repository.</span></span> <span data-ttu-id="163e9-137">In questo frammento di codice `com.databricks:spark-csv_2.10:1.4.0` è la coordinata Maven per il pacchetto **spark-csv** .</span><span class="sxs-lookup"><span data-stu-id="163e9-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is the maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="163e9-138">Di seguito viene spiegato come creare le coordinate per un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="163e9-138">Here's how you construct the coordinates for a package.</span></span>
   
    <span data-ttu-id="163e9-139">a.</span><span class="sxs-lookup"><span data-stu-id="163e9-139">a.</span></span> <span data-ttu-id="163e9-140">Individuare un pacchetto nel repository Maven.</span><span class="sxs-lookup"><span data-stu-id="163e9-140">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="163e9-141">In questa esercitazione si userà [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="163e9-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="163e9-142">b.</span><span class="sxs-lookup"><span data-stu-id="163e9-142">b.</span></span> <span data-ttu-id="163e9-143">Recuperare dal repository i valori per **GroupId**, **ArtifactId** e **Version**.</span><span class="sxs-lookup"><span data-stu-id="163e9-143">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="163e9-144">Assicurarsi che i valori che si raccolgono corrispondano al cluster.</span><span class="sxs-lookup"><span data-stu-id="163e9-144">Make sure that the values you gather match your cluster.</span></span> <span data-ttu-id="163e9-145">Si usano, in questo caso, un pacchetto Scala 2.10 e un pacchetto Spark 1.4.0, ma potrebbe essere necessario selezionare versioni diverse per la versione di Scala o di Spark appropriata al cluster.</span><span class="sxs-lookup"><span data-stu-id="163e9-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need to select different versions for the appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="163e9-146">È possibile trovare la versione di Scala nel cluster eseguendo `scala.util.Properties.versionString` nel kernel Jupyter Spark o nell'invio di Spark.</span><span class="sxs-lookup"><span data-stu-id="163e9-146">You can find out the Scala version on your cluster by running `scala.util.Properties.versionString` on the Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="163e9-147">È possibile trovare la versione di Spark nel cluster eseguendo `sc.version` nei notebook Jupyter.</span><span class="sxs-lookup"><span data-stu-id="163e9-147">You can find out the Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="163e9-148">![Usare pacchetti esterni con notebook di Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Usare pacchetti esterni con notebook di Jupyter")</span><span class="sxs-lookup"><span data-stu-id="163e9-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="163e9-149">c.</span><span class="sxs-lookup"><span data-stu-id="163e9-149">c.</span></span> <span data-ttu-id="163e9-150">Concatenare i tre valori, separati da due punti (**:**).</span><span class="sxs-lookup"><span data-stu-id="163e9-150">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="163e9-151">Eseguire la cella di codice con `%%configure` magic.</span><span class="sxs-lookup"><span data-stu-id="163e9-151">Run the code cell with the `%%configure` magic.</span></span> <span data-ttu-id="163e9-152">Questa operazione configura la sessione Livy sottostante per l'uso del pacchetto fornito.</span><span class="sxs-lookup"><span data-stu-id="163e9-152">This will configure the underlying Livy session to use the package you provided.</span></span> <span data-ttu-id="163e9-153">Nelle celle successive del notebook è ora possibile usare il pacchetto, come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="163e9-153">In the subsequent cells in the notebook, you can now use the package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="163e9-154">È quindi possibile eseguire i frammenti di codice, come mostrato di seguito, per visualizzare i dati del frame di dati creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="163e9-154">You can then run the snippets, like shown below, to view the data from the dataframe you created in the previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="163e9-155"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="163e9-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="163e9-156">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="163e9-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="163e9-157">Scenari</span><span class="sxs-lookup"><span data-stu-id="163e9-157">Scenarios</span></span>
* [<span data-ttu-id="163e9-158">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="163e9-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="163e9-159">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="163e9-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="163e9-160">Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="163e9-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="163e9-161">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="163e9-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="163e9-162">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="163e9-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="163e9-163">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="163e9-163">Create and run applications</span></span>
* [<span data-ttu-id="163e9-164">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="163e9-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="163e9-165">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="163e9-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="163e9-166">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="163e9-166">Tools and extensions</span></span>

* [<span data-ttu-id="163e9-167">Usare pacchetti Python esterni con Jupyter Notebook nei cluster Apache Spark in HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="163e9-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="163e9-168">Usare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark in Scala</span><span class="sxs-lookup"><span data-stu-id="163e9-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="163e9-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Usare il plug-in Strumenti HDInsight per IntelliJ IDEA per eseguire il debug di applicazioni Spark in remoto)</span><span class="sxs-lookup"><span data-stu-id="163e9-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="163e9-170">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="163e9-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="163e9-171">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="163e9-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="163e9-172">Installare Jupyter nel computer e connetterlo a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="163e9-172">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="163e9-173">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="163e9-173">Manage resources</span></span>
* [<span data-ttu-id="163e9-174">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="163e9-174">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="163e9-175">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="163e9-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

