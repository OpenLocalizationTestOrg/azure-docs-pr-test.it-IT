---
title: azione aaaScript - i pacchetti di installazione di Python con Jupyter in Azure HDInsight | Documenti Microsoft
description: Istruzioni dettagliate su come i cluster di pacchetti python esterno toouse notebook Jupyter delle tooconfigure di azione script toouse disponibili con HDInsight Spark.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Utilizzare i pacchetti genera Script azione tooinstall esterni Python per notebook Jupyter cluster Apache Spark in HDInsight
> [!div class="op_single_selector"]
> * [Uso di comandi Magic nelle celle](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Uso di azioni script](hdinsight-apache-spark-python-package-installation.md)
>
>

Informazioni su come toouse azioni Script tooconfigure un cluster di Apache Spark in HDInsight (Linux) toouse esterno,-il contributo della community **python** di casella pacchetti che non sono presenti cluster hello.

> [!NOTE]
> È inoltre possibile configurare un server Jupyter notebook tramite `%%configure` particolare toouse i pacchetti esterni. Per istruzioni, vedere [Usare pacchetti esterni con notebook di Jupyter nei cluster Apache Spark in HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).
> 
> 

È possibile cercare hello [indice del pacchetto](https://pypi.python.org/pypi) per l'elenco completo di hello dei pacchetti disponibili. È anche possibile ottenere un elenco dei pacchetti disponibili da altre origini. È possibile ad esempio installare pacchetti resi disponibili tramite [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) o [conda-forge](https://conda-forge.github.io/feedstocks.html).

In questo articolo si apprenderà come hello tooinstall [TensorFlow](https://www.tensorflow.org/) pacchetto tramite Script Actoin sul cluster e utilizzarlo tramite notebook Jupyter hello.

## <a name="prerequisites"></a>Prerequisiti
È necessario disporre delle seguenti hello:

* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

   > [!NOTE]
   > Se non dispone di un cluster Spark in HDInsight Linux, è possibile eseguire le azioni script durante la creazione del cluster. Visitare documentazione hello [come toouse custom script azioni](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a>Usare pacchetti esterni con i notebook Jupyter

1. Da hello [portale Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello). È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.   

2. Dal Pannello di cluster Spark hello, fare clic su **azioni Script** in **utilizzo**. Eseguire l'azione personalizzata hello che installa TensorFlow nei nodi head di hello e nodi di lavoro hello. script bash Hello possibile fare riferimento da: documentazione di hello visita https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh su [come toouse custom script azioni](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

   > [!NOTE]
   > Esistono due python installazioni cluster hello. Spark utilizzerà l'installazione di python Anaconda hello in `/usr/bin/anaconda/bin`. Fare riferimento a tale installazione nelle azioni personalizzate tramite `/usr/bin/anaconda/bin/pip` e `/usr/bin/anaconda/bin/conda`.
   > 
   > 

3. Aprire un notebook PySpark Jupyter

    ![Creare un nuovo notebook Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Creare un nuovo notebook Jupyter")

4. Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled.pynb. Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo.

    ![Specificare un nome per notebook hello](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "specificare un nome per notebook hello")

5. A questo punto verranno eseguiti il codice relativo a `import tensorflow` e l'esempio di tipo hello world. 

    Codice toocopy:

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    risultato Hello sarà simile al seguente:
    
    ![Esecuzione del codice TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Esecuzione del codice TensorFlow")



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
* [Usare pacchetti esterni con notebook di Jupyter nei cluster Apache Spark in HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)
