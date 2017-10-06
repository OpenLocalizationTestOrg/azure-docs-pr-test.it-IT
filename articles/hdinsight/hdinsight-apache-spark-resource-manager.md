---
title: cluster di risorse aaaManage per Apache Spark in HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse gestire risorse per i cluster Spark in HDInsight di Azure per ottenere prestazioni migliori.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a>Gestire le risorse del cluster Apache Spark in Azure HDInsight 

In questo articolo si apprenderà come interfacce hello tooaccess come Ambari UI e dell'interfaccia utente YARN hello Spark cronologia Server associata con il cluster Spark. Verrà inoltre Scopri come tootune hello configurazione del cluster per ottenere prestazioni ottimali.

**Prerequisiti:**

È necessario disporre delle seguenti hello:

* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-do-i-launch-hello-ambari-web-ui"></a>La modalità di avvio dell'interfaccia utente Web Ambari hello?
1. Da hello [portale Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello). È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.
2. Dal Pannello di cluster Spark hello, fare clic su **Dashboard**. Quando richiesto, immettere le credenziali di amministratore hello per cluster Spark hello.

    ![Avviare Ambari](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "Avviare Resource Manager")
3. Questo deve essere avviato hello Ambari dell'interfaccia utente Web, come illustrato di seguito.

    ![Interfaccia utente Web Ambari](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Interfaccia utente Web Ambari")   

## <a name="how-do-i-launch-hello-spark-history-server"></a>Modalità avvio hello Spark cronologia Server?
1. Da hello [portale Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello).
2. Da hello in cluster pannello **collegamenti rapidi**, fare clic su **Dashboard Cluster**. In hello **Dashboard Cluster** pannello, fare clic su **Spark cronologia Server**.

    ![Server cronologia Spark](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Server cronologia Spark")

    Quando richiesto, immettere le credenziali di amministratore hello per cluster Spark hello.

## <a name="how-do-i-launch-hello-yarn-ui"></a>Modalità di avvio dell'interfaccia utente Yarn hello?
È possibile utilizzare hello dell'interfaccia utente YARN toomonitor le applicazioni che sono in esecuzione nel cluster Spark hello.

1. Dal Pannello di hello cluster, fare clic su **Dashboard Cluster**, quindi fare clic su **YARN**.

    ![Avviare l'interfaccia utente di YARN](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > In alternativa, è possibile avviare hello dell'interfaccia utente YARN da hello Ambari UI. Fare clic su toolaunch hello Ambari UI, dal pannello cluster hello **Dashboard del Cluster**e quindi fare clic su **Dashboard del Cluster HDInsight**. Hello Ambari UI, fare clic su **YARN**, fare clic su **collegamenti rapidi**, fare clic su Gestione risorse attivo hello e quindi fare clic su **ResourceManager UI**.
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a>Che cos'è la applicazioni Spark hello cluster ottimale configurazione toorun?
Hello e tre i parametri chiave che possono essere utilizzati per la configurazione di Spark a seconda dei requisiti dell'applicazione sono `spark.executor.instances`, `spark.executor.cores`, e `spark.executor.memory`. Un Executor è un processo avviato per un'applicazione Spark. Viene eseguito sul nodo lavoro hello ed è responsabile toocarry attività hello per un'applicazione hello. numero predefinito di Hello di executor hello executor dimensioni e per ogni cluster è calcolato in base a numero hello di nodi di lavoro e le dimensioni di hello lavoro nodo. Questi elementi sono archiviati `spark-defaults.conf` nei nodi head del cluster hello.

tre parametri di configurazione Hello possono essere configurati a livello di cluster hello (per tutte le applicazioni in esecuzione nel cluster hello) o possono essere specificati per ogni singola applicazione.

### <a name="change-hello-parameters-using-ambari-ui"></a>Modificare i parametri di hello utilizzando Ambari UI
1. Scegliere hello UI Ambari **Spark**, fare clic su **configurazioni**e quindi espandere **spark-impostazioni predefinite personalizzate**.

    ![Impostare parametri con Ambari](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. i valori predefiniti di Hello sono applicazioni di Spark buona toohave 4 eseguite simultaneamente nel cluster di hello. È possibile, le modifiche questi valori dall'interfaccia utente di hello, come illustrato di seguito.

    ![Impostare parametri con Ambari](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. Fare clic su **salvare** toosave modifiche alla configurazione di hello. Nella parte superiore di hello della pagina hello, verrà richiesto toorestart hello tutti i servizi interessati. Fare clic su **Restart**.

    ![Riavviare i servizi](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a>Modificare i parametri in un'applicazione in esecuzione nel server Jupyter notebook hello
Per le applicazioni in esecuzione in server Jupyter notebook di hello, è possibile utilizzare hello `%%configure` modifiche alla configurazione di hello toomake di particolare. Idealmente, è necessario apportare tali modifiche all'inizio di hello di un'applicazione hello, prima di eseguire la prima cella di codice. In questo modo si garantisce che la configurazione hello è applicato toohello inserire il sessione, quando viene creato. Se si desidera toochange hello configurazione in una fase successiva in un'applicazione hello, è necessario utilizzare hello `-f` parametro. Tuttavia, in questo modo tutti sullo stato di avanzamento in hello applicazione andranno persi.

frammento di Hello seguente viene illustrato come toochange hello configurazione per un'applicazione in esecuzione nel server Jupyter.

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

I parametri di configurazione devono essere passati come una stringa JSON e devono essere nella riga successiva hello dopo magic hello, come illustrato nell'esempio la colonna hello.

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a>Lo script spark-submit hello modificare i parametri per un'applicazione inviato tramite
Comando seguente è riportato un esempio di come toochange hello parametri di configurazione per un'applicazione di batch che viene inviato tramite `spark-submit`.

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a>Modificare i parametri hello in un'applicazione inviato tramite cURL
Comando seguente è riportato un esempio di come toochange hello parametri di configurazione per un'applicazione di batch in cui viene inviato utilizzando cURL.

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a>Come è possibile modificare questi parametri nel server Spark Thrift?
Spark Thrift Server fornisce cluster Spark JDBC/ODBC accesso tooa e viene utilizzato tooservice query Spark SQL. Strumenti come Power BI, Tableau e così via utilizzare ODBC protocollo toocommunicate con le query di Spark SQL tooexecute Spark Thrift Server come applicazione Spark. Quando si crea un cluster Spark, due istanze di hello Spark Thrift Server vengono avviati, uno per ogni nodo head. Ogni Server di Spark Thrift sia visibile come un'applicazione di Spark in hello dell'interfaccia utente YARN.

Spark Thrift Server Usa allocazione dinamica dell'executor di nascita e pertanto hello `spark.executor.instances` non viene utilizzato. Utilizza invece Spark Thrift Server `spark.dynamicAllocation.minExecutors` e `spark.dynamicAllocation.maxExecutors` conteggio executor di hello toospecify. i parametri di configurazione di Hello `spark.executor.cores` e `spark.executor.memory` è toomodify hello executor spazio utilizzato. È possibile modificare questi parametri, come illustrato di seguito.

* Espandere hello **avanzate spark-thrift-sparkconf** i parametri di categoria tooupdate hello `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, e `spark.executor.memory`.

    ![Configurare il server Spark Thrift](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* Espandere hello **personalizzato spark-thrift-sparkconf** parametro hello di categoria tooupdate `spark.executor.cores`.

    ![Configurare il server Spark Thrift](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a>Come è possibile modificare memoria hello di hello Spark Thrift Server?
Memoria Spark Thrift Server viene configurato too25% delle dimensioni del nodo head RAM hello, fornito dimensione RAM totale hello del nodo head hello è maggiore di 14GB. È possibile utilizzare hello configurazione della memoria driver hello toochange Ambari UI, come illustrato di seguito.

* Scegliere hello UI Ambari **Spark**, fare clic su **configurazioni**, espandere **avanzate spark env**e quindi specificare il valore di hello per **spark_thrift_cmd_opts**.

    ![Configurare la RAM del server Spark Thrift](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a>La funzionalità di Business Intelligence non è in uso con il cluster Spark. Come riprendere il risorse hello?
Perché si usa l'allocazione dinamica di Spark, hello solo le risorse utilizzate dal server thrift sono risorse hello per due schemi di applicazione hello. tooreclaim queste risorse che è necessario arrestare hello servizi Thrift Server eseguiti nel cluster hello.

1. Hello Ambari UI, dal riquadro di sinistra hello, fare clic su **Spark**.
2. Nella pagina successiva di hello, fare clic su **Spark Thrift server**.

    ![Riavviare il server Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. Dovrebbe essere headnodes di hello due in cui hello Spark Thrift Server è in esecuzione. Fare clic su uno dei headnodes hello.

    ![Riavviare il server Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. la pagina successiva di Hello Elenca tutti i servizi di hello in esecuzione su tale nodo head. Dall'elenco hello hello clic sul pulsante Avanti tooSpark Thrift Server e quindi fare clic su **arrestare**.

    ![Riavviare il server Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. Ripetere questi passaggi in hello altri nodo head anche.

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a>I notebook Jupyter non vengono eseguiti come previsto. Come è possibile riavviare servizio hello?
Avvio dell'interfaccia utente Web Ambari hello come illustrato in precedenza. Dal riquadro di spostamento a sinistra di hello, fare clic su **Jupyter**, fare clic su **azioni servizio**e quindi fare clic su **riavviare tutti**. Verrà avviato servizio Jupyter hello in headnodes hello tutti.

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a>Rilevare l'esaurimento delle risorse
Avvio dell'interfaccia utente Yarn hello come illustrato in precedenza. Nella tabella le metriche del Cluster nella parte superiore dello schermo hello, controllare i valori di **di memoria utilizzata** e **memoria totale** colonne. Se i valori hello 2 sono molto simili, potrebbe non essere disponibile sufficiente risorse toostart hello successiva applicazione. Hello vale toohello **VCores utilizzato** e **VCores totale** colonne. Inoltre, nella visualizzazione principale hello, se è presente un'applicazione è rimasto **accettato** lo stato e non in fase di transizione in **esecuzione** né **non riuscito** stato, potrebbe anche trattarsi di un'indicazione che non stanno toostart sufficienti risorse.

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a>Come terminare un'esecuzione applicazione toofree risorsa?
1. In hello dell'interfaccia utente Yarn, dal pannello sinistro hello, fare clic su **esecuzione**. Elenco delle applicazioni in esecuzione hello determinare toobe applicazione hello terminato, fare clic su hello **ID**.

    ![Terminare App1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "Terminare App1")

2. Fare clic su **Kill applicazione** hello angolo superiore destro, quindi scegliere **OK**.

    ![Terminare App2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "Terminare App2")

## <a name="see-also"></a>Vedere anche
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)

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
