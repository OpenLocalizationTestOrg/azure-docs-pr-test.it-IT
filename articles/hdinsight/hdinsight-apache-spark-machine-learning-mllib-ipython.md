---
title: esempio con MLlib Spark in HDInsight - Azure di apprendimento aaaMachine | Documenti Microsoft
description: Informazioni su come toouse Spark MLlib toocreate un'app di machine learning che analizza un set di dati utilizzano la classificazione e regressione logistica.
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
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="f4a55-104">Usare Spark MLlib toobuild un machine learning applicazione e analizzare un set di dati</span><span class="sxs-lookup"><span data-stu-id="f4a55-104">Use Spark MLlib toobuild a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="f4a55-105">Informazioni su come toouse Spark **MLlib** toocreate a machine learning applicazione toodo semplice analisi predittive su un set di dati aperti.</span><span class="sxs-lookup"><span data-stu-id="f4a55-105">Learn how toouse Spark **MLlib** toocreate a machine learning application toodo simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="f4a55-106">Dalle librerie di Machine Learning integrate di Spark, questo esempio usa la *classificazione* tramite la regressione logistica.</span><span class="sxs-lookup"><span data-stu-id="f4a55-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="f4a55-107">Questo esempio è disponibile anche come notebook Jupyter su un cluster Spark (Linux) creato in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4a55-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="f4a55-108">esperienza notebook Hello consente di eseguire frammenti di codice Python hello dal blocco appunti hello stesso.</span><span class="sxs-lookup"><span data-stu-id="f4a55-108">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="f4a55-109">esercitazione di hello toofollow all'interno di un blocco note, creare un Spark cluster e avviare un server Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="f4a55-109">toofollow hello tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="f4a55-110">Eseguire quindi il blocco note hello **Spark Machine Learning - analisi predittiva su dati di ispezione di cibo utilizzando MLlib.ipynb** in hello **Python** cartella.</span><span class="sxs-lookup"><span data-stu-id="f4a55-110">Then, run hello notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under hello **Python** folder.</span></span>
>
>

<span data-ttu-id="f4a55-111">MLlib è una libreria Spark di base che fornisce diverse utilità che agevolano le attività di Machine Learning, incluse utilità adatte a:</span><span class="sxs-lookup"><span data-stu-id="f4a55-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="f4a55-112">classificazione</span><span class="sxs-lookup"><span data-stu-id="f4a55-112">Classification</span></span>
* <span data-ttu-id="f4a55-113">Regressione</span><span class="sxs-lookup"><span data-stu-id="f4a55-113">Regression</span></span>
* <span data-ttu-id="f4a55-114">Clustering</span><span class="sxs-lookup"><span data-stu-id="f4a55-114">Clustering</span></span>
* <span data-ttu-id="f4a55-115">Modellazione di argomenti</span><span class="sxs-lookup"><span data-stu-id="f4a55-115">Topic modeling</span></span>
* <span data-ttu-id="f4a55-116">Scomposizione di valori singolari e analisi in componenti principali</span><span class="sxs-lookup"><span data-stu-id="f4a55-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="f4a55-117">Testing e calcolo ipotetici di statistiche di esempio</span><span class="sxs-lookup"><span data-stu-id="f4a55-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="f4a55-118">Che cosa sono la classificazione e regressione logistica?</span><span class="sxs-lookup"><span data-stu-id="f4a55-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="f4a55-119">*Classificazione*comune è un numero di machine learning, attività, è il processo di hello di ordinamento dei dati di input in categorie.</span><span class="sxs-lookup"><span data-stu-id="f4a55-119">*Classification*, a popular machine learning task, is hello process of sorting input data into categories.</span></span> <span data-ttu-id="f4a55-120">È il processo di hello di un toofigure algoritmo di classificazione come tooassign "etichette" tooinput dati forniti.</span><span class="sxs-lookup"><span data-stu-id="f4a55-120">It is hello job of a classification algorithm toofigure out how tooassign "labels" tooinput data that you provide.</span></span> <span data-ttu-id="f4a55-121">Ad esempio, è possibile pensare di un algoritmo di apprendimento automatico che accetta le informazioni come input e viene diviso hello stock in due categorie: scorte che è necessario vendere e che è consigliabile mantenere.</span><span class="sxs-lookup"><span data-stu-id="f4a55-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides hello stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="f4a55-122">La regressione logistica è algoritmo hello utilizzato per la classificazione.</span><span class="sxs-lookup"><span data-stu-id="f4a55-122">Logistic regression is hello algorithm that you use for classification.</span></span> <span data-ttu-id="f4a55-123">L'API di regressione logistica di Spark è utile per la *classificazione binaria*, ovvero la classificazione di dati di input in uno di due gruppi.</span><span class="sxs-lookup"><span data-stu-id="f4a55-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="f4a55-124">Per altre informazioni sulle regressioni logistiche, vedere [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="f4a55-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="f4a55-125">In sintesi, hello di regressione logistica genera un *funzione logistica* che può essere utilizzato toopredict hello probabilità appartiene un vettore di input in un gruppo o altri hello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-125">In summary, hello process of logistic regression produces a *logistic function* that can be used toopredict hello probability that an input vector belongs in one group or hello other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="f4a55-126">Esempio di analisi predittiva dei dati di controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="f4a55-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="f4a55-127">In questo esempio, utilizzare tooperform Spark analisi predittiva in dati di ispezione di cibo (**Food_Inspections1.csv**) che è stato acquisito tramite hello [portale dati Città di Chicago](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="f4a55-127">In this example, you use Spark tooperform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through hello [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="f4a55-128">Questo set di dati contiene informazioni sui controlli di cibo stabilimento che sono stati eseguiti a Chicago, incluse le informazioni relative a ciascuno di essi, le violazioni di hello trovato (se presente) e hello risultati dell'ispezione hello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, hello violations found (if any), and hello results of hello inspection.</span></span> <span data-ttu-id="f4a55-129">file di dati CSV Hello è già disponibile nell'account di archiviazione hello associato al cluster hello **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-129">hello CSV data file is already available in hello storage account associated with hello cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="f4a55-130">Nei seguenti passaggi hello è sviluppare un modello toosee toopass impiegato o esito negativo di un controllo di alimenti.</span><span class="sxs-lookup"><span data-stu-id="f4a55-130">In hello steps below, you develop a model toosee what it takes toopass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="f4a55-131">Iniziare a creare un'app di Machine Learning con MLlib Spark</span><span class="sxs-lookup"><span data-stu-id="f4a55-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="f4a55-132">Da hello [portale di Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello).</span><span class="sxs-lookup"><span data-stu-id="f4a55-132">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="f4a55-133">È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-133">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="f4a55-134">Dal Pannello di cluster Spark hello, fare clic su **Dashboard Cluster**, quindi fare clic su **server Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-134">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="f4a55-135">Se richiesto, immettere le credenziali di amministratore hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-135">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f4a55-136">È anche possibile raggiungere hello server Jupyter Notebook per il cluster usando hello apertura URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="f4a55-136">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="f4a55-137">Sostituire **CLUSTERNAME** con nome hello del cluster:</span><span class="sxs-lookup"><span data-stu-id="f4a55-137">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="f4a55-138">Creare un notebook.</span><span class="sxs-lookup"><span data-stu-id="f4a55-138">Create a notebook.</span></span> <span data-ttu-id="f4a55-139">Fare clic su **Nuovo** e quindi su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="f4a55-140">![Creare un notebook Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Creare un nuovo notebook Jupyter")</span><span class="sxs-lookup"><span data-stu-id="f4a55-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="f4a55-141">Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="f4a55-141">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="f4a55-142">Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="f4a55-142">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="f4a55-143">![Specificare un nome per notebook hello](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "specificare un nome per notebook hello")</span><span class="sxs-lookup"><span data-stu-id="f4a55-143">![Provide a name for hello notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for hello notebook")</span></span>
1. <span data-ttu-id="f4a55-144">Poiché è stato creato un notebook utilizza il kernel PySpark hello, non è necessario toocreate i contesti in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="f4a55-144">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="f4a55-145">contesti di Spark e Hive Hello vengono automaticamente creati automaticamente quando si esegue prima cella di codice hello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-145">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="f4a55-146">È possibile iniziare a compilare i machine learning applicazione tramite l'importazione di tipi di hello necessari per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="f4a55-146">You can start building your machine learning application by importing hello types required for this scenario.</span></span> <span data-ttu-id="f4a55-147">toodo in tal caso, posizionare il cursore hello nella cella hello e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-147">toodo so, place hello cursor in hello cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="f4a55-148">Creare un frame di dati di input</span><span class="sxs-lookup"><span data-stu-id="f4a55-148">Construct an input dataframe</span></span>
<span data-ttu-id="f4a55-149">È possibile utilizzare `sqlContext` tooperform trasformazioni ai dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="f4a55-149">We can use `sqlContext` tooperform transformations on structured data.</span></span> <span data-ttu-id="f4a55-150">Hello prima attività consiste dati di esempio hello tooload ((**Food_Inspections1.csv**)) in un database SQL Spark *dataframe*.</span><span class="sxs-lookup"><span data-stu-id="f4a55-150">hello first task is tooload hello sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="f4a55-151">Poiché i dati non elaborati hello sono in un formato CSV, è necessario toouse hello Spark contesto toopull ogni riga del file hello in memoria come testo non strutturato. è quindi utilizzare tooparse di libreria di Python CSV ogni riga singolarmente.</span><span class="sxs-lookup"><span data-stu-id="f4a55-151">Because hello raw data is in a CSV format, we need toouse hello Spark context toopull every line of hello file into memory as unstructured text; then, you use Python's CSV library tooparse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="f4a55-152">File CSV hello è ora disponibile come un RDD.</span><span class="sxs-lookup"><span data-stu-id="f4a55-152">We now have hello CSV file as an RDD.</span></span>  <span data-ttu-id="f4a55-153">toounderstand hello lo schema di hello dati, è recuperare una riga da hello RDD.</span><span class="sxs-lookup"><span data-stu-id="f4a55-153">toounderstand hello schema of hello data, we retrieve one row from hello RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="f4a55-154">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f4a55-154">You should see an output like hello following:</span></span>

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
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="f4a55-155">Hello output precedente offre un'idea di schema hello hello del file di input.</span><span class="sxs-lookup"><span data-stu-id="f4a55-155">hello preceding output gives us an idea of hello schema of hello input file.</span></span> <span data-ttu-id="f4a55-156">Include il nome di hello di ogni stabilimento, il tipo hello stabilimento, indirizzo hello, dati hello di controlli hello e la posizione di hello, tra l'altro.</span><span class="sxs-lookup"><span data-stu-id="f4a55-156">It includes hello name of every establishment, hello type of establishment, hello address, hello data of hello inspections, and hello location, among other things.</span></span> <span data-ttu-id="f4a55-157">Selezionare di seguito alcune colonne che sono utili per l'analisi predittiva e raggruppare i risultati di hello come frame di dati, che è quindi utilizzano toocreate una tabella temporanea.</span><span class="sxs-lookup"><span data-stu-id="f4a55-157">Let's select a few columns that are useful for our predictive analysis and group hello results as a dataframe, which we then use toocreate a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="f4a55-158">Ora è disponibile un *frame di dati*, `df`, su cui è possibile eseguire l'analisi.</span><span class="sxs-lookup"><span data-stu-id="f4a55-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="f4a55-159">È presente anche la tabella temporanea **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="f4a55-160">Sono stati inclusi quattro colonne di interesse nel frame di dati hello: **id**, **nome**, **risultati**, e **violazioni**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-160">We've included four columns of interest in hello dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="f4a55-161">Verrà visualizzato un piccolo esempio dei dati hello:</span><span class="sxs-lookup"><span data-stu-id="f4a55-161">Let's get a small sample of hello data:</span></span>

        df.show(5)

    <span data-ttu-id="f4a55-162">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f4a55-162">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a><span data-ttu-id="f4a55-163">Comprendere i dati di hello</span><span class="sxs-lookup"><span data-stu-id="f4a55-163">Understand hello data</span></span>
1. <span data-ttu-id="f4a55-164">Iniziamo tooget un'idea di cosa contiene il set di dati.</span><span class="sxs-lookup"><span data-stu-id="f4a55-164">Let's start tooget a sense of what our dataset contains.</span></span> <span data-ttu-id="f4a55-165">Ad esempio, quali sono i valori diversi hello hello **risultati** colonna?</span><span class="sxs-lookup"><span data-stu-id="f4a55-165">For example, what are hello different values in hello **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="f4a55-166">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f4a55-166">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="f4a55-167">Una visualizzazione rapida ci consente di prendere in considerazione la distribuzione hello di questi risultati.</span><span class="sxs-lookup"><span data-stu-id="f4a55-167">A quick visualization can help us reason about hello distribution of these outcomes.</span></span> <span data-ttu-id="f4a55-168">Abbiamo già dati hello in una tabella temporanea **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-168">We already have hello data in a temporary table **CountResults**.</span></span> <span data-ttu-id="f4a55-169">È possibile eseguire hello seguente query SQL su hello tabella tooget una migliore comprensione del modo in cui vengono distribuiti i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-169">You can run hello following SQL query against hello table tooget a better understanding of how hello results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="f4a55-170">Hello `%%sql` magic seguita da `-o countResultsdf` assicura che output di hello di hello query è persistente in locale nel server Jupyter hello (in genere. da nodo a hello a head del cluster hello).</span><span class="sxs-lookup"><span data-stu-id="f4a55-170">hello `%%sql` magic followed by `-o countResultsdf` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="f4a55-171">output di Hello viene mantenuta come un [Pandas](http://pandas.pydata.org/) frame di dati con hello specificato nome **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-171">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **countResultsdf**.</span></span>

    <span data-ttu-id="f4a55-172">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f4a55-172">You should see an output like hello following:</span></span>

    <span data-ttu-id="f4a55-173">![Output della query SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Output della query SQL")</span><span class="sxs-lookup"><span data-stu-id="f4a55-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="f4a55-174">Per ulteriori informazioni su hello `%%sql` magic e altri magics disponibili con kernel PySpark hello, vedere [kernel disponibile sui server Jupyter notebook con i cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="f4a55-174">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="f4a55-175">È inoltre possibile utilizzare Matplotlib, una libreria utilizzata tooconstruct della visualizzazione dei dati, toocreate un tracciato.</span><span class="sxs-lookup"><span data-stu-id="f4a55-175">You can also use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="f4a55-176">Perché è necessario creare tracciato hello da hello localmente persistente **countResultsdf** frame di dati, il frammento di codice hello deve iniziare con hello `%%local` magic.</span><span class="sxs-lookup"><span data-stu-id="f4a55-176">Because hello plot must be created from hello locally persisted **countResultsdf** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="f4a55-177">In questo modo si garantisce che il codice hello viene eseguito localmente su server Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-177">This ensures that hello code is run locally on hello Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="f4a55-178">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f4a55-178">You should see an output like hello following:</span></span>

    <span data-ttu-id="f4a55-179">![Output dell'applicazione Machine Learning in Spark: grafico a torta con cinque risultati di controllo differenti](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Output del risultato di Machine Learning in Spark")</span><span class="sxs-lookup"><span data-stu-id="f4a55-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="f4a55-180">Come si può notare, un controllo può portare a cinque diversi risultati:</span><span class="sxs-lookup"><span data-stu-id="f4a55-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="f4a55-181">Business not located</span><span class="sxs-lookup"><span data-stu-id="f4a55-181">Business not located</span></span>
   * <span data-ttu-id="f4a55-182">Fail</span><span class="sxs-lookup"><span data-stu-id="f4a55-182">Fail</span></span>
   * <span data-ttu-id="f4a55-183">Pass</span><span class="sxs-lookup"><span data-stu-id="f4a55-183">Pass</span></span>
   * <span data-ttu-id="f4a55-184">Pass w/ conditions</span><span class="sxs-lookup"><span data-stu-id="f4a55-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="f4a55-185">Out of Business</span><span class="sxs-lookup"><span data-stu-id="f4a55-185">Out of Business</span></span>

     <span data-ttu-id="f4a55-186">Segnalare il problema, sviluppare un modello che chiaro risultato hello di un controllo di alimenti, violazioni hello specificato.</span><span class="sxs-lookup"><span data-stu-id="f4a55-186">Let us develop a model that can guess hello outcome of a food inspection, given hello violations.</span></span> <span data-ttu-id="f4a55-187">Poiché la regressione logistica è un metodo di classificazione binaria, rende toogroup senso i dati in due categorie: **esito negativo** e **passare**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-187">Since logistic regression is a binary classification method, it makes sense toogroup our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="f4a55-188">Un "passare con condizioni" è ancora un passaggio, pertanto quando si esegue il training del modello di hello, consideriamo hello due risultati equivalenti.</span><span class="sxs-lookup"><span data-stu-id="f4a55-188">A "Pass w/ Conditions" is still a Pass, so when we train hello model, we consider hello two results equivalent.</span></span> <span data-ttu-id="f4a55-189">Dati con hello altri risultati ("Business non disponibile" o "Out-of-Business") non sono utili in modo è rimuovere il set di training.</span><span class="sxs-lookup"><span data-stu-id="f4a55-189">Data with hello other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="f4a55-190">Deve essere corretto poiché queste due categorie costituiscono una piccola percentuale dei risultati di hello comunque.</span><span class="sxs-lookup"><span data-stu-id="f4a55-190">This should be okay since these two categories make up a very small percentage of hello results anyway.</span></span>
1. <span data-ttu-id="f4a55-191">Ora si passerà alla conversione del frame di dati esistente (`df`) in un nuovo frame di dati in cui ogni controllo è rappresentato come coppia etichetta-violazioni.</span><span class="sxs-lookup"><span data-stu-id="f4a55-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="f4a55-192">In questo caso, un'etichetta `0.0` rappresenta un controllo non superato, un'etichetta `1.0` rappresenta un controllo superato e un'etichetta `-1.0` rappresenta altri risultati,</span><span class="sxs-lookup"><span data-stu-id="f4a55-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="f4a55-193">È escludere tali altri risultati per il calcolo di frame di dati nuovi hello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-193">We filter those other results out when computing hello new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="f4a55-194">toosee quali hello con l'etichetta dati è simile, si recupera una riga.</span><span class="sxs-lookup"><span data-stu-id="f4a55-194">toosee what hello labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="f4a55-195">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f4a55-195">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a><span data-ttu-id="f4a55-196">Creare un modello di regressione logistica da hello input frame di dati</span><span class="sxs-lookup"><span data-stu-id="f4a55-196">Create a logistic regression model from hello input dataframe</span></span>
<span data-ttu-id="f4a55-197">L'attività finale è hello tooconvert con l'etichetta dati in un formato che può essere analizzato da regressione logistica.</span><span class="sxs-lookup"><span data-stu-id="f4a55-197">Our final task is tooconvert hello labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="f4a55-198">algoritmo di regressione logistica Hello tooa input deve essere un set di *coppie di funzionalità di etichetta vettore*, dove hello "vettore di funzione" è un vettore di numeri che rappresentano punti input hello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-198">hello input tooa logistic regression algorithm should be a set of *label-feature vector pairs*, where hello "feature vector" is a vector of numbers representing hello input point.</span></span> <span data-ttu-id="f4a55-199">In tal caso, è necessario tooconvert violazioni"hello" colonna, semistrutturati e contiene molti commenti nella matrice tooan testo libero, di numeri reali che una macchina facilmente comprensibile.</span><span class="sxs-lookup"><span data-stu-id="f4a55-199">So, we need tooconvert hello "violations" column, which is semi-structured and contains many comments in free-text, tooan array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="f4a55-200">Un approccio di apprendimento macchina standard per il linguaggio naturale elaborazione tooassign ogni parola distinct "index" e quindi passare un vettore toohello algoritmo di machine learning in modo che il valore di ogni indice contiene la frequenza relativa hello di tale parola nel testo hello stringa.</span><span class="sxs-lookup"><span data-stu-id="f4a55-200">One standard machine learning approach for processing natural language is tooassign each distinct word an "index", and then pass a vector toohello machine learning algorithm such that each index's value contains hello relative frequency of that word in hello text string.</span></span>

<span data-ttu-id="f4a55-201">MLlib fornisce un modo semplice di tooperform questa operazione.</span><span class="sxs-lookup"><span data-stu-id="f4a55-201">MLlib provides an easy way tooperform this operation.</span></span> <span data-ttu-id="f4a55-202">In primo luogo, "suddividere" ogni violazioni stringa tooget hello singole parole in ciascuna stringa.</span><span class="sxs-lookup"><span data-stu-id="f4a55-202">First, "tokenize" each violations string tooget hello individual words in each string.</span></span> <span data-ttu-id="f4a55-203">Quindi, usare un `HashingTF` tooconvert ogni set di token in un vettore di funzionalità che può quindi essere tooconstruct algoritmo di regressione logistica toohello passato a un modello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-203">Then, use a `HashingTF` tooconvert each set of tokens into a feature vector that can then be passed toohello logistic regression algorithm tooconstruct a model.</span></span> <span data-ttu-id="f4a55-204">Tutti questi passaggi verranno eseguiti in sequenza con una "pipeline".</span><span class="sxs-lookup"><span data-stu-id="f4a55-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a><span data-ttu-id="f4a55-205">Valutare il modello di hello in un set di dati di test separato</span><span class="sxs-lookup"><span data-stu-id="f4a55-205">Evaluate hello model on a separate test dataset</span></span>
<span data-ttu-id="f4a55-206">È possibile utilizzare il modello di hello creato in precedenza troppo*stimare* quali hello risultati dei controlli nuovo sarà, in base che sono state osservate le violazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-206">We can use hello model we created earlier too*predict* what hello results of new inspections will be, based on hello violations that were observed.</span></span> <span data-ttu-id="f4a55-207">È stato sottoposto a training questo modello nel set di dati hello **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-207">We trained this model on hello dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="f4a55-208">Segnalare il problema, utilizzare un secondo set di dati, **Food_Inspections2.csv**, troppo*valutare* hello forza di questo modello nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="f4a55-208">Let us use a second dataset, **Food_Inspections2.csv**, too*evaluate* hello strength of this model on new data.</span></span> <span data-ttu-id="f4a55-209">Il secondo set di dati (**Food_Inspections2.csv**) deve essere già nel contenitore di archiviazione predefinito hello associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="f4a55-209">This second data set (**Food_Inspections2.csv**) should already be in hello default storage container associated with hello cluster.</span></span>

1. <span data-ttu-id="f4a55-210">Hello frammento di codice seguente viene creato un nuovo frame di dati, **predictionsDf** contenente stima hello generato dal modello hello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-210">hello following snippet creates a new dataframe, **predictionsDf** that contains hello prediction generated by hello model.</span></span> <span data-ttu-id="f4a55-211">frammento di codice Hello crea anche una tabella temporanea denominata **stime** in base a hello frame di dati.</span><span class="sxs-lookup"><span data-stu-id="f4a55-211">hello snippet also creates a temporary table called **Predictions** based on hello dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="f4a55-212">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f4a55-212">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="f4a55-213">Esaminare una delle stime di hello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-213">Look at one of hello predictions.</span></span> <span data-ttu-id="f4a55-214">Eseguire questo frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="f4a55-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="f4a55-215">Non vi è una stima per hello prima voce hello set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="f4a55-215">There is a prediction for hello first entry in hello test data set.</span></span>
1. <span data-ttu-id="f4a55-216">Hello `model.transform()` metodo si applica hello stessa trasformazione tooany nuovi dati con hello stesso schema e ottenere una stima della modalità tooclassify hello dati.</span><span class="sxs-lookup"><span data-stu-id="f4a55-216">hello `model.transform()` method applies hello same transformation tooany new data with hello same schema, and arrive at a prediction of how tooclassify hello data.</span></span> <span data-ttu-id="f4a55-217">Possiamo tooget alcune statistiche semplice senso di valutare l'accuratezza delle nostri stime:</span><span class="sxs-lookup"><span data-stu-id="f4a55-217">We can do some simple statistics tooget a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="f4a55-218">output di Hello è simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4a55-218">hello output looks like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="f4a55-219">Utilizzare la regressione logistica con Spark offre un modello accurato della relazione hello tra le violazioni e le descrizioni in inglese se un'azienda consente di passare o esito negativo di un controllo di alimenti.</span><span class="sxs-lookup"><span data-stu-id="f4a55-219">Using logistic regression with Spark gives us an accurate model of hello relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-hello-prediction"></a><span data-ttu-id="f4a55-220">Creare una rappresentazione visiva della stima hello</span><span class="sxs-lookup"><span data-stu-id="f4a55-220">Create a visual representation of hello prediction</span></span>
<span data-ttu-id="f4a55-221">È ora possibile costruire un toohelp visualizzazione finale che ci motivo sui risultati di hello del test.</span><span class="sxs-lookup"><span data-stu-id="f4a55-221">We can now construct a final visualization toohelp us reason about hello results of this test.</span></span>

1. <span data-ttu-id="f4a55-222">Iniziamo estraendo stime diverse hello e risultati di hello **stime** tabella temporanea creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f4a55-222">We start by extracting hello different predictions and results from hello **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="f4a55-223">la query seguente Hello separare output di hello come *true_positive*, *false_positive*, *true_negative*, e *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="f4a55-223">hello following queries separate hello output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="f4a55-224">Nella seguente query hello è disattivare la visualizzazione utilizzando `-q` e salvare anche l'output di hello (tramite `-o`) come frame di dati che può essere quindi utilizzato con hello `%%local` magic.</span><span class="sxs-lookup"><span data-stu-id="f4a55-224">In hello queries below, we turn off visualization by using `-q` and also save hello output (by using `-o`) as dataframes that can be then used with hello `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="f4a55-225">Infine, utilizzare hello seguente frammento di codice toogenerate hello tracciato utilizzando **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-225">Finally, use hello following snippet toogenerate hello plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="f4a55-226">È necessario visualizzare hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="f4a55-226">You should see hello following output:</span></span>

    <span data-ttu-id="f4a55-227">![Output dell'applicazione Machine Learning in Spark: grafico a torta con le percentuali sui controlli alimentari con esito negativo](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Output del risultato di Machine Learning in Spark")</span><span class="sxs-lookup"><span data-stu-id="f4a55-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="f4a55-228">In questo grafico, un risultato "positivo" si riferisce ispezione alimentare toohello non riuscita, mentre un risultato negativo si riferisce tooa passato ispezione.</span><span class="sxs-lookup"><span data-stu-id="f4a55-228">In this chart, a "positive" result refers toohello failed food inspection, while a negative result refers tooa passed inspection.</span></span>

## <a name="shut-down-hello-notebook"></a><span data-ttu-id="f4a55-229">Chiudere Blocco note hello</span><span class="sxs-lookup"><span data-stu-id="f4a55-229">Shut down hello notebook</span></span>
<span data-ttu-id="f4a55-230">Al termine dell'esecuzione di un'applicazione hello, sarà necessario arrestare le risorse di hello notebook toorelease hello.</span><span class="sxs-lookup"><span data-stu-id="f4a55-230">After you have finished running hello application, you should shut down hello notebook toorelease hello resources.</span></span> <span data-ttu-id="f4a55-231">toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**.</span><span class="sxs-lookup"><span data-stu-id="f4a55-231">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="f4a55-232">Questo chiude e si chiude hello notebook.</span><span class="sxs-lookup"><span data-stu-id="f4a55-232">This shuts down and closes hello notebook.</span></span>

## <span data-ttu-id="f4a55-233"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f4a55-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="f4a55-234">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4a55-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="f4a55-235">Scenari</span><span class="sxs-lookup"><span data-stu-id="f4a55-235">Scenarios</span></span>
* [<span data-ttu-id="f4a55-236">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4a55-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f4a55-237">Spark con Machine Learning: usare Spark in HDInsight per l'analisi della temperatura di un edificio con sistemi HVAC</span><span class="sxs-lookup"><span data-stu-id="f4a55-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f4a55-238">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="f4a55-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="f4a55-239">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4a55-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="f4a55-240">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="f4a55-240">Create and run applications</span></span>
* [<span data-ttu-id="f4a55-241">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="f4a55-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f4a55-242">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="f4a55-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f4a55-243">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="f4a55-243">Tools and extensions</span></span>
* [<span data-ttu-id="f4a55-244">Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="f4a55-244">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="f4a55-245">Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota</span><span class="sxs-lookup"><span data-stu-id="f4a55-245">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f4a55-246">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4a55-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f4a55-247">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4a55-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f4a55-248">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="f4a55-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="f4a55-249">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="f4a55-249">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="f4a55-250">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="f4a55-250">Manage resources</span></span>
* [<span data-ttu-id="f4a55-251">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="f4a55-251">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f4a55-252">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4a55-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
