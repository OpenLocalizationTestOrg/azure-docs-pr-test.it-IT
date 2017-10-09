---
title: aaaData scienza con Scala e Spark in Azure | Documenti Microsoft
description: "Come toouse Scala per supervisione di machine learning attività con hello Spark MLlib e Spark ML pacchetti scalabili in un cluster Azure HDInsight Spark."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a>Analisi scientifica dei dati tramite Scala e Spark in Azure
Questo articolo illustra come toouse Scala per le attività di apprendimento supervisionato macchina con hello MLlib scalabile Spark e Spark ML pacchetti in un cluster Azure HDInsight Spark. Illustra le attività che costituiscono hello hello [il processo di analisi scientifica dei dati](http://aka.ms/datascienceprocess): inserimento di dati e l'esplorazione, visualizzazione, progettazione di funzionalità, modellazione e il consumo di modello. i modelli di Hello nell'articolo hello includono la regressione logistica e lineare, foreste casuali e alberi con Boosting sfumatura (GBTs), inoltre comune tootwo sotto la supervisione attività di machine learning:

* Problema di regressione: stima della quantità di hello suggerimento ($) per un itinerario taxi
* Classificazione binaria: stima di mancia o non mancia (1/0) per una corsa in taxi

processo di modellazione Hello richiede training e valutazione in un set di dati di test e la metrica di accuratezza pertinente. In questo articolo, utili come toostore questi modelli in archiviazione Blob di Azure e come tooscore e valutare le prestazioni predittiva. In questo articolo viene illustrata anche hello argomenti della modalità toooptimize modelli tramite la convalida incrociata e hyper-parameter sweep più avanzati. dati Hello utilizzati sono un esempio di hello 2013 NYC taxi viaggi tariffa set di dati e disponibile in GitHub.

[Scala](http://www.scala-lang.org/), un linguaggio basato su macchina virtuale Java hello integra concetti sul linguaggio funzionale e orientata agli oggetti. È un linguaggio scalabile toodistributed adatta l'elaborazione nel cloud hello, che viene eseguito nei cluster Spark di Azure.

[Spark](http://spark.apache.org/) è un framework di elaborazione parallela open source che supporta in memoria prestazioni di elaborazione tooboost hello delle applicazioni analitica dei dati di grandi dimensioni. motore di elaborazione Spark Hello viene compilato per la velocità, semplicità di utilizzo e analitica sofisticate. Le funzionalità di elaborazione distribuita in memoria rendono Spark uno strumento valido per l'esecuzione di algoritmi iterativi in calcoli grafici e di Machine Learning. Hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) pacchetto fornisce un set di API di alto livello basate su dati frame che consentono di creare e ottimizzare pratiche di machine learning pipeline uniforme. [MLlib](http://spark.apache.org/mllib/) è libreria di apprendimento scalabile di macchine di Spark, che offre funzionalità di modellazione toothis di ambiente distribuito.

[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) è offerta ospitato da Azure hello di Spark open source. Include inoltre il supporto per la Jupyter Scala notebook nel cluster Spark hello e può eseguire Spark SQL Query interattive tootransform, filtrare e visualizzare i dati archiviati nell'archiviazione Blob di Azure. Hello Scala frammenti di codice in questo articolo che forniscono soluzioni hello e visualizzare grafici rilevanti hello dati hello toovisualize eseguiti in server Jupyter notebook installato nel cluster Spark hello. passaggi di modellazione Hello in questi argomenti contengono codice che mostra come tootrain, valutare, salvare e utilizzare ogni tipo di modello.

passaggi di installazione Hello e il codice in questo articolo sono per Azure HDInsight 3.4 Spark 1.6. Tuttavia, hello codice in questo articolo e nel hello [Scala server Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) sono generici e dovrebbe funzionare in un cluster Spark. installazione del cluster di Hello e operazioni di gestione potrebbero essere leggermente diversi rispetto a quanto mostrato in questo articolo se non si utilizza HDInsight Spark.

> [!NOTE]
> Per un argomento che illustra come toouse Python anziché Scala toocomplete attività per un processo di analisi scientifica dei dati end-to-end, vedere [analisi scientifica dei dati utilizzando Spark in Azure HDInsight](machine-learning-data-science-spark-overview.md).
> 
> 

## <a name="prerequisites"></a>Prerequisiti
* È necessario disporre di una sottoscrizione di Azure. Se non è già disponibile, [ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* È necessario un hello di toocomplete cluster Azure HDInsight 3.4 Spark 1.6, seguire le procedure seguenti. toocreate un cluster, vedere le istruzioni di hello in [Introduzione: creare Apache Spark in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Impostare il tipo di cluster hello e versione hello **Seleziona tipo di Cluster** menu.

![Configurazione del tipo di cluster HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

Per una descrizione dei dati di andata e ritorno di hello NYC taxi e istruzioni su come il codice da un server Jupyter notebook nel cluster Spark hello tooexecute, vedere le sezioni pertinenti hello in [panoramica dell'analisi scientifica dei dati utilizzando Spark in Azure HDInsight](machine-learning-data-science-spark-overview.md).  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Eseguire il codice di Scala da un server Jupyter notebook nel cluster Spark hello
È possibile avviare un server Jupyter notebook da hello portale di Azure. Trovare cluster Spark hello nel dashboard e quindi fare clic su, pagina di gestione di hello tooenter per il cluster. Successivamente, fare clic su **dashboard del Cluster**, quindi fare clic su **server Jupyter Notebook** notebook hello tooopen associato al cluster Spark hello.

![Dashboard del cluster e notebook Jupyter](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

È anche possibile accedere ai notebook di Jupyter da https://&lt;clustername&gt;.azurehdinsight.net/jupyter. Sostituire *clustername* con nome hello del cluster. È necessario password hello per amministratore account tooaccess hello Jupyter notebook.

![Passare notebook tooJupyter utilizzando il nome del cluster hello](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

Selezionare **Scala** toosee una directory con alcuni esempi di predisporre notebook tale hello utilizzare API PySpark. Hello modellazione di esplorazione e di punteggio usando notebook Scala.ipynb che contiene esempi di codice hello per questo gruppo di argomenti di Spark è disponibile in [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).

È possibile caricare notebook hello direttamente da GitHub toohello server Jupyter Notebook nel cluster di Spark. Nella home page Jupyter, fare clic su hello **caricare** pulsante. In Esplora file hello incollare hello GitHub (contenuto non elaborato) URL di notebook Scala hello e quindi fare clic su **aprire**. blocco appunti Scala Hello sono disponibile in hello URL seguente:

[Exploration-Modeling-and-Scoring-using-Scala.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a>Installazione: contesti di Spark e Hive predefiniti, magic Spark e librerie Spark
### <a name="preset-spark-and-hive-contexts"></a>Contesti predefiniti di Spark e Hive
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


kernel Spark Hello forniti con i notebook Jupyter sono preimpostati contesti. Tooexplicitly set hello Spark Hive contesti o non è necessario prima di iniziare con un'applicazione hello che si sta sviluppando. Hello contesti predefiniti sono:

* `sc` per SparkContext
* `sqlContext` per HiveContext

### <a name="spark-magics"></a>Magic di Spark
Hello kernel Spark fornisce alcuni predefinite "magics", che sono comandi speciale che è possibile chiamare con `%%`. Due di questi comandi vengono utilizzati nei seguenti esempi di codice hello.

* `%%local`Specifica che il codice hello nelle righe successive verrà eseguito localmente. codice Hello deve essere valido codice di Scala.
* `%%sql -o <variable name>`: esegue una query Hive su `sqlContext`. Se hello `-o` parametro viene passato, il risultato di hello di hello query è persistente nel hello `%%local` contesto Scala di un frame di dati di Spark.

Per ulteriori informazioni su kernel hello per server Jupyter notebook e i relativi predefiniti "magics" che è stata chiamata con `%%` (ad esempio, `%%local`), vedere [cluster kernel disponibile per i notebook Jupyter con HDInsight Spark Linux HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

### <a name="import-libraries"></a>Importare le librerie
Importare hello Spark MLlib e altre librerie, occorre utilizzando hello seguente codice.

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a>Inserimento di dati
Hello hello il processo di analisi scientifica dei dati è innanzitutto i dati di hello tooingest che si desidera tooanalyze. Hello dati trasferiti da origini esterne o sistemi in cui si trova nell'ambiente di esplorazione e modellazione di dati. In questo articolo di inserimento dei dati di hello sono un esempio di 0,1% unita in join di hello taxi di andata e ritorno e tariffa file (archiviato come file tsv). ambiente di esplorazione e modellazione di dati Hello è Spark. In questa sezione contiene hello toocomplete di codice hello serie di attività:

1. Impostare i percorsi di directory per l'archiviazione di dati e modelli.
2. Lettura in hello set di dati input (archiviati come file tsv).
3. Definire uno schema di dati hello e hello pulita.
4. Creare un frame di dati puliti e memorizzarli nella cache.
5. Registrare dati hello come una tabella temporanea in SQLContext.
6. Una query sulla tabella hello e importare i risultati di hello in un frame di dati.

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a>Impostare percorsi di directory per i percorsi di archiviazione in archiviazione BLOB di Azure
Spark possono leggere e scrivere tooAzure nell'archiviazione Blob. È possibile utilizzare i dati esistenti tooprocess Spark e quindi archiviare nuovamente i risultati di hello nell'archiviazione Blob.

i modelli di toosave o file nell'archiviazione Blob, è necessario tooproperly specificare il percorso di hello. Contenitore predefinito di hello riferimento collegato cluster Spark toohello utilizzando un percorso che inizia con `wasb:///`. Fare riferimento ad altre posizioni usando `wasb://`.

Hello nell'esempio di codice seguente specifica la posizione di hello di hello toobe di dati di input letti e hello percorso tooBlob spazio di archiviazione cluster Spark toohello collegati in cui verrà salvato il modello di hello.

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a>Importare i dati, creare un RDD e definire un frame di dati in base toohello schema
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING toohello SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Output:**

Cella di tempo toorun hello: 8 secondi.

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a>Una query sulla tabella hello e importare i risultati in un frame di dati
Quindi, nella tabella query hello per tariffa passeggeri e il suggerimento dati. filtrare i dati danneggiati e americane; e stampa di più righe.

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

**Output:**

| fare_amount | passenger_count | tip_amount | tipped |
| --- | --- | --- | --- |
|        13,5 |1.0 |2,9 |1.0 |
|        16,0 |2.0 |3.4 |1.0 |
|        10,5 |2.0 |1.0 |1.0 |

## <a name="data-exploration-and-visualization"></a>Visualizzazione ed esplorazione dei dati
Dopo aver portato dati hello in Spark, hello passaggio successivo per il processo di analisi scientifica dei dati hello è toogain una comprensione più approfondita dei dati di hello tramite l'esplorazione e la visualizzazione. In questa sezione è esaminare dati taxi hello tramite query SQL. Quindi, Importa hello risultati in un tooplot frame di dati hello le variabili di destinazione e le funzionalità potenziali per l'esame visivo utilizzando hello auto-visualizzazione di Jupyter.

### <a name="use-local-and-sql-magic-tooplot-data"></a>Utilizzare locale e i dati di magic tooplot SQL
Per impostazione predefinita, è disponibile nel contesto di hello della sessione hello in modo permanente in nodi di lavoro hello output di hello di ogni frammento di codice da eseguire da un server Jupyter notebook. Se si desidera toosave un nodi di lavoro di andata e ritorno toohello per ogni calcolo e, se tutti hello i dati necessari per il calcolo è disponibile in locale nel nodo del server Jupyter hello (ovvero nodo head hello), è possibile utilizzare hello `%%local` particolare codice hello toorun frammento di codice server Jupyter hello.

* **Magic SQL** (`%%sql`). Hello kernel HDInsight Spark supporta SQLContext query HiveQL facile inline. Hello (`-o VARIABLE_NAME`) argomento persiste output di hello di query SQL hello come frame di dati Pandas server Jupyter hello. Ciò significa che sarà disponibile in modalità locale hello.
* `%%local` **magic**. Hello `%%local` magic esegue codice hello in locale nel server Jupyter hello hello nodo head del cluster HDInsight hello. In genere, si utilizza `%%local` magic in combinazione con hello `%%sql` magic con hello `-o` parametro. Hello `-o` parametro sarebbe mantenere l'output di hello di query SQL hello in locale, quindi `%%local` magic attiverà set successivo di hello di toorun frammento di codice in locale sull'output di hello delle query SQL hello in modo permanente in locale.

### <a name="query-hello-data-by-using-sql"></a>Eseguire query sui dati hello tramite SQL
Questa query recupera trip taxi hello tariffa quantità, conteggio passeggeri e quantità di suggerimento.

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

Nel seguente codice di hello, hello `%%local` magic crea un frame di dati locale, sqlResults. È possibile utilizzare sqlResults tooplot usando matplotlib.

> [!TIP]
> Il magic local viene usato più volte in questo articolo. Se il set di dati è grande, per esempio toocreate un frame di dati che può adattarsi alla memoria locale.
> 
> 

### <a name="plot-hello-data"></a>Dati hello tracciato
È possibile tracciare utilizzando codice Python dopo il frame di dati hello è nel contesto locale come frame di dati Pandas.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 kernel Spark Hello Visualizza automaticamente l'output di hello delle query SQL (HiveQL) dopo l'esecuzione di codice hello. È possibile scegliere tra diversi tipi di visualizzazioni:

* Tabella
* Grafico a torta
* Grafico a linee
* Area
* Grafico a barre

Ecco i dati di hello tooplot codice hello:

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


**Output:**

![Istogramma degli importi delle mance](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Importo della mancia per numero di passeggeri](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Importo della mancia per importo della corsa](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a>Creare le funzionalità e trasformare le funzionalità, quindi preparare i dati per l'input in funzioni di modellazione
Per le funzioni di modellazione basata sulla struttura ad albero da Spark ML e MLlib, è possibile tooprepare destinazione e le funzionalità usando varie tecniche, ad esempio binning, indicizzazione, hot una codifica e la vettorializzazione. Di seguito sono toofollow procedure hello in questa sezione:

1. Ottenere una nuova funzionalità dalla **creazione di contenitori** per gli orari di trasporto.
2. Applicare **l'indicizzazione e hot una codifica** toocategorical funzionalità.
3. **Esempio e split hello set di dati** in frazioni di training e di test.
4. **Specificare le funzionalità e la variabile di training**e creare RDD (resilient distributed dataset )o frame di dati con punti etichettati per training e test indicizzati o con codifica one-hot.
5. Automaticamente **classificare e vettorizzare funzionalità e le destinazioni** toouse come input per i modelli di machine learning.

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Ottenere una nuova funzionalità dalla creazione di contenitori per gli orari di trasporto
Questo codice viene illustrato come una nuova funzionalità inserendo ore in fase di traffico toocreate bucket e come toocache hello risultante frame di dati in memoria. In cui i frame RDDs e i dati vengono utilizzati più volte, la memorizzazione nella cache comporta tempi di esecuzione tooimproved. Di conseguenza, si saranno memorizza nella cache di frame di dati e RDDs in fasi diverse dell'hello seguire le procedure seguenti.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a>Indicizzare e applicare la codifica one-hot per le funzionalità categoriche
modellazione Hello e funzioni di MLlib richiedono funzionalità con dati di input categorici toobe indicizzato o codificato toouse precedente di stima. In questa sezione illustra come tooindex o codificare categorica funzionalità per l'input nel hello funzioni di modellazione.

È necessario tooindex o codificare i modelli in modi diversi, a seconda del modello di hello. Ad esempio, i modelli di regressione logistica e lineare richiedono codifica one-hot. Ad esempio, una funzionalità con tre categorie può essere espansa in tre colonne di funzionalità. Ogni colonna contiene 0 o 1 a seconda della categoria di hello di un'osservazione. MLlib fornisce hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funzione per la scelta di una codifica. Questo codificatore esegue il mapping di una colonna della colonna di etichetta indici tooa di vettori binari con al massimo uno a valore singolo. Con questa codifica, gli algoritmi che prevedono le funzionalità di valori numeriche, ad esempio la regressione logistica, possono essere applicato toocategorical funzionalità.

Qui si trasforma esempi tooshow solo quattro variabili sono stringhe di caratteri. È possibile indicizzare come variabili categoriche anche altre variabili, ad esempio il giorno della settimana, rappresentate da valori numerici.

Per l'indicizzazione usare la funzione `StringIndexer()` e per la codifica one-hot e le funzioni `OneHotEncoder()` di MLlib. Ecco hello tooindex codice e codificare funzionalità organizzato per categorie:

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Output:**

Cella di hello toorun ora: 4 secondi.

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a>Esempio e split hello set di dati in frazioni di training e di test
Questo codice crea un campionamento casuale dei dati hello (25%, in questo esempio). Anche se il campionamento non è necessario per questo esempio a causa delle dimensioni toohello hello del set di dati, hello articolo illustra come è possibile campionare in modo da sapere come toouse per altri problemi quando necessario. Nei campioni di grandi dimensioni questa operazione permette di risparmiare molto tempo durante il training dei modelli. Successivamente, suddividere l'esempio hello in una parte di training (75%, in questo esempio) e un test (25%, in questo esempio) toouse classificazione e la modellazione basata sulla parte.

Aggiungere una riga tooeach numero casuale (compreso tra 0 e 1) (in una colonna "rand") che può essere utilizzati tooselect convalida incrociata riduzioni durante il training.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Output:**

Cella di tempo toorun hello: 2 secondi.

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a>Specificare le funzionalità e la variabile di training e quindi creare RDD o frame di dati con punti etichettati per training e test indicizzati o con codifica one-hot.
In questa sezione contiene codice che mostra come scegliere il tipo di dati, dati di testo categorico tooindex come un'etichetta e codificarli in modo è possibile utilizzare tootrain e test di regressione logistica MLlib e altri modelli di classificazione. Gli oggetti punto etichettato sono RDD formattati come richiesto per i dati di input dalla maggior parte degli algoritmi di Machine Learning in MLlib. Un [punto etichettato](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) è un vettore locale, che può essere denso o sparso, associato a un'etichetta o a una risposta.

In questo codice, specificare variabile (dipendente) di destinazione hello e hello funzionalità toouse tootrain modelli. Creare quindi RDD o frame di dati con punti etichettati per training e test indicizzati o con codifica one-hot.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Output:**

Cella di hello toorun ora: 4 secondi.

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a>Classificare automaticamente e vettorizzare toouse funzionalità e le destinazioni come input per i modelli di machine learning
Usare Spark ML toocategorize hello destinazione e le funzionalità toouse nelle funzioni di modellazione basata sulla struttura ad albero. codice Hello completa due attività:

* Crea una destinazione per la classificazione binaria assegnando un valore pari a 0 o 1 punto dati tooeach compreso tra 0 e 1, utilizzando un valore di soglia di 0,5.
* Classifica automaticamente le funzionalità. Se il numero di hello di valori numerici distinti per tutte le funzionalità è minore di 32, tale funzionalità è stata categorizzata.

Ecco il codice hello per le attività.

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a>Modello di classificazione binaria: prevede se deve essere lasciata una mancia
In questa sezione è creare tre tipi di toopredict di modelli di classificazione binaria o meno un suggerimento deve essere a pagamento:

* Oggetto **modello di regressione logistica** utilizzando hello Spark ML `LogisticRegression()` (funzione)
* Oggetto **il modello di classificazione di foresta casuale** utilizzando hello Spark ML `RandomForestClassifier()` (funzione)
* A **sfumatura modello di classificazione albero boosting** utilizzando hello MLlib `GradientBoostedTrees()` (funzione)

### <a name="create-a-logistic-regression-model"></a>Creare un modello di regressione logistica
Successivamente, creare un modello di regressione logistica usando hello Spark ML `LogisticRegression()` (funzione). Si crea il modello di hello la compilazione di codice in una serie di passaggi:

1. **Modello di training hello** dati con un set di parametri.
2. **Valutazione del modello di hello** su un set di dati di test con le metriche.
3. **Salvare il modello di hello** nell'archiviazione Blob per un utilizzo futuro.
4. **Modello di punteggio hello** rispetto ai dati di test.
5. **Tracciare i risultati di hello** con ricevitore operativo curve caratteristica (ROC).

Ecco il codice hello per queste procedure:

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

Caricare, assegnare un punteggio e salvare i risultati di hello.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


**Output:**

ROC sui dati di test = 0.9827381497557599

Utilizzare Python locale Pandas frame tooplot hello ROC curva dei dati.

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
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


**Output:**

![Curva ROC per mancia o non mancia](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a>Creare un modello di classificazione di foresta casuale
Successivamente, creare un modello di classificazione di foresta casuale usando hello Spark ML `RandomForestClassifier()` funzione e quindi valutare il modello di hello sui dati di test.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


**Output:**

ROC sui dati di test = 0.9847103571552683

### <a name="create-a-gbt-classification-model"></a>Creare un modello di classificazione GBT
Successivamente, creare un modello di classificazione GBT utilizzando del MLlib `GradientBoostedTrees()` funzione e quindi valutare il modello di hello sui dati di test.

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


**Output:**

Area sotto la curva ROC = 0,9846895479241554

## <a name="regression-model-predict-tip-amount"></a>Modello di regressione: stimare l'importo della mancia
In questa sezione creare due tipi di quantità di regressione modelli toopredict hello Suggerimento:

* Oggetto **modello di regressione lineare regolarizzata** utilizzando hello Spark ML `LinearRegression()` (funzione). Verranno salvate modello hello e valutare il modello di hello sui dati di test.
* A **modello di regressione dell'albero boosting sfumatura** utilizzando hello Spark ML `GBTRegressor()` (funzione).

### <a name="create-a-regularized-linear-regression-model"></a>Creare un modello di regressione lineare regolarizzata
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Output:**

Cella di tempo toorun hello: 13 secondi.

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


**Output:**

R-sqr sui dati di test = 0.5960320470835743

Query successiva, hello i risultati dei test come frame di dati e utilizzare toovisualize AutoVizWidget e matplotlib.

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

codice Hello crea un frame di dati locale dall'output di hello query e vengono tracciati dati hello. Hello `%%local` magic crea un frame di dati locale, `sqlResults`, che è possibile utilizzare tooplot con matplotlib.

> [!NOTE]
> Questo magic Spark viene usato più volte in questo articolo. Se è grande quantità di hello di dati, si deve esempio toocreate un frame di dati che può adattarsi alla memoria locale.
> 
> 

Creare tracciati usando matplotlib di Python.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

**Output:**

![Importo della mancia: effettivo rispetto a stimato](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a>Creare un modello di regressione con boosting a gradienti
Creare un modello di regressione GBT utilizzando hello Spark ML `GBTRegressor()` funzione e quindi valutare il modello di hello sui dati di test.

[Alberi con boosting a gradienti](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT, Gradient boosted tree) sono insiemi di alberi delle decisioni. GBTs train alberi delle decisioni in modo iterativo toominimize una funzione di perdita. È possibile usare GBT per la classificazione e la regressione. Gli alberi GBT possono gestire funzionalità categoriche, non richiedono il ridimensionamento delle funzionalità e possono rilevare non linearità e interazioni di funzionalità. Possono anche essere usati in un'impostazione di classificazione multiclasse.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


**Output:**

Il valore R-sqr del test è: 0.7655383534596654

## <a name="advanced-modeling-utilities-for-optimization"></a>Utilità di modellazione avanzate per l'ottimizzazione
In questa sezione, usare le utilità di Machine Learning che gli sviluppatori spesso usano per l'ottimizzazione del modello. In particolare, è possibile ottimizzare i modelli di Machine Learning in tre diversi modi usando lo sweep dei parametri e la convalida incrociata:

* Suddividere i dati di hello in set di training e la convalida, ottimizzare il modello di hello tramite hyper-parameter sweep in un set di training e valutare in un set di convalida (regressione)
* Ottimizzare il modello di hello utilizzando la convalida incrociata e hyper-parameter sweep dalla funzione di Machine Learning Spark CrossValidator (classificazione binaria)
* Ottimizzare il modello di hello tramite codice personalizzato di convalida incrociata e sweep di parametri toouse qualsiasi di machine learning set di funzioni e parametri (regressione)

**La convalida incrociata** è una tecnica che consente di valutare l'accuratezza, un modello sottoposto a training su un set di dati noto generalizzerà toopredict hello funzionalità dei set di dati in cui si è ancora stato eseguito. Hello idea generale di questa tecnica è che un modello è stato sottoposto a training su un set di dati di dati noti e hello accuratezza di esecuzione delle stime viene quindi testata in un set di dati indipendente. Un'implementazione comune è toodivide un set di dati in *k*-Raggruppa e quindi eseguire il training del modello di hello in uno schema round robin su almeno una delle sezioni hello.

**Ottimizzazione di Hyper-parametro** hello problema della scelta di un set di hyper-parametri per un algoritmo di apprendimento, in genere con l'obiettivo di hello ottimizzare una misura delle prestazioni dell'algoritmo hello in un set di dati indipendente. Hyper-parameter è un valore che è necessario specificare all'esterno di routine di training modello di hello. Presupposti sui valori dei parametri di hyper possono influire sulla flessibilità hello e sull'accuratezza del modello di hello. Gli alberi delle decisioni avere hyper-parametri, ad esempio, ad esempio hello desiderato profondità e numero di foglie nell'albero hello. È necessario impostare un termine di penalità per errata classificazione per macchine a vettori di supporto (SVM).

Un'ottimizzazione comune delle modalità tooperform hyper parametro è toouse una ricerca di griglia, detto anche un **sweep di parametri**. In una ricerca di griglia, viene eseguita una ricerca completa tramite i valori hello di un subset specificato di spazio di hyper-parametro hello per un algoritmo di apprendimento. La convalida incrociata può fornire un toosort metrica prestazioni out ottimale hello prodotto dall'algoritmo di ricerca di hello griglia. Se si utilizza lo sweep dei parametri di hyper convalida incrociata, è possibile consentire l'overfitting dati tootraining modello problemi di limite. In questo modo, il modello di hello mantiene hello capacità tooapply toohello generale set di dati dalla quale hello sono stati estratti i dati di training.

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a>Ottimizzare un modello di regressione lineare con sweep di iperparametri
Successivamente, suddividere i dati in set di training e la convalida, utilizzare hyper-parameter sweep in un training set modello hello toooptimize e valutare in un set di convalida (regressione lineare).

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


**Output:**

Il valore R-sqr del test è: 0.6226484708501209

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a>Ottimizzare il modello di classificazione binaria hello utilizzando la convalida incrociata e hyper-parameter sweep
In questa sezione viene illustrato come toooptimize una classificazione binaria del modello tramite la convalida incrociata e hyper-parameter sweep. Questo metodo utilizza hello Spark ML `CrossValidator` (funzione).

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Output:**

Cella di tempo toorun hello: 33 secondi.

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a>Ottimizzare il modello di regressione lineare di hello utilizzando codice personalizzato di convalida incrociata e sweep di parametri
Successivamente, ottimizzare il modello di hello utilizzando codice personalizzato e identificare i parametri del modello migliori hello tramite criterio hello di precisione più elevata. Quindi, creare modello finale hello, valutare hello modello sui dati di test e salvare il modello di hello nell'archiviazione Blob. Infine, caricare il modello di hello, assegnare un punteggio dati di test e valutare l'accuratezza.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


**Output:**

Cella di tempo toorun hello: 61 secondi.

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a>Usare automaticamente i modelli di Machine Learning compilati con Spark con Scala
Per una panoramica degli argomenti che consentono di eseguire attività di hello che costituiscono il processo di analisi scientifica dei dati hello in Azure, vedere [processo di analisi scientifica dei dati di Team](http://aka.ms/datascienceprocess).

[Procedure dettagliate di processo di analisi scientifica dei dati di Team](data-science-process-walkthroughs.md) vengono descritte altre procedure dettagliate end-to-end che illustrano i passaggi hello in hello Team processo di analisi scientifica dei dati per scenari specifici. procedure dettagliate di Hello anche illustrano come toocombine cloud e locali strumenti e servizi in un flusso di lavoro o la pipeline di toocreate un'applicazione intelligente.

[Assegnare un punteggio i modelli di apprendimento compilato Spark](machine-learning-data-science-spark-model-consumption.md) Mostra come toouse Scala codice tooautomatically caricare e assegnare un punteggio nuovi set di dati con i modelli di apprendimento compilato in Spark e salvata nell'archiviazione Blob di Azure. È possibile seguire le istruzioni di hello purché esista e sostituire semplicemente hello codice Python con codice di Scala in questo articolo per il consumo automatico.

