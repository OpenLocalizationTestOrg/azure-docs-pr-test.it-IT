---
title: i log del sito Web aaaAnalyze con le librerie di Python di Spark - Azure | Documenti Microsoft
description: Il blocco viene illustrato come tooanalyze dati di log mediante una libreria personalizzata con Spark in HDInsight.
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
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="8269b-103">Analizzare i log del sito Web usando una libreria Python personalizzata con cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8269b-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="8269b-104">Il blocco viene illustrato come tooanalyze dati di log mediante una libreria personalizzata con Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8269b-104">This notebook demonstrates how tooanalyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="8269b-105">utilizziamo la libreria personalizzata Hello è una libreria di Python chiamata **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="8269b-105">hello custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="8269b-106">Questa esercitazione è disponibile anche come notebook di Jupyter in un cluster Spark (Linux) creato in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8269b-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="8269b-107">esperienza notebook Hello consente di eseguire frammenti di codice Python hello dal blocco appunti hello stesso.</span><span class="sxs-lookup"><span data-stu-id="8269b-107">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="8269b-108">esercitazione di hello tooperform all'interno di un blocco note, creare un cluster Spark, avviare un server Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), quindi eseguire notebook hello **analizzare i registri con Spark usando un library.ipynb personalizzato** in hello  **PySpark** cartella.</span><span class="sxs-lookup"><span data-stu-id="8269b-108">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Analyze logs with Spark using a custom library.ipynb** under hello **PySpark** folder.</span></span>
>
>

<span data-ttu-id="8269b-109">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="8269b-109">**Prerequisites:**</span></span>

<span data-ttu-id="8269b-110">È necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="8269b-110">You must have hello following:</span></span>

* <span data-ttu-id="8269b-111">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8269b-111">An Azure subscription.</span></span> <span data-ttu-id="8269b-112">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="8269b-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="8269b-113">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8269b-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="8269b-114">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="8269b-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="8269b-115">Salvare i dati non elaborati come RDD</span><span class="sxs-lookup"><span data-stu-id="8269b-115">Save raw data as an RDD</span></span>
<span data-ttu-id="8269b-116">In questa sezione, utilizziamo hello [Jupyter](https://jupyter.org) notebook associata a un cluster di Apache Spark in HDInsight toorun processi che elaborano i dati di esempio non elaborati e salvarla come una tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="8269b-116">In this section, we use hello [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight toorun jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="8269b-117">dati di esempio Hello sono un file CSV (hvac.csv) disponibile in tutti i cluster per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8269b-117">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="8269b-118">Dopo aver salvati i dati come una tabella Hive, nella sezione successiva hello si connetterà tabella Hive toohello utilizzando strumenti di Business Intelligence quali Power BI e Tableau.</span><span class="sxs-lookup"><span data-stu-id="8269b-118">Once your data is saved as a Hive table, in hello next section we will connect toohello Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="8269b-119">Da hello [portale di Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello).</span><span class="sxs-lookup"><span data-stu-id="8269b-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="8269b-120">È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8269b-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="8269b-121">Dal Pannello di cluster Spark hello, fare clic su **Dashboard Cluster**, quindi fare clic su **server Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="8269b-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="8269b-122">Se richiesto, immettere le credenziali di amministratore hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8269b-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8269b-123">È anche possibile raggiungere hello server Jupyter Notebook per il cluster usando hello apertura URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="8269b-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="8269b-124">Sostituire **CLUSTERNAME** con nome hello del cluster:</span><span class="sxs-lookup"><span data-stu-id="8269b-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="8269b-125">Creare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="8269b-125">Create a new notebook.</span></span> <span data-ttu-id="8269b-126">Fare clic su **Nuovo** e quindi su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="8269b-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="8269b-127">![Creare un nuovo notebook Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Creare un nuovo notebook Jupyter")</span><span class="sxs-lookup"><span data-stu-id="8269b-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="8269b-128">Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="8269b-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="8269b-129">Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="8269b-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="8269b-130">![Specificare un nome per notebook hello](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "specificare un nome per notebook hello")</span><span class="sxs-lookup"><span data-stu-id="8269b-130">![Provide a name for hello notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for hello notebook")</span></span>
5. <span data-ttu-id="8269b-131">Poiché è stato creato un notebook utilizza il kernel PySpark hello, non è necessario toocreate i contesti in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="8269b-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="8269b-132">Quando si esegue prima cella di codice hello contesti di Spark e Hive Hello verranno creati automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="8269b-132">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="8269b-133">È possibile avviare l'importazione di tipi di hello che sono necessari per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="8269b-133">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="8269b-134">Incollare hello seguente frammento di codice in una cella vuota e quindi premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="8269b-134">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="8269b-135">Creare un RDD usando i dati di log esempio hello già disponibili nel cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="8269b-135">Create an RDD using hello sample log data already available on hello cluster.</span></span> <span data-ttu-id="8269b-136">È possibile accedere a dati hello nell'account di archiviazione predefinito hello associato al cluster hello **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="8269b-136">You can access hello data in hello default storage account associated with hello cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="8269b-137">Recuperare un tooverify del set di log di esempio che hello passaggio precedente è stata completata.</span><span class="sxs-lookup"><span data-stu-id="8269b-137">Retrieve a sample log set tooverify that hello previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="8269b-138">Verrà visualizzato un segue toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="8269b-138">You should see an output similar toohello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="8269b-139">Analizzare i dati di log usando una libreria personalizzata di Python</span><span class="sxs-lookup"><span data-stu-id="8269b-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="8269b-140">Nell'output di hello sopra, hello contenute nelle prime due righe includono informazioni di intestazione di hello e ogni riga rimanente corrispondono allo schema di hello descritto in questa intestazione.</span><span class="sxs-lookup"><span data-stu-id="8269b-140">In hello output above, hello first couple lines include hello header information and each remaining line matches hello schema described in that header.</span></span> <span data-ttu-id="8269b-141">L'analisi di tali log potrebbe essere complessa.</span><span class="sxs-lookup"><span data-stu-id="8269b-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="8269b-142">Quindi, viene usata una libreria personalizzata di Python (**iislogparser.py**) che semplifica notevolmente l'analisi di tali log.</span><span class="sxs-lookup"><span data-stu-id="8269b-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="8269b-143">Per impostazione predefinita, questa libreria è inclusa con il cluster Spark in HDInsight in **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="8269b-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="8269b-144">Tuttavia, questa raccolta non è in hello `PYTHONPATH` in modo non è possibile usare con un'istruzione di importazione come `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="8269b-144">However, this library is not in hello `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="8269b-145">toouse questa libreria, è necessario distribuire i nodi di lavoro tooall hello.</span><span class="sxs-lookup"><span data-stu-id="8269b-145">toouse this library, we must distribute it tooall hello worker nodes.</span></span> <span data-ttu-id="8269b-146">Eseguire hello seguente frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="8269b-146">Run hello following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="8269b-147">`iislogparser`fornisce una funzione `parse_log_line` che restituisce `None` se una riga del log è una riga di intestazione e restituisce un'istanza di hello `LogLine` classe se rileva una riga del log.</span><span class="sxs-lookup"><span data-stu-id="8269b-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of hello `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="8269b-148">Hello utilizzare `LogLine` tooextract classe hello solo le righe di log da hello RDD:</span><span class="sxs-lookup"><span data-stu-id="8269b-148">Use hello `LogLine` class tooextract only hello log lines from hello RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="8269b-149">Recuperare un paio di righe log estratti tooverify che hello passaggio è stata completata.</span><span class="sxs-lookup"><span data-stu-id="8269b-149">Retrieve a couple of extracted log lines tooverify that hello step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="8269b-150">output di Hello deve essere simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8269b-150">hello output should be similar toohello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="8269b-151">Hello `LogLine` (classe), a sua volta, dispone di alcuni metodi utili, ad esempio `is_error()`, che restituisce se una voce di log ha un codice di errore.</span><span class="sxs-lookup"><span data-stu-id="8269b-151">hello `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="8269b-152">Utilizzare questo numero di hello toocompute di errori nelle righe log hello estratto e accedere nuovamente tutti hello errori tooa file diverso.</span><span class="sxs-lookup"><span data-stu-id="8269b-152">Use this toocompute hello number of errors in hello extracted log lines, and then log all hello errors tooa different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="8269b-153">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="8269b-153">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="8269b-154">È inoltre possibile utilizzare **Matplotlib** tooconstruct una visualizzazione di dati hello.</span><span class="sxs-lookup"><span data-stu-id="8269b-154">You can also use **Matplotlib** tooconstruct a visualization of hello data.</span></span> <span data-ttu-id="8269b-155">Ad esempio, se si desidera causa hello tooisolate di richieste eseguite per un lungo periodo, è possibile file hello toofind che accettano hello la maggior parte delle tooserve tempo medio.</span><span class="sxs-lookup"><span data-stu-id="8269b-155">For example, if you want tooisolate hello cause of requests that run for a long time, you might want toofind hello files that take hello most time tooserve on average.</span></span>
   <span data-ttu-id="8269b-156">frammento Hello seguente recupera hello primi 25 risorse impiegato la maggior parte delle tooserve ora una richiesta.</span><span class="sxs-lookup"><span data-stu-id="8269b-156">hello snippet below retrieves hello top 25 resources that took most time tooserve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="8269b-157">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="8269b-157">You should see an output like hello following:</span></span>

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
5. <span data-ttu-id="8269b-158">È anche possibile presentare tali informazioni sotto forma di hello di tracciato.</span><span class="sxs-lookup"><span data-stu-id="8269b-158">You can also present this information in hello form of plot.</span></span> <span data-ttu-id="8269b-159">Come un toocreate passaggio prima un tracciato, possiamo creare innanzitutto una tabella temporanea **AverageTime**.</span><span class="sxs-lookup"><span data-stu-id="8269b-159">As a first step toocreate a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="8269b-160">hello gruppi di tabella Hello registra, per ora toosee se fossero eventuali picchi di latenza insolito in qualsiasi momento particolare.</span><span class="sxs-lookup"><span data-stu-id="8269b-160">hello table groups hello logs by time toosee if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="8269b-161">È quindi possibile eseguire hello tooget query SQL seguente tutti i record di hello in hello **AverageTime** tabella.</span><span class="sxs-lookup"><span data-stu-id="8269b-161">You can then run hello following SQL query tooget all hello records in hello **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="8269b-162">Hello `%%sql` magic seguita da `-o averagetime` assicura che output di hello di hello query è persistente in locale nel server Jupyter hello (in genere. da nodo a hello a head del cluster hello).</span><span class="sxs-lookup"><span data-stu-id="8269b-162">hello `%%sql` magic followed by `-o averagetime` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="8269b-163">output di Hello viene mantenuta come un [Pandas](http://pandas.pydata.org/) frame di dati con hello specificato nome **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="8269b-163">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **averagetime**.</span></span>

   <span data-ttu-id="8269b-164">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="8269b-164">You should see an output like hello following:</span></span>

   <span data-ttu-id="8269b-165">![Output della query SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Output della query SQL")</span><span class="sxs-lookup"><span data-stu-id="8269b-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="8269b-166">Per ulteriori informazioni su hello `%%sql` magic, vedere [i parametri supportati con hello % % magic sql](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="8269b-166">For more information about hello `%%sql` magic, see [Parameters supported with hello %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="8269b-167">È ora possibile utilizzare Matplotlib, una libreria utilizzata tooconstruct della visualizzazione dei dati, toocreate un tracciato.</span><span class="sxs-lookup"><span data-stu-id="8269b-167">You can now use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="8269b-168">Perché è necessario creare tracciato hello da hello localmente persistente **averagetime** frame di dati, il frammento di codice hello deve iniziare con hello `%%local` magic.</span><span class="sxs-lookup"><span data-stu-id="8269b-168">Because hello plot must be created from hello locally persisted **averagetime** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="8269b-169">In questo modo si garantisce che il codice hello viene eseguito localmente su server Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="8269b-169">This ensures that hello code is run locally on hello Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="8269b-170">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="8269b-170">You should see an output like hello following:</span></span>

   <span data-ttu-id="8269b-171">![Output Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Output Matplotlib")</span><span class="sxs-lookup"><span data-stu-id="8269b-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="8269b-172">Al termine dell'esecuzione di un'applicazione hello, si consiglia di risorse di arresto hello notebook toorelease hello.</span><span class="sxs-lookup"><span data-stu-id="8269b-172">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="8269b-173">toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**.</span><span class="sxs-lookup"><span data-stu-id="8269b-173">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="8269b-174">Questo verrà arrestato e notebook hello Chiudi.</span><span class="sxs-lookup"><span data-stu-id="8269b-174">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="8269b-175"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8269b-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="8269b-176">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8269b-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="8269b-177">Scenari</span><span class="sxs-lookup"><span data-stu-id="8269b-177">Scenarios</span></span>
* [<span data-ttu-id="8269b-178">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8269b-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="8269b-179">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="8269b-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="8269b-180">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="8269b-180">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="8269b-181">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="8269b-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="8269b-182">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="8269b-182">Create and run applications</span></span>
* [<span data-ttu-id="8269b-183">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="8269b-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="8269b-184">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="8269b-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="8269b-185">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="8269b-185">Tools and extensions</span></span>
* [<span data-ttu-id="8269b-186">Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="8269b-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="8269b-187">Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota</span><span class="sxs-lookup"><span data-stu-id="8269b-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="8269b-188">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8269b-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="8269b-189">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="8269b-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="8269b-190">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="8269b-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="8269b-191">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="8269b-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="8269b-192">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="8269b-192">Manage resources</span></span>
* [<span data-ttu-id="8269b-193">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="8269b-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="8269b-194">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8269b-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
