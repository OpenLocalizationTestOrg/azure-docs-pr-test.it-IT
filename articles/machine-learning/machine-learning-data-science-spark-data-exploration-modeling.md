---
title: aaaData esplorazione e modellazione con Spark | Documenti Microsoft
description: "Apprendimento hello l'esplorazione dei dati e modellazione di funzionalità del toolkit di hello MLlib Spark in Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a>Modellazione ed esplorazione dei dati con Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Questa procedura dettagliata Usa l'esplorazione dei dati di HDInsight Spark toodo e classificazione binaria e modellazione di attività a un campione di hello NYC regressione taxi di andata e ritorno e presentare set di dati 2013.  Contiene passaggi hello di hello [il processo di analisi scientifica dei dati](http://aka.ms/datascienceprocess), end-to-end, utilizzando un HDInsight Spark cluster per l'elaborazione e i modelli di dati e hello hello toostore oggetti BLOB di Azure. processo Hello analizza e visualizza i dati importati da un Blob di archiviazione di Azure e quindi prepara hello dati toobuild modelli predittivi. Questi modelli sono compilazione mediante classificazione binaria toodo toolkit Spark MLlib hello e modellazione di attività di regressione.

* Hello **classificazione binaria** attività è toopredict un suggerimento è pagato viaggi hello o meno. 
* Hello **regressione** attività è quantità hello toopredict del suggerimento hello in base alle altre funzionalità di suggerimento. 

i modelli di Hello che utilizziamo includono la regressione logistica e lineare, foreste casuali e sfumati alberi con Boosting:

* [La regressione lineare con SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) è un modello di regressione lineare che utilizza un metodo dei valori descent con sfumatura Stocastica (SGD, Virtual Private Network) e gli importi di suggerimento hello toopredict la scalabilità a pagamento per l'ottimizzazione e funzionalità. 
* [La regressione logistica con LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) o regressione "logit", è un modello di regressione che può essere utilizzato quando variabile dipendente hello è organizzato per categorie toodo classificazione dei dati. LBFGS è un algoritmo di ottimizzazione quasi Newton che offre un'approssimazione algoritmo di Broyden – Fletcher – Goldfarb – Shanno (BFGS) hello utilizzando una quantità limitata di memoria del computer e che è ampiamente usati in machine learning.
* [foreste casuali](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sono insiemi di alberi delle decisioni.  Combinano molti decision trees tooreduce hello rischio di overfitting. Foreste casuali vengono utilizzate per la classificazione e regressione e possono gestire funzioni categoriche e possono essere esteso l'impostazione di classificazione multiclasse toohello. Non richiedono funzionalità scalabilità e sono in grado di toocapture non linearità e interazioni di funzionalità. Foreste casuali sono uno dei hello riuscito più modelli di machine learning per la classificazione e regressione.
* [Alberi con boosting a gradienti](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT, Gradient boosted tree) sono insiemi di alberi delle decisioni. GBTs train alberi delle decisioni in modo iterativo toominimize una funzione di perdita. GBTs vengono utilizzati per la classificazione e regressione e può gestire funzioni categoriche, non richiedono la funzionalità di scalabilità e sono in grado di toocapture non linearità e interazioni di funzionalità. Possono anche essere usati in un'impostazione di classificazione multiclasse.

i passaggi di modellazione Hello inoltre contenere codice che illustra come tootrain, valutare e salvare ogni tipo di modello. Python è stato utilizzato toocode hello soluzione e tooshow hello rilevanti tracciati.   

> [!NOTE]
> Anche se hello Spark MLlib toolkit è progettato toowork su grandi set di dati, un campione di dimensioni relativamente ridotte (circa 30 Mb utilizzando K 170 righe, circa 0,1% del set di dati NYC originale hello) viene usato per motivi di praticità. esercizio Hello indicato qui viene eseguito in modo efficiente (in circa 10 minuti) in un cluster di HDInsight con 2 nodi di lavoro. Hello stesso codice, con modifiche minori, può essere utilizzato tooprocess maggiore-set di dati, con le modifiche appropriate per la memorizzazione nella cache dei dati in memoria e la modifica delle dimensioni del cluster hello.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
È necessario un account Azure e Spark 1.6 (o 2.0 Spark) toocomplete cluster HDInsight in questa procedura dettagliata. Vedere hello [panoramica dell'analisi scientifica dei dati utilizzando Spark in Azure HDInsight](machine-learning-data-science-spark-overview.md) per istruzioni su come toosatisfy questi requisiti. Questo argomento contiene inoltre una descrizione di hello dati NYC 2013 Taxi utilizzati in questo argomento e per istruzioni su come il codice da un server Jupyter notebook nel cluster Spark hello tooexecute. 

## <a name="spark-clusters-and-notebooks"></a>Notebook e cluster Spark
La procedura di installazione e il codice forniti in questa procedura dettagliata sono per l'uso di un HDInsight Spark 1.6. Ma vengono forniti i notebook di Jupyter per i cluster HDInsight sia Spark 1.6 sia Spark 2.0. Vengono forniti una descrizione di hello blocchi appunti e collegamenti toothem in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) per il repository di GitHub hello che li contengono. Inoltre, codice hello qui e i notebook hello collegato è generico e dovrebbe funzionare in un cluster Spark. Se non si utilizza HDInsight Spark, passaggi di configurazione e gestione di cluster hello potrebbero essere leggermente diversi rispetto a quanto mostrato di seguito. Per praticità, di seguito sono collegamenti hello toohello Jupyter notebook per Spark 1.6 (toobe eseguito nel kernel pySpark hello di hello server Jupyter Notebook) e Spark 2.0 (toobe eseguito nel kernel pySpark3 hello di hello server Jupyter Notebook):

### <a name="spark-16-notebooks"></a>Notebook Spark 1.6

[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): fornisce informazioni su come l'esplorazione dei dati tooperform, modellazione e assegnazione dei punteggi con diversi algoritmi.

### <a name="spark-20-notebooks"></a>Notebook Spark 2.0
attività di classificazione e regressione Hello implementate utilizzando un cluster Spark 2.0 sono separati blocchi appunti e notebook classificazione hello utilizza un set di dati diverso:

- [Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): questo file fornisce informazioni su come l'esplorazione dei dati tooperform, modellazione e assegnazione dei punteggi in Spark 2.0 cluster tramite hello viaggi NYC Taxi e set di dati tariffa descritto [qui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Questo blocco può essere un buon punto di partenza per esplorare rapidamente codice hello che è stato fornito per Spark 2.0. Per un blocco per Appunti più dettagliata analizza hello dati NYC Taxi, vedere notebook avanti di hello in questo elenco. Vedere le note di hello seguendo questo elenco di confrontare questi notebook. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): questo file viene illustrato come tooperform dati wrangling (operazioni Spark SQL e frame di dati), l'esplorazione, modellazione e assegnazione dei punteggi usando hello viaggi NYC Taxi e tariffa set di dati descritto [ qui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): questo file viene illustrato come tooperform dati wrangling (operazioni Spark SQL e frame di dati), l'esplorazione, modellazione e assegnazione dei punteggi usando hello partenza in fase di Airline noto set di dati da 2011 e 2012. È integrato hello airline dataset con hello aeroporto weather dati (ad esempio, velocità del vento, temperatura, altitudine e così via) precedenti toomodeling, in modo queste funzionalità weather possono essere incluso nel modello di hello.

<!-- -->

> [!NOTE]
> set di dati airline Hello è stato aggiunto notebook toohello Spark 2.0 toobetter illustrano l'utilizzo di hello di algoritmi di classificazione. Vedere i seguenti collegamenti per informazioni sui set di dati in fase di partenza airline e set di dati meteo hello:

>- Dati sulle partenze puntuali dei voli della compagnia aerea: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Dati sulle condizioni atmosferiche dell'aeroporto: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
Appunti di Spark 2.0 Hello in hello taxi NYC e airline flight delay-set di dati può richiedere 10 minuti o più toorun (a seconda delle dimensioni di hello del cluster HDI). primo notebook in hello sopra elenco Hello Mostra molti aspetti di esplorazione dei dati di hello, training in un blocco per Appunti che accetta toorun meno tempo con ridotti NYC set di dati, in cui hello sono stati già aggiunti a un file taxi e fare del modello di visualizzazione e ML: [ Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) il blocco accetta un molto più breve tempo toofinish (2-3 minuti) e può essere un buon punto di partenza per esplorare rapidamente codice hello abbiamo fornito per Spark 2.0. 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
descrizioni di Hello riportate di seguito sono correlati toousing Spark 1.6. Per le versioni 2.0 Spark, utilizzare i notebook hello descritti e in precedenza. 

<!-- -->

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
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a>Importare le librerie
Per la configurazione occorre anche importare le librerie necessarie. Impostare il contesto di spark e importare le librerie necessarie con hello seguente codice:

    # IMPORT LIBRARIES
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

## <a name="data-ingestion-from-public-blob"></a>Inserimento di dati dal BLOB pubblico
Hello primo passaggio nel processo di analisi scientifica dei dati hello consiste tooingest hello dati toobe analizzati da origini in cui è si trova nell'ambiente di esplorazione e modellazione di dati. ambiente di Hello è Spark in questa procedura dettagliata. In questa sezione contiene toocomplete codice hello una serie di attività:

* inserimento hello dati esempio toobe modellata
* leggere nel set di input dati hello (archiviati come file tsv)
* formato e dati hello pulita
* Creazione di oggetti, RDD o frame di dati, e memorizzazione nella cache in memoria.
* Registrazione come tabella temporanea in un contesto SQL.

Ecco il codice hello per l'inserimento di dati.

    # INGEST DATA

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


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**OUTPUT:**

Tempo impiegato tooexecute di sopra di: 51.72 secondi

## <a name="data-exploration--visualization"></a>Visualizzazione ed esplorazione dei dati
Dopo aver inseriti dati hello in Spark, hello il passaggio successivo nel processo di analisi scientifica dei dati hello è toogain comprensione più approfondita dei dati di hello tramite l'esplorazione e la visualizzazione. In questa sezione è esaminare i dati di taxi hello utilizzando le query SQL e le variabili di destinazione di tracciato hello e funzionalità potenziali per l'esame visivo. Nello specifico, abbiamo tracciare frequenza hello dei conteggi di passeggeri in taxi trip, hello della frequenza degli importi di suggerimento e come suggerimenti variano a seconda del tipo e la quantità di pagamento.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Tracciare un istogramma che mostra le frequenze di conteggio di passeggeri nell'esempio hello di trip taxi
Questo codice e i successivi frammenti di codice è possibile utilizzare SQL tooquery magic hello dati di esempio e locale tooplot magic hello.

* **Chiave SQL (`%%sql`)** HDInsight PySpark kernel hello supporta hello sqlContext query HiveQL facile inline. Hello (-o VARIABLE_NAME) argomento mantiene l'output di hello di query SQL hello sotto forma di un frame di dati Pandas server Jupyter hello. Ciò significa che è disponibile in modalità locale hello.
* Hello  **`%%local` magic** viene utilizzato codice toorun localmente nel server di Jupyter hello, ovvero hello nodo head del cluster HDInsight hello. In genere, si utilizza `%%local` magic in combinazione con hello `%%sql` magic con parametro -o. il parametro -o Hello sarebbe ancora valide output di hello di query SQL hello in locale e quindi % % magic locale Attiva set successivo di hello di toorun frammento di codice in locale sull'output di hello delle query SQL hello in modo permanente in locale

output di Hello viene automaticamente visualizzato dopo l'esecuzione di codice hello.

Questa query recupera trip hello dal conteggio di passeggeri. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

Questo codice crea un frame di dati locale dall'output di hello query e vengono tracciati dati hello. Hello `%%local` magic crea un frame di dati locale, `sqlResults`, che può essere usato per il tracciato con matplotlib. 

> [!NOTE]
> Tale magic PySpark viene usato più volte in questa procedura dettagliata. Se è grande quantità di hello di dati, si deve esempio toocreate un frame di dati che può adattarsi alla memoria locale.
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Ecco trip di hello tooplot codice hello da passeggero conteggi

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**OUTPUT:**

![Frequenza delle corse per numero di passeggeri](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

È possibile scegliere tra diversi tipi di visualizzazioni (tabella, a torta, linea, Area o barra) utilizzando hello **tipo** pulsanti di menu in blocco per Appunti hello. tracciato barra Hello è illustrato di seguito.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Tracciare un istogramma dell'importo delle mance e della relativa variazione in base al numero di passeggeri e all'importo delle corse.
Utilizzare una data di toosample query SQL.

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
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

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


**OUTPUT:** 

![Distribuzione dell'importo delle mance](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Importo della mancia per numero di passeggeri](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Importo della mancia per importo della corsa](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Progettazione di funzionalità, trasformazione e preparazione dei dati per la modellazione
In questa sezione descrive e fornisce codice hello per le procedure utilizzate tooprepare dati per la modellazione di ML. Viene illustrato come hello toodo seguenti attività:

* Ottenere una nuova funzionalità dalla creazione di contenitori per gli orari di trasporto
* Indicizzare e codificare funzionalità categoriche
* Creare oggetti punto etichettato per l'inserimento in funzioni di apprendimento automatico
* Creare un campionamento secondario casuale dei dati hello e dividere il set di training e set di testing
* Ridimensionamento di funzionalità
* Memorizzazione nella cache di oggetti in memoria

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Ottenere una nuova funzionalità dalla creazione di contenitori per gli orari di trasporto
Questo codice viene illustrato come una nuova funzionalità inserendo ore in fase di traffico toocreate bucket e quindi come toocache hello risultante frame di dati in memoria. Quando sono utilizzati più volte resilienti distribuiti i set di dati (RDDs) e frame di dati, la memorizzazione nella cache comporta tempi di esecuzione tooimproved. Di conseguenza, nella cache RDDs e frame di dati in varie fasi in questa procedura dettagliata hello. 

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

**OUTPUT:** 

126050

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a>Indicizzare e codificare funzionalità categoriche per l'inserimento in funzioni di modellazione
Questa sezione viene illustrato come tooindex o codificare categorica funzionalità per l'input nel hello funzioni di modellazione. modellazione Hello e funzioni di MLlib richiedono funzionalità con dati di input categorici toobe indicizzato o codificato toouse precedente di stima. A seconda del modello di hello, è necessario tooindex o codificarli in modi diversi:  

* **Modellazione basata sulla struttura ad albero** richiede toobe categorie codificati come valori numerici (ad esempio, una funzionalità costituita da tre categorie potrebbe essere stata codificata con 0, 1, 2). Questo avviene tramite la funzione [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) di MLlib, Questa funzione consente di codificare una colonna stringa della colonna di etichette tooa di indici di etichetta che sono ordinati per le frequenze di etichetta. Sebbene indicizzato con i valori numerici per l'input e la gestione dei dati, algoritmi di hello basati sulla struttura ad albero possono essere tootreat specificato in modo appropriato come categorie. 
* **Modelli di regressione lineare e di Logistic** richiedono la scelta di una codifica, in cui, ad esempio, una funzionalità costituita da tre categorie può essere espanso in tre colonne di funzionalità, con ogni contiene 0 o 1 a seconda della categoria di hello di un'osservazione. Fornisce MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funzione toodo hot una codifica. Questo codificatore esegue il mapping di una colonna della colonna di etichetta indici tooa di vettori binari, con al massimo uno a valore singolo. Questa codifica consente di utilizzare gli algoritmi che prevedono le funzionalità di valori numeriche, ad esempio la regressione logistica, funzionalità toocategorical toobe applicato.

Ecco hello tooindex codice e codificare funzionalità organizzato per categorie:

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

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

**OUTPUT:**

Tempo impiegato tooexecute di sopra di: 1,28 secondi

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Creare oggetti punto etichettato per l'inserimento in funzioni di apprendimento automatico
In questa sezione contiene codice che illustra come di tipo di dati di testo categorico tooindex come etichetta punto dati e codificarli in modo che possano essere utilizzati tootrain e test MLlib regressione logistica e altri modelli di classificazione. Gli oggetti punto etichettato sono RDD (Resilient Distributed Dataset) formattati come richiesto per i dati di input dalla maggior parte degli algoritmi di apprendimento automatico in MLlib. Un [punto etichettato](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) è un vettore locale, che può essere denso o sparso, associato a un'etichetta o a una risposta.  

In questa sezione contiene codice che illustra come dati di testo categorico tooindex come un [etichetta punto](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) tipo di dati e la codifica in modo che possano essere utilizzati tootrain e test MLlib regressione logistica e altri modelli di classificazione. Gli oggetti punto etichettato RDD (Resilient Distributed Dataset) costituiti da un'etichetta, o variabile di destinazione/risposta, e da un vettore di funzionalità. Questo formato è richiesto come input dalla maggior parte degli algoritmi di apprendimento automatico in MLlib.

Ecco hello tooindex codice e codificare le funzionalità di testo per la classificazione binaria.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
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
Questo codice crea un campionamento casuale dei dati di hello (25% viene utilizzato qui). Anche se non sono richiesto per questo esempio a causa delle dimensioni toohello di hello set di dati, viene illustrato come è possibile campionare qui a per sapere come toouse per il proprio problema quando necessario. Nei campioni di grandi dimensioni questa operazione permette di risparmiare molto tempo durante il training dei modelli. Successivamente è suddivisa: esempio hello una parte di training (75%) e un test toouse parte (25 %)) nella classificazione e creazione di modelli di regressione.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

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

**OUTPUT:**

Tempo impiegato tooexecute di sopra di: 0,24 secondi

### <a name="feature-scaling"></a>Ridimensionamento di funzionalità
Funzionalità di scalabilità, noto anche come normalizzazione dei dati, si assicura che le funzionalità con ampiamente i valori sono non specificato un numero eccessivo pesare nella funzione obiettivo hello. codice per la funzionalità scalabilità Hello Usa hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) varianza di toounit tooscale hello funzionalità. Viene fornito da MLlib per l'uso nella regressione lineare con la discesa del gradiente stocastica (SGD), un algoritmo molto diffuso per il training di una vasta gamma di modelli di apprendimento automatico, come la regressione regolarizzata o le macchine a vettori di supporto (SVM).

> [!NOTE]
> È stato trovato il ridimensionamento di hello LinearRegressionWithSGD algoritmo toobe toofeature sensibili.
> 
> 

Ecco le variabili di tooscale codice hello per l'utilizzo con l'algoritmo SGD lineare di regolarizzazione hello.

    # FEATURE SCALING

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

**OUTPUT:**

Tempo impiegato tooexecute di sopra di: 13.17 secondi

### <a name="cache-objects-in-memory"></a>Memorizzazione nella cache di oggetti in memoria
tempo di Hello impiegato per il training e il testing di algoritmi di Machine Learning è possibile ridurre la memorizzazione nella cache gli oggetti frame di dati di input hello utilizzati per la classificazione, regressione, e con funzionalità di scalabilità.

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

**OUTPUT:** 

Tempo impiegato tooexecute di sopra di: 0,15 secondi

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Uso di modelli di classificazione binaria per prevedere se viene lasciata o meno una mancia
In questa sezione viene illustrato come utilizzare tre modelli per attività di classificazione binaria hello di stima di un suggerimento viene pagato per un itinerario taxi o meno. modelli di Hello presentati sono:

* Regressione logistica regolarizzata. 
* Modello di foresta casuale.
* Alberi con boosting a gradienti.

Ogni sezione di codice di compilazione del modello è suddivisa in passaggi: 

1. **training del modello** con un set di parametri
2. **Valutazione del modello** su un set di dati di test con metriche
3. **Salvataggio del modello** in un BLOB per l'uso in futuro

### <a name="classification-using-logistic-regression"></a>Classificazione tramite regressione logistica
codice Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di regressione logistica con [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) che esegue una stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa DataSet.

**Training modello di regressione logistica hello utilizzando CV e hyperparameter sweep**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**OUTPUT:** 

Coefficienti: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]

Intercetta: -0,0111216486893

Tempo impiegato tooexecute di sopra di: 14.43 secondi

**Valutazione del modello di classificazione binaria hello con le metriche standard**

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

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


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**OUTPUT:** 

Area in PR = 0,985297691373

Area in ROC = 0,983714670256

Statistiche di riepilogo

Precisione = 0,984304060189

Richiamo = 0,984304060189

Punteggio F1 = 0,984304060189

Tempo impiegato tooexecute di sopra di: 57.61 secondi

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

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
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


**OUTPUT:**

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a>Classificazione tramite foresta casuale
codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di foresta casuale che stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa set di dati.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

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
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
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

**OUTPUT:**

Area in ROC = 0,985297691373

Tempo impiegato tooexecute di sopra di: 31.09 secondi

### <a name="gradient-boosting-trees-classification"></a>Classificazione tramite alberi con boosting a gradienti
codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di alberi boosting sfumatura che stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa set di dati.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
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


**OUTPUT:**

Area in ROC = 0,985297691373

Tempo impiegato tooexecute di sopra di: 19.76 secondi

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a>Uso di modelli regressivi per prevedere l'importo delle mance per le corse in taxi
In questa sezione viene illustrato come utilizzare tre modelli per attività di regressione hello di stima quantità hello del suggerimento hello a pagamento per un itinerario taxi basato sulle altre funzionalità di suggerimento. modelli di Hello presentati sono:

* Regressione lineare regolarizzata
* Foresta casuale
* Alberi con boosting a gradienti.

Questi modelli sono stati descritti introduzione hello. Ogni sezione di codice di compilazione del modello è suddivisa in passaggi: 

1. **training del modello** con un set di parametri
2. **Valutazione del modello** su un set di dati di test con metriche
3. **Salvataggio del modello** in un BLOB per l'uso in futuro

### <a name="linear-regression-with-sgd"></a>Regressione lineare con SGD
Hello codice in questa sezione viene illustrato come toouse scalato funzionalità tootrain una regressione lineare che usa descent con sfumatura stocastica (SGD) per l'ottimizzazione, e come tooscore, valutare e salvare il modello di hello in archiviazione Blob di Azure (WASB).

> [!TIP]
> Nella nostra esperienza, si possono verificare problemi con convergenza hello dei modelli LinearRegressionWithSGD e parametri necessario toobe modificato/ottimizzata con attenzione per ottenere un modello valido. Il ridimensionamento delle variabili può essere molto utile per la convergenza. 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

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

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**OUTPUT:**

Coefficienti: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]

Intercetta: -0,853872718283

RMSE = 1,24190115863

R-sqr = 0,608017146081

Tempo impiegato tooexecute di sopra di: 58.42 secondi

### <a name="random-forest-regression"></a>Regressione tramite foresta casuale
codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare una regressione foresta casuale che stima quantità suggerimento per dati di andata e ritorno taxi NYC hello.

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
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

**OUTPUT:**

RMSE = 0,891209218139

R-sqr = 0,759661334921

Tempo impiegato tooexecute di sopra di: 49.21 secondi

### <a name="gradient-boosting-trees-regression"></a>Regressione tramite alberi con boosting a gradienti
codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di alberi boosting sfumatura che stima quantità suggerimento per dati di andata e ritorno taxi NYC hello.

**Eseguire il training e valutare**

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**OUTPUT:**

RMSE = 0,908473148639

R-sqr = 0,753835096681

Tempo impiegato tooexecute di sopra di: 34.52 secondi

**Grafico**

*tmp_results* viene registrato come una tabella Hive in una cella precedente hello. I risultati dalla tabella hello vengono visualizzati in hello *sqlResults* frame di dati per il tracciato. Ecco il codice hello

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

Ecco dati hello tooplot codice hello utilizzando server Jupyter hello.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


**OUTPUT:**

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a>Pulire gli oggetti dalla memoria
Utilizzare `unpersist()` toodelete oggetti memorizzati nella cache in memoria.

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a>Percorsi di archiviazione di record dei modelli di hello del consumo e assegnazione dei punteggi
tooconsume e punteggio di un set di dati indipendenti descritto in hello [punteggio e valutare i modelli di apprendimento compilato Spark](machine-learning-data-science-spark-model-consumption.md) argomento, è necessario toocopy e incollare i file i nomi che contiene i modelli di hello salvato creati qui in hello Notebook Jupyter consumo. Di seguito è tooprint codice hello out hello percorsi toomodel file che è necessario non esiste.

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**OUTPUT**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"

## <a name="whats-next"></a>Passaggi successivi
Dopo aver creato i modelli di classificazione e regressione con MlLib Spark hello, si è toolearn pronto come tooscore e valutare questi modelli. Ciao avanzate di esplorazione dei dati e modellazione dives notebook più approfondito in tra la convalida incrociata, hyper-parameter sweep e valutazione del modello. 

**Utilizzo del modello:** toolearn come tooscore e valutare i modelli di classificazione e regressione hello creati in questo argomento, vedere [punteggio e valutare i modelli di apprendimento macchina compilato Spark](machine-learning-data-science-spark-model-consumption.md).

**Convalida incrociata e sweep di iperparametri**: vedere [Esplorazione e modellazione avanzate dei dati con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) per informazioni su come istruire i modelli sulla convalida incrociata e lo sweep di iperparametri

