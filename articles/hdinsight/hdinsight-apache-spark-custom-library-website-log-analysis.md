---
title: 'Analizzare i log del sito Web con le librerie Python in Spark: Azure | Microsoft Docs'
description: Questo notebook dimostra come analizzare i dati dei log mediante una libreria personalizzata con Spark in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2a028beb1e9eae89d32238e61b6f67c4c059a94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="5addf-103">Analizzare i log del sito Web usando una libreria Python personalizzata con cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5addf-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="5addf-104">Questo notebook dimostra come analizzare i dati dei log mediante una libreria personalizzata con Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5addf-104">This notebook demonstrates how to analyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="5addf-105">La libreria personalizzata usata è una libreria di Python chiamata **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="5addf-105">The custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="5addf-106">Questa esercitazione è disponibile anche come notebook di Jupyter in un cluster Spark (Linux) creato in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5addf-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="5addf-107">L'esperienza offerta dal notebook consente di eseguire i frammenti di codice Python dal notebook stesso.</span><span class="sxs-lookup"><span data-stu-id="5addf-107">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="5addf-108">Per eseguire l'esercitazione da un notebook, creare un cluster Spark, avviare un notebook di Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`) e quindi eseguire il notebook **Analyze logs with Spark using a custom library.ipynb** nella cartella **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="5addf-108">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Analyze logs with Spark using a custom library.ipynb** under the **PySpark** folder.</span></span>
>
>

<span data-ttu-id="5addf-109">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="5addf-109">**Prerequisites:**</span></span>

<span data-ttu-id="5addf-110">È necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="5addf-110">You must have the following:</span></span>

* <span data-ttu-id="5addf-111">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5addf-111">An Azure subscription.</span></span> <span data-ttu-id="5addf-112">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5addf-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="5addf-113">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5addf-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="5addf-114">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="5addf-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="5addf-115">Salvare i dati non elaborati come RDD</span><span class="sxs-lookup"><span data-stu-id="5addf-115">Save raw data as an RDD</span></span>
<span data-ttu-id="5addf-116">In questa sezione viene usato il notebook di [Jupyter](https://jupyter.org) associato a un cluster Apache Spark in HDInsight per eseguire i processi che elaborano i dati di esempio non elaborati e li salvano come tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="5addf-116">In this section, we use the [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight to run jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="5addf-117">I dati di esempio sono un file con estensione csv (hvac.csv) disponibile in tutti i cluster per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5addf-117">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="5addf-118">Dopo avere salvato i dati come tabella Hive, nella sezione successiva verrà effettuata la connessione alla tabella Hive mediante strumenti di Business Intelligence come Power BI e Tableau.</span><span class="sxs-lookup"><span data-stu-id="5addf-118">Once your data is saved as a Hive table, in the next section we will connect to the Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="5addf-119">Dalla Schermata iniziale del [portale di Azure](https://portal.azure.com/) fare clic sul riquadro del cluster Spark, se è stato aggiunto sulla Schermata iniziale.</span><span class="sxs-lookup"><span data-stu-id="5addf-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="5addf-120">È anche possibile passare al cluster da **Esplora tutto** > **Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5addf-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="5addf-121">Nel pannello del cluster Spark fare clic su **Dashboard cluster** e quindi su **Notebook di Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="5addf-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="5addf-122">Se richiesto, immettere le credenziali per il cluster.</span><span class="sxs-lookup"><span data-stu-id="5addf-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5addf-123">È anche possibile raggiungere il notebook di Jupyter per il cluster aprendo l'URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="5addf-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="5addf-124">Sostituire **CLUSTERNAME** con il nome del cluster:</span><span class="sxs-lookup"><span data-stu-id="5addf-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="5addf-125">Creare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="5addf-125">Create a new notebook.</span></span> <span data-ttu-id="5addf-126">Fare clic su **Nuovo** e quindi su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="5addf-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="5addf-127">![Creare un nuovo notebook Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Creare un nuovo notebook Jupyter")</span><span class="sxs-lookup"><span data-stu-id="5addf-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="5addf-128">Un nuovo notebook verrà creato e aperto con il nome Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="5addf-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="5addf-129">Fare clic sul nome del notebook nella parte superiore e immettere un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="5addf-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="5addf-130">![Specificare un nome per il notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Specificare un nome per il notebook")</span><span class="sxs-lookup"><span data-stu-id="5addf-130">![Provide a name for the notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for the notebook")</span></span>
5. <span data-ttu-id="5addf-131">Poiché il notebook è stato creato tramite il kernel PySpark, non è necessario creare contesti in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="5addf-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="5addf-132">I contesti Spark e Hive vengono creati automaticamente quando si esegue la prima cella di codice.</span><span class="sxs-lookup"><span data-stu-id="5addf-132">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="5addf-133">È possibile iniziare con l'importazione dei tipi necessari per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="5addf-133">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="5addf-134">Incollare il frammento di codice seguente in una cella vuota e quindi premere **MAIUSC+INVIO**.</span><span class="sxs-lookup"><span data-stu-id="5addf-134">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="5addf-135">Creare un RDD con i dati di log di esempio già disponibili nel cluster.</span><span class="sxs-lookup"><span data-stu-id="5addf-135">Create an RDD using the sample log data already available on the cluster.</span></span> <span data-ttu-id="5addf-136">È possibile accedere ai dati nell'account di archiviazione predefinito associato al cluster in **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="5addf-136">You can access the data in the default storage account associated with the cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="5addf-137">Recuperare un set di log di esempio per verificare che il passaggio precedente sia stato completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="5addf-137">Retrieve a sample log set to verify that the previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="5addf-138">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5addf-138">You should see an output similar to the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="5addf-139">Analizzare i dati di log usando una libreria personalizzata di Python</span><span class="sxs-lookup"><span data-stu-id="5addf-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="5addf-140">Nell'output precedente, le prime due righe includono le informazioni di intestazione e ogni riga rimanente corrisponde allo schema descritto nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="5addf-140">In the output above, the first couple lines include the header information and each remaining line matches the schema described in that header.</span></span> <span data-ttu-id="5addf-141">L'analisi di tali log potrebbe essere complessa.</span><span class="sxs-lookup"><span data-stu-id="5addf-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="5addf-142">Quindi, viene usata una libreria personalizzata di Python (**iislogparser.py**) che semplifica notevolmente l'analisi di tali log.</span><span class="sxs-lookup"><span data-stu-id="5addf-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="5addf-143">Per impostazione predefinita, questa libreria è inclusa con il cluster Spark in HDInsight in **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="5addf-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="5addf-144">Tuttavia, questa libreria non è in `PYTHONPATH` e quindi non può essere usata tramite un'istruzione di importazione come `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="5addf-144">However, this library is not in the `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="5addf-145">Per usare questa libreria è necessario distribuirla a tutti i nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5addf-145">To use this library, we must distribute it to all the worker nodes.</span></span> <span data-ttu-id="5addf-146">Eseguire il frammento di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="5addf-146">Run the following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="5addf-147">`iislogparser` offre una funzione `parse_log_line` che restituisce `None` se una riga del log è una riga di intestazione e restituisce un'istanza della classe `LogLine` se viene rilevata una riga del log.</span><span class="sxs-lookup"><span data-stu-id="5addf-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of the `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="5addf-148">Usare la classe `LogLine` per estrarre solo le righe del log dall'RDD:</span><span class="sxs-lookup"><span data-stu-id="5addf-148">Use the `LogLine` class to extract only the log lines from the RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="5addf-149">Recuperare un paio di righe estratte del log per verificare che il passaggio sia stato completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="5addf-149">Retrieve a couple of extracted log lines to verify that the step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="5addf-150">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5addf-150">The output should be similar to the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="5addf-151">La classe `LogLine`, a sua volta, offre alcuni metodi utili, ad esempio `is_error()`, che determina se una voce di log contiene un codice di errore.</span><span class="sxs-lookup"><span data-stu-id="5addf-151">The `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="5addf-152">Usarla per calcolare il numero di errori nelle righe di log estratte e quindi registrare tutti gli errori in un file diverso.</span><span class="sxs-lookup"><span data-stu-id="5addf-152">Use this to compute the number of errors in the extracted log lines, and then log all the errors to a different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="5addf-153">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5addf-153">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="5addf-154">È anche possibile usare **Matplotlib** per costruire una visualizzazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="5addf-154">You can also use **Matplotlib** to construct a visualization of the data.</span></span> <span data-ttu-id="5addf-155">Ad esempio, se si vuole isolare la causa delle richieste in esecuzione da molto tempo si potrebbero trovare i file che mediamente richiedono più tempo per servire una richiesta.</span><span class="sxs-lookup"><span data-stu-id="5addf-155">For example, if you want to isolate the cause of requests that run for a long time, you might want to find the files that take the most time to serve on average.</span></span>
   <span data-ttu-id="5addf-156">Il frammento di codice seguente recupera le 25 risorse principali che hanno impiegato più tempo per servire una richiesta.</span><span class="sxs-lookup"><span data-stu-id="5addf-156">The snippet below retrieves the top 25 resources that took most time to serve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="5addf-157">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5addf-157">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. <span data-ttu-id="5addf-158">È anche possibile presentare queste informazioni sotto forma di tracciato.</span><span class="sxs-lookup"><span data-stu-id="5addf-158">You can also present this information in the form of plot.</span></span> <span data-ttu-id="5addf-159">Come primo passaggio per creare un tracciato, creeremo prima di tutto una tabella temporanea, **AverageTime**.</span><span class="sxs-lookup"><span data-stu-id="5addf-159">As a first step to create a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="5addf-160">La tabella raggruppa i registri in base all'ora per vedere se si sono verificati eventuali picchi di latenza insoliti in un determinato momento.</span><span class="sxs-lookup"><span data-stu-id="5addf-160">The table groups the logs by time to see if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="5addf-161">Quindi, per ottenere tutti i record della tabella **AverageTime** , è possibile eseguire la query SQL seguente.</span><span class="sxs-lookup"><span data-stu-id="5addf-161">You can then run the following SQL query to get all the records in the **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="5addf-162">Il comando speciale `%%sql` seguito da `-o averagetime` assicura che l'output della query venga mantenuto in locale nel server Jupyter, di solito il nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="5addf-162">The `%%sql` magic followed by `-o averagetime` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="5addf-163">L'output viene mantenuto come frame di dati [Pandas](http://pandas.pydata.org/) con il nome specificato **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="5addf-163">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **averagetime**.</span></span>

   <span data-ttu-id="5addf-164">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5addf-164">You should see an output like the following:</span></span>

   <span data-ttu-id="5addf-165">![Output della query SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Output della query SQL")</span><span class="sxs-lookup"><span data-stu-id="5addf-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="5addf-166">Per altre informazioni sul comando Magic `%%sql`, vedere [Parametri supportati con il comando Magic %%sql](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="5addf-166">For more information about the `%%sql` magic, see [Parameters supported with the %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="5addf-167">È ora possibile creare un tracciato tramite Matplotlib, una libreria che consente di creare visualizzazioni di dati.</span><span class="sxs-lookup"><span data-stu-id="5addf-167">You can now use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="5addf-168">Dato che il tracciato deve essere creato dal frame di dati **averagetime** con salvataggio permanente in locale, il frammento di codice deve iniziare con il magic `%%local`.</span><span class="sxs-lookup"><span data-stu-id="5addf-168">Because the plot must be created from the locally persisted **averagetime** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="5addf-169">Ciò garantisce che il codice venga eseguito localmente nel server di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="5addf-169">This ensures that the code is run locally on the Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="5addf-170">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5addf-170">You should see an output like the following:</span></span>

   <span data-ttu-id="5addf-171">![Output Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Output Matplotlib")</span><span class="sxs-lookup"><span data-stu-id="5addf-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="5addf-172">Al termine dell'esecuzione dell'applicazione, è necessario arrestare il notebook per rilasciare le risorse.</span><span class="sxs-lookup"><span data-stu-id="5addf-172">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="5addf-173">A tale scopo, dal menu **File** del notebook fare clic su **Close and Halt** (Chiudi e interrompi).</span><span class="sxs-lookup"><span data-stu-id="5addf-173">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="5addf-174">Questa operazione consente di arrestare e chiudere il notebook.</span><span class="sxs-lookup"><span data-stu-id="5addf-174">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="5addf-175"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5addf-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="5addf-176">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5addf-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="5addf-177">Scenari</span><span class="sxs-lookup"><span data-stu-id="5addf-177">Scenarios</span></span>
* [<span data-ttu-id="5addf-178">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5addf-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="5addf-179">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="5addf-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="5addf-180">Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="5addf-180">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="5addf-181">Streaming Spark: usare Spark in HDInsight per creare applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="5addf-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="5addf-182">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="5addf-182">Create and run applications</span></span>
* [<span data-ttu-id="5addf-183">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="5addf-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="5addf-184">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="5addf-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="5addf-185">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="5addf-185">Tools and extensions</span></span>
* [<span data-ttu-id="5addf-186">Usare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="5addf-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="5addf-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Usare il plug-in Strumenti HDInsight per IntelliJ IDEA per eseguire il debug di applicazioni Spark in remoto)</span><span class="sxs-lookup"><span data-stu-id="5addf-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="5addf-188">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5addf-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="5addf-189">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="5addf-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="5addf-190">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="5addf-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="5addf-191">Installare Jupyter Notebook nel computer e connetterlo a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="5addf-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="5addf-192">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="5addf-192">Manage resources</span></span>
* [<span data-ttu-id="5addf-193">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5addf-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="5addf-194">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5addf-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
