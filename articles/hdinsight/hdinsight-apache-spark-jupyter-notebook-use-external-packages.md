---
title: pacchetti Maven personalizzati aaaUse con Jupyter di Spark su HDInsight di Azure | Documenti Microsoft
description: Istruzioni dettagliate su come i cluster di pacchetti di Maven personalizzati toouse tooconfigure Jupyter notebook disponibili con HDInsight Spark.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Usare pacchetti esterni con notebook di Jupyter nei cluster Apache Spark in HDInsight
> [!div class="op_single_selector"]
> * [Uso di comandi Magic nelle celle](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Uso di azioni script](hdinsight-apache-spark-python-package-installation.md)
>
>

Informazioni su come tooconfigure un server Jupyter notebook nel cluster Apache Spark in HDInsight toouse esterno,-il contributo della community **maven** di casella pacchetti che non sono presenti cluster hello. 

È possibile cercare hello [repository Maven](http://search.maven.org/) per l'elenco completo di hello dei pacchetti disponibili. È anche possibile ottenere un elenco dei pacchetti disponibili da altre origini. Ad esempio, un elenco completo dei pacchetti creati dalla community è disponibile nel sito Web [spark-packages.org](http://spark-packages.org/).

In questo articolo si apprenderà come hello toouse [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pacchetto con notebook Jupyter hello.



## <a name="prerequisites"></a>Prerequisiti
È necessario disporre delle seguenti hello:

* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="use-external-packages-with-jupyter-notebooks"></a>Usare pacchetti esterni con i notebook Jupyter
1. Da hello [portale Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello). È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.   
2. Dal Pannello di cluster Spark hello, fare clic su **collegamenti rapidi**e quindi da hello **Dashboard Cluster** pannello, fare clic su **server Jupyter Notebook**. Se richiesto, immettere le credenziali di amministratore hello cluster hello.

    > [!NOTE]
    > È anche possibile raggiungere hello server Jupyter Notebook per il cluster usando hello apertura URL seguente nel browser. Sostituire **CLUSTERNAME** con nome hello del cluster:
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. Creare un nuovo notebook. Fare clic su **New** (Nuovo) e quindi su **Spark**.
   
    ![Creare un nuovo notebook Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Creare un nuovo notebook Jupyter")

4. Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled.pynb. Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo.
   
    ![Specificare un nome per notebook hello](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "specificare un nome per notebook hello")

5. Si utilizzerà hello `%%configure` tooconfigure magic hello notebook toouse un pacchetto esterno. Nei blocchi appunti che utilizzano i pacchetti esterni, verificare di chiamare hello `%%configure` magic nella prima cella di codice hello. Ciò garantisce che kernel hello è pacchetto hello toouse configurato prima dell'avvio della sessione hello.

    >[!IMPORTANT] 
    >Se si dimentica kernel hello tooconfigure nella prima cella hello, è possibile utilizzare hello `%%configure` con hello `-f` parametro, ma che verrà riavviato sessione hello e lo stato di avanzamento tutti andranno persa.

    | Versione HDInsight | Comando |
    |-------------------|---------|
    |Per HDInsight 3.3 e HDInsight 3.4 | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | Per HDInsight 3.5 | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. frammento di codice Hello precedente prevede che le coordinate di maven hello per pacchetto esterno di hello in Repository centrale Maven. In questo frammento, `com.databricks:spark-csv_2.10:1.4.0` è coordinate di maven hello per **spark csv** pacchetto. Di seguito viene illustrato come è costruire hello coordinate per un pacchetto.
   
    a. Individuare il pacchetto di hello in hello Maven Repository. In questa esercitazione si userà [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Dal repository hello, raccogliere i valori hello per **GroupId**, **ID**, e **versione**. Assicurarsi che i valori hello che è raccogliere corrispondano il cluster. In questo caso, si sta usando una Scala 2.10 e un pacchetto di Spark 1.4.0, ma potrebbe essere necessario versioni diverse di tooselect hello Scala o Spark versione presente nel cluster. È possibile trovare la versione di hello Scala il cluster eseguendo `scala.util.Properties.versionString` kernel Jupyter Spark hello o Invia Spark. È possibile trovare la versione di hello Spark il cluster eseguendo `sc.version` sui server Jupyter notebook.
   
    ![Usare pacchetti esterni con notebook di Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Usare pacchetti esterni con notebook di Jupyter")
   
    c. Concatenare valori hello tre, separati da due punti (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

7. Eseguire cella codice hello con hello `%%configure` magic. Consente di configurare hello sottostante inserire il sessione toouse hello pacchetto fornito. Nelle celle successive di hello in blocco per Appunti hello, ora è possibile utilizzare il pacchetto di hello, come illustrato di seguito.
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. È quindi possibile eseguire i frammenti di codice hello, come indicato di seguito, tooview hello dati hello frame di dati è stato creato nel passaggio precedente hello.
   
        df.show()
   
        df.select("Time").count()

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

* [Usare pacchetti Python esterni con Jupyter Notebook nei cluster Apache Spark in HDInsight Linux](hdinsight-apache-spark-python-package-installation.md)
* [Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)

