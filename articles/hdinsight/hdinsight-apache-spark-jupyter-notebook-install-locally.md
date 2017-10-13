---
title: Installare Jupyter localmente e connetterlo a un cluster Azure HDInsight Spark | Microsoft Docs
description: Informazioni su come installare il notebook di Jupyter in locale nel computer e su come connetterlo a un cluster Apache Spark in Azure HDInsight.
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
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: ed57a261d81352ec06fedc3ee6c6541a95370d17
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-to-apache-spark-on-hdinsight"></a>Installare un notebook di Jupyter in locale e connetterlo ad Apache Spark in HDInsight

Questo articolo illustra come installare Jupyter Notebook, insieme ai kernel personalizzati PySpark (per Python) e Spark (per Scala) e al magic Spark, e come connettere l'applicazione a un cluster HDInsight. L'installazione di Jupyter nel computer locale può essere dettata da molti motivi e può anche presentare alcuni problemi. Per altre informazioni, vedere la sezione [Perché installare Jupyter nel computer locale](#why-should-i-install-jupyter-on-my-computer) alla fine di questo articolo.

L'installazione di Jupyter e del magic Spark nel computer si articola in tre passaggi chiave.

* Installare Jupyter Notebook
* Installare i kernel PySpark e Spark con il magic Spark
* Configurare il magic Spark per l'accesso al cluster Spark in HDInsight

Per altre informazioni sui kernel personalizzati e su Spark magic disponibili per Jupyter Notebook con il cluster HDInsight, vedere [Kernel disponibili per Jupyter Notebook con cluster HDInsight Spark Linux su HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Prerequisiti
I prerequisiti elencati di seguito non riguardano l'installazione di Jupyter. Riguardano invece la connessione di Jupyter Notebook a un cluster HDInsight dopo l'installazione.

* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="install-jupyter-notebook-on-your-computer"></a>Installare Jupyter Notebook nel computer

Prima di installare i notebook Jupyter è necessario installare Python. Sia Python che Jupyter sono disponibili come parte della [distribuzione Anaconda](https://www.continuum.io/downloads). Quando si installa Anaconda, viene installata una distribuzione di Python. Dopo aver installato Anaconda, aggiungere l'installazione di Jupyter mediante l'esecuzione dei comandi appropriati.

1. Scaricare il [programma di installazione di Anaconda](https://www.continuum.io/downloads) per la piattaforma in uso ed eseguirlo. Quando si esegue l'installazione guidata, assicurarsi di selezionare l'opzione per l'aggiunta di Anaconda alla variabile PATH.
2. Eseguire il comando seguente per installare Jupyter.

        conda install jupyter

    Per altre informazioni sull'installazione di Jupyter, vedere l'argomento relativo all' [installazione di Jupyter mediante Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).

## <a name="install-the-kernels-and-spark-magic"></a>Installare i kernel e il magic Spark

Per le istruzioni su come installare il magic Spark, i kernel Spark e PySpark, seguire le istruzioni di installazione nella [documentazione sparkmagic](https://github.com/jupyter-incubator/sparkmagic#installation) su GitHub. Il primo passaggio nella documentazione relativa al magic Spark richiede di installarlo. Sostituire il primo passaggio nel collegamento con i comandi seguenti, a seconda della versione del cluster HDInsight a cui ci si connetterà. Seguire quindi i passaggi rimanenti nella documentazione relativa al magic Spark. Se si intende installare i diversi kernel, è necessario eseguire il passaggio 3 nella sezione delle istruzioni di installazione del magic Spark.

* Per i cluster v3.4, installare sparkmagic 0.2.3 eseguendo `pip install sparkmagic==0.2.3`

* Per i cluster v3.5 e v3.6, installare sparkmagic 0.11.2 eseguendo `pip install sparkmagic==0.11.2`

## <a name="configure-spark-magic-to-connect-to-hdinsight-spark-cluster"></a>Configurare il magic Spark per la connessione al cluster HDInsight Spark

Questa sezione illustra come configurare il magic Spark installato in precedenza per la connessone a un cluster Apache Spark. È necessario che tale cluster sia già stato creato in Azure HDInsight.

1. Le informazioni di configurazione di Jupyter sono in genere archiviate nella home directory dell'utente. Per individuare la home directory su una qualsiasi piattaforma del sistema operativo, digitare i comandi seguenti.

    Avviare la shell di Python. In una finestra di comando digitare quanto segue:

        python

    Nella shell di Python immettere il comando seguente per individuare la home directory.

        import os
        print(os.path.expanduser('~'))

2. Passare alla home directory e, se non esiste già, creare una cartella denominata **.sparkmagic** .
3. All'interno della cartella creare un file denominato **config.json** e aggiungere a quest'ultimo il frammento di codice JSON seguente.

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

4. Sostituire **{USERNAME}**, **{CLUSTERDNSNAME}** e **{BASE64ENCODEDPASSWORD}** con i valori appropriati. È possibile usare diverse utilità del linguaggio di programmazione preferito o uno strumento online per convertire la password corrente in una password con codifica Base64.

5. Configurare le impostazioni di heartbeat corrette in `config.json`. Queste impostazioni devono essere aggiunte allo stesso livello dei frammenti `kernel_python_credentials` e `kernel_scala_credentials` aggiunti in precedenza. Per un esempio di come e dove aggiungere le impostazioni di heartbeat, vedere questo [file config.json di esempio](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).

    * Per `sparkmagic 0.2.3` (cluster v3.4), includere:

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * Per `sparkmagic 0.11.2` (cluster v3.5 e v3.6), includere:

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    >Gli heartbeat vengono inviati per assicurare che le sessioni non vengano perse. Quando un computer va in sospensione o viene arrestato, l'heartbeat non verrà inviato e la sessione verrà quindi eliminata. Per disabilitare questo comportamento per i cluster v3.4, è possibile impostare la configurazione di Livy `livy.server.interactive.heartbeat.timeout` su `0` dall'interfaccia utente di Ambari. Per i cluster v3.5, se non si imposta la configurazione 3.5 precedente, la sessione non verrà eliminata.

6. Avviare Jupyter. Usare il comando seguente dal prompt dei comandi.

        jupyter notebook

7. Verificare che sia possibile connettersi al cluster mediante Jupyter Notebook e usare il magic Spark disponibile con i kernel. Eseguire i passaggi seguenti.

    a. Creare un nuovo notebook. Nell'angolo a destra fare clic su **Nuovo**. Verranno visualizzati il kernel predefinito **Python2** e i due nuovi kernel installati, **PySpark** e **Spark**. Fare clic su **PySpark**.

    ![Kernel nel notebook di Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernel nel notebook di Jupyter")

    b. Eseguire il frammento di codice seguente.

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    Se è stato possibile recuperare l'output, viene verificata la connessione al cluster HDInsight.

    >[!TIP]
    >Se si desidera aggiornare la configurazione del notebook per connettersi a un cluster differente, aggiornare il file config.json con un nuovo set di valori come illustrato nel Passaggio 3.

## <a name="why-should-i-install-jupyter-on-my-computer"></a>Perché installare Jupyter nel computer locale
Può esistere una serie di motivi per cui è consigliabile installare Jupyter nel computer in uso e quindi connetterlo a un cluster Spark in HDInsight.

* Anche se i notebook Jupyter sono già disponibili nel cluster Spark in Azure HDInsight, l'installazione di Jupyter nel computer offre la possibilità di creare i notebook in locale, testare l'applicazione con un cluster in esecuzione e quindi caricare i notebook nel cluster. È possibile caricare i notebook nel cluster usando Jupyter Notebook già in esecuzione sul cluster oppure salvare i notebook nella cartella /HdiNotebooks nell'account di archiviazione associato al cluster. Per altre informazioni sul modo in cui i notebook vengono archiviati nel cluster, vedere la sezione [Dove sono archiviati i notebook?](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)
* Con i notebook disponibili in locale è possibile connettersi a cluster Spark diversi in base alle esigenze dell'applicazione.
* È possibile usare GitHub per implementare un sistema di controllo del codice sorgente e usare il controllo della versione per il notebook. È anche possibile avere a disposizione un ambiente di collaborazione in cui più utenti possono lavorare allo stesso notebook.
* È possibile lavorare con i notebook in locale anche senza avere un cluster. È necessario avere un cluster solo per eseguire i test dei notebook, non per gestire manualmente i notebook o un ambiente di sviluppo.
* Può essere più semplice configurare il proprio ambiente di sviluppo locale che configurare l'installazione di Jupyter nel cluster.  È possibile sfruttare tutto il software installato localmente senza configurare uno o più cluster remoti.

> [!WARNING]
> Con Jupyter installato nel computer locale più utenti possono eseguire contemporaneamente lo stesso notebook nello stesso cluster Spark. In questo caso, vengono create più sessioni di Livy. Se si verifica un problema e si vuole eseguire il debug, tenere traccia della sessione di Livy che appartiene l'utente sarà un'attività complessa.
>
>

## <a name="seealso"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale](hdinsight-apache-spark-eventhub-streaming.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creare ed eseguire applicazioni
* [Creare un'applicazione autonoma con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Eseguire processi in modalità remota in un cluster Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Strumenti ed estensioni
* [Usare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Usare il plug-in Strumenti HDInsight per IntelliJ IDEA per eseguire il debug di applicazioni Spark in remoto)](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse del cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)
