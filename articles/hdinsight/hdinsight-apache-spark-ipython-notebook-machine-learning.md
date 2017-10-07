---
title: aaaBuild Apache Spark apprendimento applicazioni in Azure HDInsight | Documenti Microsoft
description: Istruzioni dettagliate su come applicazione in HDInsight Spark di apprendimento automatico di Apache Spark toobuild cluster utilizzando server Jupyter notebook
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
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a>Compilare applicazioni di Machine Learning Apache Spark in Azure HDInsight

Informazioni su come toobuild cluster di un'applicazione di apprendimento macchina Apache Spark usando un Spark in HDInsight. Questo articolo illustra come toouse hello server Jupyter notebook disponibili con toobuild cluster hello e test dell'applicazione. un'applicazione Hello utilizza hello esempio HVAC.csv i dati disponibili in tutti i cluster per impostazione predefinita.

**Prerequisiti:**

È necessario disporre delle seguenti hello:

* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="data"></a>Comprendere i set di dati hello
Prima di iniziare la creazione di un'applicazione hello, verrà ora analizzata la struttura di hello dei dati di hello per il quale è compilare un'applicazione hello e il tipo di hello di analisi che verranno eseguite sui dati hello. 

In questo articolo, si usa l'esempio hello **HVAC.csv** file di dati è disponibile nell'account di archiviazione di Azure associati ai cluster HDInsight hello hello. Nell'account di archiviazione hello, del file hello è **\HdiSamples\HdiSamples\SensorSampleData\hvac**. Scaricare e aprire tooget di file CSV hello uno snapshot dei dati di hello.  

![Snapshot dei dati usati per l'esempio Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot dei dati usati per l'esempio Machine Learning Spark")

dati Hello mostrano temperatura destinazione hello e hello effettivo temperatura un edificio con sistemi impianto installati. Si supponga ad esempio hello **sistema** colonna rappresenta l'ID di sistema hello e hello **SystemAge** colonna rappresenta il numero di hello di cui è stato sistema impianto hello in luogo alla generazione di hello anni.

Utilizziamo questo toopredict dati se un edificio sarà hotter o colder basata sulla temperatura destinazione hello, data un ID di sistema e l'età di sistema.

## <a name="app"></a>Scrivere un'applicazione di Machine Learning Spark usando Spark MLlib
In questa applicazione viene utilizzato un tooperform pipeline Spark ML una classificazione di documenti. Nella pipeline di hello, si suddivise documento hello in parole, convertire parole hello in un vettore di funzione numerica e infine compilare un modello di stima utilizzando le etichette e i vettori di funzioni hello. Eseguire hello un'applicazione hello toocreate i passaggi seguenti.

1. Da hello [portale Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello). È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.   
2. Dal Pannello di cluster Spark hello, fare clic su **Dashboard Cluster**, quindi fare clic su **server Jupyter Notebook**. Se richiesto, immettere le credenziali di amministratore hello cluster hello.
   
   > [!NOTE]
   > È anche possibile raggiungere hello server Jupyter Notebook per il cluster usando hello apertura URL seguente nel browser. Sostituire **CLUSTERNAME** con nome hello del cluster:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. Creare un nuovo notebook. Fare clic su **Nuovo** e quindi su **PySpark**.
   
    ![Creare un notebook di Jupyter per l'esempio di Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Creare un notebook di Jupyter per l'esempio di Machine Learning Spark")
4. Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled.pynb. Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo.
   
    ![Fornire un nome di notebook per l'esempio di Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Fornire un nome di notebook per l'esempio di Machine Learning Spark")
5. Poiché è stato creato un notebook utilizza il kernel PySpark hello, non è necessario toocreate i contesti in modo esplicito. Quando si esegue prima cella di codice hello contesti di Spark e Hive Hello verranno creati automaticamente per l'utente. È possibile avviare l'importazione di tipi di hello che sono necessari per questo scenario. Incollare hello seguente frammento di codice in una cella vuota e quindi premere **MAIUSC + INVIO**. 
   
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
6. È ora necessario caricare i dati di hello (hvac.csv), per analizzare e utilizzarlo come modello hello tootrain. A tale scopo, si definisce una funzione che controlla se è maggiore di temperatura destinazione hello hello effettivo temperatura compilazione hello. Se temperatura effettivo hello è maggiore, compilazione hello è attivo, indicato dal valore hello **1.0**. Se la temperatura reale hello è minore, compilazione hello è freddo, indicato dal valore hello **0,0**. 
   
    Hello Incolla seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. Configurare l'apprendimento Spark hello pipeline costituita da tre fasi: tokenizer hashingTF e lr. Per altre informazioni su una pipeline e funzionamento vedere <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">pipeline machine learning di Spark</a>.
   
    Hello Incolla seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. Adattare hello pipeline toohello training documento. Hello Incolla seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.
   
        model = pipeline.fit(training)
3. Verificare lo stato di avanzamento con un'applicazione hello di hello training documento toocheckpoint. Hello Incolla seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.
   
        training.show()
   
    Questo metodo dovrebbe produrre seguente toohello simile di hello output:
   
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

    Tornare indietro e verificare l'output di hello in file CSV non elaborato hello. Ad esempio, file CSV hello hello prima riga include dati:

    ![Snapshot dei dati di output per l'esempio Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Snapshot dei dati di output per l'esempio Machine Learning Spark")

    Si noti come temperatura effettivo hello è minore di temperatura destinazione hello suggerendo compilazione hello freddo. Pertanto, nell'output di hello training hello valore per **etichetta** in hello prima riga è **0,0**, il che significa edificio hello non è attivo.

1. Preparare un modello con training di hello toorun set di dati contro. toodo in tal caso, si passa su un ID di sistema e l'età di sistema (indicato come **SystemInfo** nell'output di hello training), e si stima modello hello hello se la compilazione con l'età di sistema e l'ID di sistema potrebbe essere hotter (indicato dalle 1.0) o dispositivo di raffreddamento ( indicato da 0,0).
   
   Hello Incolla seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. Infine, è possibile eseguire stime sui dati di test hello. Hello Incolla seguente frammento di codice in una cella vuota e premere **MAIUSC + INVIO**.
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. Verrà visualizzato un segue toohello simili di output:
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   Hello prima riga stima hello, si noterà che per un sistema impianto con 20 ID e la validità di sistema di 25 anni, compilazione hello sarà attivo (**stima = 1.0**). primo valore di Hello per DenseVector (0.49999) corrisponde toohello stima 0,0 e il valore secondo hello (0.5001) stima toohello 1.0. Nell'output di hello, anche se il secondo valore di hello è solo leggermente superiore, viene illustrato il modello di hello **stima = 1.0**.
4. Al termine dell'esecuzione di un'applicazione hello, si consiglia di risorse di arresto hello notebook toorelease hello. toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**. Questo verrà arrestato e notebook hello Chiudi.

## <a name="anaconda"></a>Usare la libreria Anaconda scikit-learn per Machine Learning Spark
I cluster Apache Spark in HDInsight includono librerie Anaconda. Ciò include anche hello **scikit-informazioni** libreria per machine learning. libreria Hello include anche diversi set di dati che è possibile utilizzare applicazioni di esempio toobuild direttamente da un server Jupyter notebook. Per esempi sull'utilizzo di hello scikit-libreria di informazioni, vedere [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).

## <a name="seealso"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
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

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
