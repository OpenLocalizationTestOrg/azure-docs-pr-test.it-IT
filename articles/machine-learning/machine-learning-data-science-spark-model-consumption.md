---
title: aaaOperationalize compilato Spark modelli di machine learning | Documenti Microsoft
description: Come tooload e modelli di apprendimento punteggio archiviati in Azure Blob Storage (WASB) con Python.
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
ms.openlocfilehash: c5fadcb13257b94dcb28a522be454f6e03dfa991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="b68ee-103">Rendere operativi i modelli di apprendimento automatico compilati con Spark</span><span class="sxs-lookup"><span data-stu-id="b68ee-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="b68ee-104">Questo argomento viene illustrato come toooperationalize un modello di apprendimento macchina salvata (ML) usando Python in HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="b68ee-104">This topic shows how toooperationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="b68ee-105">Viene descritto come tooload machine learning i modelli che sono stati compilati utilizzando MLlib Spark e archiviati in archiviazione Blob di Azure (WASB) e come tooscore con set di dati che sono anche stati archiviati in WASB.</span><span class="sxs-lookup"><span data-stu-id="b68ee-105">It describes how tooload machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how tooscore them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="b68ee-106">Mostra dati di input hello come toopre-process, utilizzando le funzionalità di trasformazione hello funzioni di indicizzazione e la codifica in hello MLlib toolkit, e come toocreate un oggetto di etichetta punto dati che può essere utilizzato come input per il punteggio con i modelli di hello ML.</span><span class="sxs-lookup"><span data-stu-id="b68ee-106">It shows how toopre-process hello input data, transform features using hello indexing and encoding functions in hello MLlib toolkit, and how toocreate a labeled point data object that can be used as input for scoring with hello ML models.</span></span> <span data-ttu-id="b68ee-107">modelli di Hello utilizzati per il punteggio includono Linear Regression, Logistic Regression, modelli di foreste casuali e sfumatura Boosting i modelli di albero.</span><span class="sxs-lookup"><span data-stu-id="b68ee-107">hello models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="b68ee-108">Cluster Spark e notebook di Jupyter</span><span class="sxs-lookup"><span data-stu-id="b68ee-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="b68ee-109">Passaggi di installazione e toooperationalize codice hello un modello di Machine Learning disponibili in questa procedura dettagliata per l'utilizzo di un cluster HDInsight Spark 1.6, nonché un cluster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="b68ee-109">Setup steps and hello code toooperationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="b68ee-110">codice di Hello per queste procedure viene fornito anche nel server Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="b68ee-110">hello code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="b68ee-111">Notebook per Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="b68ee-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="b68ee-112">Hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) server Jupyter notebook viene illustrato come toooperationalize un modello salvato usando Python in HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b68ee-112">hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how toooperationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="b68ee-113">Notebook per Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="b68ee-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="b68ee-114">toomodify hello Jupyter notebook toouse 1.6 Spark con un cluster HDInsight Spark 2.0, sostituire i file di codice Python hello con [questo file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="b68ee-114">toomodify hello Jupyter notebook for Spark 1.6 toouse with an HDInsight Spark 2.0 cluster, replace hello Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="b68ee-115">Questo codice viene illustrato come i modelli di hello tooconsume creati in Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="b68ee-115">This code shows how tooconsume hello models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b68ee-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b68ee-116">Prerequisites</span></span>

1. <span data-ttu-id="b68ee-117">È necessario un account Azure e Spark 1.6 (o 2.0 Spark) toocomplete cluster HDInsight in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="b68ee-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="b68ee-118">Vedere hello [panoramica dell'analisi scientifica dei dati utilizzando Spark in Azure HDInsight](machine-learning-data-science-spark-overview.md) per istruzioni su come toosatisfy questi requisiti.</span><span class="sxs-lookup"><span data-stu-id="b68ee-118">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="b68ee-119">Questo argomento contiene inoltre una descrizione di hello dati NYC 2013 Taxi utilizzati in questo argomento e per istruzioni su come il codice da un server Jupyter notebook nel cluster Spark hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="b68ee-119">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 
2. <span data-ttu-id="b68ee-120">È inoltre necessario creare hello modelli di machine learning toobe con punteggio qui l'esecuzione di hello [l'esplorazione dei dati e modellazione con Spark](machine-learning-data-science-spark-data-exploration-modeling.md) l'argomento relativo a cluster Spark 1.6 hello o un notebook hello Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="b68ee-120">You must also create hello machine learning models toobe scored here by working through hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for hello Spark 1.6 cluster or hello Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="b68ee-121">notebook Hello Spark 2.0 utilizzare un set di dati aggiuntivo per attività di classificazione hello, hello noto Airline in orario partenza set di dati da 2011 e 2012.</span><span class="sxs-lookup"><span data-stu-id="b68ee-121">hello Spark 2.0 notebooks use an additional data set for hello classification task, hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="b68ee-122">Vengono forniti una descrizione di hello blocchi appunti e collegamenti toothem in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) per il repository di GitHub hello che li contengono.</span><span class="sxs-lookup"><span data-stu-id="b68ee-122">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="b68ee-123">Inoltre, codice hello qui e i notebook hello collegato è generico e dovrebbe funzionare in un cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="b68ee-123">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="b68ee-124">Se non si utilizza HDInsight Spark, passaggi di configurazione e gestione di cluster hello potrebbero essere leggermente diversi rispetto a quanto mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b68ee-124">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="b68ee-125">Il programma di installazione: hello, librerie e percorsi di archiviazione predefinito contesto Spark</span><span class="sxs-lookup"><span data-stu-id="b68ee-125">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="b68ee-126">Spark è in grado di tooan tooread e di scrittura Blob di archiviazione di Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="b68ee-126">Spark is able tooread and write tooan Azure Storage Blob (WASB).</span></span> <span data-ttu-id="b68ee-127">Pertanto, i dati esistenti archiviate possono essere elaborati utilizzando Spark e hello risultati WASB archiviato nuovamente in.</span><span class="sxs-lookup"><span data-stu-id="b68ee-127">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="b68ee-128">modelli toosave o file in WASB, percorso hello deve toobe specificato correttamente.</span><span class="sxs-lookup"><span data-stu-id="b68ee-128">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="b68ee-129">Hello del cluster Spark toohello contenitore collegato predefinito possibile farvi riferimento tramite un che inizia con: *"wasb / /"*.</span><span class="sxs-lookup"><span data-stu-id="b68ee-129">hello default container attached toohello Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="b68ee-130">esempio di codice seguente Hello Specifica percorso hello di hello dati toobe leggere e hello percorso per l'output di hello modello archiviazione directory toowhich hello modello viene salvato.</span><span class="sxs-lookup"><span data-stu-id="b68ee-130">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="b68ee-131">Impostare percorsi di directory per i percorsi di archiviazione in WASB</span><span class="sxs-lookup"><span data-stu-id="b68ee-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="b68ee-132">I modelli vengono salvati in: "wasb:///user/remoteuser/NYCTaxi/Models".</span><span class="sxs-lookup"><span data-stu-id="b68ee-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="b68ee-133">Se questo percorso non è impostato correttamente, i modelli non vengono caricati per l'assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="b68ee-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="b68ee-134">Hello risultati con punteggi sono stati salvati: "wasb: / / / utente/remoteuser/NYCTaxi/ScoredResults".</span><span class="sxs-lookup"><span data-stu-id="b68ee-134">hello scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="b68ee-135">Se toofolder percorso hello è errata, i risultati non vengono salvati in tale cartella.</span><span class="sxs-lookup"><span data-stu-id="b68ee-135">If hello path toofolder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="b68ee-136">percorsi di file Hello possono essere copiati e incollati in segnaposto hello in questo codice dall'output di hello dell'ultima cella di hello di hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span><span class="sxs-lookup"><span data-stu-id="b68ee-136">hello file path locations can be copied and pasted into hello placeholders in this code from hello output of hello last cell of hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="b68ee-137">Ecco i percorsi di directory tooset codice hello:</span><span class="sxs-lookup"><span data-stu-id="b68ee-137">Here is hello code tooset directory paths:</span></span> 

    # LOCATION OF DATA tooBE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR hello MODELS tooBE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="b68ee-138">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b68ee-138">**OUTPUT:**</span></span>

<span data-ttu-id="b68ee-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="b68ee-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="b68ee-140">Importare le librerie</span><span class="sxs-lookup"><span data-stu-id="b68ee-140">Import libraries</span></span>
<span data-ttu-id="b68ee-141">Impostare il contesto di spark e importare le librerie necessarie con hello seguente di codice</span><span class="sxs-lookup"><span data-stu-id="b68ee-141">Set spark context and import necessary libraries with hello following code</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="b68ee-142">Contesto di Spark preimpostato e magic di PySpark</span><span class="sxs-lookup"><span data-stu-id="b68ee-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="b68ee-143">kernel PySpark Hello forniti con i notebook Jupyter dispone di un contesto predefinito.</span><span class="sxs-lookup"><span data-stu-id="b68ee-143">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="b68ee-144">Pertanto, non è necessario contesti di Spark o Hive hello tooset in modo esplicito prima di iniziare con un'applicazione hello che si sta sviluppando.</span><span class="sxs-lookup"><span data-stu-id="b68ee-144">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="b68ee-145">I contesti sono disponibili per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b68ee-145">These are available for you by default.</span></span> <span data-ttu-id="b68ee-146">Questi contesti sono:</span><span class="sxs-lookup"><span data-stu-id="b68ee-146">These contexts are:</span></span>

* <span data-ttu-id="b68ee-147">sc per Spark</span><span class="sxs-lookup"><span data-stu-id="b68ee-147">sc - for Spark</span></span> 
* <span data-ttu-id="b68ee-148">sqlContext per Hive</span><span class="sxs-lookup"><span data-stu-id="b68ee-148">sqlContext - for Hive</span></span>

<span data-ttu-id="b68ee-149">Hello kernel PySpark fornisce alcuni predefinite "magics", che sono comandi speciale che è possibile chiamare con % %.</span><span class="sxs-lookup"><span data-stu-id="b68ee-149">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="b68ee-150">Negli esempi di codice seguenti sono usati due comandi di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="b68ee-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="b68ee-151">**% % locale** specificato che il codice hello nelle righe successive viene eseguito localmente.</span><span class="sxs-lookup"><span data-stu-id="b68ee-151">**%%local** Specified that hello code in subsequent lines is executed locally.</span></span> <span data-ttu-id="b68ee-152">Deve trattarsi di codice Python valido.</span><span class="sxs-lookup"><span data-stu-id="b68ee-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="b68ee-153">**%%sql -o <variable name>**</span><span class="sxs-lookup"><span data-stu-id="b68ee-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="b68ee-154">Esegue una query Hive sqlContext hello.</span><span class="sxs-lookup"><span data-stu-id="b68ee-154">Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="b68ee-155">Se viene passato il parametro -o hello, il risultato di hello di hello query è persistente nel hello % % contesto Python locale come un frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="b68ee-155">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="b68ee-156">Per ulteriori informazioni su kernel hello per notebook Jupyter e hello predefiniti "magics" che forniscono, vedere [cluster kernel disponibile per i server Jupyter notebook con Linux di HDInsight Spark in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="b68ee-156">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="b68ee-157">Inserire i dati e creare un frame di dati pulito</span><span class="sxs-lookup"><span data-stu-id="b68ee-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="b68ee-158">In questa sezione contiene codice hello per una serie di attività richiesto tooingest hello dati toobe con punteggio.</span><span class="sxs-lookup"><span data-stu-id="b68ee-158">This section contains hello code for a series of tasks required tooingest hello data toobe scored.</span></span> <span data-ttu-id="b68ee-159">Lettura in un campione di 0,1% unita in join di hello taxi di andata e ritorno e tariffa file (archiviati come file tsv), dati in formato hello e quindi crea un frame di dati pulito.</span><span class="sxs-lookup"><span data-stu-id="b68ee-159">Read in a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file), format hello data, and then creates a clean data frame.</span></span>

<span data-ttu-id="b68ee-160">Hello taxi di andata e ritorno e tariffa i file sono stati aggiunti in base hello procedura il: [hello Team processo di analisi scientifica dei dati in azione: utilizzo dei cluster HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="b68ee-160">hello taxi trip and fare files were joined based on hello procedure provided in the: [hello Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF hello FILE FROM HEADER
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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b68ee-161">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b68ee-161">**OUTPUT:**</span></span>

<span data-ttu-id="b68ee-162">Tempo impiegato tooexecute di sopra di: 46.37 secondi</span><span class="sxs-lookup"><span data-stu-id="b68ee-162">Time taken tooexecute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="b68ee-163">Preparare i dati per l'assegnazione dei punteggi in Spark</span><span class="sxs-lookup"><span data-stu-id="b68ee-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="b68ee-164">In questa sezione viene illustrato come tooindex, codificare e scalare tooprepare organizzato per categorie di funzionalità per l'utilizzo in algoritmi di apprendimento supervisionato MLlib per la classificazione e regressione.</span><span class="sxs-lookup"><span data-stu-id="b68ee-164">This section shows how tooindex, encode, and scale categorical features tooprepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="b68ee-165">Trasformazione di funzionalità: indicizzare e codificare funzionalità categoriche per l'inserimento in modelli per l'assegnazione dei punteggi</span><span class="sxs-lookup"><span data-stu-id="b68ee-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="b68ee-166">Questa sezione viene illustrato come tooindex dati categorici utilizzando un `StringIndexer` e codificare funzionalità con `OneHotEncoder` di input in modelli hello.</span><span class="sxs-lookup"><span data-stu-id="b68ee-166">This section shows how tooindex categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into hello models.</span></span>

<span data-ttu-id="b68ee-167">Hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) codifica di una colonna stringa della colonna di etichette tooa di indici di etichetta.</span><span class="sxs-lookup"><span data-stu-id="b68ee-167">hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels tooa column of label indices.</span></span> <span data-ttu-id="b68ee-168">gli indici di Hello sono ordinati per le frequenze di etichetta.</span><span class="sxs-lookup"><span data-stu-id="b68ee-168">hello indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="b68ee-169">Hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) esegue il mapping di una colonna della colonna di etichetta indici tooa di vettori binari, con al massimo uno a valore singolo.</span><span class="sxs-lookup"><span data-stu-id="b68ee-169">hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="b68ee-170">Questa codifica consente di utilizzare gli algoritmi che prevede funzionalità con valori continui, come la regressione logistica, funzionalità toocategorical toobe applicato.</span><span class="sxs-lookup"><span data-stu-id="b68ee-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

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
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is hello cleaned one from above
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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b68ee-171">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b68ee-171">**OUTPUT:**</span></span>

<span data-ttu-id="b68ee-172">Tempo impiegato tooexecute di sopra di: 5,37 secondi</span><span class="sxs-lookup"><span data-stu-id="b68ee-172">Time taken tooexecute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="b68ee-173">Creare oggetti RDD con matrici di funzionalità per l'inserimento in modelli</span><span class="sxs-lookup"><span data-stu-id="b68ee-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="b68ee-174">In questa sezione contiene codice che illustra come dati di testo categorico tooindex come un RDD dell'oggetto e a caldo uno codificare in modo da poterli usate tootrain test MLlib la regressione logistica ed e i modelli basati sulla struttura ad albero.</span><span class="sxs-lookup"><span data-stu-id="b68ee-174">This section contains code that shows how tooindex categorical text data as an RDD object and one-hot encode it so it can be used tootrain and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="b68ee-175">Hello indicizzate vengono memorizzati in [resilienti Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) oggetti.</span><span class="sxs-lookup"><span data-stu-id="b68ee-175">hello indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="b68ee-176">Si tratta di astrazione di base hello in Spark.</span><span class="sxs-lookup"><span data-stu-id="b68ee-176">These are hello basic abstraction in Spark.</span></span> <span data-ttu-id="b68ee-177">Un oggetto RDD rappresenta una raccolta partizionata non modificabile di elementi su cui è possibile operare in parallelo con Spark.</span><span class="sxs-lookup"><span data-stu-id="b68ee-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="b68ee-178">Contiene anche il codice che illustra come dati tooscale con hello `StandardScalar` forniti da MLlib per la regressione lineare con stocastico sfumatura Descent (SGD), un algoritmo comune per il training di una vasta gamma di modelli di machine learning.</span><span class="sxs-lookup"><span data-stu-id="b68ee-178">It also contains code that shows how tooscale data with hello `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="b68ee-179">Hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) è usato tooscale hello funzionalità toounit varianza.</span><span class="sxs-lookup"><span data-stu-id="b68ee-179">hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used tooscale hello features toounit variance.</span></span> <span data-ttu-id="b68ee-180">Funzionalità di scalabilità, noto anche come normalizzazione dei dati, si assicura che le funzionalità con ampiamente i valori sono non specificato un numero eccessivo pesare nella funzione obiettivo hello.</span><span class="sxs-lookup"><span data-stu-id="b68ee-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> 

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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b68ee-181">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b68ee-181">**OUTPUT:**</span></span>

<span data-ttu-id="b68ee-182">Tempo impiegato tooexecute di sopra di: 11.72 secondi</span><span class="sxs-lookup"><span data-stu-id="b68ee-182">Time taken tooexecute above cell: 11.72 seconds</span></span>

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a><span data-ttu-id="b68ee-183">Assegnare un punteggio con modello di regressione logistica hello e salvare l'output tooblob</span><span class="sxs-lookup"><span data-stu-id="b68ee-183">Score with hello Logistic Regression Model and save output tooblob</span></span>
<span data-ttu-id="b68ee-184">codice di Hello in questa sezione viene illustrato come tooload un modello di regressione logistica che è stata salvata in Azure nell'archiviazione blob e utilizzarlo o meno un suggerimento è pagato toopredict in viaggio taxi, assegnare un punteggio, con le metriche di classificazione standard e quindi salvare e tracciare hello risultati tooblob spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b68ee-184">hello code in this section shows how tooload a Logistic Regression Model that has been saved in Azure blob storage and use it toopredict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot hello results tooblob storage.</span></span> <span data-ttu-id="b68ee-185">risultati con punteggio Hello vengono archiviati negli oggetti RDD.</span><span class="sxs-lookup"><span data-stu-id="b68ee-185">hello scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) tooBLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="b68ee-186">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b68ee-186">**OUTPUT:**</span></span>

<span data-ttu-id="b68ee-187">Tempo impiegato tooexecute di sopra di: 19.22 secondi</span><span class="sxs-lookup"><span data-stu-id="b68ee-187">Time taken tooexecute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="b68ee-188">Assegnare punteggi a un modello di regressione lineare</span><span class="sxs-lookup"><span data-stu-id="b68ee-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="b68ee-189">È stato usato [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) a pagamento di un modello di regressione lineare usando valori descent con sfumatura Stocastica (SGD, Virtual Private Network) per quantità di hello toopredict ottimizzazione del suggerimento tootrain.</span><span class="sxs-lookup"><span data-stu-id="b68ee-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain a linear regression model using Stochastic Gradient Descent (SGD) for optimization toopredict hello amount of tip paid.</span></span> 

<span data-ttu-id="b68ee-190">codice di Hello in questa sezione viene illustrato come tooload un modello di regressione lineare dall'archiviazione blob di Azure, assegna un punteggio con variabili scalate e quindi salvare blob di back-toohello risultati hello.</span><span class="sxs-lookup"><span data-stu-id="b68ee-190">hello code in this section shows how tooload a Linear Regression Model from Azure blob storage, score using scaled variables, and then save hello results back toohello blob.</span></span>

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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="b68ee-191">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b68ee-191">**OUTPUT:**</span></span>

<span data-ttu-id="b68ee-192">Tempo impiegato tooexecute di sopra di: 16.63 secondi</span><span class="sxs-lookup"><span data-stu-id="b68ee-192">Time taken tooexecute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="b68ee-193">Assegnare punteggi a modelli di foresta casuale per la classificazione e la regressione</span><span class="sxs-lookup"><span data-stu-id="b68ee-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="b68ee-194">codice Hello in questa sezione viene illustrato come hello tooload salvate classificazione e regressione i modelli di foresta casuale salvata nell'archiviazione blob di Azure, assegnare un punteggio delle relative prestazioni con classificazione standard e le misure di regressione e quindi salvare hello risultati tooblob indietro archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b68ee-194">hello code in this section shows how tooload hello saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span>

<span data-ttu-id="b68ee-195">[foreste casuali](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="b68ee-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="b68ee-196">Combinano molti decision trees tooreduce hello rischio di overfitting.</span><span class="sxs-lookup"><span data-stu-id="b68ee-196">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="b68ee-197">Foreste casuali possono gestire funzioni categoriche, estendere l'impostazione di classificazione multiclasse toohello, non richiedono la funzionalità di scalabilità e sono in grado di toocapture non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b68ee-197">Random forests can handle categorical features, extend toohello multiclass classification setting, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="b68ee-198">Foreste casuali sono uno dei hello riuscito più modelli di machine learning per la classificazione e regressione.</span><span class="sxs-lookup"><span data-stu-id="b68ee-198">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="b68ee-199">[spark.mllib](http://spark.apache.org/mllib/) supporta foreste casuali per la classificazione binaria e multiclasse e per la regressione, con funzionalità sia continue che categoriche.</span><span class="sxs-lookup"><span data-stu-id="b68ee-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="b68ee-200">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b68ee-200">**OUTPUT:**</span></span>

<span data-ttu-id="b68ee-201">Tempo impiegato tooexecute di sopra di: 31.07 secondi</span><span class="sxs-lookup"><span data-stu-id="b68ee-201">Time taken tooexecute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="b68ee-202">Assegnare punteggi a modelli di alberi con boosting a gradienti per la classificazione e la regressione</span><span class="sxs-lookup"><span data-stu-id="b68ee-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="b68ee-203">codice di Hello in questa sezione viene illustrato come classificazione tooload sfumatura Boosting i modelli di albero di regressione dall'archiviazione blob di Azure, assegnare un punteggio delle relative prestazioni con classificazione standard e le misure di regressione e quindi salvare hello risultati tooblob indietro archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b68ee-203">hello code in this section shows how tooload classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span> 

<span data-ttu-id="b68ee-204">**spark.mllib** supporta gli alberi GBT per la classificazione binaria e per la regressione, con funzionalità sia continue che categoriche.</span><span class="sxs-lookup"><span data-stu-id="b68ee-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="b68ee-205">[alberi con boosting a gradienti](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="b68ee-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="b68ee-206">GBTs train alberi delle decisioni in modo iterativo toominimize una funzione di perdita.</span><span class="sxs-lookup"><span data-stu-id="b68ee-206">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="b68ee-207">GBTs può gestire funzioni categoriche, non richiedono la funzionalità di scalabilità e sono in grado di toocapture non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b68ee-207">GBTs can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="b68ee-208">Possono anche essere usati in un'impostazione di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="b68ee-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    #LOAD AND SCORE hello MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b68ee-209">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b68ee-209">**OUTPUT:**</span></span>

<span data-ttu-id="b68ee-210">Tempo impiegato tooexecute di sopra di: 14.6 secondi</span><span class="sxs-lookup"><span data-stu-id="b68ee-210">Time taken tooexecute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="b68ee-211">Pulire gli oggetti dalla memoria e stampare i percorsi di file con punteggio</span><span class="sxs-lookup"><span data-stu-id="b68ee-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH tooSCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="b68ee-212">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b68ee-212">**OUTPUT:**</span></span>

<span data-ttu-id="b68ee-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="b68ee-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="b68ee-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="b68ee-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="b68ee-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="b68ee-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="b68ee-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="b68ee-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="b68ee-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="b68ee-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="b68ee-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="b68ee-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="b68ee-219">Utilizzare i modelli Spark da un'interfaccia Web</span><span class="sxs-lookup"><span data-stu-id="b68ee-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="b68ee-220">Spark fornisce un meccanismo tooremotely invia i processi batch o query interattive attraverso un resto interfacciarsi con un componente chiamato inserire il.</span><span class="sxs-lookup"><span data-stu-id="b68ee-220">Spark provides a mechanism tooremotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="b68ee-221">Livy è abilitato per impostazione predefinita nel cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="b68ee-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="b68ee-222">Per altre informazioni, vedere [Inviare processi Spark in modalità remota tramite Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="b68ee-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="b68ee-223">È possibile utilizzare inserire il tooremotely invia un processo batch punteggi di un file che viene archiviato in un blob di Azure e quindi scrive blob tooanother di hello risultati.</span><span class="sxs-lookup"><span data-stu-id="b68ee-223">You can use Livy tooremotely submit a job that batch scores a file that is stored in an Azure blob and then writes hello results tooanother blob.</span></span> <span data-ttu-id="b68ee-224">toodo, script Python hello da caricare</span><span class="sxs-lookup"><span data-stu-id="b68ee-224">toodo this, you upload hello Python script from</span></span>  
<span data-ttu-id="b68ee-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob del cluster Spark hello.</span><span class="sxs-lookup"><span data-stu-id="b68ee-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob of hello Spark cluster.</span></span> <span data-ttu-id="b68ee-226">È possibile utilizzare uno strumento come **Microsoft Azure Storage Explorer** o **AzCopy** blob cluster toohello di toocopy hello script.</span><span class="sxs-lookup"><span data-stu-id="b68ee-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** toocopy hello script toohello cluster blob.</span></span> <span data-ttu-id="b68ee-227">In questo caso è stato caricato script hello troppo***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="b68ee-227">In our case we uploaded hello script too***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="b68ee-228">Hello chiavi di accesso che è necessario è reperibile nel portale di hello hello account di archiviazione associato al cluster Spark hello.</span><span class="sxs-lookup"><span data-stu-id="b68ee-228">hello access keys that you need can be found on hello portal for hello storage account associated with hello Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="b68ee-229">Una volta caricato il percorso toothis, questo script viene eseguito all'interno di cluster Spark hello in un contesto distribuito.</span><span class="sxs-lookup"><span data-stu-id="b68ee-229">Once uploaded toothis location, this script runs within hello Spark cluster in a distributed context.</span></span> <span data-ttu-id="b68ee-230">Carica il modello di hello ed esegue stime sui file di input basati sul modello hello.</span><span class="sxs-lookup"><span data-stu-id="b68ee-230">It loads hello model and runs predictions on input files based on hello model.</span></span>  

<span data-ttu-id="b68ee-231">È possibile richiamare lo script in modalità remota tramite una semplice richiesta HTTPS/REST in Livy.</span><span class="sxs-lookup"><span data-stu-id="b68ee-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="b68ee-232">Ecco un curl comando tooconstruct hello HTTP richiesta tooinvoke hello script Python in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="b68ee-232">Here is a curl command tooconstruct hello HTTP request tooinvoke hello Python script remotely.</span></span> <span data-ttu-id="b68ee-233">Sostituire CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME con i valori appropriati di hello per il cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="b68ee-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with hello appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="b68ee-234">È possibile utilizzare qualsiasi linguaggio per il processo hello sistema remoto tooinvoke hello Spark tramite inserire il mediante una semplice chiamata HTTPS con l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="b68ee-234">You can use any language on hello remote system tooinvoke hello Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="b68ee-235">Sarebbe libreria Python richieste di hello toouse pratico quando si effettua questa chiamata HTTP, ma non è attualmente installato per impostazione predefinita nelle funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b68ee-235">It would be convenient toouse hello Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="b68ee-236">Vengono quindi usate altre librerie HTTP.</span><span class="sxs-lookup"><span data-stu-id="b68ee-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="b68ee-237">Di seguito è riportato il codice Python hello per chiamata hello HTTP:</span><span class="sxs-lookup"><span data-stu-id="b68ee-237">Here is hello Python code for hello HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF hello REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY hello PYTHON SCRIPT tooRUN ON hello SPARK CLUSTER
    # IN hello FILE PARAMETER OF hello JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="b68ee-238">È inoltre possibile aggiungere questo codice Python troppo[Azure funzioni](https://azure.microsoft.com/documentation/services/functions/) tootrigger un invio di processi di Spark che assegna un punteggio a un blob in base a diversi eventi timer, creazione o aggiornamento di un blob.</span><span class="sxs-lookup"><span data-stu-id="b68ee-238">You can also add this Python code too[Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="b68ee-239">Se si preferisce un'esperienza client disponibile codice, utilizzare hello [Azure logica app](https://azure.microsoft.com/documentation/services/app-service/logic/) batch di Spark hello tooinvoke punteggio definendo un'azione HTTP su hello **logica App progettazione** e impostando i relativi parametri.</span><span class="sxs-lookup"><span data-stu-id="b68ee-239">If you prefer a code free client experience, use hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark batch scoring by defining an HTTP action on hello **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="b68ee-240">Nel portale di Azure creare una nuova app per la logica selezionando **+Nuovo** -> **Web e dispositivi mobili** -> **App per la logica**.</span><span class="sxs-lookup"><span data-stu-id="b68ee-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="b68ee-241">toobring backup hello **logica App progettazione**, immettere il nome di hello dell'App per la logica di hello e piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="b68ee-241">toobring up hello **Logic Apps Designer**, enter hello name of hello Logic App and App Service Plan.</span></span>
* <span data-ttu-id="b68ee-242">Selezionare un'azione HTTP e immettere i parametri di hello mostrati nella seguente illustrazione hello:</span><span class="sxs-lookup"><span data-stu-id="b68ee-242">Select an HTTP action and enter hello parameters shown in hello following figure:</span></span>

![Progettazione app per la logica](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="b68ee-244">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b68ee-244">What's next?</span></span>
<span data-ttu-id="b68ee-245">**Convalida incrociata e sweep di iperparametri**: vedere [Esplorazione e modellazione avanzate dei dati con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) per informazioni su come istruire i modelli sulla convalida incrociata e lo sweep di iperparametri.</span><span class="sxs-lookup"><span data-stu-id="b68ee-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

