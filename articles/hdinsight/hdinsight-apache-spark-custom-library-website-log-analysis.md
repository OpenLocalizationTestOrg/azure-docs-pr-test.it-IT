---
title: i log del sito Web aaaAnalyze con le librerie di Python di Spark - Azure | Documenti Microsoft
description: Il blocco viene illustrato come tooanalyze dati di log mediante una libreria personalizzata con Spark in HDInsight.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a>Analizzare i log del sito Web usando una libreria Python personalizzata con cluster Spark in HDInsight

Il blocco viene illustrato come tooanalyze dati di log mediante una libreria personalizzata con Spark in HDInsight. utilizziamo la libreria personalizzata Hello è una libreria di Python chiamata **iislogparser.py**.

> [!TIP]
> Questa esercitazione è disponibile anche come notebook di Jupyter in un cluster Spark (Linux) creato in HDInsight. esperienza notebook Hello consente di eseguire frammenti di codice Python hello dal blocco appunti hello stesso. esercitazione di hello tooperform all'interno di un blocco note, creare un cluster Spark, avviare un server Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), quindi eseguire notebook hello **analizzare i registri con Spark usando un library.ipynb personalizzato** in hello  **PySpark** cartella.
>
>

**Prerequisiti:**

È necessario disporre delle seguenti hello:

* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="save-raw-data-as-an-rdd"></a>Salvare i dati non elaborati come RDD
In questa sezione, utilizziamo hello [Jupyter](https://jupyter.org) notebook associata a un cluster di Apache Spark in HDInsight toorun processi che elaborano i dati di esempio non elaborati e salvarla come una tabella Hive. dati di esempio Hello sono un file CSV (hvac.csv) disponibile in tutti i cluster per impostazione predefinita.

Dopo aver salvati i dati come una tabella Hive, nella sezione successiva hello si connetterà tabella Hive toohello utilizzando strumenti di Business Intelligence quali Power BI e Tableau.

1. Da hello [portale di Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello). È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.   
2. Dal Pannello di cluster Spark hello, fare clic su **Dashboard Cluster**, quindi fare clic su **server Jupyter Notebook**. Se richiesto, immettere le credenziali di amministratore hello cluster hello.

   > [!NOTE]
   > È anche possibile raggiungere hello server Jupyter Notebook per il cluster usando hello apertura URL seguente nel browser. Sostituire **CLUSTERNAME** con nome hello del cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Creare un nuovo notebook. Fare clic su **Nuovo** e quindi su **PySpark**.

    ![Creare un nuovo notebook Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Creare un nuovo notebook Jupyter")
4. Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled.pynb. Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo.

    ![Specificare un nome per notebook hello](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "specificare un nome per notebook hello")
5. Poiché è stato creato un notebook utilizza il kernel PySpark hello, non è necessario toocreate i contesti in modo esplicito. Quando si esegue prima cella di codice hello contesti di Spark e Hive Hello verranno creati automaticamente per l'utente. È possibile avviare l'importazione di tipi di hello che sono necessari per questo scenario. Incollare hello seguente frammento di codice in una cella vuota e quindi premere **MAIUSC + INVIO**.

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. Creare un RDD usando i dati di log esempio hello già disponibili nel cluster di hello. È possibile accedere a dati hello nell'account di archiviazione predefinito hello associato al cluster hello **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. Recuperare un tooverify del set di log di esempio che hello passaggio precedente è stata completata.

        logs.take(5)

    Verrà visualizzato un segue toohello simili di output:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a>Analizzare i dati di log usando una libreria personalizzata di Python
1. Nell'output di hello sopra, hello contenute nelle prime due righe includono informazioni di intestazione di hello e ogni riga rimanente corrispondono allo schema di hello descritto in questa intestazione. L'analisi di tali log potrebbe essere complessa. Quindi, viene usata una libreria personalizzata di Python (**iislogparser.py**) che semplifica notevolmente l'analisi di tali log. Per impostazione predefinita, questa libreria è inclusa con il cluster Spark in HDInsight in **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.

    Tuttavia, questa raccolta non è in hello `PYTHONPATH` in modo non è possibile usare con un'istruzione di importazione come `import iislogparser`. toouse questa libreria, è necessario distribuire i nodi di lavoro tooall hello. Eseguire hello seguente frammento di codice.

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. `iislogparser`fornisce una funzione `parse_log_line` che restituisce `None` se una riga del log è una riga di intestazione e restituisce un'istanza di hello `LogLine` classe se rileva una riga del log. Hello utilizzare `LogLine` tooextract classe hello solo le righe di log da hello RDD:

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. Recuperare un paio di righe log estratti tooverify che hello passaggio è stata completata.

       logLines.take(2)

   output di Hello deve essere simile toohello seguenti:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. Hello `LogLine` (classe), a sua volta, dispone di alcuni metodi utili, ad esempio `is_error()`, che restituisce se una voce di log ha un codice di errore. Utilizzare questo numero di hello toocompute di errori nelle righe log hello estratto e accedere nuovamente tutti hello errori tooa file diverso.

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   Verrà visualizzato un output simile hello seguente:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. È inoltre possibile utilizzare **Matplotlib** tooconstruct una visualizzazione di dati hello. Ad esempio, se si desidera causa hello tooisolate di richieste eseguite per un lungo periodo, è possibile file hello toofind che accettano hello la maggior parte delle tooserve tempo medio.
   frammento Hello seguente recupera hello primi 25 risorse impiegato la maggior parte delle tooserve ora una richiesta.

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   Verrà visualizzato un output simile hello seguente:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. È anche possibile presentare tali informazioni sotto forma di hello di tracciato. Come un toocreate passaggio prima un tracciato, possiamo creare innanzitutto una tabella temporanea **AverageTime**. hello gruppi di tabella Hello registra, per ora toosee se fossero eventuali picchi di latenza insolito in qualsiasi momento particolare.

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. È quindi possibile eseguire hello tooget query SQL seguente tutti i record di hello in hello **AverageTime** tabella.

       %%sql -o averagetime
       SELECT * FROM AverageTime

   Hello `%%sql` magic seguita da `-o averagetime` assicura che output di hello di hello query è persistente in locale nel server Jupyter hello (in genere. da nodo a hello a head del cluster hello). output di Hello viene mantenuta come un [Pandas](http://pandas.pydata.org/) frame di dati con hello specificato nome **averagetime**.

   Verrà visualizzato un output simile hello seguente:

   ![Output della query SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Output della query SQL")

   Per ulteriori informazioni su hello `%%sql` magic, vedere [i parametri supportati con hello % % magic sql](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
7. È ora possibile utilizzare Matplotlib, una libreria utilizzata tooconstruct della visualizzazione dei dati, toocreate un tracciato. Perché è necessario creare tracciato hello da hello localmente persistente **averagetime** frame di dati, il frammento di codice hello deve iniziare con hello `%%local` magic. In questo modo si garantisce che il codice hello viene eseguito localmente su server Jupyter hello.

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   Verrà visualizzato un output simile hello seguente:

   ![Output Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Output Matplotlib")
8. Al termine dell'esecuzione di un'applicazione hello, si consiglia di risorse di arresto hello notebook toorelease hello. toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**. Questo verrà arrestato e notebook hello Chiudi.

## <a name="seealso"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale](hdinsight-apache-spark-eventhub-streaming.md)

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
