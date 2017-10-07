---
title: aaaInstall Jupyter localmente & connettere il cluster di Azure HDInsight Spark tooan | Documenti Microsoft
description: Informazioni su come tooinstall server Jupyter notebook in locale nel computer e connetterla tooan cluster Apache Spark in HDInsight di Azure.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a>Installare server Jupyter notebook nel computer e connettere tooApache Spark in HDInsight

In questo articolo viene illustrato come tooinstall server Jupyter notebook, hello PySpark personalizzato (per Python) e kernel Spark (per la Scala) con nascita magic e connettere i cluster di HDInsight tooan notebook hello. Può esistere un numero di motivi tooinstall Jupyter sul computer locale e possono essere presenti anche alcune problematiche. Per ulteriori informazioni, vedere la sezione hello [perché è consigliabile installare Jupyter computer](#why-should-i-install-jupyter-on-my-computer) alla fine di hello di questo articolo.

Sono disponibili tre passaggi chiavi per l'installazione di server Jupyter e hello magic Spark nel computer.

* Installare Jupyter Notebook
* Installare hello PySpark e directcompute Spark con hello magic Spark
* Configurare Spark magic tooaccess cluster Spark in HDInsight

Per ulteriori informazioni su kernel personalizzata hello e magic Spark hello disponibili per notebook Jupyter con cluster HDInsight, vedere [kernel disponibile per i server Jupyter notebook con Apache Spark Linux cluster HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Prerequisiti
prerequisiti di Hello elencati di seguito non sono presenti per l'installazione Jupyter. Si tratta per il cluster HDInsight connessione hello Jupyter notebook tooan dopo aver installato notebook hello.

* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="install-jupyter-notebook-on-your-computer"></a>Installare Jupyter Notebook nel computer

Prima di installare i notebook Jupyter è necessario installare Python. Python e Jupyter sono entrambe disponibili come parte di hello [distribuzione Anaconda](https://www.continuum.io/downloads). Quando si installa Anaconda, viene installata una distribuzione di Python. Una volta installato Anaconda, aggiungere installazione Jupyter hello eseguendo i comandi appropriati.

1. Scaricare hello [installer Anaconda](https://www.continuum.io/downloads) per la piattaforma e il programma di installazione di hello esecuzione. Durante l'installazione guidata in esecuzione hello, assicurarsi di selezionare variabile PATH di hello opzione tooadd Anaconda tooyour.
2. Comando che segue di esecuzione hello tooinstall Jupyter.

        conda install jupyter

    Per altre informazioni sull'installazione di Jupyter, vedere l'argomento relativo all' [installazione di Jupyter mediante Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).

## <a name="install-hello-kernels-and-spark-magic"></a>Installare kernel hello e magic Spark

Per istruzioni su come magic di Spark hello tooinstall, hello PySpark e kernel Spark, seguire le istruzioni di installazione hello in hello [sparkmagic documentazione](https://github.com/jupyter-incubator/sparkmagic#installation) su GitHub. Hello primo passaggio nella documentazione di magic Spark hello chiesto magic Spark tooinstall. Sostituire il primo passaggio nel collegamento hello con hello seguenti comandi, a seconda della versione di hello del cluster HDInsight hello che ci si connetterà. Successivamente, seguire hello rimanenti passaggi nella documentazione di magic Spark hello. Se si desidera kernel di tooinstall hello differenti, è necessario eseguire il passaggio 3 nella sezione di istruzioni di installazione magic Spark hello.

* Per i cluster v3.4, installare sparkmagic 0.2.3 eseguendo `pip install sparkmagic==0.2.3`

* Per i cluster v3.5 e v3.6, installare sparkmagic 0.11.2 eseguendo `pip install sparkmagic==0.11.2`

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a>Configurare cluster di Spark tooHDInsight tooconnect magic Spark

In questa sezione è configurare magic Spark hello installato cluster Apache Spark tooan precedenti tooconnect che è necessario avere già creato in Azure HDInsight.

1. informazioni di configurazione Jupyter Hello è in genere archiviato nella home directory di hello gli utenti. toolocate comandi della home directory in qualsiasi piattaforma del sistema operativo, hello tipo seguente.

    Avviare shell di Python hello. In una finestra di comando digitare seguente hello:

        python

    Nella shell di Python hello, immettere hello successivo comando toofind home directory di hello.

        import os
        print(os.path.expanduser('~'))

2. Passare toohello home directory e creare una cartella denominata **.sparkmagic** se non esiste già.
3. Nella cartella hello, creare un file denominato **config. JSON** e aggiungere hello seguente frammento di codice JSON all'interno.

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. Sostituire **{USERNAME}**, **{CLUSTERDNSNAME}** e **{BASE64ENCODEDPASSWORD}** con i valori appropriati. È possibile utilizzare un numero di utilità il linguaggio di programmazione preferito o la password con codifica base64 di toogenerate online per la password effettiva.

5. Configurare impostazioni Heartbeat corrette hello in `config.json`. È necessario aggiungere queste impostazioni in hello stesso livello come hello `kernel_python_credentials` e `kernel_scala_credentials` frammenti di codice le aggiunte in precedenza. Per un esempio di come e dove tooadd hello le impostazioni di heartbeat, vedere questo [config. JSON di esempio](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).

    * Per `sparkmagic 0.2.3` (cluster v3.4), includere:

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * Per `sparkmagic 0.11.2` (cluster v3.5 e v3.6), includere:

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    >Tooensure che le sessioni non vengono comunicate vengono inviati heartbeat. Quando un computer passa toosleep o è stato arrestato, non vengono inviati heartbeat hello, risultante in corso di sessione hello puliti. Per i cluster v3.4, se si desidera toodisable questo comportamento, è possibile impostare hello configurazione inserire il `livy.server.interactive.heartbeat.timeout` troppo`0` da hello Ambari UI. Per la versione 3.5 di cluster, se non si imposta configurazione hello 3.5 precedente, la sessione hello non verrà eliminata.

6. Avviare Jupyter. Utilizzare hello comando seguente dal prompt dei comandi di hello.

        jupyter notebook

7. Verificare che sia possibile connettersi toohello cluster utilizzando notebook Jupyter hello e che è possibile utilizzare magic Spark hello disponibile con il kernel hello. Eseguire hello alla procedura seguente.

    a. Creare un nuovo notebook. Nell'angolo destro hello, fare clic su **New**. Dovrebbe essere kernel predefinito hello **Python2** e hello due directcompute nuova che si installano, **PySpark** e **Spark**. Fare clic su **PySpark**.

    ![Kernel nel notebook di Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernel nel notebook di Jupyter")

    b. Eseguire hello seguente frammento di codice.

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    Se è possibile recuperare correttamente l'output di hello, viene verificato il cluster HDInsight toohello di connessione.

    >[!TIP]
    >Se si desidera tooupdate hello notebook configurazione tooconnect tooa diverso del cluster, aggiornare config. JSON hello con nuovo set di hello di valori, come illustrato nel passaggio 3 precedente.

## <a name="why-should-i-install-jupyter-on-my-computer"></a>Perché installare Jupyter nel computer locale
Può essere un numero di motivi per cui si tooinstall Jupyter nel computer in uso e quindi connetterlo del cluster tooa Spark in HDInsight.

* Anche se Jupyter notebook sono già disponibili nel cluster di hello Spark in HDInsight di Azure, installare Jupyter computer fornisce hello toocreate opzione notebook localmente, testare l'applicazione rispetto a un cluster in esecuzione e quindi caricare hello cluster toohello notebook. cluster di toohello notebook hello tooupload, è possibile caricare tali utilizzando server Jupyter notebook hello che è in esecuzione o hello cluster oppure salvarle toohello /HdiNotebooks cartella nell'account di archiviazione hello associato hello cluster. Per ulteriori informazioni sulla modalità di archiviazione in cluster hello notebook, vedere [in cui sono archiviati i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?
* Con notebook hello disponibili in locale, è possibile connettere il cluster di Spark toodifferent in base alle esigenze dell'applicazione.
* È possibile usare GitHub tooimplement un sistema di controllo del codice sorgente e controllo della versione per notebook hello. È inoltre possibile impostare un ambiente di collaborazione in cui più utenti lavorino con hello stesso blocco note.
* È possibile lavorare con i notebook in locale anche senza avere un cluster. È sufficiente un tootest cluster i blocchi appunti di base, non toomanually gestire i blocchi appunti o un ambiente di sviluppo.
* Può essere tooconfigure più semplice ambiente di sviluppo locale che non l'installazione di server Jupyter tooconfigure hello in cluster hello.  È possibile sfruttare tutti i software hello installato localmente senza configurare uno o più cluster remoto.

> [!WARNING]
> Con Jupyter installato nel computer locale, più utenti possono eseguire hello stesso blocco appunti sul cluster Spark stesso in hello hello contemporaneamente. In questo caso, vengono create più sessioni di Livy. Se si verifica un problema e si desidera che sarà tootrack un'attività complessa la sessione di inserire il cui appartiene l'utente toowhich toodebug.
>
>

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
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)
