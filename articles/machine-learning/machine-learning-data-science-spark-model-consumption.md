---
title: Rendere operativi i modelli di apprendimento automatico compilati con Spark | Documentazione Microsoft
description: Informazioni su come caricare e assegnare punteggi ai modelli di apprendimento salvati in Archiviazione BLOB di Azure (WASB) con Python.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 626305a2-0abf-4642-afb0-dad0f6bd24e9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 00fec675bed0137473f7e3c5ddfe9c3c0e8344c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="13218-103">Rendere operativi i modelli di apprendimento automatico compilati con Spark</span><span class="sxs-lookup"><span data-stu-id="13218-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="13218-104">Questo argomento illustra come rendere operativo un modello di apprendimento automatico (ML) salvato mediante Python in cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="13218-104">This topic shows how to operationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="13218-105">Descrive come caricare modelli di apprendimento automatico compilati con MLlib di Spark e archiviati in BLOB di Archiviazione di Azure (WASB) e come assegnare loro un punteggio con dataset archiviati in WASB.</span><span class="sxs-lookup"><span data-stu-id="13218-105">It describes how to load machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how to score them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="13218-106">Illustra come pre-elaborare i dati di input, come trasformare le funzionalità con le funzioni di codifica e indicizzazione nel toolkit MLlib e come creare un oggetto dati punto etichettato da usare come input per l'assegnazione dei punteggi con i modelli di apprendimento automatico.</span><span class="sxs-lookup"><span data-stu-id="13218-106">It shows how to pre-process the input data, transform features using the indexing and encoding functions in the MLlib toolkit, and how to create a labeled point data object that can be used as input for scoring with the ML models.</span></span> <span data-ttu-id="13218-107">I modelli usati per l'assegnazione dei punteggi includono la regressione lineare, la regressione logistica, le foreste casuali e gli alberi con boosting a gradienti.</span><span class="sxs-lookup"><span data-stu-id="13218-107">The models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="13218-108">Cluster Spark e notebook di Jupyter</span><span class="sxs-lookup"><span data-stu-id="13218-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="13218-109">La procedura di configurazione e il codice per rendere operativo un modello ML, forniti in questa procedura dettagliata, sono applicabili sia con cluster HDInsight Spark 1.6 sia che con cluster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="13218-109">Setup steps and the code to operationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="13218-110">Il codice per queste procedure è fornito anche nel notebook di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="13218-110">The code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="13218-111">Notebook per Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="13218-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="13218-112">Il notebook di Jupyter [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) illustra come rendere operativo un modello salvato usando Python sui cluster di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13218-112">The [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how to operationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="13218-113">Notebook per Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="13218-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="13218-114">Al fine di modificare il notebook di Jupyter per Spark 1.6 per l'uso di un cluster HDInsight Spark 2.0, sostituire il file di codice Python con [questo file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="13218-114">To modify the Jupyter notebook for Spark 1.6 to use with an HDInsight Spark 2.0 cluster, replace the Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="13218-115">Questo codice illustra come usare i modelli creati in Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="13218-115">This code shows how to consume the models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="13218-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="13218-116">Prerequisites</span></span>

1. <span data-ttu-id="13218-117">Per completare questa procedura dettagliata sono necessari un account Azure e un cluster HDInsight Spark 1.6 o 2.0.</span><span class="sxs-lookup"><span data-stu-id="13218-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster to complete this walkthrough.</span></span> <span data-ttu-id="13218-118">Per istruzioni su come soddisfare questi requisiti, vedere [Panoramica dell'analisi scientifica dei dati con Spark in Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13218-118">See the [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how to satisfy these requirements.</span></span> <span data-ttu-id="13218-119">Questo argomento contiene inoltre una descrizione dei dati dei taxi di NYC per il 2013 usati qui e istruzioni su come eseguire il codice da un notebook Jupyter nel cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="13218-119">That topic also contains a description of the NYC 2013 Taxi data used here and instructions on how to execute code from a Jupyter notebook on the Spark cluster.</span></span> 
2. <span data-ttu-id="13218-120">È anche necessario creare i modelli di Machine Learning per l'assegnazione dei punteggi seguendo le istruzioni nell'argomento [Modellazione ed esplorazione dei dati con Spark](machine-learning-data-science-spark-data-exploration-modeling.md) per il cluster Spark 1.6 o i notebook Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="13218-120">You must also create the machine learning models to be scored here by working through the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for the Spark 1.6 cluster or the Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="13218-121">I notebook Spark 2.0 usano un dataset aggiuntivo per l'attività di classificazione, il noto dataset sulle partenze puntuali dei voli tra il 2011 e il 2012.</span><span class="sxs-lookup"><span data-stu-id="13218-121">The Spark 2.0 notebooks use an additional data set for the classification task, the well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="13218-122">Vengono inoltre forniti una descrizione dei notebook e i relativi collegamenti nel [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) per il repository GitHub che li contiene.</span><span class="sxs-lookup"><span data-stu-id="13218-122">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="13218-123">Inoltre, il codice in questo esempio e nei notebook collegati è generico e funzionerà in qualsiasi cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="13218-123">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="13218-124">Se non si usa HDInsight Spark, i passaggi di configurazione e gestione del cluster possono essere leggermente diversi rispetto a quanto illustrato qui.</span><span class="sxs-lookup"><span data-stu-id="13218-124">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="13218-125">Configurazione: percorsi di archiviazione, librerie e contesto Spark preimpostato</span><span class="sxs-lookup"><span data-stu-id="13218-125">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="13218-126">Spark può eseguire operazioni di lettura e scrittura in un BLOB del servizio di archiviazione di Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="13218-126">Spark is able to read and write to an Azure Storage Blob (WASB).</span></span> <span data-ttu-id="13218-127">I dati esistenti archiviati in WASB possono essere elaborati con Spark e i relativi risultati possono essere memorizzati nuovamente in BLOB di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="13218-127">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="13218-128">Per salvare file o modelli in WASB, è necessario specificare correttamente il percorso.</span><span class="sxs-lookup"><span data-stu-id="13218-128">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="13218-129">È possibile fare riferimento al contenitore predefinito collegato al cluster Spark usando un percorso che inizia con: *"wasb//"*.</span><span class="sxs-lookup"><span data-stu-id="13218-129">The default container attached to the Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="13218-130">L'esempio di codice seguente specifica il percorso dei dati da leggere e il percorso della directory di archiviazione del modello in cui viene salvato l'output del modello.</span><span class="sxs-lookup"><span data-stu-id="13218-130">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="13218-131">Impostare percorsi di directory per i percorsi di archiviazione in WASB</span><span class="sxs-lookup"><span data-stu-id="13218-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="13218-132">I modelli vengono salvati in: "wasb:///user/remoteuser/NYCTaxi/Models".</span><span class="sxs-lookup"><span data-stu-id="13218-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="13218-133">Se questo percorso non è impostato correttamente, i modelli non vengono caricati per l'assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="13218-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="13218-134">I risultati con punteggio vengono salvati in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span><span class="sxs-lookup"><span data-stu-id="13218-134">The scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="13218-135">Se il percorso della cartella non è corretto, i risultati non vengono salvati nella cartella.</span><span class="sxs-lookup"><span data-stu-id="13218-135">If the path to folder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="13218-136">È possibile incollare i percorsi dei file nei segnaposto di questo codice dopo averli copiati dall'output dell'ultima cella del notebook **machine-learning-data-science-spark-data-exploration-modeling.ipynb** .</span><span class="sxs-lookup"><span data-stu-id="13218-136">The file path locations can be copied and pasted into the placeholders in this code from the output of the last cell of the **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="13218-137">Ecco il codice per impostare i percorsi di directory:</span><span class="sxs-lookup"><span data-stu-id="13218-137">Here is the code to set directory paths:</span></span> 

    # LOCATION OF DATA TO BE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THE LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE THE LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR THE MODELS TO BE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="13218-138">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="13218-138">**OUTPUT:**</span></span>

<span data-ttu-id="13218-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="13218-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="13218-140">Importare le librerie</span><span class="sxs-lookup"><span data-stu-id="13218-140">Import libraries</span></span>
<span data-ttu-id="13218-141">Impostare il contesto Spark e importare le librerie necessarie usando il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="13218-141">Set spark context and import necessary libraries with the following code</span></span>

    #IMPORT LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="13218-142">Contesto di Spark preimpostato e magic di PySpark</span><span class="sxs-lookup"><span data-stu-id="13218-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="13218-143">I kernel PySpark forniti con i notebook di Jupyter hanno un contesto preimpostato,</span><span class="sxs-lookup"><span data-stu-id="13218-143">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="13218-144">quindi non è necessario impostare esplicitamente i contesti Spark o Hive prima di iniziare a usare l'applicazione in fase di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="13218-144">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="13218-145">I contesti sono disponibili per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="13218-145">These are available for you by default.</span></span> <span data-ttu-id="13218-146">Questi contesti sono:</span><span class="sxs-lookup"><span data-stu-id="13218-146">These contexts are:</span></span>

* <span data-ttu-id="13218-147">sc per Spark</span><span class="sxs-lookup"><span data-stu-id="13218-147">sc - for Spark</span></span> 
* <span data-ttu-id="13218-148">sqlContext per Hive</span><span class="sxs-lookup"><span data-stu-id="13218-148">sqlContext - for Hive</span></span>

<span data-ttu-id="13218-149">Il kernel PySpark offre alcuni “magic” predefiniti, ovvero comandi speciali che è possibile chiamare con %%.</span><span class="sxs-lookup"><span data-stu-id="13218-149">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="13218-150">Negli esempi di codice seguenti sono usati due comandi di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="13218-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="13218-151">**%%local**: specifica che il codice presente nelle righe successive viene eseguito localmente.</span><span class="sxs-lookup"><span data-stu-id="13218-151">**%%local** Specified that the code in subsequent lines is executed locally.</span></span> <span data-ttu-id="13218-152">Deve trattarsi di codice Python valido.</span><span class="sxs-lookup"><span data-stu-id="13218-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="13218-153">**%%sql -o <variable name>**</span><span class="sxs-lookup"><span data-stu-id="13218-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="13218-154">Esegue una query Hive su sqlContext.</span><span class="sxs-lookup"><span data-stu-id="13218-154">Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="13218-155">Se viene passato il parametro -o, il risultato della query viene salvato in modo permanente nel contesto Python %%local come frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="13218-155">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="13218-156">Per altre informazioni sui kernel per i notebook di Jupyter e i "magic" predefiniti messi a disposizione, vedere [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md) (Kernel disponibili per i notebook di Jupyter con cluster Apache Spark in HDInsight Linux).</span><span class="sxs-lookup"><span data-stu-id="13218-156">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="13218-157">Inserire i dati e creare un frame di dati pulito</span><span class="sxs-lookup"><span data-stu-id="13218-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="13218-158">Questa sezione contiene il codice per una serie di attività necessarie per inserire i dati per l'assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="13218-158">This section contains the code for a series of tasks required to ingest the data to be scored.</span></span> <span data-ttu-id="13218-159">Leggere un campione unito in join pari allo 0,1% del file TSV relativo alle corse e alle tariffe dei taxi, formattare i dati e creare un frame di dati pulito.</span><span class="sxs-lookup"><span data-stu-id="13218-159">Read in a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file), format the data, and then creates a clean data frame.</span></span>

<span data-ttu-id="13218-160">I file relativi alle corse e alle tariffe dei taxi sono stati uniti seguendo la procedura illustrata nell'articolo [Processo di analisi scientifica dei dati per i team in azione: uso dei cluster Hadoop di HDInsight](machine-learning-data-science-process-hive-walkthrough.md) .</span><span class="sxs-lookup"><span data-stu-id="13218-160">The taxi trip and fare files were joined based on the procedure provided in the: [The Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF THE FILE FROM HEADER
    schema_string = taxi_test_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # CREATE DATA FRAME
    taxi_df_test = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_test_cleaned = taxi_df_test.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_cleaned.cache()
    taxi_df_test_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_test_cleaned.registerTempTable("taxi_test")

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="13218-161">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="13218-161">**OUTPUT:**</span></span>

<span data-ttu-id="13218-162">Tempo impiegato per eseguire questa cella: 46,37 secondi.</span><span class="sxs-lookup"><span data-stu-id="13218-162">Time taken to execute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="13218-163">Preparare i dati per l'assegnazione dei punteggi in Spark</span><span class="sxs-lookup"><span data-stu-id="13218-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="13218-164">Questa sezione illustra come indicizzare, codificare e ridimensionare le caratteristiche categoriche per prepararle all'uso in algoritmi di apprendimento supervisionato di MLlib, per la classificazione e la regressione.</span><span class="sxs-lookup"><span data-stu-id="13218-164">This section shows how to index, encode, and scale categorical features to prepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="13218-165">Trasformazione di funzionalità: indicizzare e codificare funzionalità categoriche per l'inserimento in modelli per l'assegnazione dei punteggi</span><span class="sxs-lookup"><span data-stu-id="13218-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="13218-166">Questa sezione illustra come indicizzare dati categorici con `StringIndexer` e codificare funzionalità con `OneHotEncoder` per l'inserimento nei modelli.</span><span class="sxs-lookup"><span data-stu-id="13218-166">This section shows how to index categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into the models.</span></span>

<span data-ttu-id="13218-167">[StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) esegue la codifica di una colonna stringa di etichette in una colonna di indici etichetta.</span><span class="sxs-lookup"><span data-stu-id="13218-167">The [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels to a column of label indices.</span></span> <span data-ttu-id="13218-168">Gli indici sono ordinati in base alla frequenza delle etichette.</span><span class="sxs-lookup"><span data-stu-id="13218-168">The indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="13218-169">[OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) esegue il mapping di una colonna di indici etichetta a una colonna di vettori binari, con al massimo un singolo valore unico.</span><span class="sxs-lookup"><span data-stu-id="13218-169">The [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="13218-170">Questa codifica permette di applicare a funzionalità categoriche gli algoritmi che prevedono funzionalità con valori continui, ad esempio la regressione logistica.</span><span class="sxs-lookup"><span data-stu-id="13218-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, to be applied to categorical features.</span></span>

    #INDEX AND ONE-HOT ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_test 
    """
    taxi_df_test_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_with_newFeatures.cache()
    taxi_df_test_with_newFeatures.count()

    # INDEX AND ONE-HOT ENCODING
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is the cleaned one from above
    indexed = model.transform(taxi_df_test_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND ENCODE TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="13218-171">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="13218-171">**OUTPUT:**</span></span>

<span data-ttu-id="13218-172">Tempo impiegato per eseguire questa cella: 5,37 secondi.</span><span class="sxs-lookup"><span data-stu-id="13218-172">Time taken to execute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="13218-173">Creare oggetti RDD con matrici di funzionalità per l'inserimento in modelli</span><span class="sxs-lookup"><span data-stu-id="13218-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="13218-174">Questa sezione contiene codice che illustra come indicizzare dati di testo categorici come oggetti RDD e come usare la codifica one-hot per codificarli per l'uso per il training e il testing della regressione logistica MLlib e dei modelli basati su albero.</span><span class="sxs-lookup"><span data-stu-id="13218-174">This section contains code that shows how to index categorical text data as an RDD object and one-hot encode it so it can be used to train and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="13218-175">I dati indicizzati vengono archiviati come oggetti [RDD (Resilient Distributed Dataset)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) .</span><span class="sxs-lookup"><span data-stu-id="13218-175">The indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="13218-176">Si tratta dell'astrazione di base in Spark.</span><span class="sxs-lookup"><span data-stu-id="13218-176">These are the basic abstraction in Spark.</span></span> <span data-ttu-id="13218-177">Un oggetto RDD rappresenta una raccolta partizionata non modificabile di elementi su cui è possibile operare in parallelo con Spark.</span><span class="sxs-lookup"><span data-stu-id="13218-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="13218-178">Contiene anche codice che mostra come ridimensionare i dati con `StandardScalar` , fornito da MLlib per l'uso nella regressione lineare con la discesa del gradiente stocastica (SGD), un algoritmo molto diffuso per il training di una vasta gamma di modelli di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="13218-178">It also contains code that shows how to scale data with the `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="13218-179">[StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) viene usato per ridimensionare le funzionalità alla varianza unitaria.</span><span class="sxs-lookup"><span data-stu-id="13218-179">The [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used to scale the features to unit variance.</span></span> <span data-ttu-id="13218-180">Il ridimensionamento di funzionalità, noto anche come normalizzazione dei dati, permette di fare in modo che alle funzionalità con valori molto dispersi non venga attribuito un peso eccessivo nella funzione obiettivo.</span><span class="sxs-lookup"><span data-stu-id="13218-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> 

    # CREATE RDD OBJECTS WITH FEATURE ARRAYS FOR INPUT INTO MODELS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTESTbinary = encodedFinal.map(parseRowIndexingBinary)
    oneHotTESTbinary = encodedFinal.map(parseRowOneHotBinary)

    # FOR REGRESSION CLASSIFICATION TRAINING AND TESTING
    indexedTESTreg = encodedFinal.map(parseRowIndexingRegression)
    oneHotTESTreg = encodedFinal.map(parseRowOneHotRegression)

    # SCALING FEATURES FOR LINEARREGRESSIONWITHSGD MODEL
    scaler = StandardScaler(withMean=False, withStd=True).fit(oneHotTESTreg)
    oneHotTESTregScaled = scaler.transform(oneHotTESTreg)

    # CACHE RDDS IN MEMORY
    indexedTESTbinary.cache();
    oneHotTESTbinary.cache();
    indexedTESTreg.cache();
    oneHotTESTreg.cache();
    oneHotTESTregScaled.cache();

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="13218-181">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="13218-181">**OUTPUT:**</span></span>

<span data-ttu-id="13218-182">Tempo impiegato per eseguire questa cella: 11,72 secondi.</span><span class="sxs-lookup"><span data-stu-id="13218-182">Time taken to execute above cell: 11.72 seconds</span></span>

## <a name="score-with-the-logistic-regression-model-and-save-output-to-blob"></a><span data-ttu-id="13218-183">Assegnare punteggi con il modello di regressione logistica e salvare l'output in BLOB</span><span class="sxs-lookup"><span data-stu-id="13218-183">Score with the Logistic Regression Model and save output to blob</span></span>
<span data-ttu-id="13218-184">Il codice riportato in questa sezione illustra come caricare un modello di regressione logistica che è stato salvato in un archivio BLOB di Azure e come usarlo per prevedere se viene lasciata una mancia per una corsa in taxi, assegnare un punteggio con metriche di classificazione standard e quindi salvare e tracciare i risultati nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="13218-184">The code in this section shows how to load a Logistic Regression Model that has been saved in Azure blob storage and use it to predict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot the results to blob storage.</span></span> <span data-ttu-id="13218-185">I risultati con punteggio vengono archiviati in oggetti RDD.</span><span class="sxs-lookup"><span data-stu-id="13218-185">The scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) TO BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="13218-186">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="13218-186">**OUTPUT:**</span></span>

<span data-ttu-id="13218-187">Tempo impiegato per eseguire questa cella: 19,22 secondi.</span><span class="sxs-lookup"><span data-stu-id="13218-187">Time taken to execute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="13218-188">Assegnare punteggi a un modello di regressione lineare</span><span class="sxs-lookup"><span data-stu-id="13218-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="13218-189">Per il training di un modello di regressione lineare con il metodo di discesa del gradiente stocastica (SGD) per l'ottimizzazione allo scopo di prevedere l'importo delle mance lasciate è stato usato [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD).</span><span class="sxs-lookup"><span data-stu-id="13218-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) to train a linear regression model using Stochastic Gradient Descent (SGD) for optimization to predict the amount of tip paid.</span></span> 

<span data-ttu-id="13218-190">Il codice riportato in questa sezione illustra come caricare un modello di regressione lineare dall'archivio BLOB di Azure, assegnare un punteggio con variabili ridimensionate e salvare nuovamente i risultati nel BLOB.</span><span class="sxs-lookup"><span data-stu-id="13218-190">The code in this section shows how to load a Linear Regression Model from Azure blob storage, score using scaled variables, and then save the results back to the blob.</span></span>

    #SCORE LINEAR REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #LOAD LIBRARIES
    from pyspark.mllib.regression import LinearRegressionWithSGD, LinearRegressionModel

    # LOAD MODEL AND SCORE USING ** SCALED VARIABLES **
    savedModel = LinearRegressionModel.load(sc, linearRegFileLoc)
    predictions = oneHotTESTregScaled.map(lambda features: (float(savedModel.predict(features))))

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = scoredResultDir + linearregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="13218-191">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="13218-191">**OUTPUT:**</span></span>

<span data-ttu-id="13218-192">Tempo impiegato per eseguire questa cella: 16,63 secondi.</span><span class="sxs-lookup"><span data-stu-id="13218-192">Time taken to execute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="13218-193">Assegnare punteggi a modelli di foresta casuale per la classificazione e la regressione</span><span class="sxs-lookup"><span data-stu-id="13218-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="13218-194">Il codice riportato in questa sezione illustra come caricare i modelli di foresta casuale per la classificazione e la regressione salvati nell'archivio BLOB di Azure, assegnare punteggi alle relative prestazioni con misure di classificazione e regressione standard e salvare nuovamente i risultati nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="13218-194">The code in this section shows how to load the saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save the results back to blob storage.</span></span>

<span data-ttu-id="13218-195">[foreste casuali](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="13218-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="13218-196">Queste foreste combinano diversi alberi delle decisioni per ridurre il rischio di overfitting.</span><span class="sxs-lookup"><span data-stu-id="13218-196">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="13218-197">Le foreste casuali possono gestire funzionalità categoriche, si estendono all'impostazione di classificazione multiclasse, non richiedono il ridimensionamento delle funzionalità e possono rilevare non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="13218-197">Random forests can handle categorical features, extend to the multiclass classification setting, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="13218-198">Le foreste casuali sono tra i modelli di apprendimento automatico più diffusi per la classificazione e la regressione.</span><span class="sxs-lookup"><span data-stu-id="13218-198">Random forests are one of the most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="13218-199">[spark.mllib](http://spark.apache.org/mllib/) supporta foreste casuali per la classificazione binaria e multiclasse e per la regressione, con funzionalità sia continue che categoriche.</span><span class="sxs-lookup"><span data-stu-id="13218-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="13218-200">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="13218-200">**OUTPUT:**</span></span>

<span data-ttu-id="13218-201">Tempo impiegato per eseguire questa cella: 31,07 secondi.</span><span class="sxs-lookup"><span data-stu-id="13218-201">Time taken to execute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="13218-202">Assegnare punteggi a modelli di alberi con boosting a gradienti per la classificazione e la regressione</span><span class="sxs-lookup"><span data-stu-id="13218-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="13218-203">Il codice riportato in questa sezione illustra come caricare i modelli di alberi con boosting a gradienti (GBT) per la classificazione e la regressione salvati nell'archivio BLOB di Azure, assegnare punteggi alle relative prestazioni con misure di classificazione e regressione standard e salvare nuovamente i risultati nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="13218-203">The code in this section shows how to load classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save the results back to blob storage.</span></span> 

<span data-ttu-id="13218-204">**spark.mllib** supporta gli alberi GBT per la classificazione binaria e per la regressione, con funzionalità sia continue che categoriche.</span><span class="sxs-lookup"><span data-stu-id="13218-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="13218-205">[alberi con boosting a gradienti](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="13218-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="13218-206">Gli alberi GBT eseguono il training degli alberi delle decisioni in modo iterativo per ridurre al minimo la perdita di funzioni.</span><span class="sxs-lookup"><span data-stu-id="13218-206">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="13218-207">Gli alberi GBT possono gestire funzionalità categoriche, non richiedono il ridimensionamento delle funzionalità e possono rilevare non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="13218-207">GBTs can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="13218-208">Possono anche essere usati in un'impostazione di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="13218-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB

    #LOAD AND SCORE THE MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="13218-209">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="13218-209">**OUTPUT:**</span></span>

<span data-ttu-id="13218-210">Tempo impiegato per eseguire questa cella: 14,6 secondi.</span><span class="sxs-lookup"><span data-stu-id="13218-210">Time taken to execute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="13218-211">Pulire gli oggetti dalla memoria e stampare i percorsi di file con punteggio</span><span class="sxs-lookup"><span data-stu-id="13218-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH TO SCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="13218-212">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="13218-212">**OUTPUT:**</span></span>

<span data-ttu-id="13218-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="13218-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="13218-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="13218-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="13218-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="13218-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="13218-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="13218-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="13218-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="13218-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="13218-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="13218-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="13218-219">Utilizzare i modelli Spark da un'interfaccia Web</span><span class="sxs-lookup"><span data-stu-id="13218-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="13218-220">Spark offre un meccanismo che permette di inviare in modalità remota processi batch o query interattive tramite un'interfaccia REST con un componente denominato Livy.</span><span class="sxs-lookup"><span data-stu-id="13218-220">Spark provides a mechanism to remotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="13218-221">Livy è abilitato per impostazione predefinita nel cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="13218-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="13218-222">Per altre informazioni, vedere [Inviare processi Spark in modalità remota tramite Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="13218-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="13218-223">Livy può essere usato per inviare in modalità remota un processo che assegna punteggi in batch a un file archiviato in un BLOB di Azure e quindi scrive i risultati in un altro BLOB.</span><span class="sxs-lookup"><span data-stu-id="13218-223">You can use Livy to remotely submit a job that batch scores a file that is stored in an Azure blob and then writes the results to another blob.</span></span> <span data-ttu-id="13218-224">A tale scopo, caricare lo script Python da </span><span class="sxs-lookup"><span data-stu-id="13218-224">To do this, you upload the Python script from</span></span>  
<span data-ttu-id="13218-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) nel BLOB del cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="13218-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) to the blob of the Spark cluster.</span></span> <span data-ttu-id="13218-226">Per copiare lo script nel BLOB del cluster, è possibile usare uno strumento come **Microsoft Azure Storage Explorer** o **AzCopy**.</span><span class="sxs-lookup"><span data-stu-id="13218-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** to copy the script to the cluster blob.</span></span> <span data-ttu-id="13218-227">In questo caso lo script è stato caricato in ***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="13218-227">In our case we uploaded the script to ***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="13218-228">Le chiavi di accesso necessarie sono reperibili nel portale dell'account di archiviazione associato al cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="13218-228">The access keys that you need can be found on the portal for the storage account associated with the Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="13218-229">Dopo essere stato caricato in questo percorso, lo script viene eseguito all'interno del cluster Spark in un contesto distribuito.</span><span class="sxs-lookup"><span data-stu-id="13218-229">Once uploaded to this location, this script runs within the Spark cluster in a distributed context.</span></span> <span data-ttu-id="13218-230">Lo script carica il modello ed esegue le previsioni sui file di input in base al modello.</span><span class="sxs-lookup"><span data-stu-id="13218-230">It loads the model and runs predictions on input files based on the model.</span></span>  

<span data-ttu-id="13218-231">È possibile richiamare lo script in modalità remota tramite una semplice richiesta HTTPS/REST in Livy.</span><span class="sxs-lookup"><span data-stu-id="13218-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="13218-232">Di seguito è riportato un comando curl per costruire la richiesta HTTP per richiamare lo script Python in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="13218-232">Here is a curl command to construct the HTTP request to invoke the Python script remotely.</span></span> <span data-ttu-id="13218-233">Sostituire CLUSTERLOGIN, CLUSTERPASSWORD e CLUSTERNAME con i valori appropriati per il cluster Spark usato.</span><span class="sxs-lookup"><span data-stu-id="13218-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with the appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND TO INVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="13218-234">Con una semplice chiamata HTTPS con autenticazione di base è possibile usare qualsiasi linguaggio nel sistema remoto per richiamare il processo Spark tramite Livy.</span><span class="sxs-lookup"><span data-stu-id="13218-234">You can use any language on the remote system to invoke the Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="13218-235">Potrebbe essere preferibile usare la libreria di richieste Python quando si esegue la chiamata HTTP, ma attualmente non è installata per impostazione predefinita in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="13218-235">It would be convenient to use the Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="13218-236">Vengono quindi usate altre librerie HTTP.</span><span class="sxs-lookup"><span data-stu-id="13218-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="13218-237">Di seguito è riportato il codice Python per la chiamata HTTP:</span><span class="sxs-lookup"><span data-stu-id="13218-237">Here is the Python code for the HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF THE REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY THE PYTHON SCRIPT TO RUN ON THE SPARK CLUSTER
    # IN THE FILE PARAMETER OF THE JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="13218-238">È anche possibile aggiungere questo codice Python a [Funzioni di Azure](https://azure.microsoft.com/documentation/services/functions/) per attivare l'invio di un processo Spark che assegna punteggi a un BLOB in base a vari eventi, ad esempio un timer, la creazione o l'aggiornamento di un BLOB.</span><span class="sxs-lookup"><span data-stu-id="13218-238">You can also add this Python code to [Azure Functions](https://azure.microsoft.com/documentation/services/functions/) to trigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="13218-239">Se si preferisce non ricorrere al codice, usare [App per la logica di Azure](https://azure.microsoft.com/documentation/services/app-service/logic/) per richiamare l'assegnazione di punteggi batch di Spark definendo un'azione HTTP in **Progettazione app per la logica** e impostando i parametri.</span><span class="sxs-lookup"><span data-stu-id="13218-239">If you prefer a code free client experience, use the [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) to invoke the Spark batch scoring by defining an HTTP action on the **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="13218-240">Nel portale di Azure creare una nuova app per la logica selezionando **+Nuovo** -> **Web e dispositivi mobili** -> **App per la logica**.</span><span class="sxs-lookup"><span data-stu-id="13218-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="13218-241">Per visualizzare **Progettazione app per la logica**, immettere il nome dell'app per la logica e il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="13218-241">To bring up the **Logic Apps Designer**, enter the name of the Logic App and App Service Plan.</span></span>
* <span data-ttu-id="13218-242">Selezionare un'azione HTTP e immettere i parametri mostrati nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="13218-242">Select an HTTP action and enter the parameters shown in the following figure:</span></span>

![Progettazione app per la logica](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="13218-244">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13218-244">What's next?</span></span>
<span data-ttu-id="13218-245">**Convalida incrociata e sweep di iperparametri**: vedere [Esplorazione e modellazione avanzate dei dati con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) per informazioni su come istruire i modelli sulla convalida incrociata e lo sweep di iperparametri.</span><span class="sxs-lookup"><span data-stu-id="13218-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

