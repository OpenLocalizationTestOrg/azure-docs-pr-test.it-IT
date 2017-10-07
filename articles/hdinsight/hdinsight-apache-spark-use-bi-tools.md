---
title: aaaSpark BI utilizzando gli strumenti di visualizzazione di dati in Azure HDInsight | Documenti Microsoft
description: Usare gli strumenti di visualizzazione di dati per l'analisi con Apache Spark BI nei cluster HDInsight
keywords: apache spark bi, spark bi, visualizzazione dei dati spark, spark business intelligence
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a>Apache Spark BI usando gli strumenti di visualizzazione di dati con Azure HDInsight

Informazioni su come toouse visualizzazione dei dati degli strumenti come Power BI e Tableau tooanalyze un set di dati di esempio non elaborato con Apache Spark BI nei cluster HDInsight.

> [!NOTE]
> La connettività con gli strumenti di business intelligence descritta in questo articolo non è supportata su Spark 2.1 in Azure HDInsight 3.6 Preview. Solo le versioni 1.6 e 2.0 di Spark (HDInsight 3.4 e 3.5 rispettivamente) sono supportate.
>

Questa esercitazione è disponibile anche come notebook di Jupyter in un cluster Spark HDInsight. esperienza notebook Hello consente di eseguire frammenti di codice Python hello dal blocco appunti hello stesso. esercitazione di hello tooperform all'interno di un blocco note, creare un cluster Spark, avviare un server Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), quindi eseguire notebook hello **strumenti BI di uso con Apache Spark in HDInsight.ipynb** in hello **Python**  cartella.

## <a name="prerequisites"></a>Prerequisiti

* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="hivetable"></a>Preparare i dati per la visualizzazione dei dati di Spark

In questa sezione, utilizziamo hello [Jupyter](https://jupyter.org) notebook da un HDInsight Spark cluster toorun i processi che elaborano i dati di esempio non elaborati e salvarlo come tabella. dati di esempio Hello sono un file CSV (hvac.csv) disponibile in tutti i cluster per impostazione predefinita. Dopo aver salvati i dati come una tabella, nella sezione successiva di hello è utilizzare BI strumenti tooconnect toohello tabella ed eseguire visualizzazioni dei dati.

> [!NOTE]
> Se si sta eseguendo hello passaggi in questo articolo dopo il completamento istruzioni hello [eseguire query interattive in un cluster HDInsight Spark](hdinsight-apache-spark-load-data-run-query.md), è possibile ignorare tooStep 8 riportato di seguito.
>

1. Da hello [portale di Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello). È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.   

2. Dal Pannello di cluster Spark hello, fare clic su **Dashboard Cluster**, quindi fare clic su **server Jupyter Notebook**. Se richiesto, immettere le credenziali di amministratore hello cluster hello.

   > [!NOTE]
   > È anche possibile raggiungere hello server Jupyter Notebook per il cluster usando hello apertura URL seguente nel browser. Sostituire **CLUSTERNAME** con nome hello del cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Creare un notebook. Fare clic su **Nuovo** e quindi su **PySpark**.

    ![Creare un notebook di Jupyter per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Creare un notebook di Jupyter per Apache Spark BI")

4. Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled.pynb. Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo.

    ![Specificare un nome per notebook hello per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "specificare un nome per notebook hello per Apache Spark BI")

5. Poiché è stato creato un notebook utilizza il kernel PySpark hello, non è necessario toocreate i contesti in modo esplicito. contesti di Spark e Hive Hello vengono automaticamente creati automaticamente quando si esegue prima cella di codice hello. È possibile avviare l'importazione di tipi di hello necessari per questo scenario. toodo in tal caso, posizionare il cursore hello nella cella hello e premere **MAIUSC + INVIO**.

        from pyspark.sql import *

6. Caricare i dati di esempio in una tabella temporanea. Quando si crea un cluster Spark in HDInsight, file di dati di esempio hello, **hvac.csv**, account di archiviazione toohello copiato associata in **\HdiSamples\HdiSamples\SensorSampleData\hvac**.

    In una cella vuota, incollare l'esempio hello frammento e premere **MAIUSC + INVIO**. Questo frammento di codice registra dati hello in una tabella denominata **impianto**.

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. Verificare che la tabella hello creata correttamente. È possibile utilizzare hello `%%sql` particolare query Hive toorun direttamente. Per ulteriori informazioni su hello `%%sql` magic e altri magics disponibili con kernel PySpark hello, vedere [kernel disponibile sui server Jupyter notebook con i cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SHOW TABLES

    Viene visualizzato un output come il seguente:

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    Hello solo le tabelle che presentano FALSO in hello **isTemporary** colonna sono tabelle hive archiviate in metastore hello e sono accessibili da strumenti di Business Intelligence hello. In questa esercitazione, la connessione è toohello **impianto** tabella creata.

8. Verificare che la tabella hello contiene dati di hello destinato. In una cella vuota in blocco per Appunti hello, copiare l'esempio hello frammento e premere **MAIUSC + INVIO**.

        %%sql
        SELECT * FROM hvac LIMIT 10

9. Arresto delle hello notebook toorelease hello risorse. toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**.

## <a name="powerbi"></a>Usare Power BI per la visualizzazione dei dati di Spark

> [!NOTE]
> Questa sezione è applicabile solo a Spark 1.6 in HDInsight 3.4 e Spark 2.0 in HDInsight 3.5.
>
>

Dopo aver salvato i dati di hello come una tabella, è possibile utilizzare i dati di Power BI tooconnect toohello e visualizzarla toocreate report, dashboard e così via.

1. Assicurarsi di avere accesso tooPower BI. È possibile ottenere una sottoscrizione di anteprima gratuita di Power BI da [http://www.powerbi.com/](http://www.powerbi.com/).

2. Accedi troppo[Power BI](http://www.powerbi.com/).

3. Dal basso hello del riquadro di sinistra hello, fare clic su **recupera dati**.

4. In hello **recupera dati** pagina **importare o connettersi tooData**, per **database**, fare clic su **ottenere**.

    ![Ottenere i dati in Power BI per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Ottenere i dati in Power BI per Apache Spark BI")

5. Nella schermata successiva hello, fare clic su **Spark in HDInsight** e quindi fare clic su **Connetti**. Quando richiesto, immettere l'URL del cluster hello (`mysparkcluster.azurehdinsight.net`) e hello credenziali tooconnect toohello cluster.

    ![Connessione BI Spark tooApache](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "connettersi tooApache BI Spark")

    Dopo aver stabilita la connessione hello, Power BI viene avviata l'importazione di dati dal cluster di hello Spark in HDInsight.

6. Power BI Importa i dati hello e aggiunge un **Spark** set di dati in hello **set di dati** intestazione. Fare clic su set di dati di hello tooopen un nuovi dati hello toovisualize di foglio di lavoro. È inoltre possibile salvare il foglio di lavoro hello come un report. un foglio di lavoro, da hello toosave **File** menu, fare clic su **salvare**.

    ![Riquadro di Apache Spark BI nel dashboard di Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Riquadro di Apache Spark BI nel dashboard di Power BI")
7. Si noti che hello **campi** elenco sulla destra hello Elenca hello **impianto** tabella creata in precedenza. Espandere hello tabella toosee hello campi hello tabella, come definito in precedenza nel blocco note.

      ![Elencare le tabelle nel dashboard di Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Elencare le tabelle nel dashboard di Apache Spark BI")

8. Compilare una varianza di hello tooshow visualizzazione tra temperatura di destinazione e la temperatura effettiva per ogni compilazione. Selezionare i dati di dispositivo toovisualize, **grafico ad Area** (mostrati in una casella rossa). asse hello toodefine, trascinamento e rilascio hello **BuildingID** campo **asse**, e **ActualTemp**/**TargetTemp** i campi in **valore**.

    ![Creare le visualizzazioni di dati usando Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Creare le visualizzazioni di dati usando Apache Spark BI")

9. Per impostazione predefinita, la visualizzazione hello Mostra somma hello per **ActualTemp** e **TargetTemp**. Per entrambi hello campi da hello elenco a discesa, selezionare **Media** tooget una media di effettivo e la temperatura di destinazione per entrambi gli edifici.

    ![Creare le visualizzazioni di dati usando Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Creare le visualizzazioni di dati usando Apache Spark BI")

10. La visualizzazione di dati deve essere simile toohello uno nella schermata di hello. Sposta il cursore sopra hello visualizzazione tooget descrizioni con i dati pertinenti.

    ![Creare le visualizzazioni di dati usando Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Creare le visualizzazioni di dati usando Apache Spark BI")

11. Fare clic su **salvare** da hello menu principali e specificare un nome di report. È anche possibile aggiungere visual hello. Quando si aggiunge una visualizzazione, viene archiviata nel dashboard è possibile registrare l'ultimo valore di hello a colpo d'occhio.

   È possibile aggiungere visualizzazioni tante desiderato per hello stesso set di dati, per poi aggiungerli toohello dashboard per uno snapshot dei dati. Inoltre, cluster Spark in HDInsight sono connessi tooPower BI con direct connettersi. In questo modo si garantisce che Power BI ha sempre hello la maggior parte dei dati aggiornati dal cluster non è necessario per set di dati hello tooschedule aggiornamenti.

## <a name="tableau"></a>Usare Tableau Desktop per la visualizzazione dei dati Spark

> [!NOTE]
> Questa sezione è applicabile solo per i cluster Spark 1.5.2 creati in Azure HDInsight.
>
>

1. Installare [Tableau Desktop](http://www.tableau.com/products/desktop) computer hello in cui si esegue questa esercitazione Apache Spark BI.

2. Assicurarsi che nel computer sia installato un driver ODBC di Microsoft Spark. È possibile installare il driver hello [qui](http://go.microsoft.com/fwlink/?LinkId=616229).

1. Avviare Tableau Desktop. Nel riquadro di sinistra hello, dall'elenco di hello del server tooconnect, fare clic su **Spark SQL**. Se Spark SQL non è elencata per impostazione predefinita nel riquadro di sinistra hello, sarà possibile trovarlo tramite clic **più server**.
2. Nella casella di dialogo connessione Spark SQL hello, fornire i valori di hello, come illustrato nella schermata di hello e quindi fare clic su **OK**.

    ![Connetti tooa cluster per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "cluster tooa Connetti per Apache Spark BI")

    elenchi a discesa autenticazione Hello **servizio di Microsoft Azure HDInsight** come opzione, solo se è installato hello [Driver ODBC di Microsoft Spark](http://go.microsoft.com/fwlink/?LinkId=616229) computer hello.
3. Nella schermata successiva hello da hello **Schema** elenco a discesa, fare clic su hello **trovare** icona e quindi fare clic su **predefinito**.

    ![Trovare lo schema per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Trovare lo schema per Apache Spark BI")
4. Per hello **tabella** campo, fare clic su hello **trovare** sull'icona Nuovo toolist tutti hello Hive tabelle disponibili nel cluster hello. Dovrebbe essere hello **impianto** tabella creata in precedenza mediante blocco note hello.

    ![Trovare la tabella per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Trovare la tabella per Apache Spark BI")
5. Trascinare e rilasciare hello tabella toohello superiore casella hello destra. Tableau Importa dati hello e schema hello viene visualizzato come evidenziato nella finestra hello rosso.

    ![Aggiungere tabelle tooTableau per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "aggiungere tabelle tooTableau per Apache Spark BI")
6. Fare clic su hello **Sheet1** scheda in basso a sinistra di hello. Rendere una visualizzazione che mostra le temperature effettivi per tutti gli edifici e destinazione medio hello per ogni data. Trascinare **data** e **ID compilazione** troppo**colonne** e **Temp effettivo**/**destinazione Temp**troppo**righe**. In **segni**selezionare **Area** toouse una mappa dell'area di visualizzazione dei dati Spark.

     ![Aggiungere campi per la visualizzazione dei dati Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Aggiungere campi per la visualizzazione dei dati Spark")
7. Per impostazione predefinita, vengono visualizzati i campi di temperatura di hello come aggregazione. Se si desidera invece temperature di hello tooshow, è possibile farlo discesa hello, come illustrato di seguito.

    ![Eseguire la media della temperatura per la visualizzazione dei dati Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Eseguire la media della temperatura per la visualizzazione dei dati Spark")

8. È anche possibile super-imporre una mappa di temperatura hello in altri tooget meglio della differenza tra le temperature effettive e di destinazione. Spostare l'angolo di toohello mouse hello della mappa area inferiore hello fino a visualizzare hello handle forma evidenziato in un cerchio rosso. Trascinare hello mappa toohello altra mappa hello top e versione hello mouse quando viene visualizzato a forma di hello evidenziato nel rettangolo rosso.

    ![Unire mappe per la visualizzazione dei dati Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Unire mappe per la visualizzazione dei dati Spark")

     Come illustrato nella schermata di hello, occorre modificare la visualizzazione di dati:

    ![Output di Tableau per la visualizzazione dei dati Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Output di Tableau per la visualizzazione dei dati Spark")
9. Fare clic su **salvare** foglio di lavoro toosave hello. È possibile creare dashboard e aggiungere uno o più tooit fogli.

## <a name="next-steps"></a>Passaggi successivi

Finora è stato descritto come creare dati di Spark tooquery di frame toocreate un cluster e quindi accedere ai dati da strumenti di Business Intelligence. È ora possibile esaminare le istruzioni su come toomanage hello risorse cluster e il debug di processi in esecuzione in un cluster HDInsight Spark.

* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)

