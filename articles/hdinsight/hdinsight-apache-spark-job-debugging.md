---
title: aaaDebug Apache Spark processi in esecuzione in Azure HDInsight | Documenti Microsoft
description: Utilizzo dell'interfaccia utente YARN, interfaccia utente di Spark e la cronologia di Spark server tootrack ed eseguire il debug dei processi in esecuzione in un cluster Spark in HDInsight di Azure
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>Eseguire il debug di processi Apache Spark in esecuzione in Azure HDInsight

In questo articolo si apprenderà come tootrack e debug nascita processi in esecuzione nel cluster di HDInsight con hello dell'interfaccia utente YARN, interfaccia utente di Spark e hello Spark cronologia Server. Per questo articolo, si inizierà un processo di Spark utilizzando un notebook disponibile con i cluster di Spark hello, **Machine learning: analisi predittiva su dati di ispezione di cibo utilizzando MLLib**. È possibile utilizzare passaggi hello di sotto di un'applicazione che è stato inviato utilizzando qualsiasi altro approccio, ad esempio, tootrack **spark-submit**.

## <a name="prerequisites"></a>Prerequisiti
È necessario disporre delle seguenti hello:

* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* È consigliabile esecuzione è stata avviata notebook hello, ** [Machine learning: analisi predittiva su dati di ispezione di cibo utilizzando MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**. Per istruzioni su come toorun il blocco, seguire hello collegamento.  

## <a name="track-an-application-in-hello-yarn-ui"></a>Tenere traccia di un'applicazione hello YARN UI
1. Avvio dell'interfaccia utente YARN hello. Dal Pannello di hello cluster, fare clic su **Dashboard Cluster**, quindi fare clic su **YARN**.
   
    ![Avviare l'interfaccia utente di YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > In alternativa, è possibile avviare hello dell'interfaccia utente YARN da hello Ambari UI. Fare clic su toolaunch hello Ambari UI, dal pannello cluster hello **Dashboard del Cluster**e quindi fare clic su **Dashboard del Cluster HDInsight**. Hello Ambari UI, fare clic su **YARN**, fare clic su **collegamenti rapidi**, fare clic su Gestione risorse attivo hello e quindi fare clic su **ResourceManager UI**.    
   > 
   > 
2. Poiché è stato avviato il processo di Spark hello notebook Jupyter, un'applicazione hello ha nome hello **remotesparkmagics** (questo è il nome di hello per tutte le applicazioni che vengono avviati da notebook hello). Fare clic su ID applicazione hello contro hello applicazione nome tooget ulteriori informazioni sul processo hello. Verrà avviata la visualizzazione di applicazioni hello.
   
    ![Trovare un ID applicazione di Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    Per le applicazioni avviate dal notebook Jupyter hello, è sempre stato hello **esecuzione** fino a quando non si esce da notebook hello.
3. Dalla visualizzazione applicazione hello, è possibile visualizzare ulteriormente toofind i contenitori di hello associata a un'applicazione hello e registri di hello (stdout/stderr). È anche possibile avviare l'interfaccia utente di Spark hello facendo clic sul collegamento corrispondente toohello hello **rilevamento URL**, come illustrato di seguito. 
   
    ![Scaricare i log del contenitore](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a>Tenere traccia di un'applicazione hello Spark UI
Nell'interfaccia utente di Spark hello, è possibile scorrere verso il basso processi Spark hello generati dall'applicazione hello che è stato avviato in precedenza.

1. toolaunch hello Spark UI, dalla visualizzazione applicazione hello, fare clic su collegamento hello contro hello **rilevamento URL**, come illustrato nella cattura di schermata hello precedente. È possibile visualizzare tutti i processi di Spark hello avviati da un'applicazione hello in esecuzione in server Jupyter notebook di hello.
   
    ![Visualizzare processi Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. Fare clic su hello **executor** toosee informazioni di elaborazione e archiviazione per ogni esecutore della scheda. È inoltre possibile recuperare nello stack di chiamate hello facendo clic su hello **Thread Dump** collegamento.
   
    ![Visualizzare gli executor Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. Fare clic su hello **fasi** scheda fasi hello toosee associate a un'applicazione hello.
   
    ![Visualizzare le fasi di Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    Ogni fase può avere più attività per cui è possibile visualizzare le statistiche di esecuzione, come illustrato di seguito.
   
    ![Visualizzare le fasi di Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. Dalla pagina dei dettagli di hello fase, è possibile avviare visualizzazione DAG. Espandere hello **visualizzazione DAG** collegamento nella parte superiore di hello della pagina di hello, come illustrato di seguito.
   
    ![Mostrare la visualizzazione DAG delle fasi di Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    DAG o diretta Aclyic grafico rappresenta hello nelle diverse fasi applicazione hello. Ogni casella blu nel grafico hello rappresenta un'operazione di Spark richiamata da un'applicazione hello.
5. Dalla pagina dei dettagli di hello fase, è possibile avviare visualizzazione della cronologia di applicazione hello. Espandere hello **evento Timeline** collegamento nella parte superiore di hello della pagina di hello, come illustrato di seguito.
   
    ![Visualizzare e la sequenza temporale di eventi delle fasi di Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    Consente di visualizzare gli eventi di Spark hello forma hello di una sequenza temporale. visualizzazione cronologia Hello è disponibile a tre livelli, tra i processi, all'interno di un processo e all'interno di una fase. immagine di Hello precedente acquisisce visualizzazione cronologia hello per una determinata fase.
   
   > [!TIP]
   > Se si seleziona hello **Abilita zoom** casella di controllo, è possibile scorrere a sinistra e destra in visualizzazione cronologia hello.
   > 
   > 
6. Altre schede nell'interfaccia utente di Spark hello forniscono informazioni utili sull'istanza di Spark hello anche.
   
   * Scheda archiviazione - se l'applicazione crea un RDDs, è possibile trovare informazioni su quelli nella scheda archiviazione hello.
   * Scheda ambiente - questa scheda vengono fornite numerose informazioni utili sull'istanza, ad esempio hello Spark 
     * Versione di Scala
     * Directory log di eventi associato hello cluster
     * Numero di core esecutore per un'applicazione hello
     * e così via.

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a>Trovare informazioni sui processi completati utilizzando hello Spark cronologia Server
Al termine di un processo, informazioni di hello processo hello sono persistente nel hello Spark cronologia Server.

1. Fare clic su toolaunch hello Spark cronologia Server, dal Pannello di cluster hello, **Dashboard del Cluster**, quindi fare clic su **Spark cronologia Server**.
   
    ![Avviare Server cronologia Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > In alternativa, è anche possibile avviare hello interfaccia utente del Server Spark cronologia da hello Ambari UI. Fare clic su toolaunch hello Ambari UI, dal pannello cluster hello **Dashboard del Cluster**e quindi fare clic su **Dashboard del Cluster HDInsight**. Hello Ambari UI, fare clic su **Spark**, fare clic su **collegamenti rapidi**, quindi fare clic su **interfaccia utente del Server Spark cronologia**.
   > 
   > 
2. Si noterà che tutte le applicazioni elencate hello completata. Fare clic su un toodrill ID applicazione verso il basso in un'applicazione per altre informazioni.
   
    ![Avviare Server cronologia Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a>Vedere anche
*  [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a>Per gli analisti dei dati

* [Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Application Insight telemetry data analysis using Spark in HDInsight (Analisi dei dati di telemetria di Application Insights con Spark in HDInsight)](hdinsight-spark-analyze-application-insight-logs.md)
* [Usare Caffe in Azure HDInsight Spark per l'apprendimento avanzato distribuito](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Per gli sviluppatori di Spark

* [Creare un'applicazione autonoma con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Eseguire processi in modalità remota in un cluster Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale](hdinsight-apache-spark-eventhub-streaming.md)
* [Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


