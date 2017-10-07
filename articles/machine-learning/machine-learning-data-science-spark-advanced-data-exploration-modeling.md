---
title: l'esplorazione dei dati aaaAdvanced e modellazione con Spark | Documenti Microsoft
description: Utilizzare l'esplorazione dei dati di toodo HDInsight Spark ed eseguirne il training modelli di classificazione e regressione binari con l'ottimizzazione della convalida incrociata e hyperparameter.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a>Esplorazione e modellazione avanzate dei dati con Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Questa procedura dettagliata Usa HDInsight Spark toodo train ed esplorazione dei binaria e classificazione dei dati utilizzando la convalida incrociata di modelli di regressione e ottimizzazione hyperparameter su un campione di hello NYC taxi di andata e ritorno e presentare set di dati 2013. Contiene passaggi hello di hello [il processo di analisi scientifica dei dati](http://aka.ms/datascienceprocess), end-to-end, utilizzando un HDInsight Spark cluster per l'elaborazione e i modelli di dati e hello hello toostore oggetti BLOB di Azure. processo Hello analizza e visualizza i dati importati da un Blob di archiviazione di Azure e quindi prepara hello dati toobuild modelli predittivi. Python è stato utilizzato toocode hello soluzione e tooshow hello rilevanti tracciati. Questi modelli sono compilazione mediante classificazione binaria toodo toolkit Spark MLlib hello e modellazione di attività di regressione. 

* Hello **classificazione binaria** attività è toopredict un suggerimento è pagato viaggi hello o meno. 
* Hello **regressione** attività è quantità hello toopredict del suggerimento hello in base alle altre funzionalità di suggerimento. 

i passaggi di modellazione Hello inoltre contenere codice che illustra come tootrain, valutare e salvare ogni tipo di modello. Hello argomento vengono illustrate alcune delle hello stesso messa a terra come hello [l'esplorazione dei dati e modellazione con Spark](machine-learning-data-science-spark-data-exploration-modeling.md) argomento. Ma più "avanzato" che usa anche la convalida incrociata con hyperparameter sweep tootrain modelli di classificazione e regressione in modo ottimale accurati. 

**La convalida incrociata (CV)** è una tecnica che consente di valutare un modello sottoposto a training su un set di dati noto anche come consente di generalizzare toopredicting hello funzionalità dei set di dati in cui si è ancora stato eseguito.  Un'implementazione comune utilizzata in questo argomento è toodivide un set di dati in sezioni di K e quindi eseguire il training del modello di hello in uno schema round robin su almeno una delle sezioni hello. viene valutato il possibilità Hello di hello modello tooprediction in modo accurato quando testato hello indipendente dal set di dati in questo modello di hello tootrain riduzione non usato.

**Ottimizzazione Hyperparameter** hello problema della scelta di un set di iperparametri per un algoritmo di apprendimento, in genere con l'obiettivo di hello ottimizzare una misura delle prestazioni dell'algoritmo hello in un set di dati indipendente. **Iperparametri** sono valori che devono essere specificati all'esterno di procedure training modello di hello. Presupposti relativi questi valori possono influire flessibilità hello e accuratezza dei modelli di hello. Gli alberi delle decisioni hanno iperparametri, ad esempio, come lo si desidera hello profondità e numero di foglie nell'albero di hello. Le macchine a vettori di supporto (SVM, Support Vector Machine) richiedono l'impostazione di una penalità per errata classificazione. 

Un'ottimizzazione comune delle modalità tooperform hyperparameter utilizzata in questo argomento è una ricerca di griglia, o un **sweep di parametri**. Si tratta di eseguendo una ricerca completa tramite i valori hello un subset di spazio hyperparameter hello specificato per un algoritmo di apprendimento. Convalida incrociata può fornire un toosort metrica prestazioni out ottimale hello prodotto dall'algoritmo di ricerca di hello griglia. CV utilizzato con hyperparameter sweep problemi di limite consente l'overfitting di un dati tootraining del modello in modo che hello modello consente di mantenere hello capacità tooapply toohello generale set di dati dalla quale hello sono stati estratti i dati di training.

i modelli di Hello che utilizziamo includono la regressione logistica e lineare, foreste casuali e sfumati alberi con Boosting:

* [La regressione lineare con SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) è un modello di regressione lineare che utilizza un metodo dei valori descent con sfumatura Stocastica (SGD, Virtual Private Network) e gli importi di suggerimento hello toopredict la scalabilità a pagamento per l'ottimizzazione e funzionalità. 
* [La regressione logistica con LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) o regressione "logit", è un modello di regressione che può essere utilizzato quando variabile dipendente hello è organizzato per categorie toodo classificazione dei dati. LBFGS è un algoritmo di ottimizzazione quasi Newton che offre un'approssimazione algoritmo di Broyden – Fletcher – Goldfarb – Shanno (BFGS) hello utilizzando una quantità limitata di memoria del computer e che è ampiamente usati in machine learning.
* [foreste casuali](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sono insiemi di alberi delle decisioni.  Combinano molti decision trees tooreduce hello rischio di overfitting. Foreste casuali vengono utilizzate per la classificazione e regressione e possono gestire funzioni categoriche e possono essere esteso l'impostazione di classificazione multiclasse toohello. Non richiedono funzionalità scalabilità e sono in grado di toocapture non linearità e interazioni di funzionalità. Foreste casuali sono uno dei hello riuscito più modelli di machine learning per la classificazione e regressione.
* [Alberi con boosting a gradienti](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT, Gradient boosted tree) sono insiemi di alberi delle decisioni. GBTs train alberi delle decisioni in modo iterativo toominimize una funzione di perdita. GBTs vengono utilizzati per la classificazione e regressione e può gestire funzioni categoriche, non richiedono la funzionalità di scalabilità e sono in grado di toocapture non linearità e interazioni di funzionalità. Possono anche essere usati in un'impostazione di classificazione multiclasse.

Esempi di utilizzo CV e Hyperparameter di modellazione durante lo sweep vengono visualizzati per il problema di classificazione binaria hello. Più semplici (senza parametro sweep) sono illustrati esempi dell'argomento principale di hello per le attività di regressione. Tuttavia, nell'appendice hello, viene presentata anche la convalida tramite net elastico per la regressione lineare e CV con parametro durante lo sweep di regressione di foresta casuale. Hello **elastica net** è un metodo di regressione regolarizzata per la regressione lineare di adattamento modelli in modo lineare combina metriche di tipo L1 e L2 hello come sanzioni di hello [lazo](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) e [bordo in rilievo](https://en.wikipedia.org/wiki/Tikhonov_regularization) metodi.   

> [!NOTE]
> Anche se hello Spark MLlib toolkit è progettato toowork su grandi set di dati, un campione di dimensioni relativamente ridotte (circa 30 Mb utilizzando K 170 righe, circa 0,1% del set di dati NYC originale hello) viene usato per motivi di praticità. esercizio Hello indicato qui viene eseguito in modo efficiente (in circa 10 minuti) in un cluster di HDInsight con 2 nodi di lavoro. Hello stesso codice, con modifiche minori, può essere utilizzato tooprocess maggiore-set di dati, con le modifiche appropriate per la memorizzazione nella cache dei dati in memoria e la modifica delle dimensioni del cluster hello.
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a>Configurazione: notebook e cluster Spark
La procedura di installazione e il codice forniti in questa procedura dettagliata sono per l'uso di un HDInsight Spark 1.6. Ma vengono forniti i notebook di Jupyter per i cluster HDInsight sia Spark 1.6 sia Spark 2.0. Vengono forniti una descrizione di hello blocchi appunti e collegamenti toothem in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) per il repository di GitHub hello che li contengono. Inoltre, codice hello qui e i notebook hello collegato è generico e dovrebbe funzionare in un cluster Spark. Se non si utilizza HDInsight Spark, passaggi di configurazione e gestione di cluster hello potrebbero essere leggermente diversi rispetto a quanto mostrato di seguito. Per praticità, di seguito sono notebook Jupyter di hello collegamenti toohello per 1.6 Spark e 2.0 toobe eseguito nel kernel pyspark hello del server Jupyter Notebook hello:

### <a name="spark-16-notebooks"></a>Notebook Spark 1.6

[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): include gli argomenti nel notebook numero 1 e modella lo sviluppo usando l'ottimizzazione degli iperparametri e la convalida incrociata.

### <a name="spark-20-notebooks"></a>Notebook Spark 2.0

[Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): questo file fornisce informazioni su come l'esplorazione dei dati tooperform, modellazione e assegnazione dei punteggi in Spark 2.0 cluster.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Il programma di installazione: hello, librerie e percorsi di archiviazione predefinito contesto Spark
Spark è in grado di tooAzure tooread e di scrittura Blob di archiviazione (noto anche come WASB). Pertanto, i dati esistenti archiviate possono essere elaborati utilizzando Spark e hello risultati WASB archiviato nuovamente in.

modelli toosave o file in WASB, percorso hello deve toobe specificato correttamente. Hello del cluster Spark toohello contenitore collegato predefinito possibile farvi riferimento tramite un che inizia con: "wasb: / / /". "wasb://" fa riferimento ad altri percorsi.

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Impostare percorsi di directory per i percorsi di archiviazione in WASB
esempio di codice seguente Hello Specifica percorso hello di hello dati toobe leggere e hello percorso per l'output di hello modello archiviazione directory toowhich hello modello viene salvato:

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

**OUTPUT**

datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)

### <a name="import-libraries"></a>Importare le librerie
Importare le librerie necessarie con hello seguente codice:

    # LOAD PYSPARK LIBRARIES
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
kernel PySpark Hello forniti con i notebook Jupyter dispone di un contesto predefinito. Pertanto, non è necessario contesti di Spark o Hive hello tooset in modo esplicito prima di iniziare con un'applicazione hello che si sta sviluppando. Questi contesti sono disponibili per impostazione predefinita. Questi contesti sono:

* sc per Spark 
* sqlContext per Hive

Hello kernel PySpark fornisce alcuni predefinite "magics", che sono comandi speciale che è possibile chiamare con % %. Negli esempi di codice seguenti sono usati due comandi di questo tipo.

* **% % locale** specifica che il codice hello nelle righe successive toobe eseguite localmente. Deve trattarsi di codice Python valido.
* **% % sql -o <variable name>**  esegue una query Hive sqlContext hello. Se viene passato il parametro -o hello, il risultato di hello di hello query è persistente nel hello % % contesto Python locale come un frame di dati Pandas.

Per ulteriori informazioni su kernel hello per notebook Jupyter e hello predefiniti "magics" che forniscono, vedere [cluster kernel disponibile per i server Jupyter notebook con Linux di HDInsight Spark in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="data-ingestion-from-public-blob"></a>Inserimento di dati dal BLOB pubblico:
Hello primo passaggio nel processo di analisi scientifica dei dati hello è tooingest hello dati toobe analizzati da origini in cui si trova nell'ambiente di esplorazione e modellazione di dati. In questa procedura dettagliata l'ambiente è Spark. In questa sezione contiene toocomplete codice hello una serie di attività:

* inserimento hello dati esempio toobe modellata
* leggere nel set di input dati hello (archiviati come file tsv)
* formato e dati hello pulita
* Creazione di oggetti, RDD o frame di dati, e memorizzazione nella cache in memoria.
* Registrazione come tabella temporanea in un contesto SQL.

Ecco il codice hello per l'inserimento di dati.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
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

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**OUTPUT**

Tempo impiegato tooexecute di sopra di: 276.62 secondi

## <a name="data-exploration--visualization"></a>Visualizzazione ed esplorazione dei dati
Dopo aver inseriti dati hello in Spark, hello il passaggio successivo nel processo di analisi scientifica dei dati hello è toogain comprensione più approfondita dei dati di hello tramite l'esplorazione e la visualizzazione. In questa sezione è esaminare i dati di taxi hello utilizzando le query SQL e le variabili di destinazione di tracciato hello e funzionalità potenziali per l'esame visivo. Nello specifico, abbiamo tracciare frequenza hello dei conteggi di passeggeri in taxi trip, hello della frequenza degli importi di suggerimento e come suggerimenti variano a seconda del tipo e la quantità di pagamento.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Tracciare un istogramma che mostra le frequenze di conteggio di passeggeri nell'esempio hello di trip taxi
Questo codice e i successivi frammenti di codice è possibile utilizzare SQL tooquery magic hello dati di esempio e locale tooplot magic hello.

* **Chiave SQL (`%%sql`)** HDInsight PySpark kernel hello supporta hello sqlContext query HiveQL facile inline. Hello (-o VARIABLE_NAME) argomento mantiene l'output di hello di query SQL hello sotto forma di un frame di dati Pandas server Jupyter hello. Ciò significa che è disponibile in modalità locale hello.
* Hello  **`%%local` magic** viene utilizzato codice toorun localmente nel server di Jupyter hello, ovvero hello nodo head del cluster HDInsight hello. In genere, si utilizza `%%local` magic dopo hello `%%sql -o` magic è toorun utilizzata una query. il parametro -o Hello sarebbe ancora valide output di hello di query SQL hello in locale. Quindi hello `%%local` trigger magic hello set successivo di toorun frammenti di codice in locale sull'output di hello delle query SQL hello che ha reso persistente in locale. output di Hello viene automaticamente visualizzato dopo l'esecuzione di codice hello.

Questa query recupera trip hello dal conteggio di passeggeri. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


Questo codice crea un frame di dati locale dall'output di hello query e vengono tracciati dati hello. Hello `%%local` magic crea un frame di dati locale, `sqlResults`, che può essere usato per il tracciato con matplotlib. 

> [!NOTE]
> Tale magic PySpark viene usato più volte in questa procedura dettagliata. Se è grande quantità di hello di dati, si deve esempio toocreate un frame di dati che può adattarsi alla memoria locale.
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Ecco trip di hello tooplot codice hello da passeggero conteggi

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**OUTPUT**

![Frequenza delle corse per numero di passeggeri](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

È possibile scegliere tra diversi tipi di visualizzazioni (tabella, a torta, linea, Area o barra) utilizzando hello **tipo** pulsanti di menu in blocco per Appunti hello. tracciato barra Hello è illustrato di seguito.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Tracciare un istogramma dell'importo delle mance e della relativa variazione in base al numero di passeggeri e all'importo delle corse.
Utilizzare una data di toosample query SQL...

    # SQL SQUERY
    %%sql -q -o sqlResults
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train 
        WHERE passenger_count > 0 
        AND passenger_count < 7
        AND fare_amount > 0 
        AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 
        AND tip_amount < 25


Questa cella codice utilizza hello SQL query toocreate tre vengono tracciati hello dati.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


**OUTPUT:** 

![Distribuzione dell'importo delle mance](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Importo della mancia per numero di passeggeri](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Importo della mancia per importo della corsa](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Progettazione di funzionalità, trasformazione e preparazione dei dati per la modellazione
In questa sezione descrive e fornisce codice hello per le procedure utilizzate tooprepare dati per la modellazione di ML. Viene illustrato come hello toodo seguenti attività:

* Creare una nuova funzionalità dalla partizione di contenitori per gli orari di trasporto
* Indicizzare funzionalità categoriche e applicare la codifica one-hot
* Creare oggetti punto etichettato per l'inserimento in funzioni di apprendimento automatico
* Creare un campionamento secondario casuale dei dati hello e dividere il set di training e set di testing
* Ridimensionamento di funzionalità
* Memorizzazione nella cache di oggetti in memoria

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a>Creare una nuova funzionalità dalla partizione di contenitori per gli orari di trasporto
Questo codice viene illustrato come toocreate sempre una nuova funzionalità suddividendo il traffico in bin e come toocache hello risultante frame di dati in memoria. La memorizzazione nella cache comporta il tempo di esecuzione tooimproved dove resilienti Distributed set di dati (RDDs) e frame di dati vengono utilizzati più volte. RDD e frame di dati vengono quindi memorizzati nella cache in varie fasi di questa procedura dettagliata.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

**OUTPUT**

126050

### <a name="index-and-one-hot-encode-categorical-features"></a>Indicizzare funzionalità categoriche e applicare la codifica one-hot
Questa sezione viene illustrato come tooindex o codificare categorica funzionalità per l'input nel hello funzioni di modellazione. Hello modellazione e stimare le funzioni di MLlib richiedono che funzionalità organizzato per categorie dei dati di input deve essere indicizzata o codificata toouse precedente. 

A seconda del modello di hello, è necessario tooindex o codificarli in modi diversi. Ad esempio, modelli Logistic e regressione lineare richiedono hot una codifica, in cui, ad esempio, una funzionalità costituita da tre categorie può essere espanso in tre colonne di funzionalità, con ogni contiene 0 o 1 a seconda della categoria di hello di un'osservazione. Fornisce MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funzione toodo hot una codifica. Questo codificatore esegue il mapping di una colonna della colonna di etichetta indici tooa di vettori binari, con al massimo uno a valore singolo. Questa codifica consente di utilizzare gli algoritmi che prevedono le funzionalità di valori numeriche, ad esempio la regressione logistica, funzionalità toocategorical toobe applicato.

Ecco hello tooindex codice e codificare funzionalità organizzato per categorie:

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
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

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**OUTPUT**

Tempo impiegato tooexecute di sopra di: 3,14 secondi

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Creare oggetti punto etichettato per l'inserimento in funzioni di apprendimento automatico
In questa sezione contiene codice che illustra come tipo di dati di testo categorico tooindex come etichetta punto dati e come tooencode è. Questa funzione Prepara, toobe utilizzato tootrain test MLlib la regressione logistica ed e altri modelli di classificazione. Gli oggetti punto etichettato sono RDD (Resilient Distributed Dataset) formattati come richiesto per i dati di input dalla maggior parte degli algoritmi di apprendimento automatico in MLlib. Un [punto etichettato](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) è un vettore locale, che può essere denso o sparso, associato a un'etichetta o a una risposta.

Ecco hello tooindex codice e codificare le funzionalità di testo per la classificazione binaria.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


Ecco il codice hello tooencode indice testo categorico funzionalità per l'analisi di regressione lineare.

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a>Creare un campionamento secondario casuale dei dati hello e dividere il set di training e set di testing
Questo codice crea un campionamento casuale dei dati di hello (25% viene utilizzato qui). Anche se non sono richiesto per questo esempio a causa delle dimensioni toohello di hello set di dati, viene illustrato come è possibile campionare i dati hello qui. Si può stabilire come toouse per il proprio problema se necessario. Nei campioni di grandi dimensioni questa operazione permette di risparmiare molto tempo durante il training dei modelli. Successivamente è suddivisa: esempio hello una parte di training (75%) e un test toouse parte (25 %)) nella classificazione e creazione di modelli di regressione.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**OUTPUT**

Tempo impiegato tooexecute di sopra di: 0,31 secondi

### <a name="feature-scaling"></a>Ridimensionamento di funzionalità
Funzionalità di scalabilità, noto anche come normalizzazione dei dati, si assicura che le funzionalità con ampiamente i valori sono non specificato un numero eccessivo pesare nella funzione obiettivo hello. codice per la funzionalità scalabilità Hello Usa hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) varianza di toounit tooscale hello funzionalità. Viene fornito da MLlib per l'uso nella regressione lineare con Stochastic Gradient Descent (SGD). SGD è un algoritmo molto diffuso per il training di una vasta gamma di modelli di apprendimento automatico, come la regressione regolarizzata o le macchine a vettori di supporto (SVM).   

> [!TIP]
> È stato trovato il ridimensionamento di hello LinearRegressionWithSGD algoritmo toobe toofeature sensibili.   
> 
> 

Ecco le variabili di tooscale codice hello per l'utilizzo con l'algoritmo SGD lineare di regolarizzazione hello.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**OUTPUT**

Tempo impiegato tooexecute di sopra di: 11.67 secondi

### <a name="cache-objects-in-memory"></a>Memorizzazione nella cache di oggetti in memoria
tempo per il training e testing di algoritmi di Machine Learning Hello può essere ridotto limitando la memorizzazione nella cache i frame di dati di input hello gli oggetti utilizzati per la classificazione di regressione e, con funzionalità di scalabilità.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**OUTPUT** 

Tempo impiegato tooexecute di sopra di: 0,13 secondi

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Uso di modelli di classificazione binaria per prevedere se viene lasciata o meno una mancia
In questa sezione viene illustrato come utilizzare tre modelli per attività di classificazione binaria hello di stima di un suggerimento viene pagato per un itinerario taxi o meno. modelli di Hello presentati sono:

* Regressione logistica 
* Foresta casuale
* Alberi con boosting a gradienti.

Ogni sezione di codice di compilazione del modello è suddivisa in passaggi: 

1. **training del modello** con un set di parametri
2. **Valutazione del modello** su un set di dati di test con metriche
3. **Salvataggio del modello** in un BLOB per l'uso in futuro

Viene illustrato come toodo convalida incrociata (CV) con il parametro sweep in due modi:

1. Utilizzando **generico** codice personalizzato che può essere applicato tooany algoritmo nel parametro MLlib e tooany imposta in un algoritmo. 
2. Utilizzo di hello **pySpark funzione pipeline CrossValidator**. Si noti che CrossValidator presenta alcune limitazioni per Spark 1.5.0: 
   
   * I modelli di pipeline non possono essere salvati/resi persistenti per un utilizzo futuro.
   * Non può essere usato per ogni parametro in un modello.
   * Non può essere usato per ogni algoritmo MLlib.

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a>Generico tra la convalida e lo sweep hyperparameter utilizzati con l'algoritmo di regressione logistica hello per la classificazione binaria
codice Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di regressione logistica con [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) che esegue una stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa DataSet. Training del modello Hello tra la convalida (CV) e lo sweep hyperparameter implementato con codice personalizzato che può essere applicato tooany di hello in MLlib algoritmi di apprendimento.   

> [!NOTE]
> esecuzione di Hello del codice personalizzato CV può richiedere alcuni minuti.
> 
> 

**Training modello di regressione logistica hello utilizzando CV e hyperparameter sweep**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**OUTPUT**

Coefficienti: [0,0082065285375, -0,0223675576104, -0,0183812028036, -3,48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]

Intercetta: -0,0111216486893

Tempo impiegato tooexecute di sopra di: 14.43 secondi

**Valutazione del modello di classificazione binaria hello con le metriche standard**

codice Hello in questa sezione viene illustrato come tooevaluate una regressione logistica del modello su un test-set di dati, tra cui un tracciato di hello curva ROC.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**OUTPUT**

Area in PR = 0,985336538462

Area in ROC = 0,983383274312

Statistiche di riepilogo

Precisione = 0,984174341679

Richiamo = 0,984174341679

Punteggio F1 = 0,984174341679

Tempo impiegato tooexecute di sopra di: 2.67 secondi

**Tracciare una curva ROC hello.**

Hello *predictionAndLabelsDF* viene registrato come una tabella, *tmp_results*, nella cella precedente hello. *tmp_results* possibile toodo utilizzato query e restituire i risultati in hello sqlResults-frame di dati per il tracciato. Ecco il codice hello.

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Ecco le stime di toomake codice hello e hello tracciato curva ROC.

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**OUTPUT**

![Curva ROC di regressione logistica per approccio generico](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

**Rendere persistente il modello in un BLOB per l'utilizzo in futuro**

codice Hello in questa sezione viene illustrato come la regressione logistica toosave hello del modello per l'utilizzo.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


**OUTPUT**

Tempo impiegato tooexecute di sopra di: 34.57 secondi

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a>Usare la funzione della pipeline CrossValidator di MLlib con il modello di regressione logistica (regressione elastica)
codice Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di regressione logistica con [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) che esegue una stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa DataSet. Training del modello Hello utilizzando la convalida incrociata (CV) e hyperparameter sweep con hello MLlib CrossValidator pipeline funzione implementata per CV con sweep di parametri.   

> [!NOTE]
> esecuzione di Hello del codice MLlib CV può richiedere alcuni minuti.
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**OUTPUT**

Tempo impiegato tooexecute di sopra di: 107.98 secondi

**Tracciare una curva ROC hello.**

Hello *predictionAndLabelsDF* viene registrato come una tabella, *tmp_results*, nella cella precedente hello. *tmp_results* possibile toodo utilizzato query e restituire i risultati in hello sqlResults-frame di dati per il tracciato. Ecco il codice hello.

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

Di seguito è riportata la curva ROC hello codice tooplot hello.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**OUTPUT**

![Curva ROC di regressione logistica con CrossValidator di MLlib](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a>Classificazione tramite foresta casuale
codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare una regressione foresta casuale che stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa set di dati.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**OUTPUT**

Area in ROC = 0,985336538462

Tempo impiegato tooexecute di sopra di: 26.72 secondi

### <a name="gradient-boosting-trees-classification"></a>Classificazione tramite alberi con boosting a gradienti
codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di alberi boosting sfumatura che stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa set di dati.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**OUTPUT**

Area in ROC = 0,985336538462

Tempo impiegato tooexecute di sopra di: 28.13 secondi

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a>Prevedere l'importo delle mance con di modelli di regressione (senza usare la convalida incrociata)
Questa sezione viene illustrato come utilizzare tre modelli per attività di regressione hello: stimare hello suggerimento quantità pagata per un itinerario taxi basato sulle altre funzionalità di suggerimento. modelli di Hello presentati sono:

* Regressione lineare regolarizzata
* Foresta casuale
* Alberi con boosting a gradienti.

Questi modelli sono stati descritti introduzione hello. Ogni sezione di codice di compilazione del modello è suddivisa in passaggi: 

1. **training del modello** con un set di parametri
2. **Valutazione del modello** su un set di dati di test con metriche
3. **Salvataggio del modello** in un BLOB per l'uso in futuro   

> AZURE Nota: La convalida incrociata non viene usata con hello tre i modelli di regressione in questa sezione, poiché questa operazione è stata illustrata in dettaglio per i modelli di regressione logistica hello. Un esempio che illustra come toouse CV con elastico netto per la regressione lineare viene fornito in hello appendice di questo argomento.
> 
> AZURE Nota: Nella nostra esperienza, possono esserci problemi con la convergenza dei modelli LinearRegressionWithSGD e parametri necessario toobe modificato/ottimizzata con attenzione per ottenere un modello valido. Il ridimensionamento delle variabili può essere molto utile per la convergenza. Regressione net elastica, illustrata nell'argomento toothis appendice hello nonché anziché LinearRegressionWithSGD.
> 
> 

### <a name="linear-regression-with-sgd"></a>Regressione lineare con SGD
Hello codice in questa sezione viene illustrato come toouse scalato funzionalità tootrain una regressione lineare che usa descent con sfumatura stocastica (SGD) per l'ottimizzazione, e come tooscore, valutare e salvare il modello di hello in archiviazione Blob di Azure (WASB).

> [!TIP]
> Nella nostra esperienza, si possono verificare problemi con convergenza hello dei modelli LinearRegressionWithSGD e parametri necessario toobe modificato/ottimizzata con attenzione per ottenere un modello valido. Il ridimensionamento delle variabili può essere molto utile per la convergenza.
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**OUTPUT**

Coefficienti: [0,0141707753435, -0,0252930927087, -0,0231442517137, 0,247070902996, 0,312544147152, 0,360296120645, 0,0122079566092, -0,00456498588241, -0,0898228505177, 0,0714046248793, 0,102171263868, 0,100022455632, -0,00289545676449, -0,00791124681938, 0,54396316518, -0,536293513569, 0,0119076553369, -0,0173039244582, 0,0119632796147, 0,00146764882502]

Intercetta: 0,854507624459

RMSE = 1,23485131376

R-sqr = 0,597963951127

Tempo impiegato tooexecute di sopra di: 38.62 secondi

### <a name="random-forest-regression"></a>Regressione tramite foresta casuale
codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di foresta casuale che stima quantità suggerimento per dati di andata e ritorno taxi NYC hello.   

> [!NOTE]
> La convalida incrociata con parametro sweep con codice personalizzato viene fornita nell'appendice hello.
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**OUTPUT**

RMSE = 0,931981967875

R-sqr = 0,733445485802

Tempo impiegato tooexecute di sopra di: 25.98 secondi

### <a name="gradient-boosting-trees-regression"></a>Regressione tramite alberi con boosting a gradienti
codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di alberi boosting sfumatura che stima quantità suggerimento per dati di andata e ritorno taxi NYC hello.

**Eseguire il training e valutare**

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**OUTPUT**

RMSE = 0,928172197114

R-sqr = 0,732680354389

Tempo impiegato tooexecute di sopra di: 20,9 secondi

**Grafico**

*tmp_results* viene registrato come una tabella Hive in una cella precedente hello. I risultati dalla tabella hello vengono visualizzati in hello *sqlResults* frame di dati per il tracciato. Ecco il codice hello

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Ecco dati hello tooplot codice hello utilizzando server Jupyter hello.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a>Appendice: Attività di regressione aggiuntive tramite convalida incrociata con sweep di parametri
Questa appendice contiene una visualizzazione di codice come CV toodo tramite net elastico per la regressione lineare e come CV toodo con parametro sweep con codice personalizzato per la regressione di foresta casuale.

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a>Convalida incrociata con Elastic Net per la regressione lineare
codice di Hello in questa sezione viene illustrato come toodo superano la convalida utilizzando elastica netto per la regressione lineare e come tooevaluate hello modello rispetto a dati di test.

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**OUTPUT**

Tempo impiegato tooexecute di sopra di: 161.21 secondi

**Eseguire la valutazione con la metrica R-SQR**

*tmp_results* viene registrato come una tabella Hive in una cella precedente hello. I risultati dalla tabella hello vengono visualizzati in hello *sqlResults* frame di dati per il tracciato. Ecco il codice hello

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


Di seguito è toocalculate codice hello sqr di R.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


**OUTPUT**

R-sqr = 0,619184907088

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a>Convalida incrociata con sweep di parametri usando codice personalizzato per la regressione tramite foresta casuale
codice di Hello in questa sezione viene illustrato come toodo convalida incrociata con lo sweep di parametri con codice personalizzato per la regressione di foreste casuali e come tooevaluate hello modello rispetto a dati di test.

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**OUTPUT**

RMSE = 0,906972198262

R-sqr = 0,740751197012

Tempo impiegato tooexecute di sopra di: 69.17 secondi

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a>Pulire gli oggetti dalla memoria e stampare i percorsi dei modelli
Utilizzare `unpersist()` toodelete oggetti memorizzati nella cache in memoria.

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


**OUTPUT**

PythonRDD[122] at RDD at PythonRDD.scala: 43

* * Stampa percorso toomodel file toobe utilizzato in blocco per Appunti consumo hello. * * tooconsume e punteggio indipendente-set di dati, è necessario toocopy e incollare questi nomi di file in "Notebook consumo" hello.

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**OUTPUT**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"

## <a name="whats-next"></a>Passaggi successivi
Dopo aver creato i modelli di classificazione e regressione con MlLib Spark hello, si è toolearn pronto come tooscore e valutare questi modelli.

**Utilizzo del modello:** toolearn come tooscore e valutare i modelli di classificazione e regressione hello creati in questo argomento, vedere [punteggio e valutare i modelli di apprendimento macchina compilato Spark](machine-learning-data-science-spark-model-consumption.md).

