---
title: cluster notebook Zeppelin aaaUse con Apache Spark in HDInsight di Azure | Documenti Microsoft
description: Istruzioni dettagliate su come cluster di notebook Zeppelin toouse con Apache Spark in HDInsight di Azure.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a>Usare i notebook di Zeppelin con cluster Apache Spark in Azure HDInsight

I cluster di HDInsight Spark sono notebook Zeppelin che è possibile utilizzare i processi di Spark toorun. In questo articolo viene illustrato come toouse hello notebook Zeppelin in un cluster HDInsight.

> [!NOTE]
> I notebook Zeppelin sono disponibili solo per Spark 1.6.3 in HDInsight 3.5 e Spark 2.1.0 in HDInsight 3.6.
>

**Prerequisiti:**

* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="launch-a-zeppelin-notebook"></a>Avviare un notebook Zeppelin
1. Dal Pannello di cluster Spark hello, fare clic su **Dashboard Cluster**, quindi fare clic su **Zeppelin Notebook**. Se richiesto, immettere le credenziali di amministratore hello cluster hello.
   
   > [!NOTE]
   > È anche possibile raggiungere hello Notebook Zeppelin per il cluster usando hello apertura URL seguente nel browser. Sostituire **CLUSTERNAME** con nome hello del cluster:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. Creare un nuovo notebook. Riquadro intestazione hello fare clic su **Notebook**, quindi fare clic su **Crea nuova nota**.
   
    ![Creare un nuovo notebook Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Creare un nuovo notebook Zeppelin")
   
    Immettere un nome per notebook hello e quindi fare clic su **Crea nota**.
3. Assicurarsi inoltre che l'intestazione di blocco per Appunti hello Mostra lo stato connesso. Viene indicato da un punto verde nell'angolo superiore destro di hello.
   
    ![Stato del notebook Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Stato del notebook Zeppelin")
4. Caricare i dati di esempio in una tabella temporanea. Quando si crea un cluster Spark in HDInsight, file di dati di esempio hello, **hvac.csv**, account di archiviazione toohello copiato associata in **\HdiSamples\SensorSampleData\hvac**.
   
    Nel paragrafo vuoto hello creata per impostazione predefinita nel nuovo notebook hello, incollare hello seguente frammento di codice.
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    Premere **MAIUSC + INVIO** oppure fare clic su hello **riprodurre** pulsante per frammento di codice hello paragrafo toorun hello. stato Hello nell'angolo destro hello di paragrafo hello deve sullo stato di avanzamento da pronto, in sospeso, tooFINISHED in esecuzione. output di Hello viene visualizzato nella parte inferiore di hello di hello stesso paragraph. schermata di Hello è simile hello seguenti:
   
    ![Creare una tabella temporanea dai dati non elaborati](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Creare una tabella temporanea dai dati non elaborati")
   
    È anche possibile fornire un paragrafo tooeach titolo. Nell'angolo destro hello, fare clic su hello **impostazioni** icona e quindi fare clic su **Mostra titolo**.
5. È ora possibile eseguire istruzioni SQL Spark in hello **impianto** tabella. Incollare hello seguente query in un nuovo paragrafo. Hello query recupera l'ID compilazione hello e hello differenza destinazione hello e temperature effettive per ogni compilazione in una determinata data. Premere **MAIUSC + INVIO**.
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    Hello **sql %** istruzione all'inizio di hello indica interprete di hello notebook toouse hello inserire il Scala.
   
    Hello seguente schermata Mostra output di hello.
   
    ![Esecuzione di un'istruzione SQL Spark utilizzando blocco note hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "eseguire un'istruzione SQL Spark utilizzando blocco note hello")
   
     Fare clic su hello visualizzazione Opzioni (evidenziato nel rettangolo) tooswitch tra diverse rappresentazioni per hello stesso output. Fare clic su **impostazioni** toochoose quali costituiscono hello chiave e i valori nell'output di hello. acquisizione schermo precedente viene Hello **buildingID** come chiave di hello e Media hello di **temp_diff** come valore di hello.
6. È inoltre possibile eseguire istruzioni SQL Spark utilizzo di variabili nelle query hello. Hello successivo illustrato frammento di codice come una variabile, toodefine **Temp**, in query hello con i valori possibili hello desiderato tooquery con. Quando si esegue prima query hello, un elenco a discesa viene popolato automaticamente con i valori hello specificato per la variabile hello.
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    Incollare questo frammento di codice in un nuovo paragrafo e premere **MAIUSC+INVIO**. Hello seguente schermata Mostra output di hello.
   
    ![Esecuzione di un'istruzione SQL Spark utilizzando blocco note hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "eseguire un'istruzione SQL Spark utilizzando blocco note hello")
   
    Per le query successive, è possibile selezionare un nuovo valore dall'elenco a discesa hello e rieseguire la query hello. Fare clic su **impostazioni** toochoose quali costituiscono hello chiave e i valori nell'output di hello. Hello acquisizione schermo precedente viene **buildingID** come chiave hello, hello medio di **temp_diff** come valore hello e **targettemp** come gruppo hello.
7. Riavviare l'applicazione hello tooexit interprete di inserire il hello. In tal caso, aprire le impostazioni di interprete facendo hello connesso in nome utente dall'angolo in alto a destra hello toodo e quindi fare clic su **interprete**.
   
    ![Avviare l'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Output Hive")
8. Scorrere le impostazioni di interprete tooLivy e quindi fare clic su **riavviare**.
   
    ![Riavviare hello inserire il intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "riavviare hello Zeppelin intepreter")

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a>Utilizzo di pacchetti esterni con notebook hello
È possibile configurare notebook Zeppelin hello in cluster Apache Spark in HDInsight (Linux) toouse esterni, il contributo della community i pacchetti che non sono inclusi out-of-the-box in cluster hello. È possibile cercare hello [repository Maven](http://search.maven.org/) per l'elenco completo di hello dei pacchetti disponibili. È anche possibile ottenere un elenco dei pacchetti disponibili da altre origini. Ad esempio, un elenco completo dei pacchetti creati dalla community è disponibile nel sito Web [spark-packages.org](http://spark-packages.org/).

In questo articolo, verrà visualizzato come hello toouse [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pacchetto con notebook Jupyter hello.

1. Aprire le impostazioni dell'interprete. Nell'angolo superiore destro di hello, fare clic su hello connesso in nome utente e quindi fare clic su **interprete**.
   
    ![Avviare l'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Output Hive")
2. Scorrere le impostazioni di interprete tooLivy e quindi fare clic su **modifica**.
   
    ![Modificare le impostazioni dell'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Modificare le impostazioni dell'interprete")
3. Aggiungere una nuova chiave denominata **livy.spark.jars.packages** e impostarne il valore in formato hello `group:id:version`. Pertanto, se si desidera hello toouse [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pacchetto, è necessario impostare il valore di hello della chiave di hello troppo`com.databricks:spark-csv_2.10:1.4.0`.
   
    ![Modificare le impostazioni dell'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Modificare le impostazioni dell'interprete")
   
    Fare clic su **salvare** e quindi riavviare hello interprete di inserire il.
4. **Suggerimento**: se si desidera toounderstand come tooarrive valore hello chiave hello immessi sopra, ecco come.
   
    a. Individuare il pacchetto di hello in hello Maven Repository. In questa esercitazione è stato usato [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Dal repository hello, raccogliere i valori hello per **GroupId**, **ID**, e **versione**.
   
    ![Usare pacchetti esterni con notebook di Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Usare pacchetti esterni con notebook di Jupyter")
   
    c. Concatenare valori hello tre, separati da due punti (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a>Dove è hello notebook Zeppelin salvate?
notebook Zeppelin Hello vengono salvate toohello headnodes di cluster. Pertanto, se si elimina il cluster di hello, verranno eliminati anche i notebook hello. Se si desidera toopreserve i blocchi appunti per utilizzarli in altri cluster, è necessario esportarli dopo aver hello processi in esecuzione. tooexport un blocco per Appunti, fare clic su hello **esportare** icona come illustrato nell'immagine di hello riportata di seguito.

![Scaricare notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "notebook hello Download")

Ciò consente di risparmiare notebook hello come un file JSON nel percorso di download.

## <a name="livy-session-management"></a>Gestione delle sessioni di Livy
Quando si esegue primo paragrafo di codice hello nel blocco note Zeppelin, viene creata una nuova sessione di inserire il nel cluster di HDInsight Spark. Tale sessione sarà condivisa da tutti i notebook Zeppelin creati successivamente. Se ad alcune hello motivo inserire il sessione è terminata (riavviare il computer del cluster, e così via), non sarà in grado di toorun processi dal blocco appunti Zeppelin hello.

In tal caso, è necessario eseguire operazioni prima di iniziare l'esecuzione di processi da un blocco per Appunti Zeppelin hello. 

1. Riavviare hello interprete di inserire il blocco appunti Zeppelin hello. In tal caso, aprire le impostazioni di interprete facendo hello connesso in nome utente dall'angolo in alto a destra hello toodo e quindi fare clic su **interprete**.
   
    ![Avviare l'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Output Hive")
2. Scorrere le impostazioni di interprete tooLivy e quindi fare clic su **riavviare**.
   
    ![Riavviare hello inserire il intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "riavviare hello Zeppelin intepreter")
3. Eseguire una cella di codice da un notebook Zeppelin esistente. Questo crea una nuova sessione di inserire il cluster HDInsight hello.

## <a name="seealso"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale](hdinsight-apache-spark-eventhub-streaming.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creare ed eseguire applicazioni
* [Creare un'applicazione autonoma con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Eseguire processi in modalità remota in un cluster Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Strumenti ed estensioni
* [Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







