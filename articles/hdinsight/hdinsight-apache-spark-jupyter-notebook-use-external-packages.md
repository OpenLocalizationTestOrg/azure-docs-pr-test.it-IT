---
title: pacchetti Maven personalizzati aaaUse con Jupyter di Spark su HDInsight di Azure | Documenti Microsoft
description: Istruzioni dettagliate su come i cluster di pacchetti di Maven personalizzati toouse tooconfigure Jupyter notebook disponibili con HDInsight Spark.
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
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="c6379-103">Usare pacchetti esterni con notebook di Jupyter nei cluster Apache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c6379-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6379-104">Uso di comandi Magic nelle celle</span><span class="sxs-lookup"><span data-stu-id="c6379-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="c6379-105">Uso di azioni script</span><span class="sxs-lookup"><span data-stu-id="c6379-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="c6379-106">Informazioni su come tooconfigure un server Jupyter notebook nel cluster Apache Spark in HDInsight toouse esterno,-il contributo della community **maven** di casella pacchetti che non sono presenti cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c6379-106">Learn how tooconfigure a Jupyter notebook in Apache Spark cluster on HDInsight toouse external, community-contributed **maven** packages that are not included out-of-the-box in hello cluster.</span></span> 

<span data-ttu-id="c6379-107">È possibile cercare hello [repository Maven](http://search.maven.org/) per l'elenco completo di hello dei pacchetti disponibili.</span><span class="sxs-lookup"><span data-stu-id="c6379-107">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="c6379-108">È anche possibile ottenere un elenco dei pacchetti disponibili da altre origini.</span><span class="sxs-lookup"><span data-stu-id="c6379-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="c6379-109">Ad esempio, un elenco completo dei pacchetti creati dalla community è disponibile nel sito Web [spark-packages.org](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="c6379-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="c6379-110">In questo articolo si apprenderà come hello toouse [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pacchetto con notebook Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="c6379-110">In this article, you will learn how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="c6379-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c6379-111">Prerequisites</span></span>
<span data-ttu-id="c6379-112">È necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="c6379-112">You must have hello following:</span></span>

* <span data-ttu-id="c6379-113">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c6379-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="c6379-114">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="c6379-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="c6379-115">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="c6379-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="c6379-116">Da hello [portale Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello).</span><span class="sxs-lookup"><span data-stu-id="c6379-116">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="c6379-117">È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c6379-117">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="c6379-118">Dal Pannello di cluster Spark hello, fare clic su **collegamenti rapidi**e quindi da hello **Dashboard Cluster** pannello, fare clic su **server Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="c6379-118">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="c6379-119">Se richiesto, immettere le credenziali di amministratore hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c6379-119">If prompted, enter hello admin credentials for hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c6379-120">È anche possibile raggiungere hello server Jupyter Notebook per il cluster usando hello apertura URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="c6379-120">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="c6379-121">Sostituire **CLUSTERNAME** con nome hello del cluster:</span><span class="sxs-lookup"><span data-stu-id="c6379-121">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="c6379-122">Creare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="c6379-122">Create a new notebook.</span></span> <span data-ttu-id="c6379-123">Fare clic su **New** (Nuovo) e quindi su **Spark**.</span><span class="sxs-lookup"><span data-stu-id="c6379-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="c6379-124">![Creare un nuovo notebook Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Creare un nuovo notebook Jupyter")</span><span class="sxs-lookup"><span data-stu-id="c6379-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="c6379-125">Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="c6379-125">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="c6379-126">Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="c6379-126">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="c6379-127">![Specificare un nome per notebook hello](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "specificare un nome per notebook hello")</span><span class="sxs-lookup"><span data-stu-id="c6379-127">![Provide a name for hello notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="c6379-128">Si utilizzerà hello `%%configure` tooconfigure magic hello notebook toouse un pacchetto esterno.</span><span class="sxs-lookup"><span data-stu-id="c6379-128">You will use hello `%%configure` magic tooconfigure hello notebook toouse an external package.</span></span> <span data-ttu-id="c6379-129">Nei blocchi appunti che utilizzano i pacchetti esterni, verificare di chiamare hello `%%configure` magic nella prima cella di codice hello.</span><span class="sxs-lookup"><span data-stu-id="c6379-129">In notebooks that use external packages, make sure you call hello `%%configure` magic in hello first code cell.</span></span> <span data-ttu-id="c6379-130">Ciò garantisce che kernel hello è pacchetto hello toouse configurato prima dell'avvio della sessione hello.</span><span class="sxs-lookup"><span data-stu-id="c6379-130">This ensures that hello kernel is configured toouse hello package before hello session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="c6379-131">Se si dimentica kernel hello tooconfigure nella prima cella hello, è possibile utilizzare hello `%%configure` con hello `-f` parametro, ma che verrà riavviato sessione hello e lo stato di avanzamento tutti andranno persa.</span><span class="sxs-lookup"><span data-stu-id="c6379-131">If you forget tooconfigure hello kernel in hello first cell, you can use hello `%%configure` with hello `-f` parameter, but that will restart hello session and all progress will be lost.</span></span>

    | <span data-ttu-id="c6379-132">Versione HDInsight</span><span class="sxs-lookup"><span data-stu-id="c6379-132">HDInsight version</span></span> | <span data-ttu-id="c6379-133">Comando</span><span class="sxs-lookup"><span data-stu-id="c6379-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="c6379-134">Per HDInsight 3.3 e HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="c6379-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="c6379-135">Per HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="c6379-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="c6379-136">frammento di codice Hello precedente prevede che le coordinate di maven hello per pacchetto esterno di hello in Repository centrale Maven.</span><span class="sxs-lookup"><span data-stu-id="c6379-136">hello snippet above expects hello maven coordinates for hello external package in Maven Central Repository.</span></span> <span data-ttu-id="c6379-137">In questo frammento, `com.databricks:spark-csv_2.10:1.4.0` è coordinate di maven hello per **spark csv** pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c6379-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is hello maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="c6379-138">Di seguito viene illustrato come è costruire hello coordinate per un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c6379-138">Here's how you construct hello coordinates for a package.</span></span>
   
    <span data-ttu-id="c6379-139">a.</span><span class="sxs-lookup"><span data-stu-id="c6379-139">a.</span></span> <span data-ttu-id="c6379-140">Individuare il pacchetto di hello in hello Maven Repository.</span><span class="sxs-lookup"><span data-stu-id="c6379-140">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="c6379-141">In questa esercitazione si userà [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="c6379-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="c6379-142">b.</span><span class="sxs-lookup"><span data-stu-id="c6379-142">b.</span></span> <span data-ttu-id="c6379-143">Dal repository hello, raccogliere i valori hello per **GroupId**, **ID**, e **versione**.</span><span class="sxs-lookup"><span data-stu-id="c6379-143">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="c6379-144">Assicurarsi che i valori hello che è raccogliere corrispondano il cluster.</span><span class="sxs-lookup"><span data-stu-id="c6379-144">Make sure that hello values you gather match your cluster.</span></span> <span data-ttu-id="c6379-145">In questo caso, si sta usando una Scala 2.10 e un pacchetto di Spark 1.4.0, ma potrebbe essere necessario versioni diverse di tooselect hello Scala o Spark versione presente nel cluster.</span><span class="sxs-lookup"><span data-stu-id="c6379-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need tooselect different versions for hello appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="c6379-146">È possibile trovare la versione di hello Scala il cluster eseguendo `scala.util.Properties.versionString` kernel Jupyter Spark hello o Invia Spark.</span><span class="sxs-lookup"><span data-stu-id="c6379-146">You can find out hello Scala version on your cluster by running `scala.util.Properties.versionString` on hello Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="c6379-147">È possibile trovare la versione di hello Spark il cluster eseguendo `sc.version` sui server Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="c6379-147">You can find out hello Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="c6379-148">![Usare pacchetti esterni con notebook di Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Usare pacchetti esterni con notebook di Jupyter")</span><span class="sxs-lookup"><span data-stu-id="c6379-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="c6379-149">c.</span><span class="sxs-lookup"><span data-stu-id="c6379-149">c.</span></span> <span data-ttu-id="c6379-150">Concatenare valori hello tre, separati da due punti (**:**).</span><span class="sxs-lookup"><span data-stu-id="c6379-150">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="c6379-151">Eseguire cella codice hello con hello `%%configure` magic.</span><span class="sxs-lookup"><span data-stu-id="c6379-151">Run hello code cell with hello `%%configure` magic.</span></span> <span data-ttu-id="c6379-152">Consente di configurare hello sottostante inserire il sessione toouse hello pacchetto fornito.</span><span class="sxs-lookup"><span data-stu-id="c6379-152">This will configure hello underlying Livy session toouse hello package you provided.</span></span> <span data-ttu-id="c6379-153">Nelle celle successive di hello in blocco per Appunti hello, ora è possibile utilizzare il pacchetto di hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c6379-153">In hello subsequent cells in hello notebook, you can now use hello package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="c6379-154">È quindi possibile eseguire i frammenti di codice hello, come indicato di seguito, tooview hello dati hello frame di dati è stato creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="c6379-154">You can then run hello snippets, like shown below, tooview hello data from hello dataframe you created in hello previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="c6379-155"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c6379-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="c6379-156">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c6379-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="c6379-157">Scenari</span><span class="sxs-lookup"><span data-stu-id="c6379-157">Scenarios</span></span>
* [<span data-ttu-id="c6379-158">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c6379-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c6379-159">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="c6379-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c6379-160">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="c6379-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c6379-161">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="c6379-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="c6379-162">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c6379-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="c6379-163">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="c6379-163">Create and run applications</span></span>
* [<span data-ttu-id="c6379-164">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="c6379-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c6379-165">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="c6379-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c6379-166">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="c6379-166">Tools and extensions</span></span>

* [<span data-ttu-id="c6379-167">Usare pacchetti Python esterni con Jupyter Notebook nei cluster Apache Spark in HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="c6379-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="c6379-168">Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="c6379-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c6379-169">Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota</span><span class="sxs-lookup"><span data-stu-id="c6379-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c6379-170">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c6379-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="c6379-171">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="c6379-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c6379-172">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="c6379-172">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="c6379-173">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="c6379-173">Manage resources</span></span>
* [<span data-ttu-id="c6379-174">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="c6379-174">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="c6379-175">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c6379-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

