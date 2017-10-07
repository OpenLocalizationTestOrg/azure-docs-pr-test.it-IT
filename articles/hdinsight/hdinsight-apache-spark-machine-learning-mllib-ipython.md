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
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a>Usare Spark MLlib toobuild un machine learning applicazione e analizzare un set di dati

Informazioni su come toouse Spark **MLlib** toocreate a machine learning applicazione toodo semplice analisi predittive su un set di dati aperti. Dalle librerie di Machine Learning integrate di Spark, questo esempio usa la *classificazione* tramite la regressione logistica. 

> [!TIP]
> Questo esempio è disponibile anche come notebook Jupyter su un cluster Spark (Linux) creato in HDInsight. esperienza notebook Hello consente di eseguire frammenti di codice Python hello dal blocco appunti hello stesso. esercitazione di hello toofollow all'interno di un blocco note, creare un Spark cluster e avviare un server Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`). Eseguire quindi il blocco note hello **Spark Machine Learning - analisi predittiva su dati di ispezione di cibo utilizzando MLlib.ipynb** in hello **Python** cartella.
>
>

MLlib è una libreria Spark di base che fornisce diverse utilità che agevolano le attività di Machine Learning, incluse utilità adatte a:

* classificazione
* Regressione
* Clustering
* Modellazione di argomenti
* Scomposizione di valori singolari e analisi in componenti principali
* Testing e calcolo ipotetici di statistiche di esempio

## <a name="what-are-classification-and-logistic-regression"></a>Che cosa sono la classificazione e regressione logistica?
*Classificazione*comune è un numero di machine learning, attività, è il processo di hello di ordinamento dei dati di input in categorie. È il processo di hello di un toofigure algoritmo di classificazione come tooassign "etichette" tooinput dati forniti. Ad esempio, è possibile pensare di un algoritmo di apprendimento automatico che accetta le informazioni come input e viene diviso hello stock in due categorie: scorte che è necessario vendere e che è consigliabile mantenere.

La regressione logistica è algoritmo hello utilizzato per la classificazione. L'API di regressione logistica di Spark è utile per la *classificazione binaria*, ovvero la classificazione di dati di input in uno di due gruppi. Per altre informazioni sulle regressioni logistiche, vedere [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).

In sintesi, hello di regressione logistica genera un *funzione logistica* che può essere utilizzato toopredict hello probabilità appartiene un vettore di input in un gruppo o altri hello.  

## <a name="predictive-analysis-example-on-food-inspection-data"></a>Esempio di analisi predittiva dei dati di controllo degli alimenti
In questo esempio, utilizzare tooperform Spark analisi predittiva in dati di ispezione di cibo (**Food_Inspections1.csv**) che è stato acquisito tramite hello [portale dati Città di Chicago](https://data.cityofchicago.org/). Questo set di dati contiene informazioni sui controlli di cibo stabilimento che sono stati eseguiti a Chicago, incluse le informazioni relative a ciascuno di essi, le violazioni di hello trovato (se presente) e hello risultati dell'ispezione hello. file di dati CSV Hello è già disponibile nell'account di archiviazione hello associato al cluster hello **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.

Nei seguenti passaggi hello è sviluppare un modello toosee toopass impiegato o esito negativo di un controllo di alimenti.

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a>Iniziare a creare un'app di Machine Learning con MLlib Spark
1. Da hello [portale di Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello). È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.   
1. Dal Pannello di cluster Spark hello, fare clic su **Dashboard Cluster**, quindi fare clic su **server Jupyter Notebook**. Se richiesto, immettere le credenziali di amministratore hello cluster hello.

   > [!NOTE]
   > È anche possibile raggiungere hello server Jupyter Notebook per il cluster usando hello apertura URL seguente nel browser. Sostituire **CLUSTERNAME** con nome hello del cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. Creare un notebook. Fare clic su **Nuovo** e quindi su **PySpark**.

    ![Creare un notebook Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Creare un nuovo notebook Jupyter")
1. Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled.pynb. Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo.

    ![Specificare un nome per notebook hello](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "specificare un nome per notebook hello")
1. Poiché è stato creato un notebook utilizza il kernel PySpark hello, non è necessario toocreate i contesti in modo esplicito. contesti di Spark e Hive Hello vengono automaticamente creati automaticamente quando si esegue prima cella di codice hello. È possibile iniziare a compilare i machine learning applicazione tramite l'importazione di tipi di hello necessari per questo scenario. toodo in tal caso, posizionare il cursore hello nella cella hello e premere **MAIUSC + INVIO**.

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a>Creare un frame di dati di input
È possibile utilizzare `sqlContext` tooperform trasformazioni ai dati strutturati. Hello prima attività consiste dati di esempio hello tooload ((**Food_Inspections1.csv**)) in un database SQL Spark *dataframe*.

1. Poiché i dati non elaborati hello sono in un formato CSV, è necessario toouse hello Spark contesto toopull ogni riga del file hello in memoria come testo non strutturato. è quindi utilizzare tooparse di libreria di Python CSV ogni riga singolarmente.

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. File CSV hello è ora disponibile come un RDD.  toounderstand hello lo schema di hello dati, è recuperare una riga da hello RDD.

        inspections.take(1)

    Verrà visualizzato un output simile hello seguente:

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
1. Hello output precedente offre un'idea di schema hello hello del file di input. Include il nome di hello di ogni stabilimento, il tipo hello stabilimento, indirizzo hello, dati hello di controlli hello e la posizione di hello, tra l'altro. Selezionare di seguito alcune colonne che sono utili per l'analisi predittiva e raggruppare i risultati di hello come frame di dati, che è quindi utilizzano toocreate una tabella temporanea.

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. Ora è disponibile un *frame di dati*, `df`, su cui è possibile eseguire l'analisi. È presente anche la tabella temporanea **CountResults**. Sono stati inclusi quattro colonne di interesse nel frame di dati hello: **id**, **nome**, **risultati**, e **violazioni**.

    Verrà visualizzato un piccolo esempio dei dati hello:

        df.show(5)

    Verrà visualizzato un output simile hello seguente:

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

## <a name="understand-hello-data"></a>Comprendere i dati di hello
1. Iniziamo tooget un'idea di cosa contiene il set di dati. Ad esempio, quali sono i valori diversi hello hello **risultati** colonna?

        df.select('results').distinct().show()

    Verrà visualizzato un output simile hello seguente:

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
1. Una visualizzazione rapida ci consente di prendere in considerazione la distribuzione hello di questi risultati. Abbiamo già dati hello in una tabella temporanea **CountResults**. È possibile eseguire hello seguente query SQL su hello tabella tooget una migliore comprensione del modo in cui vengono distribuiti i risultati di hello.

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    Hello `%%sql` magic seguita da `-o countResultsdf` assicura che output di hello di hello query è persistente in locale nel server Jupyter hello (in genere. da nodo a hello a head del cluster hello). output di Hello viene mantenuta come un [Pandas](http://pandas.pydata.org/) frame di dati con hello specificato nome **countResultsdf**.

    Verrà visualizzato un output simile hello seguente:

    ![Output della query SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Output della query SQL")

    Per ulteriori informazioni su hello `%%sql` magic e altri magics disponibili con kernel PySpark hello, vedere [kernel disponibile sui server Jupyter notebook con i cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
1. È inoltre possibile utilizzare Matplotlib, una libreria utilizzata tooconstruct della visualizzazione dei dati, toocreate un tracciato. Perché è necessario creare tracciato hello da hello localmente persistente **countResultsdf** frame di dati, il frammento di codice hello deve iniziare con hello `%%local` magic. In questo modo si garantisce che il codice hello viene eseguito localmente su server Jupyter hello.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Verrà visualizzato un output simile hello seguente:

    ![Output dell'applicazione Machine Learning in Spark: grafico a torta con cinque risultati di controllo differenti](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Output del risultato di Machine Learning in Spark")
1. Come si può notare, un controllo può portare a cinque diversi risultati:

   * Business not located
   * Fail
   * Pass
   * Pass w/ conditions
   * Out of Business

     Segnalare il problema, sviluppare un modello che chiaro risultato hello di un controllo di alimenti, violazioni hello specificato. Poiché la regressione logistica è un metodo di classificazione binaria, rende toogroup senso i dati in due categorie: **esito negativo** e **passare**. Un "passare con condizioni" è ancora un passaggio, pertanto quando si esegue il training del modello di hello, consideriamo hello due risultati equivalenti. Dati con hello altri risultati ("Business non disponibile" o "Out-of-Business") non sono utili in modo è rimuovere il set di training. Deve essere corretto poiché queste due categorie costituiscono una piccola percentuale dei risultati di hello comunque.
1. Ora si passerà alla conversione del frame di dati esistente (`df`) in un nuovo frame di dati in cui ogni controllo è rappresentato come coppia etichetta-violazioni. In questo caso, un'etichetta `0.0` rappresenta un controllo non superato, un'etichetta `1.0` rappresenta un controllo superato e un'etichetta `-1.0` rappresenta altri risultati, È escludere tali altri risultati per il calcolo di frame di dati nuovi hello.

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    toosee quali hello con l'etichetta dati è simile, si recupera una riga.

        labeledData.take(1)

    Verrà visualizzato un output simile hello seguente:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a>Creare un modello di regressione logistica da hello input frame di dati
L'attività finale è hello tooconvert con l'etichetta dati in un formato che può essere analizzato da regressione logistica. algoritmo di regressione logistica Hello tooa input deve essere un set di *coppie di funzionalità di etichetta vettore*, dove hello "vettore di funzione" è un vettore di numeri che rappresentano punti input hello. In tal caso, è necessario tooconvert violazioni"hello" colonna, semistrutturati e contiene molti commenti nella matrice tooan testo libero, di numeri reali che una macchina facilmente comprensibile.

Un approccio di apprendimento macchina standard per il linguaggio naturale elaborazione tooassign ogni parola distinct "index" e quindi passare un vettore toohello algoritmo di machine learning in modo che il valore di ogni indice contiene la frequenza relativa hello di tale parola nel testo hello stringa.

MLlib fornisce un modo semplice di tooperform questa operazione. In primo luogo, "suddividere" ogni violazioni stringa tooget hello singole parole in ciascuna stringa. Quindi, usare un `HashingTF` tooconvert ogni set di token in un vettore di funzionalità che può quindi essere tooconstruct algoritmo di regressione logistica toohello passato a un modello. Tutti questi passaggi verranno eseguiti in sequenza con una "pipeline".

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a>Valutare il modello di hello in un set di dati di test separato
È possibile utilizzare il modello di hello creato in precedenza troppo*stimare* quali hello risultati dei controlli nuovo sarà, in base che sono state osservate le violazioni di hello. È stato sottoposto a training questo modello nel set di dati hello **Food_Inspections1.csv**. Segnalare il problema, utilizzare un secondo set di dati, **Food_Inspections2.csv**, troppo*valutare* hello forza di questo modello nuovi dati. Il secondo set di dati (**Food_Inspections2.csv**) deve essere già nel contenitore di archiviazione predefinito hello associato hello cluster.

1. Hello frammento di codice seguente viene creato un nuovo frame di dati, **predictionsDf** contenente stima hello generato dal modello hello. frammento di codice Hello crea anche una tabella temporanea denominata **stime** in base a hello frame di dati.

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    Verrà visualizzato un output simile hello seguente:

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
1. Esaminare una delle stime di hello. Eseguire questo frammento di codice:

        predictionsDf.take(1)

   Non vi è una stima per hello prima voce hello set di dati di test.
1. Hello `model.transform()` metodo si applica hello stessa trasformazione tooany nuovi dati con hello stesso schema e ottenere una stima della modalità tooclassify hello dati. Possiamo tooget alcune statistiche semplice senso di valutare l'accuratezza delle nostri stime:

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    output di Hello è simile hello seguenti:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    Utilizzare la regressione logistica con Spark offre un modello accurato della relazione hello tra le violazioni e le descrizioni in inglese se un'azienda consente di passare o esito negativo di un controllo di alimenti.

## <a name="create-a-visual-representation-of-hello-prediction"></a>Creare una rappresentazione visiva della stima hello
È ora possibile costruire un toohelp visualizzazione finale che ci motivo sui risultati di hello del test.

1. Iniziamo estraendo stime diverse hello e risultati di hello **stime** tabella temporanea creata in precedenza. la query seguente Hello separare output di hello come *true_positive*, *false_positive*, *true_negative*, e *false_negative*. Nella seguente query hello è disattivare la visualizzazione utilizzando `-q` e salvare anche l'output di hello (tramite `-o`) come frame di dati che può essere quindi utilizzato con hello `%%local` magic.

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. Infine, utilizzare hello seguente frammento di codice toogenerate hello tracciato utilizzando **Matplotlib**.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    È necessario visualizzare hello seguente output:

    ![Output dell'applicazione Machine Learning in Spark: grafico a torta con le percentuali sui controlli alimentari con esito negativo](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Output del risultato di Machine Learning in Spark")

    In questo grafico, un risultato "positivo" si riferisce ispezione alimentare toohello non riuscita, mentre un risultato negativo si riferisce tooa passato ispezione.

## <a name="shut-down-hello-notebook"></a>Chiudere Blocco note hello
Al termine dell'esecuzione di un'applicazione hello, sarà necessario arrestare le risorse di hello notebook toorelease hello. toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**. Questo chiude e si chiude hello notebook.

## <a name="seealso"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: usare Spark in HDInsight per l'analisi della temperatura di un edificio con sistemi HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale](hdinsight-apache-spark-eventhub-streaming.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creare ed eseguire applicazioni
* [Creare un'applicazione autonoma con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Eseguire processi in modalità remota in un cluster Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Strumenti ed estensioni
* [Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)
