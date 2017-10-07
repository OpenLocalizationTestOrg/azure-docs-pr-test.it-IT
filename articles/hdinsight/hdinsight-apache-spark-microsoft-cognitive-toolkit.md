---
title: aaaMicrosoft cognitivi Toolkit con Azure HDInsight Spark per deep learning | Documenti Microsoft
description: "Informazioni su come un training Microsoft cognitivi Toolkit completa modello di apprendimento può essere applicato tooa set di dati utilizzando hello Spark Python API in un cluster Azure HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a>Usare il modello di apprendimento approfondito Microsoft Cognitive Toolkit con un cluster Azure HDInsight Spark

In questo articolo, hello i passaggi seguenti.

1. Eseguire un tooinstall script personalizzato Microsoft cognitivi Toolkit in un cluster Azure HDInsight Spark.

2. Caricare un toosee cluster Spark di Jupyter notebook toohello come tooapply con training Microsoft cognitivi Toolkit deep learning toofiles modello in un Account di archiviazione Blob di Azure utilizzando hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)

## <a name="prerequisites"></a>Prerequisiti

* **Una sottoscrizione di Azure**. Prima di iniziare questa esercitazione, è necessario disporre di un abbonamento ad Azure. Vedere [Crea subito il tuo account Azure gratuito](https://azure.microsoft.com/free).

* **Cluster Azure HDInsight Spark**. Per eseguire la procedura dell'articolo, creare un cluster Spark 2.0. Per le istruzioni, vedere [Creare un cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-does-this-solution-flow"></a>Svolgimento della soluzione

Questa soluzione è suddivisa tra questo articolo e un notebook di Jupyter che deve essere caricato come parte di questa esercitazione. In questo articolo è completare hello alla procedura seguente:

* Eseguire un'azione di script in un cluster di HDInsight Spark tooinstall Microsoft cognitivi Toolkit e Python pacchetti.
* Caricare notebook Jupyter hello che esegue hello soluzione toohello cluster HDInsight Spark.

Hello seguenti passaggi rimanenti vengono trattati in notebook Jupyter hello.

- Caricare immagini di esempio in un set di dati resilienti distribuito di Spark o RDD
   - Caricare i moduli e definire i set di impostazioni
   - Scaricare hello set di dati in locale nel cluster Spark hello
   - Convertire i set di dati hello in un RDD
- Immagini di hello punteggio usando un modello del Toolkit cognitivi con training
   - Scaricare il cluster Spark toohello di hello training Toolkit cognitivi modello
   - Definire le funzioni toobe usata dai nodi di lavoro
   - Immagini di punteggio hello nei nodi di lavoro
   - Valutare l'accuratezza del modello


## <a name="install-microsoft-cognitive-toolkit"></a>Installare Microsoft Cognitive Toolkit

È possibile installare Microsoft Cognitive Toolkit in un cluster Spark tramite l'azione script. Genera script azione utilizza componenti tooinstall script personalizzati nel cluster hello che non sono disponibili per impostazione predefinita. È possibile utilizzare uno script personalizzato hello da hello del portale di Azure tramite HDInsight .NET SDK oppure tramite Azure PowerShell. È inoltre possibile utilizzare hello script tooinstall hello toolkit come parte della creazione del cluster, o dopo i cluster di hello sia in esecuzione. 

In questo articolo, utilizziamo hello tooinstall portale hello toolkit, dopo aver creato il cluster hello. Per altri modi toorun hello uno script personalizzato, vedere [HDInsight personalizzare cluster tramite Script azione](hdinsight-hadoop-customize-cluster-linux.md).

### <a name="using-hello-azure-portal"></a>Utilizzo di hello portale di Azure

Per istruzioni su come toouse hello Azure Portal toorun eseguito uno script di azione, vedere [HDInsight personalizzare cluster tramite Script azione](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation). Assicurarsi di fornire hello seguente input tooinstall Microsoft cognitivi Toolkit.

* Specificare un valore per nome dell'azione script hello.

* Per **URI script Bash**, immettere `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.

* Verificare che si esegue uno script hello solo in hello nodi head e di lavoro e deselezionare tutti hello altre caselle di controllo.

* Fare clic su **Crea**.

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a>Caricare hello Jupyter notebook tooAzure cluster HDInsight Spark

hello toouse Microsoft cognitivi Toolkit con cluster Azure HDInsight Spark hello, è necessario caricare notebook Jupyter hello **CNTK_model_scoring_on_Spark_walkthrough.ipynb** cluster Azure HDInsight Spark toohello. Il notebook è disponibile in GitHub all'indirizzo [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).

1. Repository di GitHub hello clone [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration). Per istruzioni tooclone, vedere [clonazione di un repository](https://help.github.com/articles/cloning-a-repository/).

2. Hello portale di Azure, aprire Pannello cluster Spark hello in cui è già stato eseguito il provisioning, fare clic su **Dashboard Cluster**, quindi fare clic su **server Jupyter notebook**.

    È anche possibile avviare notebook Jupyter hello passando toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`. Sostituire \<clustername > con nome hello del cluster HDInsight.

3. Notebook Jupyter hello, fare clic su **caricare** in hello nell'angolo superiore destro e quindi passare toohello percorso in cui è stato clonato repository GitHub hello.

    ![Caricare Jupyter notebook tooAzure cluster HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "caricare Jupyter notebook tooAzure cluster HDInsight Spark")

4. Fare ancora clic su **Carica**.

5. Dopo aver caricato notebook hello, fare clic sul nome del blocco appunti hello hello e segui le istruzioni di hello in blocco per Appunti hello stesso come tooload hello set di dati e come eseguire l'esercitazione hello.

## <a name="see-also"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale](hdinsight-apache-spark-eventhub-streaming.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Application Insight telemetry data analysis using Spark in HDInsight (Analisi dei dati di telemetria di Application Insights con Spark in HDInsight)](hdinsight-spark-analyze-application-insight-logs.md)

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

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
