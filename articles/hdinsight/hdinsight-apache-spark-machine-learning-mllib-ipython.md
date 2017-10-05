---
title: Esempio di Machine Learning con MLlib Spark in HDInsight di Azure | Microsoft Docs
description: Informazioni su come usare MLlib Spark per creare un'app di Machine Learning che analizza un set di dati usando una classificazione tramite la regressione logistica.
keywords: machine learning in spark, esempio machine learning in spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: e563d4f51c9e27b20df47eca6d3eb00ac79e854f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-spark-mllib-to-build-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="aa6c5-104">Usare MLlib Spark per creare un'applicazione di Machine Learning e analizzare un set di dati</span><span class="sxs-lookup"><span data-stu-id="aa6c5-104">Use Spark MLlib to build a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="aa6c5-105">Informazioni su come usare **MLlib** Spark per creare un'applicazione di Machine Learning che effettui analisi predittive semplici su un set di dati aperto.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-105">Learn how to use Spark **MLlib** to create a machine learning application to do simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="aa6c5-106">Dalle librerie di Machine Learning integrate di Spark, questo esempio usa la *classificazione* tramite la regressione logistica.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="aa6c5-107">Questo esempio è disponibile anche come notebook Jupyter su un cluster Spark (Linux) creato in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="aa6c5-108">L'esperienza offerta dal notebook consente di eseguire i frammenti di codice Python dal notebook stesso.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-108">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="aa6c5-109">Per seguire l'esercitazione da un notebook, creare un cluster Spark e avviare un notebook Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="aa6c5-109">To follow the tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="aa6c5-110">Eseguire quindi il notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** nella cartella **Python**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-110">Then, run the notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under the **Python** folder.</span></span>
>
>

<span data-ttu-id="aa6c5-111">MLlib è una libreria Spark di base che fornisce diverse utilità che agevolano le attività di Machine Learning, incluse utilità adatte a:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="aa6c5-112">classificazione</span><span class="sxs-lookup"><span data-stu-id="aa6c5-112">Classification</span></span>
* <span data-ttu-id="aa6c5-113">Regressione</span><span class="sxs-lookup"><span data-stu-id="aa6c5-113">Regression</span></span>
* <span data-ttu-id="aa6c5-114">Clustering</span><span class="sxs-lookup"><span data-stu-id="aa6c5-114">Clustering</span></span>
* <span data-ttu-id="aa6c5-115">Modellazione di argomenti</span><span class="sxs-lookup"><span data-stu-id="aa6c5-115">Topic modeling</span></span>
* <span data-ttu-id="aa6c5-116">Scomposizione di valori singolari e analisi in componenti principali</span><span class="sxs-lookup"><span data-stu-id="aa6c5-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="aa6c5-117">Testing e calcolo ipotetici di statistiche di esempio</span><span class="sxs-lookup"><span data-stu-id="aa6c5-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="aa6c5-118">Che cosa sono la classificazione e regressione logistica?</span><span class="sxs-lookup"><span data-stu-id="aa6c5-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="aa6c5-119">La *classificazione*, un'attività comune di apprendimento automatico, è il processo di ordinamento dei dati in categorie.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-119">*Classification*, a popular machine learning task, is the process of sorting input data into categories.</span></span> <span data-ttu-id="aa6c5-120">È il processo eseguito da un algoritmo di classificazione per determinare come assegnare le "etichette" ai dati di input specificati.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-120">It is the job of a classification algorithm to figure out how to assign "labels" to input data that you provide.</span></span> <span data-ttu-id="aa6c5-121">Si pensi, ad esempio, a un algoritmo di apprendimento automatico che accetta informazioni sulle azioni come input e divide le azioni in due categorie: azioni da vendere e azioni da conservare.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides the stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="aa6c5-122">La regressione logistica è l'algoritmo usato per la classificazione.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-122">Logistic regression is the algorithm that you use for classification.</span></span> <span data-ttu-id="aa6c5-123">L'API di regressione logistica di Spark è utile per la *classificazione binaria*, ovvero la classificazione di dati di input in uno di due gruppi.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="aa6c5-124">Per altre informazioni sulle regressioni logistiche, vedere [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="aa6c5-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="aa6c5-125">Riepilogando, il processo di regressione logistica genera una *funzione logistica* che può essere usata per stimare la probabilità che un vettore di input appartenga a un gruppo o all'altro.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-125">In summary, the process of logistic regression produces a *logistic function* that can be used to predict the probability that an input vector belongs in one group or the other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="aa6c5-126">Esempio di analisi predittiva dei dati di controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="aa6c5-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="aa6c5-127">In questo esempio si userà Spark per eseguire un'analisi predittiva dei dati del controllo degli alimenti (**Food_Inspections1.csv**) acquisiti dal [portale dati della città di Chicago](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="aa6c5-127">In this example, you use Spark to perform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through the [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="aa6c5-128">Questo set di dati contiene informazioni sui controlli degli alimenti condotti a Chicago, incluse informazioni su ogni stabilimento controllato, sulle eventuali violazioni riscontrate e sui risultati del controllo.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, the violations found (if any), and the results of the inspection.</span></span> <span data-ttu-id="aa6c5-129">Il file di dati in formato CSV è già disponibile nell'account di archiviazione associato al cluster in **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-129">The CSV data file is already available in the storage account associated with the cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="aa6c5-130">Nei passaggi seguenti, si svilupperà un modello per sapere che cosa serve per superare o non superare un controllo sugli alimenti.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-130">In the steps below, you develop a model to see what it takes to pass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="aa6c5-131">Iniziare a creare un'app di Machine Learning con MLlib Spark</span><span class="sxs-lookup"><span data-stu-id="aa6c5-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="aa6c5-132">Dalla Schermata iniziale del [portale di Azure](https://portal.azure.com/) fare clic sul riquadro del cluster Spark, se è stato aggiunto sulla Schermata iniziale.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-132">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="aa6c5-133">È anche possibile passare al cluster da **Esplora tutto** > **Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-133">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="aa6c5-134">Nel pannello del cluster Spark fare clic su **Dashboard cluster** e quindi su **Notebook di Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-134">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="aa6c5-135">Se richiesto, immettere le credenziali per il cluster.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-135">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="aa6c5-136">È anche possibile raggiungere il notebook di Jupyter per il cluster aprendo l'URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-136">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="aa6c5-137">Sostituire **CLUSTERNAME** con il nome del cluster:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-137">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="aa6c5-138">Creare un notebook.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-138">Create a notebook.</span></span> <span data-ttu-id="aa6c5-139">Fare clic su **Nuovo** e quindi su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="aa6c5-140">![Creare un notebook Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Creare un nuovo notebook Jupyter")</span><span class="sxs-lookup"><span data-stu-id="aa6c5-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="aa6c5-141">Un nuovo notebook verrà creato e aperto con il nome Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-141">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="aa6c5-142">Fare clic sul nome del notebook nella parte superiore e immettere un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-142">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="aa6c5-143">![Specificare un nome per il notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Specificare un nome per il notebook")</span><span class="sxs-lookup"><span data-stu-id="aa6c5-143">![Provide a name for the notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for the notebook")</span></span>
1. <span data-ttu-id="aa6c5-144">Poiché il notebook è stato creato tramite il kernel PySpark, non è necessario creare contesti in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-144">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="aa6c5-145">I contesti Spark e Hive vengono creati automaticamente quando si esegue la prima cella di codice.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-145">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="aa6c5-146">È possibile iniziare a compilare l'applicazione di Machine Learning  importando i tipi necessari per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-146">You can start building your machine learning application by importing the types required for this scenario.</span></span> <span data-ttu-id="aa6c5-147">A tale scopo, posizionare il cursore nella cella e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-147">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="aa6c5-148">Creare un frame di dati di input</span><span class="sxs-lookup"><span data-stu-id="aa6c5-148">Construct an input dataframe</span></span>
<span data-ttu-id="aa6c5-149">È possibile che venga usato `sqlContext` per eseguire trasformazioni sui dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-149">We can use `sqlContext` to perform transformations on structured data.</span></span> <span data-ttu-id="aa6c5-150">La prima attività è il caricamento dei dati di esempio (**Food_Inspections1.csv**) in un *frame di dati* Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-150">The first task is to load the sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="aa6c5-151">Poiché i dati non elaborati sono in formato con estensione csv, è necessario usare il contesto Spark per eseguire il pull di ogni riga del file nella memoria come testo non strutturato, quindi si usa la libreria CSV di Python per analizzare ogni singola riga.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-151">Because the raw data is in a CSV format, we need to use the Spark context to pull every line of the file into memory as unstructured text; then, you use Python's CSV library to parse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="aa6c5-152">Il file con estensione csv ora è disponibile come RDD.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-152">We now have the CSV file as an RDD.</span></span>  <span data-ttu-id="aa6c5-153">Per comprendere lo schema dei dati, viene recuperata una riga da RDD.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-153">To understand the schema of the data, we retrieve one row from the RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="aa6c5-154">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-154">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of the plumbing section of the Municipal Code of Chicago and Rules and Regulation of the Board of Health. OBSEVERD THE 3 COMPARTMENT SINK BACKING UP INTO THE 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding to protect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED TO REPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN THE REAR CHILDREN AREA,IN THE KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED TO REPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY THE 15MOS AREA. NEED TO BE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY THE EXPOSED HAND SINK IN THE KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: The floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED TO ELEVATE ALL FOOD ITEMS 6INCH OFF THE FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="aa6c5-155">L'output precedente dà un'idea dello schema del file di input.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-155">The preceding output gives us an idea of the schema of the input file.</span></span> <span data-ttu-id="aa6c5-156">Include nome, tipo, indirizzo di ogni stabilimento, la data dei controlli e la loro ubicazione, oltre ad altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-156">It includes the name of every establishment, the type of establishment, the address, the data of the inspections, and the location, among other things.</span></span> <span data-ttu-id="aa6c5-157">Ora si selezionano alcune colonne utili per le analisi predittive e si raggruppano i risultati come dataframe, da usare poi per creare una tabella temporanea.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-157">Let's select a few columns that are useful for our predictive analysis and group the results as a dataframe, which we then use to create a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="aa6c5-158">Ora è disponibile un *frame di dati*, `df`, su cui è possibile eseguire l'analisi.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="aa6c5-159">È presente anche la tabella temporanea **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="aa6c5-160">Nel dataframe sono state incluse quattro colonne importanti: **id**, **name**, **results** e **violations**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-160">We've included four columns of interest in the dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="aa6c5-161">Prendere un piccolo campione di dati:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-161">Let's get a small sample of the data:</span></span>

        df.show(5)

    <span data-ttu-id="aa6c5-162">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-162">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES TO ...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-the-data"></a><span data-ttu-id="aa6c5-163">Informazioni sui dati</span><span class="sxs-lookup"><span data-stu-id="aa6c5-163">Understand the data</span></span>
1. <span data-ttu-id="aa6c5-164">Ora si determinerà il contenuto del set di dati.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-164">Let's start to get a sense of what our dataset contains.</span></span> <span data-ttu-id="aa6c5-165">Ad esempio, quali sono i diversi valori della colona **results** ?</span><span class="sxs-lookup"><span data-stu-id="aa6c5-165">For example, what are the different values in the **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="aa6c5-166">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-166">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. <span data-ttu-id="aa6c5-167">Una visualizzazione rapida aiuta a riflettere sulla distribuzione di questi risultati.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-167">A quick visualization can help us reason about the distribution of these outcomes.</span></span> <span data-ttu-id="aa6c5-168">Sono già disponibili i dati nella tabella temporanea **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-168">We already have the data in a temporary table **CountResults**.</span></span> <span data-ttu-id="aa6c5-169">Per comprendere meglio il modo in cui i risultati vengono distribuiti, è possibile eseguire la query SQL seguente sulla tabella.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-169">You can run the following SQL query against the table to get a better understanding of how the results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="aa6c5-170">Il comando speciale `%%sql` seguito da `-o countResultsdf` assicura che l'output della query venga mantenuto in locale nel server Jupyter, di solito il nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-170">The `%%sql` magic followed by `-o countResultsdf` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="aa6c5-171">L'output viene conservato come frame di dati [Pandas](http://pandas.pydata.org/) con il nome specificato **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-171">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **countResultsdf**.</span></span>

    <span data-ttu-id="aa6c5-172">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-172">You should see an output like the following:</span></span>

    <span data-ttu-id="aa6c5-173">![Output della query SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Output della query SQL")</span><span class="sxs-lookup"><span data-stu-id="aa6c5-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="aa6c5-174">Per altre informazioni sul comando Magic `%%sql` e sugli altri comandi Magic disponibili con il kernel PySpark, vedere [Kernel disponibili per i notebook di Jupyter con cluster Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="aa6c5-174">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="aa6c5-175">È anche possibile creare un tracciato tramite Matplotlib, una libreria che consente di creare visualizzazioni di dati.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-175">You can also use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="aa6c5-176">Poiché il tracciato deve essere creato dal frame di dati **countResultsdf** conservato in locale, il frammento di codice deve iniziare con `%%local`.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-176">Because the plot must be created from the locally persisted **countResultsdf** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="aa6c5-177">Ciò garantisce che il codice venga eseguito localmente nel server di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-177">This ensures that the code is run locally on the Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="aa6c5-178">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-178">You should see an output like the following:</span></span>

    <span data-ttu-id="aa6c5-179">![Output dell'applicazione Machine Learning in Spark: grafico a torta con cinque risultati di controllo differenti](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Output del risultato di Machine Learning in Spark")</span><span class="sxs-lookup"><span data-stu-id="aa6c5-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="aa6c5-180">Come si può notare, un controllo può portare a cinque diversi risultati:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="aa6c5-181">Business not located</span><span class="sxs-lookup"><span data-stu-id="aa6c5-181">Business not located</span></span>
   * <span data-ttu-id="aa6c5-182">Fail</span><span class="sxs-lookup"><span data-stu-id="aa6c5-182">Fail</span></span>
   * <span data-ttu-id="aa6c5-183">Pass</span><span class="sxs-lookup"><span data-stu-id="aa6c5-183">Pass</span></span>
   * <span data-ttu-id="aa6c5-184">Pass w/ conditions</span><span class="sxs-lookup"><span data-stu-id="aa6c5-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="aa6c5-185">Out of Business</span><span class="sxs-lookup"><span data-stu-id="aa6c5-185">Out of Business</span></span>

     <span data-ttu-id="aa6c5-186">Sviluppare ora un modello che può ricavare il risultato di un controllo degli alimenti, una volta determinate le violazioni.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-186">Let us develop a model that can guess the outcome of a food inspection, given the violations.</span></span> <span data-ttu-id="aa6c5-187">Poiché la regressione logistica è un metodo di classificazione binaria, è consigliabile raggruppare i dati in due categorie: **Fail** e **Pass**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-187">Since logistic regression is a binary classification method, it makes sense to group our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="aa6c5-188">"Pass w/ Conditions" fa parte della categoria Pass, quindi, quando si esegue il training del modello, i due risultati saranno considerati equivalenti.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-188">A "Pass w/ Conditions" is still a Pass, so when we train the model, we consider the two results equivalent.</span></span> <span data-ttu-id="aa6c5-189">I dati con gli altri risultati ("Business Not Located", "Out of Business"), non essendo utili, verranno rimossi dal set di training.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-189">Data with the other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="aa6c5-190">Non dovrebbero verificarsi problemi, perché queste due categorie costituiscono solo una percentuale minima dei risultati.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-190">This should be okay since these two categories make up a very small percentage of the results anyway.</span></span>
1. <span data-ttu-id="aa6c5-191">Ora si passerà alla conversione del frame di dati esistente (`df`) in un nuovo frame di dati in cui ogni controllo è rappresentato come coppia etichetta-violazioni.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="aa6c5-192">In questo caso, un'etichetta `0.0` rappresenta un controllo non superato, un'etichetta `1.0` rappresenta un controllo superato e un'etichetta `-1.0` rappresenta altri risultati,</span><span class="sxs-lookup"><span data-stu-id="aa6c5-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="aa6c5-193">che verranno esclusi durante il calcolo del nuovo dataframe.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-193">We filter those other results out when computing the new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="aa6c5-194">Recuperare una riga dai dati con etichetta per verificare come appare.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-194">To see what the labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="aa6c5-195">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-195">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of the food establishment and all parts of the property used in connection with the operation of the establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF THE FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: The flow of air discharged from kitchen fans shall always be through a duct to a point above the roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT TO DINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT TO OFFICE.")]

## <a name="create-a-logistic-regression-model-from-the-input-dataframe"></a><span data-ttu-id="aa6c5-196">Creare un modello di regressione logistica dal frame di dati di input</span><span class="sxs-lookup"><span data-stu-id="aa6c5-196">Create a logistic regression model from the input dataframe</span></span>
<span data-ttu-id="aa6c5-197">L'ultima attività è la conversione dei dati con etichetta in un formato che possa essere analizzato dalla regressione logistica.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-197">Our final task is to convert the labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="aa6c5-198">L'input per un algoritmo di regressione logistica deve essere un set di *coppie etichetta-vettore di funzionalità*, dove il "vettore di funzionalità" è un vettore di numeri che rappresenta il punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-198">The input to a logistic regression algorithm should be a set of *label-feature vector pairs*, where the "feature vector" is a vector of numbers representing the input point.</span></span> <span data-ttu-id="aa6c5-199">È quindi necessario poter convertire la colonna "violations", che è semistrutturata e contiene numerosi commenti in testo libero, in una matrice di numeri reali facilmente comprensibili per un computer.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-199">So, we need to convert the "violations" column, which is semi-structured and contains many comments in free-text, to an array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="aa6c5-200">Un approccio di apprendimento automatico standard per l'elaborazione del linguaggio naturale consiste nell'assegnare a ogni singola parola un "indice" e quindi nel passare un vettore all'algoritmo di apprendimento automatico in modo che ogni valore dell'indice contenga la frequenza relativa di tale parola nella stringa di testo.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-200">One standard machine learning approach for processing natural language is to assign each distinct word an "index", and then pass a vector to the machine learning algorithm such that each index's value contains the relative frequency of that word in the text string.</span></span>

<span data-ttu-id="aa6c5-201">MLlib consente di eseguire facilmente questa operazione.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-201">MLlib provides an easy way to perform this operation.</span></span> <span data-ttu-id="aa6c5-202">In primo luogo, suddividere in token ogni stringa di violazione per ottenere le parole singole in ogni stringa.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-202">First, "tokenize" each violations string to get the individual words in each string.</span></span> <span data-ttu-id="aa6c5-203">Quindi, usare un `HashingTF` per convertire ogni set di token in un vettore di funzione da passare successivamente all'algoritmo di regressione logistica per creare un modello.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-203">Then, use a `HashingTF` to convert each set of tokens into a feature vector that can then be passed to the logistic regression algorithm to construct a model.</span></span> <span data-ttu-id="aa6c5-204">Tutti questi passaggi verranno eseguiti in sequenza con una "pipeline".</span><span class="sxs-lookup"><span data-stu-id="aa6c5-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-the-model-on-a-separate-test-dataset"></a><span data-ttu-id="aa6c5-205">Valutare il modello in un set di dati di test separato</span><span class="sxs-lookup"><span data-stu-id="aa6c5-205">Evaluate the model on a separate test dataset</span></span>
<span data-ttu-id="aa6c5-206">È possibile usare il modello creato prima per *stimare* quali saranno i risultati dei nuovi controlli, in base alle violazioni osservate.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-206">We can use the model we created earlier to *predict* what the results of new inspections will be, based on the violations that were observed.</span></span> <span data-ttu-id="aa6c5-207">Il training di questo modello è stato eseguito nel set di dati **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-207">We trained this model on the dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="aa6c5-208">Si userà ora un secondo set di dati, **Food_Inspections2.csv**, per *valutare* l'efficacia di questo modello sui nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-208">Let us use a second dataset, **Food_Inspections2.csv**, to *evaluate* the strength of this model on new data.</span></span> <span data-ttu-id="aa6c5-209">Questo secondo set di dati (**Food_Inspections2.csv**) dovrebbe trovarsi già nel contenitore di archiviazione predefinito associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-209">This second data set (**Food_Inspections2.csv**) should already be in the default storage container associated with the cluster.</span></span>

1. <span data-ttu-id="aa6c5-210">Il frammento di codice seguente crea un nuovo dataframe, **predictionsDf** contenente la stima generata dal modello.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-210">The following snippet creates a new dataframe, **predictionsDf** that contains the prediction generated by the model.</span></span> <span data-ttu-id="aa6c5-211">Il frammento di codice crea anche la tabella temporanea **Predictions** basata sul dataframe.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-211">The snippet also creates a temporary table called **Predictions** based on the dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="aa6c5-212">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-212">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. <span data-ttu-id="aa6c5-213">Esaminare una delle stime.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-213">Look at one of the predictions.</span></span> <span data-ttu-id="aa6c5-214">Eseguire questo frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="aa6c5-215">La stima per la prima voce verrà visualizzata nel set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-215">There is a prediction for the first entry in the test data set.</span></span>
1. <span data-ttu-id="aa6c5-216">Il metodo `model.transform()` applicherà la stessa trasformazione ai nuovi dati con lo stesso schema e formulerà una stima per la classificazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-216">The `model.transform()` method applies the same transformation to any new data with the same schema, and arrive at a prediction of how to classify the data.</span></span> <span data-ttu-id="aa6c5-217">È possibile calcolare alcune semplici statistiche per comprendere l'accuratezza delle stime:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-217">We can do some simple statistics to get a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="aa6c5-218">L'output è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="aa6c5-218">The output looks like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="aa6c5-219">L'uso della regressione logistica con Spark offre un modello accurato della relazione tra le descrizioni delle violazioni in inglese e la probabilità che una determinata azienda superi o meno un controllo degli alimenti.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-219">Using logistic regression with Spark gives us an accurate model of the relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-the-prediction"></a><span data-ttu-id="aa6c5-220">Creare una rappresentazione visiva della stima</span><span class="sxs-lookup"><span data-stu-id="aa6c5-220">Create a visual representation of the prediction</span></span>
<span data-ttu-id="aa6c5-221">Per comprendere meglio i risultati di questo test, ora è possibile creare una visualizzazione finale.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-221">We can now construct a final visualization to help us reason about the results of this test.</span></span>

1. <span data-ttu-id="aa6c5-222">Iniziare dall'estrazione delle diverse stime e dei vari risultati dalla tabella temporanea **Predictions** creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-222">We start by extracting the different predictions and results from the **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="aa6c5-223">Le query seguenti separano l'output in *true_positive*, *false_positive*, *true_negative* e *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-223">The following queries separate the output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="aa6c5-224">Nelle query seguenti disattivare la visualizzazione usando `-q` e tramite `-o` salvare l'output come frame di dati utilizzabili con il comando speciale `%%local`.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-224">In the queries below, we turn off visualization by using `-q` and also save the output (by using `-o`) as dataframes that can be then used with the `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="aa6c5-225">Usare infine il frammento di codice seguente per generare il tracciato con **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-225">Finally, use the following snippet to generate the plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="aa6c5-226">Dovrebbe venire visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-226">You should see the following output:</span></span>

    <span data-ttu-id="aa6c5-227">![Output dell'applicazione Machine Learning in Spark: grafico a torta con le percentuali sui controlli alimentari con esito negativo](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Output del risultato di Machine Learning in Spark")</span><span class="sxs-lookup"><span data-stu-id="aa6c5-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="aa6c5-228">In questo grafico un risultato positivo indica il controllo degli alimenti non superato, mentre un risultato negativo indica un controllo superato.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-228">In this chart, a "positive" result refers to the failed food inspection, while a negative result refers to a passed inspection.</span></span>

## <a name="shut-down-the-notebook"></a><span data-ttu-id="aa6c5-229">Arrestare il notebook</span><span class="sxs-lookup"><span data-stu-id="aa6c5-229">Shut down the notebook</span></span>
<span data-ttu-id="aa6c5-230">Al termine dell'esecuzione dell'applicazione, è necessario arrestare il notebook per rilasciare le risorse.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-230">After you have finished running the application, you should shut down the notebook to release the resources.</span></span> <span data-ttu-id="aa6c5-231">A tale scopo, dal menu **File** del notebook fare clic su **Close and Halt** (Chiudi e interrompi).</span><span class="sxs-lookup"><span data-stu-id="aa6c5-231">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="aa6c5-232">Il notebook viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="aa6c5-232">This shuts down and closes the notebook.</span></span>

## <span data-ttu-id="aa6c5-233"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="aa6c5-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="aa6c5-234">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa6c5-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="aa6c5-235">Scenari</span><span class="sxs-lookup"><span data-stu-id="aa6c5-235">Scenarios</span></span>
* [<span data-ttu-id="aa6c5-236">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa6c5-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="aa6c5-237">Spark con Machine Learning: usare Spark in HDInsight per l'analisi della temperatura di un edificio con sistemi HVAC</span><span class="sxs-lookup"><span data-stu-id="aa6c5-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="aa6c5-238">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="aa6c5-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="aa6c5-239">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa6c5-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="aa6c5-240">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="aa6c5-240">Create and run applications</span></span>
* [<span data-ttu-id="aa6c5-241">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="aa6c5-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="aa6c5-242">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="aa6c5-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="aa6c5-243">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="aa6c5-243">Tools and extensions</span></span>
* [<span data-ttu-id="aa6c5-244">Usare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="aa6c5-244">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="aa6c5-245">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Usare il plug-in Strumenti HDInsight per IntelliJ IDEA per eseguire il debug di applicazioni Spark in remoto)</span><span class="sxs-lookup"><span data-stu-id="aa6c5-245">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="aa6c5-246">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa6c5-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="aa6c5-247">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa6c5-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="aa6c5-248">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="aa6c5-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="aa6c5-249">Installare Jupyter Notebook nel computer e connetterlo a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="aa6c5-249">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="aa6c5-250">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="aa6c5-250">Manage resources</span></span>
* [<span data-ttu-id="aa6c5-251">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa6c5-251">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="aa6c5-252">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa6c5-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
