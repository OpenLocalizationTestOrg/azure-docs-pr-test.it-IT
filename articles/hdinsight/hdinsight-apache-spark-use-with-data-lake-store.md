---
title: aaaUse dati tooanalyze Apache Spark in archivio Azure Data Lake | Documenti Microsoft
description: Eseguire i processi di Spark tooanalyze dati archiviati nell'archivio Azure Data Lake
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a>Utilizzare i dati di tooanalyze cluster HDInsight Spark in archivio Data Lake

In questa esercitazione, si utilizza server Jupyter notebook disponibili con i cluster di HDInsight Spark toorun un processo che legge i dati da un account archivio Data Lake.

## <a name="prerequisites"></a>Prerequisiti

* Account di Azure Data Lake Store. Seguire le istruzioni di hello in [introduzione archivio Azure Data Lake tramite il portale di Azure hello](../data-lake-store/data-lake-store-get-started-portal.md).

* Cluster Azure HDInsight Spark con Data Lake Store come risorsa di archiviazione. Seguire le istruzioni di hello in [creare un cluster HDInsight con archivio Data Lake tramite il portale di Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    
## <a name="prepare-hello-data"></a>Preparare i dati di hello

> [!NOTE]
> Non è necessario tooperform questo passaggio se è stato creato il cluster di HDInsight hello con archivio Data Lake come spazio di archiviazione predefinito. i processi di creazione di cluster Hello aggiunge alcuni dati di esempio nell'account archivio Data Lake hello specificato durante la creazione di cluster hello. Ignorare la sezione toohello [cluster HDInsight usare Spark con archivio Data Lake](#use-an-hdinsight-spark-cluster-with-data-lake-store).
>
>

Se è stato creato un cluster HDInsight con archivio Data Lake come ulteriore spazio di archiviazione e Blob di archiviazione di Azure come spazio di archiviazione predefinito, è necessario innanzitutto copiare su alcuni toohello di dati di esempio account archivio Data Lake. È possibile utilizzare i dati di esempio hello hello che BLOB di archiviazione di Azure associata a cluster HDInsight hello. È possibile utilizzare hello [ADLCopy strumento](http://aka.ms/downloadadlcopy) toodo in modo. Scaricare e installare lo strumento hello dal collegamento hello.

1. Aprire un prompt dei comandi e passare toohello directory in cui AdlCopy è installato, in genere `%HOMEPATH%\Documents\adlcopy`.

2. Eseguire hello successivo comando toocopy un blob specifico da hello origine contenitore tooa archivio Data Lake:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Hello copia **HVAC.csv** del file di dati di esempio in **/HdiSamples/HdiSamples/SensorSampleData/impianto/** toohello account archivio Azure Data Lake. frammento di codice Hello dovrebbe essere simile:

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > Verificare che si hello file e i nomi di percorso sono in lettere maiuscole iniziali hello.
   >
   >
3. Sarà richiesto tooenter credenziali hello per hello sottoscrizione di Azure in cui si dispone di account archivio Data Lake. Verrà visualizzato un esempio di toohello simile output:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    file di dati Hello (**HVAC.csv**) verranno copiati in una cartella **/hvac** in hello account archivio Data Lake.

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a>Usare un cluster HDInsight Spark con Data Lake Store

1. Da hello [portale Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello). È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.

2. Dal Pannello di cluster Spark hello, fare clic su **collegamenti rapidi**e quindi da hello **Dashboard Cluster** pannello, fare clic su **server Jupyter Notebook**. Se richiesto, immettere le credenziali di amministratore hello cluster hello.

   > [!NOTE]
   > È anche possibile raggiungere hello server Jupyter Notebook per il cluster usando hello apertura URL seguente nel browser. Sostituire **CLUSTERNAME** con nome hello del cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Creare un nuovo notebook. Fare clic su **Nuovo** e quindi su **PySpark**.

    ![Creare un nuovo notebook Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Creare un nuovo notebook Jupyter")

4. Poiché è stato creato un notebook utilizza il kernel PySpark hello, non è necessario toocreate i contesti in modo esplicito. Quando si esegue prima cella di codice hello contesti di Spark e Hive Hello verranno creati automaticamente per l'utente. È possibile avviare l'importazione di tipi di hello necessari per questo scenario. toodo incollare in tal caso, hello seguente frammento di codice in una cella e premere **MAIUSC + INVIO**.

        from pyspark.sql.types import *

    Ogni volta che viene eseguito un processo in Jupyter, verrà visualizzato il titolo della finestra del browser web un **(occupata)** stato insieme a titolo di hello notebook. Verrà visualizzato anche un toohello Avanti cerchio pieno **PySpark** testo nell'angolo superiore destro di hello. Dopo aver completato il processo di hello, verrà modificato tooa cerchio.

     ![Stato di un processo del notebook Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Stato di un processo del notebook Jupyter")

5. Caricare i dati di esempio in una tabella temporanea utilizzando hello **HVAC.csv** file copiato account archivio Data Lake toohello. È possibile accedere a dati hello in account archivio Data Lake hello utilizzando hello seguente modello di URL.

    * Se si dispone di archivio Data Lake come spazio di archiviazione predefinito, HVAC.csv sarà simile toohello percorso hello URL seguente:

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        In alternativa, è anche possibile usare un formato abbreviato come illustrato di seguito hello:

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * Se si dispone di archivio Data Lake come ulteriore spazio di archiviazione, HVAC.csv sarà nel percorso di hello in cui è stato copiato, ad esempio:

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     In una cella vuota, hello Incolla esempio di codice seguente sostituire **MYDATALAKESTORE** con il nome dell'account archivio Data Lake e premere **MAIUSC + INVIO**. Questo esempio di codice registra dati hello in una tabella temporanea denominata **impianto**.

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. Perché si sta usando un kernel PySpark, è ora possibile direttamente eseguire una query SQL per la tabella temporanea hello **impianto** appena creato utilizzando hello `%%sql` magic. Per ulteriori informazioni su hello `%%sql` magic, nonché altri magics disponibili con kernel PySpark hello, vedere [kernel disponibile sui server Jupyter notebook con i cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. Una volta completato il processo di hello, hello seguente tabulari output viene visualizzato per impostazione predefinita.

      ![Tabella di output dei risultati della query](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Tabella di output dei risultati della query")

     È inoltre possibile visualizzare i risultati hello in anche altre visualizzazioni. Ad esempio, un grafico ad area per hello stesso output sarebbe simile al seguente hello.

     ![Grafico ad area dei risultati della query](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Grafico ad area dei risultati della query")

8. Al termine dell'esecuzione di un'applicazione hello, si consiglia di risorse di arresto hello notebook toorelease hello. toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**. Questo verrà arrestato e notebook hello Chiudi.


## <a name="next-steps"></a>Passaggi successivi

* [Creare un toorun di applicazione Scala autonomo nel cluster di Apache Spark](hdinsight-apache-spark-create-standalone-application.md)
* [Utilizzare gli strumenti di HDInsight in Azure Toolkit per le applicazioni per il cluster HDInsight Spark Linux Spark toocreate IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizzare gli strumenti di HDInsight in Azure Toolkit per Eclipse toocreate Spark applicazioni cluster HDInsight Spark Linux](hdinsight-apache-spark-eclipse-tool-plugin.md)
