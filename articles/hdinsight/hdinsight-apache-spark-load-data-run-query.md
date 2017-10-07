---
title: aaaRun query interattive in un cluster Azure HDInsight Spark | Documenti Microsoft
description: "Guida introduttiva di HDInsight Spark in modalità di cluster toocreate un Apache Spark in HDInsight."
keywords: guida introduttiva spark,spark interattivo,query interattiva,hdinsight spark,azure spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a>Eseguire query interattive in un cluster HDInsight Spark

In questo articolo, si utilizza un server Jupyter notebook toorun interattivo Spark query SQL su un cluster Spark. Server Jupyter notebook è un'applicazione basata su browser che estende hello esperienza interattiva basata su console toohello Web. Per ulteriori informazioni, vedere [notebook Jupyter hello](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).

Per questa esercitazione, si userà hello **PySpark** kernel in hello Jupyter notebook toorun una query SQL Spark interattiva. I notebook di Jupyter nei cluster HDInsight supportano anche due altri kernel: **PySpark3** e **Spark**. Per ulteriori informazioni su kernel hello e hello vantaggi derivanti dall'utilizzo **PySpark**, vedere [cluster kernel notebook Jupyter utilizzo con Apache Spark in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Prerequisiti

* **Cluster Azure HDInsight Spark**. Per istruzioni, vedere [Creare un cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a>Creare un server Jupyter notebook query interattive toorun

query toorun, utilizziamo i dati di esempio che per impostazione predefinita nel servizio di archiviazione hello associato hello cluster disponibile. È necessario, tuttavia, caricare prima i dati in Spark come un dataframe. Dopo aver creato hello frame di dati, è possibile eseguire query su di esso utilizzando notebook Jupyter hello. In questa sezione si analizzerà come:

* Registrare un set di dati di esempio come un dataframe di Spark.
* Eseguire query sul frame di dati hello.

1. Aprire hello [portale di Azure](https://portal.azure.com/). Se si è scelto di dashboard di toohello toopin hello del cluster, fare clic su riquadro cluster hello dal Pannello di hello dashboard toolaunch hello cluster.

    Se si non blocca hello cluster toohello dashboard nel riquadro di sinistra hello, fare clic su **cluster HDInsight**, quindi fare clic su cluster hello è stato creato.

3. In **Collegamenti rapidi** fare clic su **Dashboard cluster** e quindi su **Notebook di Jupyter**. Se richiesto, immettere le credenziali di amministratore hello cluster hello.

   ![Aprire Server Jupyter notebook toorun Spark SQL query interattivo](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "aprire Jupyter notebook toorun interattivo Spark nella query SQL")

   > [!NOTE]
   > È inoltre possibile accedere notebook Jupyter hello per il cluster usando hello apertura URL seguente nel browser. Sostituire **CLUSTERNAME** con nome hello del cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Creare un notebook. Fare clic su **Nuovo** e quindi su **PySpark**.

   ![Creare una query di Spark SQL interattiva Jupyter notebook toorun](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "creare una query di Spark SQL interattiva Jupyter notebook toorun")

   Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled(Untitled.pynb).

4. Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo, se si desidera.

    ![Specificare un nome per hello Jupter notebook toorun Spark query interattivo da](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "specificare un nome per hello Jupter notebook toorun Spark query interattivo da")

5. Esempio hello Incolla del codice in una cella vuota e quindi premere **MAIUSC + INVIO** codice hello toorun. codice Hello Importa i tipi di hello richiesti per questo scenario:

        from pyspark.sql.types import *

    Poiché è stato creato un notebook utilizza il kernel PySpark hello, non è necessario toocreate i contesti in modo esplicito. contesti di Spark e Hive Hello vengono automaticamente creati automaticamente quando si esegue prima cella di codice hello.

    ![Stato della query interattiva Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Stato della query interattiva Spark SQL")

    Ogni volta che si esegue una query interattiva in Jupyter, il titolo della finestra del browser web viene illustrato un **(occupata)** stato insieme a titolo di hello notebook. Viene visualizzato anche un toohello Avanti cerchio pieno **PySpark** testo nell'angolo superiore destro di hello. Dopo aver completato il processo di hello, assume la forma cerchio tooa.

6. Prima di caricare i dati hello in un cluster Spark, vediamo uno snapshot dell'elemento. Hello dati di esempio utilizzati in questa esercitazione sono disponibili come file CSV in tutti i cluster di HDInsight Spark **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**. dati Hello acquisisce le variazioni di temperatura hello di un edificio. Di seguito è hello prime righe di dati hello.

    ![Snapshot di dati per query SQL Spark interattive](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot di dati per query SQL Spark interattive")

6. Creare un frame di dati e una tabella temporanea (**impianto**) eseguendo hello seguente codice. Per questa esercitazione, è non creare tutte le colonne di hello in una tabella temporanea hello come colonne toohello confrontati in dati CSV non elaborati hello. 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Dopo aver creato una tabella di hello, eseguire query interattivo sui dati hello, utilizzare hello seguente codice.

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   Perché si sta usando un kernel PySpark, è ora possibile direttamente eseguire una query SQL interattiva per la tabella temporanea hello **impianto** creato utilizzando hello `%%sql` magic. Per ulteriori informazioni su hello `%%sql` magic e altri magics disponibili con kernel PySpark hello, vedere [kernel disponibile sui server Jupyter notebook con i cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

   Hello seguente tabulari output viene visualizzato per impostazione predefinita.

     ![Tabella di output dei risultati della query interattiva Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabella di output dei risultati della query interattiva Spark")

    È inoltre possibile visualizzare i risultati hello in anche altre visualizzazioni. Ad esempio, un grafico ad area per hello stesso output sarebbe simile al seguente hello.

    ![Grafico ad area dei risultati della query interattiva Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Grafico ad area dei risultati della query interattiva Spark")

9. Arresto delle risorse cluster di hello notebook toorelease hello al termine dell'esecuzione di un'applicazione hello. toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**.

## <a name="next-step"></a>Passaggio successivo

In questo articolo si è appreso toorun query interattive in Spark usando server Jupyter notebook. In uno strumento analitica di Business Intelligence quali Power BI e Tableau di anticipo toohello Avanti articolo toosee come dati di hello che è registrato in Spark possono essere estratti. 

> [!div class="nextstepaction"]
>[Spark BI usando gli strumenti di visualizzazione di dati con Azure HDInsight](hdinsight-apache-spark-use-bi-tools.md)




