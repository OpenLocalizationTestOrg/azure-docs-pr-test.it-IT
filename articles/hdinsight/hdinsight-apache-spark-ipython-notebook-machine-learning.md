---
title: aaaBuild Apache Spark apprendimento applicazioni in Azure HDInsight | Documenti Microsoft
description: Istruzioni dettagliate su come applicazione in HDInsight Spark di apprendimento automatico di Apache Spark toobuild cluster utilizzando server Jupyter notebook
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="0cf01-103">Compilare applicazioni di Machine Learning Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0cf01-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="0cf01-104">Informazioni su come toobuild cluster di un'applicazione di apprendimento macchina Apache Spark usando un Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0cf01-104">Learn how toobuild an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="0cf01-105">Questo articolo illustra come toouse hello server Jupyter notebook disponibili con toobuild cluster hello e test dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0cf01-105">This article shows how toouse hello Jupyter notebook available with hello cluster toobuild and test this application.</span></span> <span data-ttu-id="0cf01-106">un'applicazione Hello utilizza hello esempio HVAC.csv i dati disponibili in tutti i cluster per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="0cf01-106">hello application uses hello sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="0cf01-107">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="0cf01-107">**Prerequisites:**</span></span>

<span data-ttu-id="0cf01-108">È necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="0cf01-108">You must have hello following:</span></span>

* <span data-ttu-id="0cf01-109">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0cf01-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="0cf01-110">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="0cf01-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="0cf01-111"><a name="data"></a>Comprendere i set di dati hello</span><span class="sxs-lookup"><span data-stu-id="0cf01-111"><a name="data"></a>Understand hello data set</span></span>
<span data-ttu-id="0cf01-112">Prima di iniziare la creazione di un'applicazione hello, verrà ora analizzata la struttura di hello dei dati di hello per il quale è compilare un'applicazione hello e il tipo di hello di analisi che verranno eseguite sui dati hello.</span><span class="sxs-lookup"><span data-stu-id="0cf01-112">Before we start building hello application, let us understand hello structure of hello data for which we build hello application and hello kind of analysis we will do on hello data.</span></span> 

<span data-ttu-id="0cf01-113">In questo articolo, si usa l'esempio hello **HVAC.csv** file di dati è disponibile nell'account di archiviazione di Azure associati ai cluster HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="0cf01-113">In this article, we use hello sample **HVAC.csv** data file that is available in hello Azure Storage account that you associated with hello HDInsight cluster.</span></span> <span data-ttu-id="0cf01-114">Nell'account di archiviazione hello, del file hello è **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-114">Within hello storage account, hello file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="0cf01-115">Scaricare e aprire tooget di file CSV hello uno snapshot dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="0cf01-115">Download and open hello CSV file tooget a snapshot of hello data.</span></span>  

<span data-ttu-id="0cf01-116">![Snapshot dei dati usati per l'esempio Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot dei dati usati per l'esempio Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="0cf01-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="0cf01-117">dati Hello mostrano temperatura destinazione hello e hello effettivo temperatura un edificio con sistemi impianto installati.</span><span class="sxs-lookup"><span data-stu-id="0cf01-117">hello data shows hello target temperature and hello actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="0cf01-118">Si supponga ad esempio hello **sistema** colonna rappresenta l'ID di sistema hello e hello **SystemAge** colonna rappresenta il numero di hello di cui è stato sistema impianto hello in luogo alla generazione di hello anni.</span><span class="sxs-lookup"><span data-stu-id="0cf01-118">Let's assume hello **System** column represents hello system ID and hello **SystemAge** column represents hello number of years hello HVAC system has been in place at hello building.</span></span>

<span data-ttu-id="0cf01-119">Utilizziamo questo toopredict dati se un edificio sarà hotter o colder basata sulla temperatura destinazione hello, data un ID di sistema e l'età di sistema.</span><span class="sxs-lookup"><span data-stu-id="0cf01-119">We use this data toopredict whether a building will be hotter or colder based on hello target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="0cf01-120"><a name="app"></a>Scrivere un'applicazione di Machine Learning Spark usando Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="0cf01-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="0cf01-121">In questa applicazione viene utilizzato un tooperform pipeline Spark ML una classificazione di documenti.</span><span class="sxs-lookup"><span data-stu-id="0cf01-121">In this application we use a Spark ML pipeline tooperform a document classification.</span></span> <span data-ttu-id="0cf01-122">Nella pipeline di hello, si suddivise documento hello in parole, convertire parole hello in un vettore di funzione numerica e infine compilare un modello di stima utilizzando le etichette e i vettori di funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="0cf01-122">In hello pipeline, we split hello document into words, convert hello words into a numerical feature vector, and finally build a prediction model using hello feature vectors and labels.</span></span> <span data-ttu-id="0cf01-123">Eseguire hello un'applicazione hello toocreate i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="0cf01-123">Perform hello following steps toocreate hello application.</span></span>

1. <span data-ttu-id="0cf01-124">Da hello [portale Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello).</span><span class="sxs-lookup"><span data-stu-id="0cf01-124">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="0cf01-125">È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-125">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="0cf01-126">Dal Pannello di cluster Spark hello, fare clic su **Dashboard Cluster**, quindi fare clic su **server Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-126">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="0cf01-127">Se richiesto, immettere le credenziali di amministratore hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0cf01-127">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0cf01-128">È anche possibile raggiungere hello server Jupyter Notebook per il cluster usando hello apertura URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="0cf01-128">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="0cf01-129">Sostituire **CLUSTERNAME** con nome hello del cluster:</span><span class="sxs-lookup"><span data-stu-id="0cf01-129">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="0cf01-130">Creare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="0cf01-130">Create a new notebook.</span></span> <span data-ttu-id="0cf01-131">Fare clic su **Nuovo** e quindi su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="0cf01-132">![Creare un notebook di Jupyter per l'esempio di Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Creare un notebook di Jupyter per l'esempio di Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="0cf01-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="0cf01-133">Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="0cf01-133">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="0cf01-134">Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="0cf01-134">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="0cf01-135">![Fornire un nome di notebook per l'esempio di Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Fornire un nome di notebook per l'esempio di Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="0cf01-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="0cf01-136">Poiché è stato creato un notebook utilizza il kernel PySpark hello, non è necessario toocreate i contesti in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="0cf01-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="0cf01-137">Quando si esegue prima cella di codice hello contesti di Spark e Hive Hello verranno creati automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="0cf01-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="0cf01-138">È possibile avviare l'importazione di tipi di hello che sono necessari per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="0cf01-138">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="0cf01-139">Incollare hello seguente frammento di codice in una cella vuota e quindi premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-139">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. <span data-ttu-id="0cf01-140">È ora necessario caricare i dati di hello (hvac.csv), per analizzare e utilizzarlo come modello hello tootrain.</span><span class="sxs-lookup"><span data-stu-id="0cf01-140">You must now load hello data (hvac.csv), parse it, and use it tootrain hello model.</span></span> <span data-ttu-id="0cf01-141">A tale scopo, si definisce una funzione che controlla se è maggiore di temperatura destinazione hello hello effettivo temperatura compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="0cf01-141">For this, you define a function that checks whether hello actual temperature of hello building is greater than hello target temperature.</span></span> <span data-ttu-id="0cf01-142">Se temperatura effettivo hello è maggiore, compilazione hello è attivo, indicato dal valore hello **1.0**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-142">If hello actual temperature is greater, hello building is hot, denoted by hello value **1.0**.</span></span> <span data-ttu-id="0cf01-143">Se la temperatura reale hello è minore, compilazione hello è freddo, indicato dal valore hello **0,0**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-143">If hello actual temperature is lesser, hello building is cold, denoted by hello value **0.0**.</span></span> 
   
    <span data-ttu-id="0cf01-144">Hello Incolla seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-144">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="0cf01-145">Configurare l'apprendimento Spark hello pipeline costituita da tre fasi: tokenizer hashingTF e lr.</span><span class="sxs-lookup"><span data-stu-id="0cf01-145">Configure hello Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="0cf01-146">Per altre informazioni su una pipeline e funzionamento vedere <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">pipeline machine learning di Spark</a>.</span><span class="sxs-lookup"><span data-stu-id="0cf01-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="0cf01-147">Hello Incolla seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-147">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="0cf01-148">Adattare hello pipeline toohello training documento.</span><span class="sxs-lookup"><span data-stu-id="0cf01-148">Fit hello pipeline toohello training document.</span></span> <span data-ttu-id="0cf01-149">Hello Incolla seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-149">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="0cf01-150">Verificare lo stato di avanzamento con un'applicazione hello di hello training documento toocheckpoint.</span><span class="sxs-lookup"><span data-stu-id="0cf01-150">Verify hello training document toocheckpoint your progress with hello application.</span></span> <span data-ttu-id="0cf01-151">Hello Incolla seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-151">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="0cf01-152">Questo metodo dovrebbe produrre seguente toohello simile di hello output:</span><span class="sxs-lookup"><span data-stu-id="0cf01-152">This should give hello output similar toohello following:</span></span>
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    <span data-ttu-id="0cf01-153">Tornare indietro e verificare l'output di hello in file CSV non elaborato hello.</span><span class="sxs-lookup"><span data-stu-id="0cf01-153">Go back and verify hello output against hello raw CSV file.</span></span> <span data-ttu-id="0cf01-154">Ad esempio, file CSV hello hello prima riga include dati:</span><span class="sxs-lookup"><span data-stu-id="0cf01-154">For example, hello first row hello CSV file has this data:</span></span>

    <span data-ttu-id="0cf01-155">![Snapshot dei dati di output per l'esempio Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Snapshot dei dati di output per l'esempio Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="0cf01-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="0cf01-156">Si noti come temperatura effettivo hello è minore di temperatura destinazione hello suggerendo compilazione hello freddo.</span><span class="sxs-lookup"><span data-stu-id="0cf01-156">Notice how hello actual temperature is less than hello target temperature suggesting hello building is cold.</span></span> <span data-ttu-id="0cf01-157">Pertanto, nell'output di hello training hello valore per **etichetta** in hello prima riga è **0,0**, il che significa edificio hello non è attivo.</span><span class="sxs-lookup"><span data-stu-id="0cf01-157">Hence in hello training output, hello value for **label** in hello first row is **0.0**, which means hello building is not hot.</span></span>

1. <span data-ttu-id="0cf01-158">Preparare un modello con training di hello toorun set di dati contro.</span><span class="sxs-lookup"><span data-stu-id="0cf01-158">Prepare a data set toorun hello trained model against.</span></span> <span data-ttu-id="0cf01-159">toodo in tal caso, si passa su un ID di sistema e l'età di sistema (indicato come **SystemInfo** nell'output di hello training), e si stima modello hello hello se la compilazione con l'età di sistema e l'ID di sistema potrebbe essere hotter (indicato dalle 1.0) o dispositivo di raffreddamento ( indicato da 0,0).</span><span class="sxs-lookup"><span data-stu-id="0cf01-159">toodo so, we would pass on a system ID and system age (denoted as **SystemInfo** in hello training output), and hello model would predict whether hello building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="0cf01-160">Hello Incolla seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-160">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="0cf01-161">Infine, è possibile eseguire stime sui dati di test hello.</span><span class="sxs-lookup"><span data-stu-id="0cf01-161">Finally, make predictions on hello test data.</span></span> <span data-ttu-id="0cf01-162">Hello Incolla seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-162">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="0cf01-163">Verrà visualizzato un segue toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="0cf01-163">You should see an output similar toohello following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="0cf01-164">Hello prima riga stima hello, si noterà che per un sistema impianto con 20 ID e la validità di sistema di 25 anni, compilazione hello sarà attivo (**stima = 1.0**).</span><span class="sxs-lookup"><span data-stu-id="0cf01-164">From hello first row in hello prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, hello building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="0cf01-165">primo valore di Hello per DenseVector (0.49999) corrisponde toohello stima 0,0 e il valore secondo hello (0.5001) stima toohello 1.0.</span><span class="sxs-lookup"><span data-stu-id="0cf01-165">hello first value for DenseVector (0.49999) corresponds toohello  prediction 0.0 and hello second value (0.5001) corresponds toohello prediction 1.0.</span></span> <span data-ttu-id="0cf01-166">Nell'output di hello, anche se il secondo valore di hello è solo leggermente superiore, viene illustrato il modello di hello **stima = 1.0**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-166">In hello output, even though hello second value is only marginally higher, hello model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="0cf01-167">Al termine dell'esecuzione di un'applicazione hello, si consiglia di risorse di arresto hello notebook toorelease hello.</span><span class="sxs-lookup"><span data-stu-id="0cf01-167">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="0cf01-168">toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**.</span><span class="sxs-lookup"><span data-stu-id="0cf01-168">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="0cf01-169">Questo verrà arrestato e notebook hello Chiudi.</span><span class="sxs-lookup"><span data-stu-id="0cf01-169">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="0cf01-170"><a name="anaconda"></a>Usare la libreria Anaconda scikit-learn per Machine Learning Spark</span><span class="sxs-lookup"><span data-stu-id="0cf01-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="0cf01-171">I cluster Apache Spark in HDInsight includono librerie Anaconda.</span><span class="sxs-lookup"><span data-stu-id="0cf01-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="0cf01-172">Ciò include anche hello **scikit-informazioni** libreria per machine learning.</span><span class="sxs-lookup"><span data-stu-id="0cf01-172">This also includes hello **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="0cf01-173">libreria Hello include anche diversi set di dati che è possibile utilizzare applicazioni di esempio toobuild direttamente da un server Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="0cf01-173">hello library also includes various data sets that you can use toobuild sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="0cf01-174">Per esempi sull'utilizzo di hello scikit-libreria di informazioni, vedere [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="0cf01-174">For examples on using hello scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="0cf01-175"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0cf01-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="0cf01-176">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0cf01-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="0cf01-177">Scenari</span><span class="sxs-lookup"><span data-stu-id="0cf01-177">Scenarios</span></span>
* [<span data-ttu-id="0cf01-178">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0cf01-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="0cf01-179">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="0cf01-179">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="0cf01-180">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="0cf01-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="0cf01-181">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0cf01-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="0cf01-182">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="0cf01-182">Create and run applications</span></span>
* [<span data-ttu-id="0cf01-183">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="0cf01-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="0cf01-184">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="0cf01-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="0cf01-185">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="0cf01-185">Tools and extensions</span></span>
* [<span data-ttu-id="0cf01-186">Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="0cf01-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="0cf01-187">Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota</span><span class="sxs-lookup"><span data-stu-id="0cf01-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="0cf01-188">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0cf01-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="0cf01-189">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="0cf01-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="0cf01-190">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="0cf01-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="0cf01-191">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="0cf01-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="0cf01-192">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="0cf01-192">Manage resources</span></span>
* [<span data-ttu-id="0cf01-193">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="0cf01-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="0cf01-194">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0cf01-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
