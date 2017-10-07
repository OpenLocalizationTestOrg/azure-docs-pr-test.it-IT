---
title: aaaAnalyze Application Insights registra con Spark - HDInsight di Azure | Documenti Microsoft
description: "Informazioni sulle modalità di registrazione archiviazione tooblob tooexport Application Insights e quindi analizzare i log di hello con Spark in HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 883beae6-9839-45b5-94f7-7eb0f4534ad5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 11ed8cf68dba8d5f9d6e4a65eba0d2b5a950cd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-application-insights-telemetry-logs-with-spark-on-hdinsight"></a>Analizzare i log di Application Insights Telemetry con Spark in HDInsight

Informazioni su come toouse nascita in HDInsight tooanalyze dati di telemetria di Application Insights.

[Visual Studio Application Insights](../application-insights/app-insights-overview.md) è un servizio di analisi dei dati che consente di monitorare le applicazioni Web. I dati di telemetria generati da Application Insights possono essere esportato tooAzure archiviazione. Una volta dati hello in archiviazione di Azure, HDInsight può essere utilizzato tooanalyze è.

## <a name="prerequisites"></a>Prerequisiti

* Un'applicazione che viene configurato toouse Application Insights.

* Familiarità con la creazione di un cluster HDInsight basato su Linux. Per altre informazioni, vedere [Introduzione: Creare un cluster Apache Spark in Azure HDInsight ed eseguire query interattive usando Spark SQL](hdinsight-apache-spark-jupyter-spark-sql.md).

  > [!IMPORTANT]
  > passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un Web browser.

Hello risorse seguenti sono state utilizzate per lo sviluppo e test di questo documento:

* Dati di telemetria di Application Insights è stati generati utilizzando una [app web Node. js configurato toouse Application Insights](../application-insights/app-insights-nodejs.md).

* Un Spark basati su Linux nella versione 3.5 del cluster HDInsight è stato utilizzato tooanalyze hello dati.

## <a name="architecture-and-planning"></a>Architettura e pianificazione

Hello seguente diagramma viene illustrata l'architettura del servizio di questo esempio hello:

![diagramma che mostra i dati che vanno dall'archiviazione tooblob Application Insights, quindi elaborati da Spark in HDInsight](./media/hdinsight-spark-analyze-application-insight-logs/appinsightshdinsight.png)

### <a name="azure-storage"></a>Archiviazione di Azure

Application Insights può essere configurato toocontinuously esportazione telemetria informazioni tooblobs. HDInsight può quindi leggere i dati archiviati in BLOB hello. Tuttavia, esistono alcuni requisiti da seguire:

* **Percorso**: se l'Account di archiviazione hello e HDInsight si trovano in posizioni diverse, potrebbero riscontrare latenza. Aumenta anche costi, come i costi di uscita vengono applicata toodata lo spostamento tra le aree.

    > [!WARNING]
    > L'uso di un account di archiviazione in una località diversa rispetto a HDInsight non è supportato.

* **Tipo di BLOB**: in HDInsight sono supportati solo BLOB in blocchi. Application Insights per impostazione predefinita i BLOB in blocchi toousing, in modo dovrebbe funzionare con HDInsight per impostazione predefinita.

Per informazioni sull'aggiunta di ulteriore spazio di archiviazione tooan esistente cluster HDInsight, vedere hello [aggiungere account di archiviazione aggiuntivi](hdinsight-hadoop-add-storage.md) documento.

### <a name="data-schema"></a>Schema dei dati

Application Insights fornisce [Esporta modello di dati](../application-insights/app-insights-export-data-model.md) informazioni per il formato di dati di telemetria hello esportata tooblobs. passaggi di Hello in questo documento usano toowork Spark SQL con dati hello. Spark SQL può generare automaticamente uno schema per la struttura di dati JSON hello registrato da Application Insights.

## <a name="export-telemetry-data"></a>Esportare i dati di telemetria

Seguire i passaggi di hello in [configurare esportazione continua](../application-insights/app-insights-export-telemetry.md) tooconfigure il tooan di informazioni telemetria di Application Insights tooexport archiviazione di Azure blob.

## <a name="configure-hdinsight-tooaccess-hello-data"></a>Configurare i dati di hello tooaccess HDInsight

Se si sta creando un cluster HDInsight, aggiungere l'account di archiviazione hello durante la creazione del cluster.

hello tooadd cluster esistente tooan Account di archiviazione di Azure, utilizzare le informazioni di hello in hello [aggiungere altri account di archiviazione](hdinsight-hadoop-add-storage.md) documento.

## <a name="analyze-hello-data-pyspark"></a>Analizzare i dati di hello: PySpark

1. Da hello [portale di Azure](https://portal.azure.com), selezionare il Spark in HDInsight cluster. Da hello **collegamenti rapidi** selezionare **dashboard del Cluster**, quindi selezionare **server Jupyter Notebook** dal pannello Dashboard__ Cluster hello.

    ![dashboard del cluster Hello](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)

2. In hello angolo superiore destro della pagina Jupyter hello, selezionare **New**e quindi **PySpark**. Si apre una nuova scheda del browser contenente un notebook di Jupyter basato su Python.

3. Nel primo campo hello (chiamato un **cella**) nella pagina hello immettere hello seguente testo:

   ```python
   sc._jsc.hadoopConfiguration().set('mapreduce.input.fileinputformat.input.dir.recursive', 'true')
   ```

    Questo codice consente di configurare Spark toorecursively accesso hello struttura di directory per i dati di input hello. Telemetria di Application Insights è tooa connesso directory struttura simile toohello `/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Utilizzare **MAIUSC + INVIO** codice hello toorun. Sul lato sinistro di cella hello, hello un '\*' viene visualizzato tra hello tra parentesi quadre tooindicate che codice hello in questa cella è in esecuzione. Una volta che è stata completata, hello '\*' Modifica numero tooa e output toohello simile dopo il testo viene visualizzato sotto la cella hello:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    pyspark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Viene creata una nuova cella di sotto di hello un primo. Immettere hello seguente testo nella nuova cella hello. Sostituire `CONTAINER` e `STORAGEACCOUNT` con nome di account di archiviazione di Azure hello e nome del contenitore blob che contiene i dati di Application Insights.

   ```python
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Utilizzare **MAIUSC + INVIO** tooexecute questa cella. Viene visualizzato un toohello simile di risultati seguente testo:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    percorso wasb Hello restituito è il percorso di hello di hello dati di telemetria di Application Insights. Hello modifica `hdfs dfs -ls` riga hello cella toouse hello wasb percorso restituito e quindi usare **MAIUSC + INVIO** toorun della cella hello nuovamente. Questa volta, i risultati di hello deve essere visualizzato directory hello che contengono dati di telemetria.

   > [!NOTE]
   > Della parte restante di hello di hello i passaggi illustrati in questa sezione, hello `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` directory è stata utilizzata. La struttura della directory potrebbe essere diversa.

6. Nella cella successiva hello, immettere il seguente codice hello: sostituire `WASB_PATH` con percorso hello dal passaggio precedente hello.

   ```python
   jsonFiles = sc.textFile('WASB_PATH')
   jsonData = sqlContext.read.json(jsonFiles)
   ```

    Questo codice crea un frame di dati dal file JSON hello esportati dal processo di esportazione continua hello. Utilizzare **MAIUSC + INVIO** toorun questa cella.
7. Nella cella successiva hello, immettere ed eseguire hello seguente schema hello tooview Spark creato per i file JSON hello:

   ```python
   jsonData.printSchema()
   ```

    schema di Hello per ogni tipo di dati di telemetria è diverso. esempio Hello è hello schema generato per le richieste web (dati archiviati in hello `Requests` sottodirectory):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)
8. Utilizzare hello seguente tooregister hello frame di dati di una tabella temporanea ed eseguire una query su dati hello:

   ```python
   jsonData.registerTempTable("requests")
   df = sqlContext.sql("select context.location.city from requests where context.location.city is not null")
   df.show()
   ```

    Questa query restituisce informazioni città hello per 20 record superiore hello in context.location.city non è null.

   > [!NOTE]
   > la struttura del contesto Hello è presente in tutti i dati di telemetria registrati da Application Insights. elemento città Hello non può essere inserita nei log. Utilizzare hello schema tooidentify altri elementi che è possibile eseguire una query che potrebbero contenere dati per i log.

    Questa query restituisce toohello di informazioni simili seguente testo:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="analyze-hello-data-scala"></a>Analizzare i dati di hello: Scala

1. Da hello [portale di Azure](https://portal.azure.com), selezionare il Spark in HDInsight cluster. Da hello **collegamenti rapidi** selezionare **dashboard del Cluster**, quindi selezionare **server Jupyter Notebook** dal pannello Dashboard__ Cluster hello.

    ![dashboard del cluster Hello](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)
2. In hello angolo superiore destro della pagina Jupyter hello, selezionare **New**e quindi **Scala**. Si apre una nuova scheda del browser contenente un notebook di Jupyter basato su Scala.
3. Nel primo campo hello (chiamato un **cella**) nella pagina hello immettere hello seguente testo:

   ```scala
   sc.hadoopConfiguration.set("mapreduce.input.fileinputformat.input.dir.recursive", "true")
   ```

    Questo codice consente di configurare Spark toorecursively accesso hello struttura di directory per i dati di input hello. Dati di telemetria di Application Insights registrati struttura di directory tooa simile troppo`/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Utilizzare **MAIUSC + INVIO** codice hello toorun. Sul lato sinistro di cella hello, hello un '\*' viene visualizzato tra hello tra parentesi quadre tooindicate che codice hello in questa cella è in esecuzione. Una volta che è stata completata, hello '\*' Modifica numero tooa e output toohello simile dopo il testo viene visualizzato sotto la cella hello:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    spark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Viene creata una nuova cella di sotto di hello un primo. Immettere hello seguente testo nella nuova cella hello. Sostituire `CONTAINER` e `STORAGEACCOUNT` con nome di account di archiviazione di Azure hello e nome del contenitore blob che contiene l'Application Insights accede.

   ```scala
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Utilizzare **MAIUSC + INVIO** tooexecute questa cella. Viene visualizzato un toohello simile di risultati seguente testo:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    percorso wasb Hello restituito è il percorso di hello di hello dati di telemetria di Application Insights. Hello modifica `hdfs dfs -ls` riga hello cella toouse hello wasb percorso restituito e quindi usare **MAIUSC + INVIO** toorun della cella hello nuovamente. Questa volta, i risultati di hello deve essere visualizzato directory hello che contengono dati di telemetria.

   > [!NOTE]
   > Della parte restante di hello di hello i passaggi illustrati in questa sezione, hello `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` directory è stata utilizzata. Questa directory potrebbe non esistere, a meno che i dati di telemetria non siano destinati a un'app Web.

6. Nella cella successiva hello, immettere il seguente codice hello: sostituire `WASB\_PATH` con percorso hello dal passaggio precedente hello.

   ```scala
   var jsonFiles = sc.textFile('WASB_PATH')
   val sqlContext = new org.apache.spark.sql.SQLContext(sc)
   var jsonData = sqlContext.read.json(jsonFiles)
   ```

    Questo codice crea un frame di dati dal file JSON hello esportati dal processo di esportazione continua hello. Utilizzare **MAIUSC + INVIO** toorun questa cella.

7. Nella cella successiva hello, immettere ed eseguire hello seguente schema hello tooview Spark creato per i file JSON hello:

   ```scala
   jsonData.printSchema
   ```

    schema di Hello per ogni tipo di dati di telemetria è diverso. esempio Hello è hello schema generato per le richieste web (dati archiviati in hello `Requests` sottodirectory):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)

8. Utilizzare hello seguente tooregister hello frame di dati di una tabella temporanea ed eseguire una query su dati hello:

   ```scala
   jsonData.registerTempTable("requests")
   var city = sqlContext.sql("select context.location.city from requests where context.location.city is not null limit 10").show()
   ```

    Questa query restituisce informazioni città hello per 20 record superiore hello in context.location.city non è null.

   > [!NOTE]
   > la struttura del contesto Hello è presente in tutti i dati di telemetria registrati da Application Insights. elemento città Hello non può essere inserita nei log. Utilizzare hello schema tooidentify altri elementi che è possibile eseguire una query che potrebbero contenere dati per i log.
   >
   >

    Questa query restituisce toohello di informazioni simili seguente testo:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori esempi di utilizzo toowork Spark con dati e servizi in Azure, vedere hello seguenti documenti:

* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usare Spark in HDInsight per la compilazione di applicazioni di streaming](hdinsight-apache-spark-eventhub-streaming.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

Per informazioni sulla creazione e l'esecuzione di Spark applicazioni, vedere hello seguenti documenti:

* [Creare un'applicazione autonoma con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Eseguire processi in modalità remota in un cluster Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)
