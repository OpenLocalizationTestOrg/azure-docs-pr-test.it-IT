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
# <a name="operationalize-spark-built-machine-learning-models"></a>Rendere operativi i modelli di apprendimento automatico compilati con Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Questo argomento viene illustrato come toooperationalize un modello di apprendimento macchina salvata (ML) usando Python in HDInsight Spark cluster. Viene descritto come tooload machine learning i modelli che sono stati compilati utilizzando MLlib Spark e archiviati in archiviazione Blob di Azure (WASB) e come tooscore con set di dati che sono anche stati archiviati in WASB. Mostra dati di input hello come toopre-process, utilizzando le funzionalità di trasformazione hello funzioni di indicizzazione e la codifica in hello MLlib toolkit, e come toocreate un oggetto di etichetta punto dati che può essere utilizzato come input per il punteggio con i modelli di hello ML. modelli di Hello utilizzati per il punteggio includono Linear Regression, Logistic Regression, modelli di foreste casuali e sfumatura Boosting i modelli di albero.

## <a name="spark-clusters-and-jupyter-notebooks"></a>Cluster Spark e notebook di Jupyter
Passaggi di installazione e toooperationalize codice hello un modello di Machine Learning disponibili in questa procedura dettagliata per l'utilizzo di un cluster HDInsight Spark 1.6, nonché un cluster Spark 2.0. codice di Hello per queste procedure viene fornito anche nel server Jupyter notebook.

### <a name="notebook-for-spark-16"></a>Notebook per Spark 1.6
Hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) server Jupyter notebook viene illustrato come toooperationalize un modello salvato usando Python in HDInsight cluster. 

### <a name="notebook-for-spark-20"></a>Notebook per Spark 2.0
toomodify hello Jupyter notebook toouse 1.6 Spark con un cluster HDInsight Spark 2.0, sostituire i file di codice Python hello con [questo file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py). Questo codice viene illustrato come i modelli di hello tooconsume creati in Spark 2.0.


## <a name="prerequisites"></a>Prerequisiti

1. È necessario un account Azure e Spark 1.6 (o 2.0 Spark) toocomplete cluster HDInsight in questa procedura dettagliata. Vedere hello [panoramica dell'analisi scientifica dei dati utilizzando Spark in Azure HDInsight](machine-learning-data-science-spark-overview.md) per istruzioni su come toosatisfy questi requisiti. Questo argomento contiene inoltre una descrizione di hello dati NYC 2013 Taxi utilizzati in questo argomento e per istruzioni su come il codice da un server Jupyter notebook nel cluster Spark hello tooexecute. 
2. È inoltre necessario creare hello modelli di machine learning toobe con punteggio qui l'esecuzione di hello [l'esplorazione dei dati e modellazione con Spark](machine-learning-data-science-spark-data-exploration-modeling.md) l'argomento relativo a cluster Spark 1.6 hello o un notebook hello Spark 2.0. 
3. notebook Hello Spark 2.0 utilizzare un set di dati aggiuntivo per attività di classificazione hello, hello noto Airline in orario partenza set di dati da 2011 e 2012. Vengono forniti una descrizione di hello blocchi appunti e collegamenti toothem in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) per il repository di GitHub hello che li contengono. Inoltre, codice hello qui e i notebook hello collegato è generico e dovrebbe funzionare in un cluster Spark. Se non si utilizza HDInsight Spark, passaggi di configurazione e gestione di cluster hello potrebbero essere leggermente diversi rispetto a quanto mostrato di seguito. 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Il programma di installazione: hello, librerie e percorsi di archiviazione predefinito contesto Spark
Spark è in grado di tooan tooread e di scrittura Blob di archiviazione di Azure (WASB). Pertanto, i dati esistenti archiviate possono essere elaborati utilizzando Spark e hello risultati WASB archiviato nuovamente in.

modelli toosave o file in WASB, percorso hello deve toobe specificato correttamente. Hello del cluster Spark toohello contenitore collegato predefinito possibile farvi riferimento tramite un che inizia con: *"wasb / /"*. esempio di codice seguente Hello Specifica percorso hello di hello dati toobe leggere e hello percorso per l'output di hello modello archiviazione directory toowhich hello modello viene salvato. 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Impostare percorsi di directory per i percorsi di archiviazione in WASB
I modelli vengono salvati in: "wasb:///user/remoteuser/NYCTaxi/Models". Se questo percorso non è impostato correttamente, i modelli non vengono caricati per l'assegnazione dei punteggi.

Hello risultati con punteggi sono stati salvati: "wasb: / / / utente/remoteuser/NYCTaxi/ScoredResults". Se toofolder percorso hello è errata, i risultati non vengono salvati in tale cartella.   

> [!NOTE]
> percorsi di file Hello possono essere copiati e incollati in segnaposto hello in questo codice dall'output di hello dell'ultima cella di hello di hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.   
> 
> 

Ecco i percorsi di directory tooset codice hello: 

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

**OUTPUT:**

datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)

### <a name="import-libraries"></a>Importare le librerie
Impostare il contesto di spark e importare le librerie necessarie con hello seguente di codice

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


### <a name="preset-spark-context-and-pyspark-magics"></a>Contesto di Spark preimpostato e magic di PySpark
kernel PySpark Hello forniti con i notebook Jupyter dispone di un contesto predefinito. Pertanto, non è necessario contesti di Spark o Hive hello tooset in modo esplicito prima di iniziare con un'applicazione hello che si sta sviluppando. I contesti sono disponibili per impostazione predefinita. Questi contesti sono:

* sc per Spark 
* sqlContext per Hive

Hello kernel PySpark fornisce alcuni predefinite "magics", che sono comandi speciale che è possibile chiamare con % %. Negli esempi di codice seguenti sono usati due comandi di questo tipo.

* **% % locale** specificato che il codice hello nelle righe successive viene eseguito localmente. Deve trattarsi di codice Python valido.
* **%%sql -o <variable name>** 
* Esegue una query Hive sqlContext hello. Se viene passato il parametro -o hello, il risultato di hello di hello query è persistente nel hello % % contesto Python locale come un frame di dati Pandas.

Per ulteriori informazioni su kernel hello per notebook Jupyter e hello predefiniti "magics" che forniscono, vedere [cluster kernel disponibile per i server Jupyter notebook con Linux di HDInsight Spark in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a>Inserire i dati e creare un frame di dati pulito
In questa sezione contiene codice hello per una serie di attività richiesto tooingest hello dati toobe con punteggio. Lettura in un campione di 0,1% unita in join di hello taxi di andata e ritorno e tariffa file (archiviati come file tsv), dati in formato hello e quindi crea un frame di dati pulito.

Hello taxi di andata e ritorno e tariffa i file sono stati aggiunti in base hello procedura il: [hello Team processo di analisi scientifica dei dati in azione: utilizzo dei cluster HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) argomento.

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

**OUTPUT:**

Tempo impiegato tooexecute di sopra di: 46.37 secondi

## <a name="prepare-data-for-scoring-in-spark"></a>Preparare i dati per l'assegnazione dei punteggi in Spark
In questa sezione viene illustrato come tooindex, codificare e scalare tooprepare organizzato per categorie di funzionalità per l'utilizzo in algoritmi di apprendimento supervisionato MLlib per la classificazione e regressione.

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a>Trasformazione di funzionalità: indicizzare e codificare funzionalità categoriche per l'inserimento in modelli per l'assegnazione dei punteggi
Questa sezione viene illustrato come tooindex dati categorici utilizzando un `StringIndexer` e codificare funzionalità con `OneHotEncoder` di input in modelli hello.

Hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) codifica di una colonna stringa della colonna di etichette tooa di indici di etichetta. gli indici di Hello sono ordinati per le frequenze di etichetta. 

Hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) esegue il mapping di una colonna della colonna di etichetta indici tooa di vettori binari, con al massimo uno a valore singolo. Questa codifica consente di utilizzare gli algoritmi che prevede funzionalità con valori continui, come la regressione logistica, funzionalità toocategorical toobe applicato.

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

**OUTPUT:**

Tempo impiegato tooexecute di sopra di: 5,37 secondi

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a>Creare oggetti RDD con matrici di funzionalità per l'inserimento in modelli
In questa sezione contiene codice che illustra come dati di testo categorico tooindex come un RDD dell'oggetto e a caldo uno codificare in modo da poterli usate tootrain test MLlib la regressione logistica ed e i modelli basati sulla struttura ad albero. Hello indicizzate vengono memorizzati in [resilienti Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) oggetti. Si tratta di astrazione di base hello in Spark. Un oggetto RDD rappresenta una raccolta partizionata non modificabile di elementi su cui è possibile operare in parallelo con Spark.

Contiene anche il codice che illustra come dati tooscale con hello `StandardScalar` forniti da MLlib per la regressione lineare con stocastico sfumatura Descent (SGD), un algoritmo comune per il training di una vasta gamma di modelli di machine learning. Hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) è usato tooscale hello funzionalità toounit varianza. Funzionalità di scalabilità, noto anche come normalizzazione dei dati, si assicura che le funzionalità con ampiamente i valori sono non specificato un numero eccessivo pesare nella funzione obiettivo hello. 

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

**OUTPUT:**

Tempo impiegato tooexecute di sopra di: 11.72 secondi

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a>Assegnare un punteggio con modello di regressione logistica hello e salvare l'output tooblob
codice di Hello in questa sezione viene illustrato come tooload un modello di regressione logistica che è stata salvata in Azure nell'archiviazione blob e utilizzarlo o meno un suggerimento è pagato toopredict in viaggio taxi, assegnare un punteggio, con le metriche di classificazione standard e quindi salvare e tracciare hello risultati tooblob spazio di archiviazione. risultati con punteggio Hello vengono archiviati negli oggetti RDD. 

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

**OUTPUT:**

Tempo impiegato tooexecute di sopra di: 19.22 secondi

## <a name="score-a-linear-regression-model"></a>Assegnare punteggi a un modello di regressione lineare
È stato usato [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) a pagamento di un modello di regressione lineare usando valori descent con sfumatura Stocastica (SGD, Virtual Private Network) per quantità di hello toopredict ottimizzazione del suggerimento tootrain. 

codice di Hello in questa sezione viene illustrato come tooload un modello di regressione lineare dall'archiviazione blob di Azure, assegna un punteggio con variabili scalate e quindi salvare blob di back-toohello risultati hello.

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


**OUTPUT:**

Tempo impiegato tooexecute di sopra di: 16.63 secondi

## <a name="score-classification-and-regression-random-forest-models"></a>Assegnare punteggi a modelli di foresta casuale per la classificazione e la regressione
codice Hello in questa sezione viene illustrato come hello tooload salvate classificazione e regressione i modelli di foresta casuale salvata nell'archiviazione blob di Azure, assegnare un punteggio delle relative prestazioni con classificazione standard e le misure di regressione e quindi salvare hello risultati tooblob indietro archiviazione.

[foreste casuali](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sono insiemi di alberi delle decisioni.  Combinano molti decision trees tooreduce hello rischio di overfitting. Foreste casuali possono gestire funzioni categoriche, estendere l'impostazione di classificazione multiclasse toohello, non richiedono la funzionalità di scalabilità e sono in grado di toocapture non linearità e interazioni di funzionalità. Foreste casuali sono uno dei hello riuscito più modelli di machine learning per la classificazione e regressione.

[spark.mllib](http://spark.apache.org/mllib/) supporta foreste casuali per la classificazione binaria e multiclasse e per la regressione, con funzionalità sia continue che categoriche. 

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

**OUTPUT:**

Tempo impiegato tooexecute di sopra di: 31.07 secondi

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a>Assegnare punteggi a modelli di alberi con boosting a gradienti per la classificazione e la regressione
codice di Hello in questa sezione viene illustrato come classificazione tooload sfumatura Boosting i modelli di albero di regressione dall'archiviazione blob di Azure, assegnare un punteggio delle relative prestazioni con classificazione standard e le misure di regressione e quindi salvare hello risultati tooblob indietro archiviazione. 

**spark.mllib** supporta gli alberi GBT per la classificazione binaria e per la regressione, con funzionalità sia continue che categoriche. 

[alberi con boosting a gradienti](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) sono insiemi di alberi delle decisioni. GBTs train alberi delle decisioni in modo iterativo toominimize una funzione di perdita. GBTs può gestire funzioni categoriche, non richiedono la funzionalità di scalabilità e sono in grado di toocapture non linearità e interazioni di funzionalità. Possono anche essere usati in un'impostazione di classificazione multiclasse.

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

**OUTPUT:**

Tempo impiegato tooexecute di sopra di: 14.6 secondi

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a>Pulire gli oggetti dalla memoria e stampare i percorsi di file con punteggio
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


**OUTPUT:**

logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt

linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949

randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt

randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt

BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt

BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt

## <a name="consume-spark-models-through-a-web-interface"></a>Utilizzare i modelli Spark da un'interfaccia Web
Spark fornisce un meccanismo tooremotely invia i processi batch o query interattive attraverso un resto interfacciarsi con un componente chiamato inserire il. Livy è abilitato per impostazione predefinita nel cluster HDInsight Spark. Per altre informazioni, vedere [Inviare processi Spark in modalità remota tramite Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md). 

È possibile utilizzare inserire il tooremotely invia un processo batch punteggi di un file che viene archiviato in un blob di Azure e quindi scrive blob tooanother di hello risultati. toodo, script Python hello da caricare  
[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob del cluster Spark hello. È possibile utilizzare uno strumento come **Microsoft Azure Storage Explorer** o **AzCopy** blob cluster toohello di toocopy hello script. In questo caso è stato caricato script hello troppo***wasb:///example/python/ConsumeGBNYCReg.py***.   

> [!NOTE]
> Hello chiavi di accesso che è necessario è reperibile nel portale di hello hello account di archiviazione associato al cluster Spark hello. 
> 
> 

Una volta caricato il percorso toothis, questo script viene eseguito all'interno di cluster Spark hello in un contesto distribuito. Carica il modello di hello ed esegue stime sui file di input basati sul modello hello.  

È possibile richiamare lo script in modalità remota tramite una semplice richiesta HTTPS/REST in Livy.  Ecco un curl comando tooconstruct hello HTTP richiesta tooinvoke hello script Python in modalità remota. Sostituire CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME con i valori appropriati di hello per il cluster Spark.

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

È possibile utilizzare qualsiasi linguaggio per il processo hello sistema remoto tooinvoke hello Spark tramite inserire il mediante una semplice chiamata HTTPS con l'autenticazione di base.   

> [!NOTE]
> Sarebbe libreria Python richieste di hello toouse pratico quando si effettua questa chiamata HTTP, ma non è attualmente installato per impostazione predefinita nelle funzioni di Azure. Vengono quindi usate altre librerie HTTP.   
> 
> 

Di seguito è riportato il codice Python hello per chiamata hello HTTP:

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


È inoltre possibile aggiungere questo codice Python troppo[Azure funzioni](https://azure.microsoft.com/documentation/services/functions/) tootrigger un invio di processi di Spark che assegna un punteggio a un blob in base a diversi eventi timer, creazione o aggiornamento di un blob. 

Se si preferisce un'esperienza client disponibile codice, utilizzare hello [Azure logica app](https://azure.microsoft.com/documentation/services/app-service/logic/) batch di Spark hello tooinvoke punteggio definendo un'azione HTTP su hello **logica App progettazione** e impostando i relativi parametri. 

* Nel portale di Azure creare una nuova app per la logica selezionando **+Nuovo** -> **Web e dispositivi mobili** -> **App per la logica**. 
* toobring backup hello **logica App progettazione**, immettere il nome di hello dell'App per la logica di hello e piano di servizio App.
* Selezionare un'azione HTTP e immettere i parametri di hello mostrati nella seguente illustrazione hello:

![Progettazione app per la logica](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a>Passaggi successivi
**Convalida incrociata e sweep di iperparametri**: vedere [Esplorazione e modellazione avanzate dei dati con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) per informazioni su come istruire i modelli sulla convalida incrociata e lo sweep di iperparametri.

