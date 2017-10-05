---
title: Compilare applicazioni di Machine Learning Apache Spark in Azure HDInsight | Microsoft Docs
description: Istruzioni dettagliate su come compilare applicazioni di Machine Learning Apache Spark nei cluster HDInsight Spark usando il notebook di Jupyter
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
ms.openlocfilehash: 158ade4612104020e0231794e7123ea5cad6c459
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="d2932-103">Compilare applicazioni di Machine Learning Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2932-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="d2932-104">Informazioni su come compilare un'applicazione di Machine Learning Apache Spark usando un cluster Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d2932-104">Learn how to build an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="d2932-105">Questo articolo illustra come usare il notebook di Jupyter disponibile con il cluster per compilare e testare questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="d2932-105">This article shows how to use the Jupyter notebook available with the cluster to build and test this application.</span></span> <span data-ttu-id="d2932-106">L'applicazione usa i dati di HVAC.csv di esempio disponibili in tutti i cluster per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d2932-106">The application uses the sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="d2932-107">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="d2932-107">**Prerequisites:**</span></span>

<span data-ttu-id="d2932-108">È necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d2932-108">You must have the following:</span></span>

* <span data-ttu-id="d2932-109">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d2932-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="d2932-110">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="d2932-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="d2932-111"><a name="data"></a>Informazioni sul set di dati</span><span class="sxs-lookup"><span data-stu-id="d2932-111"><a name="data"></a>Understand the data set</span></span>
<span data-ttu-id="d2932-112">Prima di iniziare la compilazione dell'applicazione, comprendere la struttura dei dati per cui si compila l'applicazione e il tipo di analisi che verrà eseguita sui dati.</span><span class="sxs-lookup"><span data-stu-id="d2932-112">Before we start building the application, let us understand the structure of the data for which we build the application and the kind of analysis we will do on the data.</span></span> 

<span data-ttu-id="d2932-113">In questo articolo viene usato il file di dati di esempio **HVAC.csv** disponibile nell'account di archiviazione di Azure associato al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d2932-113">In this article, we use the sample **HVAC.csv** data file that is available in the Azure Storage account that you associated with the HDInsight cluster.</span></span> <span data-ttu-id="d2932-114">All'interno dell'account di archiviazione, il file si trova nel percorso: **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="d2932-114">Within the storage account, the file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="d2932-115">Scaricare e aprire il file con estensione csv per ottenere uno snapshot dei dati.</span><span class="sxs-lookup"><span data-stu-id="d2932-115">Download and open the CSV file to get a snapshot of the data.</span></span>  

<span data-ttu-id="d2932-116">![Snapshot dei dati usati per l'esempio Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot dei dati usati per l'esempio Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="d2932-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="d2932-117">I dati illustrano la temperatura di destinazione e la temperatura effettiva di un edificio con sistemi HVAC installati.</span><span class="sxs-lookup"><span data-stu-id="d2932-117">The data shows the target temperature and the actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="d2932-118">Si supponga che la colonna **System** rappresenti l'ID del sistema e la colonna **SystemAge** il numero di anni in cui il sistema HVAC è stato installato nell'edificio.</span><span class="sxs-lookup"><span data-stu-id="d2932-118">Let's assume the **System** column represents the system ID and the **SystemAge** column represents the number of years the HVAC system has been in place at the building.</span></span>

<span data-ttu-id="d2932-119">Questi dati sono usati per stimare se un edificio è caldo o freddo in base alla temperatura di destinazione, in base a un ID di sistema e all'età di sistema.</span><span class="sxs-lookup"><span data-stu-id="d2932-119">We use this data to predict whether a building will be hotter or colder based on the target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="d2932-120"><a name="app"></a>Scrivere un'applicazione di Machine Learning Spark usando Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="d2932-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="d2932-121">In questa applicazione viene usata una pipeline di Spark ML per eseguire una classificazione di documento.</span><span class="sxs-lookup"><span data-stu-id="d2932-121">In this application we use a Spark ML pipeline to perform a document classification.</span></span> <span data-ttu-id="d2932-122">Nella pipeline si è suddiviso il documento in parole, convertite le parole in un vettore di funzionalità numerico e infine creato un modello di stima usando i vettori di funzionalità e le etichette.</span><span class="sxs-lookup"><span data-stu-id="d2932-122">In the pipeline, we split the document into words, convert the words into a numerical feature vector, and finally build a prediction model using the feature vectors and labels.</span></span> <span data-ttu-id="d2932-123">Procedere come descritto di seguito per creare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d2932-123">Perform the following steps to create the application.</span></span>

1. <span data-ttu-id="d2932-124">Dalla Schermata iniziale del [portale di Azure](https://portal.azure.com/)fare clic sul riquadro del cluster Spark (se è stato aggiunto sulla Schermata iniziale).</span><span class="sxs-lookup"><span data-stu-id="d2932-124">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="d2932-125">È anche possibile passare al cluster da **Esplora tutto** > **Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d2932-125">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="d2932-126">Nel pannello del cluster Spark fare clic su **Dashboard cluster** e quindi su **Notebook di Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="d2932-126">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="d2932-127">Se richiesto, immettere le credenziali per il cluster.</span><span class="sxs-lookup"><span data-stu-id="d2932-127">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d2932-128">È anche possibile raggiungere il notebook di Jupyter per il cluster aprendo l'URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="d2932-128">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="d2932-129">Sostituire **CLUSTERNAME** con il nome del cluster:</span><span class="sxs-lookup"><span data-stu-id="d2932-129">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="d2932-130">Creare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="d2932-130">Create a new notebook.</span></span> <span data-ttu-id="d2932-131">Fare clic su **Nuovo** e quindi su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="d2932-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="d2932-132">![Creare un notebook di Jupyter per l'esempio di Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Creare un notebook di Jupyter per l'esempio di Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="d2932-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="d2932-133">Un nuovo notebook verrà creato e aperto con il nome Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="d2932-133">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="d2932-134">Fare clic sul nome del notebook nella parte superiore e immettere un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="d2932-134">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="d2932-135">![Fornire un nome di notebook per l'esempio di Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Fornire un nome di notebook per l'esempio di Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="d2932-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="d2932-136">Poiché il notebook è stato creato tramite il kernel PySpark, non è necessario creare contesti in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="d2932-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="d2932-137">I contesti Spark e Hive vengono creati automaticamente quando si esegue la prima cella di codice.</span><span class="sxs-lookup"><span data-stu-id="d2932-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="d2932-138">È possibile iniziare con l'importazione dei tipi necessari per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="d2932-138">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="d2932-139">Incollare il frammento di codice seguente in una cella vuota e quindi premere **MAIUSC+INVIO**.</span><span class="sxs-lookup"><span data-stu-id="d2932-139">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
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
6. <span data-ttu-id="d2932-140">È ora necessario caricare i dati (hvac.csv), da analizzare e usare per eseguire il training del modello.</span><span class="sxs-lookup"><span data-stu-id="d2932-140">You must now load the data (hvac.csv), parse it, and use it to train the model.</span></span> <span data-ttu-id="d2932-141">A tale scopo, è possibile definire una funzione che controlla se la temperatura effettiva dell'edificio è maggiore della temperatura di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d2932-141">For this, you define a function that checks whether the actual temperature of the building is greater than the target temperature.</span></span> <span data-ttu-id="d2932-142">Se la temperatura effettiva è maggiore, l’edificio è caldo ed è contrassegnato dal valore **1.0**.</span><span class="sxs-lookup"><span data-stu-id="d2932-142">If the actual temperature is greater, the building is hot, denoted by the value **1.0**.</span></span> <span data-ttu-id="d2932-143">Se la temperatura effettiva è inferiore, l’edificio è freddo ed è contrassegnato dal valore **0.0**.</span><span class="sxs-lookup"><span data-stu-id="d2932-143">If the actual temperature is lesser, the building is cold, denoted by the value **0.0**.</span></span> 
   
    <span data-ttu-id="d2932-144">Incollare il seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="d2932-144">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List the structure of data for better understanding. Because the data will be
        # loaded as an array, this structure makes it easy to understand what each element
        # in the array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses the raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load the raw HVAC.csv file, parse it using the function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="d2932-145">Configurare la pipeline di machine learning Spark che è costituita da tre fasi: tokenizer, hashingTF, e lr.</span><span class="sxs-lookup"><span data-stu-id="d2932-145">Configure the Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="d2932-146">Per altre informazioni su una pipeline e funzionamento vedere <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">pipeline machine learning di Spark</a>.</span><span class="sxs-lookup"><span data-stu-id="d2932-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="d2932-147">Incollare il seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="d2932-147">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="d2932-148">Adattare la pipeline al documento di formazione.</span><span class="sxs-lookup"><span data-stu-id="d2932-148">Fit the pipeline to the training document.</span></span> <span data-ttu-id="d2932-149">Incollare il seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="d2932-149">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="d2932-150">Verificare il documento di formazione per controllare lo stato di avanzamento con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d2932-150">Verify the training document to checkpoint your progress with the application.</span></span> <span data-ttu-id="d2932-151">Incollare il seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="d2932-151">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="d2932-152">Questo dovrebbe fornire un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d2932-152">This should give the output similar to the following:</span></span>
   
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

    <span data-ttu-id="d2932-153">Tornare indietro e verificare l'output nel file con estensione csv non elaborato.</span><span class="sxs-lookup"><span data-stu-id="d2932-153">Go back and verify the output against the raw CSV file.</span></span> <span data-ttu-id="d2932-154">Ad esempio, la prima riga del file con estensione csv ha dati:</span><span class="sxs-lookup"><span data-stu-id="d2932-154">For example, the first row the CSV file has this data:</span></span>

    <span data-ttu-id="d2932-155">![Snapshot dei dati di output per l'esempio Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Snapshot dei dati di output per l'esempio Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="d2932-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="d2932-156">Si noti come la temperatura effettiva è inferiore alla temperatura di destinazione. Questo dato indica che l'edificio è freddo.</span><span class="sxs-lookup"><span data-stu-id="d2932-156">Notice how the actual temperature is less than the target temperature suggesting the building is cold.</span></span> <span data-ttu-id="d2932-157">Nell'output di training, il valore per **label** nella prima riga è **0.0**, che indica che l'edificio non è caldo.</span><span class="sxs-lookup"><span data-stu-id="d2932-157">Hence in the training output, the value for **label** in the first row is **0.0**, which means the building is not hot.</span></span>

1. <span data-ttu-id="d2932-158">Preparazione per l'esecuzione del training modello rispetto a un set di dati.</span><span class="sxs-lookup"><span data-stu-id="d2932-158">Prepare a data set to run the trained model against.</span></span> <span data-ttu-id="d2932-159">A tale scopo, si passa a un ID di sistema e all'età di sistema (indicati come **SystemInfo** nell'output di formazione), e il modello potrebbe prevedere se la compilazione con tale ID di sistema ed età di sistema sarebbe più calda (contrassegnata da 1.0) o fredda (contrassegnata da 0.0).</span><span class="sxs-lookup"><span data-stu-id="d2932-159">To do so, we would pass on a system ID and system age (denoted as **SystemInfo** in the training output), and the model would predict whether the building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="d2932-160">Incollare il seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="d2932-160">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="d2932-161">Infine, eseguire stime sui dati di test.</span><span class="sxs-lookup"><span data-stu-id="d2932-161">Finally, make predictions on the test data.</span></span> <span data-ttu-id="d2932-162">Incollare il seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="d2932-162">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="d2932-163">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d2932-163">You should see an output similar to the following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="d2932-164">Nella prima riga di stima, si noterà che per un sistema HVAC con ID 20 e validità del sistema di 25 anni, l’edificio sarà caldo (**stima = 1.0**).</span><span class="sxs-lookup"><span data-stu-id="d2932-164">From the first row in the prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, the building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="d2932-165">Il primo valore per DenseVector (0.49999) corrisponde alla stima 0.0 e il secondo valore (0.5001) corrisponde alla stima 1.0.</span><span class="sxs-lookup"><span data-stu-id="d2932-165">The first value for DenseVector (0.49999) corresponds to the  prediction 0.0 and the second value (0.5001) corresponds to the prediction 1.0.</span></span> <span data-ttu-id="d2932-166">Nell'output, anche se il secondo valore è solo leggermente superiore, viene illustrato il modello **stima=1.0**.</span><span class="sxs-lookup"><span data-stu-id="d2932-166">In the output, even though the second value is only marginally higher, the model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="d2932-167">Al termine dell'esecuzione dell'applicazione, è necessario arrestare il notebook per rilasciare le risorse.</span><span class="sxs-lookup"><span data-stu-id="d2932-167">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="d2932-168">A tale scopo, dal menu **File** del notebook fare clic su **Close and Halt** (Chiudi e interrompi).</span><span class="sxs-lookup"><span data-stu-id="d2932-168">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="d2932-169">Questa operazione consente di arrestare e chiudere il notebook.</span><span class="sxs-lookup"><span data-stu-id="d2932-169">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="d2932-170"><a name="anaconda"></a>Usare la libreria Anaconda scikit-learn per Machine Learning Spark</span><span class="sxs-lookup"><span data-stu-id="d2932-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="d2932-171">I cluster Apache Spark in HDInsight includono librerie Anaconda.</span><span class="sxs-lookup"><span data-stu-id="d2932-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="d2932-172">Include inoltre la libreria **scikit-informazioni** per machine learning.</span><span class="sxs-lookup"><span data-stu-id="d2932-172">This also includes the **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="d2932-173">La libreria include inoltre diversi set di dati che è possibile usare per compilare applicazioni di esempio direttamente da un notebook Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d2932-173">The library also includes various data sets that you can use to build sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="d2932-174">Per esempi sull'uso della libreria scikit-learn, vedere [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="d2932-174">For examples on using the scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="d2932-175"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d2932-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="d2932-176">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2932-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="d2932-177">Scenari</span><span class="sxs-lookup"><span data-stu-id="d2932-177">Scenarios</span></span>
* [<span data-ttu-id="d2932-178">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2932-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="d2932-179">Spark con Machine Learning: utilizzare Spark in HDInsight per stimare i risultati dell'ispezione cibo</span><span class="sxs-lookup"><span data-stu-id="d2932-179">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="d2932-180">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="d2932-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="d2932-181">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2932-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="d2932-182">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="d2932-182">Create and run applications</span></span>
* [<span data-ttu-id="d2932-183">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="d2932-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="d2932-184">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="d2932-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="d2932-185">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="d2932-185">Tools and extensions</span></span>
* [<span data-ttu-id="d2932-186">Usare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark in Scala</span><span class="sxs-lookup"><span data-stu-id="d2932-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="d2932-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Usare il plug-in Strumenti HDInsight per IntelliJ IDEA per eseguire il debug di applicazioni Spark in remoto)</span><span class="sxs-lookup"><span data-stu-id="d2932-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="d2932-188">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2932-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="d2932-189">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2932-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="d2932-190">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="d2932-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="d2932-191">Installare Jupyter Notebook nel computer e connetterlo a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="d2932-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="d2932-192">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="d2932-192">Manage resources</span></span>
* [<span data-ttu-id="d2932-193">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2932-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="d2932-194">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2932-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
