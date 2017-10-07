---
title: 'Azure Toolkit for IntelliJ: Creare applicazioni Spark per un cluster HDInsight | Microsoft Docs'
description: Utilizzare hello Azure Toolkit per le applicazioni di Spark toodevelop IntelliJ scritte in Scala e inviarli tooan cluster HDInsight Spark.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Utilizzare Azure Toolkit per le applicazioni per un cluster HDInsight Spark toocreate IntelliJ

Utilizzare hello Azure Toolkit per le applicazioni di Spark toodevelop plug-in IntelliJ scritte in Scala e quindi inviarli tooan cluster HDInsight Spark direttamente dall'ambiente di sviluppo integrato (IDE) di hello IntelliJ. È possibile utilizzare hello plug-in diversi modi:

* Sviluppare e inviare un'applicazione Spark in Scala in un cluster HDInsight Spark.
* Accedere alle risorse cluster HDInsight Spark di Azure.
* Sviluppare ed eseguire un'applicazione Spark in Scala localmente.

toocreate il progetto, hello vista [creare applicazioni Spark con hello Azure Toolkit per IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.

> [!IMPORTANT]
> È possibile utilizzare questo plug-in toocreate e inviare le applicazioni solo per un cluster HDInsight Spark in Linux.
> 

## <a name="prerequisites"></a>Prerequisiti

- Un cluster Apache Spark in HDInsight Linux. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
- Kit di sviluppo di Oracle Java. È possibile installarlo dal hello [sito Web Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
- IntelliJ IDEA. In questo articolo viene usata la versione 2017.1. È possibile installarlo dal hello [sito Web JetBrains](https://www.jetbrains.com/idea/download/).

## <a name="install-azure-toolkit-for-intellij"></a>Installare il Toolkit di Azure per IntelliJ
Per le istruzioni di installazione vedere [Installare Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="sign-in-tooyour-azure-subscription"></a>Accedi tooyour sottoscrizione di Azure

1. Avviare hello IntelliJ IDE, quindi aprire Esplora Azure. In hello **vista** dal menu **finestre degli strumenti**, quindi selezionare **Esplora Azure**.
       
   ![collegamento Esplora Azure Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. Pulsante destro del mouse hello **Azure** nodo e quindi selezionare **Accedi**.

3. In hello **Azure Accedi** nella finestra di dialogo **Accedi**, quindi immettere le credenziali di Azure.

    ![Hello Azure Sign nella finestra di dialogo](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. Dopo avere effettuato, hello **sottoscrizioni selezionare** tutti hello sottoscrizioni Azure in cui sono associate elenchi di finestra di dialogo casella hello credenziali. Seleziona hello **selezionare** pulsante.

    ![la finestra di dialogo selezionare le sottoscrizioni di Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. In hello **Esplora Azure** espandere **HDInsight** hello tooview cluster HDInsight Spark presenti nella sottoscrizione.
   
    ![Cluster HDInsight Spark in Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. tooview hello risorse (ad esempio, gli account di archiviazione) che sono associate ai cluster hello, è possibile espandere ulteriormente un nodo del nome del cluster.
   
    ![Nodo di tipo nome del cluster espanso](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Eseguire un'applicazione Spark in Scala in un cluster HDInsight Spark

1. Avviare IntelliJ IDEA e creare un progetto. In hello **nuovo progetto** finestra di dialogo casella, hello seguenti: 

   a. Selezionare **HDInsight** > **Spark on HDInsight (Scala)** (Spark in HDInsight - Scala).

   b. In hello **strumento di compilazione** selezionare uno dei hello seguenti, in base tooyour necessità:

      * **Maven**, per ottenere supporto per la creazione guidata di un progetto Scala
      * **SBT**, per la gestione delle dipendenze hello e la compilazione per il progetto di Scala hello

    ![finestra di dialogo Nuovo progetto Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. Selezionare **Avanti**.

3. Hello Scala-creazione del progetto verrà rilevato automaticamente se è stato installato hello Scala plug-in. Selezionare **Installa**.

   ![Verifica del plug-in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. hello toodownload Scala plug-in, seleziona **OK**. Seguire le istruzioni di hello toorestart IntelliJ. 

   ![finestra di dialogo dell'installazione di plug-in Scala Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. In hello **nuovo progetto** finestra hello seguenti:  

    ![Selezione di hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   a. Immettere un nome e un percorso per il progetto.

   b. In hello **Project SDK** elenco a discesa, seleziona **Java 1.8** per cluster 2. x di Spark hello o selezionare **Java 1.7** per cluster 1. x di hello Spark.

   c. In hello **versione Spark** elenco a discesa, creazione guidata nuovo progetto di Scala si integra la versione corretta di hello per SDK Spark e SDK di Scala. Se la versione del cluster Spark hello è precedente alla versione 2.0, selezionare **nascita 1. x**. In caso contrario, selezionare **Spark 2.x**. In questo esempio viene usata la versione **Spark 2.0.2 (Scala 2.11.8)**.

6. Selezionare **Fine**.

7. progetto Spark Hello crea automaticamente un elemento. elemento hello tooview, hello seguenti:

   a. In hello **File** dal menu **struttura del progetto**.

   b. In hello **struttura del progetto** nella finestra di dialogo **elementi** tooview hello predefinito l'elemento viene creato. È inoltre possibile creare la propria artefatto selezionando hello sul segno più (**+**).

      ![Informazioni di elementi nella finestra di dialogo hello](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. Aggiungere il codice sorgente dell'applicazione eseguendo hello seguenti:

   a. In Esplora progetti, fare doppio clic su **src**, punto troppo**New**, quindi selezionare **Scala classe**.
      
      ![Comandi per la creazione di una classe Scala in Project Explorer (Esplora progetti)](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   b. In hello **Crea nuova classe Scala** finestra di dialogo, specificare un nome, selezionare **oggetto** in hello **tipo** e quindi selezionare **OK**.
      
      ![Finestra di dialogo Create New Scala Class (Crea nuova classe Scala)](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   c. In hello **MyClusterApp.scala** file, incollare hello seguente codice. Hello codice legge i dati di hello da HVAC.csv (disponibile in tutti i cluster HDInsight Spark), recupera le righe di hello che contengono solo una cifra nella colonna di settimo hello nel file CSV hello e scrive l'output di hello troppo**/HVACOut** in predefinito hello contenitore di archiviazione per cluster hello.

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. Eseguire un'applicazione hello in un cluster HDInsight Spark eseguendo hello seguenti:

   a. In Esplora progetti, nome del progetto hello e quindi scegliere **tooHDInsight inviare applicazione Spark**.
      
      ![comando tooHDInsight inviare Spark applicazione Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   b. Si sono tooenter richieste le credenziali di sottoscrizione di Azure. In hello **invio Spark** fornire hello seguente i valori nella finestra di dialogo e quindi selezionare **Invia**.
      
      * Per **nascita cluster (solo Linux)**, selezionare l'applicazione di cluster di HDInsight Spark in cui si desidera toorun hello.

      * Selezionare un elemento dal progetto IntelliJ hello o selezionarne uno dall'unità disco rigido hello.

      * In hello **nome della classe principale** casella, i puntini di sospensione selezionare hello (**...** ), selezionare la classe principale hello nel codice sorgente dell'applicazione, quindi **OK**.

        ![finestra di dialogo Seleziona classe Main Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * Poiché il codice dell'applicazione hello in questo esempio non richiede argomenti della riga di comando o fare riferimento a contenitori o file, è possibile lasciare hello rimanenti caselle vuote. Dopo aver fornito tutte le informazioni di hello, la finestra di dialogo hello dovrebbe essere simile a hello seguente immagine.
        
        ![la finestra di dialogo di invio Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   c. Hello **invio Spark** scheda nella parte inferiore di hello della finestra hello deve iniziare la visualizzazione di stato di avanzamento hello. È anche possibile arrestare un'applicazione hello selezionando pulsante rosso hello hello **invio Spark** finestra.
      
      ![finestra di invio Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      toolearn come tooaccess hello output del processo, vedere hello "accesso e gestire i cluster di HDInsight Spark usando Azure Toolkit per IntelliJ" più avanti in questo articolo.

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Eseguire o eseguire il debug di un'applicazione Spark Scala in un cluster HDInsight Spark
Si consiglia inoltre di un altro modo per cluster di toohello hello Spark applicazione di invio. È possibile farlo impostando i parametri di hello in hello **le configurazioni di esecuzione/Debug** IDE. Per altre informazioni vedere [Eseguire il debug remoto delle applicazioni Spark su un cluster HDInsight con Azure Toolkit for IntelliJ tramite SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a>Accedere e gestire i cluster HDInsight Spark tramite il Toolkit di Azure per IntelliJ
È possibile eseguire diverse operazioni mediante il Toolkit Azure per IntelliJ.

### <a name="access-hello-job-view"></a>Visualizzazione processo hello di accesso
1. In Esplora Azure espandere **HDInsight**, espandere il nome del cluster Spark hello e quindi selezionare **processi**.  

    ![Nodo di visualizzazione dei processi](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Nel riquadro di destra hello, hello **Visualizza processo Spark** scheda vengono visualizzate tutte le applicazioni che sono state eseguite nel cluster hello hello. Selezionare il nome di hello di un'applicazione hello per cui si desiderano toosee ulteriori dettagli.

    ![Dettagli applicazione](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. toodisplay esecuzione processo informazioni di base, passare il mouse sul grafico processi hello. grafico di fasi tooview hello e le informazioni che ogni processo viene generato l'errore, selezionare un nodo nel grafico processi hello.

    ![Dettagli delle fasi dei processi](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. tooview utilizzati di frequente i log, ad esempio *Driver Stderr*, *Driver Stdout*, e *informazioni di Directory*selezionare hello **Log** scheda.

    ![Dettagli del log](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. È anche possibile visualizzare hello cronologia Spark dell'interfaccia utente e dell'interfaccia utente di YARN (a livello di applicazione hello) hello selezionando un collegamento nella parte superiore di hello della finestra hello.

### <a name="access-hello-spark-history-server"></a>Server di accesso hello Spark cronologia
1. In Azure Explorer espandere **HDInsight**, fare clic con il pulsante destro del mouse sul nome del cluster Spark e quindi scegliere **Open Spark History UI** (Apri UI cronologia Spark). 

2. Quando richiesto, immettere le credenziali di amministratore del cluster di hello, specificata durante la configurazione di cluster hello.

3. Nel dashboard di server hello Spark cronologia, è possibile utilizzare hello applicazione nome toolook per un'applicazione hello appena finita in esecuzione. In hello codice precedente, impostare il nome di applicazione hello utilizzando `val conf = new SparkConf().setAppName("MyClusterApp")`. Il nome dell'applicazione Spark è quindi **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Avviare il portale di Ambari hello
1. In Azure Explorer espandere **HDInsight**, fare clic con il pulsante destro del mouse sul nome del cluster Spark e quindi scegliere **Open Cluster Management Portal (Ambari)** (Apri il portale di gestione cluster - Ambari). 

2. Quando richiesto, immettere le credenziali di amministratore hello per cluster hello. Queste credenziali è stato specificato durante l'installazione del cluster hello.

### <a name="manage-azure-subscriptions"></a>Gestire le sottoscrizioni di Azure
Per impostazione predefinita, Azure Toolkit per IntelliJ sono elencati i cluster Spark hello da tutte le sottoscrizioni di Azure. Se necessario, è possibile specificare che si desidera tooaccess le sottoscrizioni di hello. 

1. In soluzioni di Azure, fare clic hello **Azure** nodo radice e quindi selezionare **Gestisci sottoscrizioni**. 

2. Nella finestra di dialogo hello cancellare hello caselle di controllo successive toohello sottoscrizioni che non desidera tooaccess e quindi selezionare **Chiudi**. È inoltre possibile selezionare **Sign Out** se si desidera toosign fuori la sottoscrizione di Azure.

## <a name="run-a-spark-scala-application-locally"></a>Eseguire un'applicazione Spark in Scala localmente
È possibile utilizzare Azure Toolkit per le applicazioni di Scala Spark toorun IntelliJ in locale nella workstation. applicazioni Hello in genere non è necessario accedere toocluster alle risorse, ad esempio i contenitori di archiviazione, ed è possibile eseguire tali test in locale.

### <a name="prerequisite"></a>Prerequisito
Mentre si esegue un'applicazione hello locale Spark Scala in un computer Windows, è possibile ricevere un'eccezione, come illustrato in [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). perché WinUtils.exe manca in Windows, si verifica un'eccezione di Hello. 

tooresolve questo errore, [scaricare hello eseguibile](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa percorso, ad esempio **C:\WinUtils\bin**. Quindi, aggiungere la variabile di ambiente hello **HADOOP_HOME**e impostare il valore di hello della variabile hello troppo**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Eseguire un'applicazione Spark in Scala locale
1. Avviare IntelliJ IDEA e creare un progetto. 

2. In hello **nuovo progetto** finestra di dialogo casella, hello seguenti:
   
    a. Selezionare **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)** (Spark su esecuzione di esempio locale HDInsight - Scala).

    b. In hello **strumento di compilazione** selezionare uno dei hello seguenti, in base tooyour necessità:

      * **Maven**, per ottenere supporto per la creazione guidata di un progetto Scala
      * **SBT**, per la gestione delle dipendenze hello e la compilazione per il progetto di Scala hello

    ![finestra di dialogo Nuovo progetto Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. Selezionare **Avanti**.
 
4. Nella finestra successiva hello hello seguenti:
   
    a. Immettere un nome e un percorso per il progetto.

    b. In hello **Project SDK** elenco a discesa selezionare una versione di Java che è successiva alla versione 1.7.

    c. In hello **versione Spark** elenco a discesa, la versione di hello selezionare di Scala che si desidera toouse: Scala 2.11.x per Spark 2.0 o Scala 2.10.x per Spark 1.6.

    ![finestra di dialogo Nuovo progetto Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. Selezionare **Fine**.

6. modello di Hello aggiunge un codice di esempio (**LogQuery**) in hello **src** cartella che è possibile eseguire in locale nel computer in uso.
   
    ![Percorso di LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. Pulsante destro del mouse hello **LogQuery** dell'applicazione e quindi selezionare **esecuzione 'LogQuery'**. In hello **eseguire** scheda nella parte inferiore di hello, viene visualizzato un output simile hello seguente:
   
   ![Risultato dell'esecuzione locale dell'applicazione Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a>Converti esistente IntelliJ IDEA applicazioni toouse Azure Toolkit per IntelliJ
È possibile convertire hello Spark Scala le applicazioni esistenti create in IntelliJ IDEA toobe compatibili con Azure Toolkit per IntelliJ. È quindi possibile utilizzare hello toosubmit plug-in hello applicazioni tooan cluster HDInsight Spark.

1. Per un'applicazione di Scala Spark esistente che è stata creata tramite IntelliJ IDEA, aprire il file di .iml associato hello.

2. Livello di radice hello è un **modulo** elemento hello seguente:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   Modifica hello elemento tooadd `UniqueKey="HDInsightTool"` così che hello **modulo** elemento simile hello seguenti:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. Salvare le modifiche di hello. L'applicazione dovrebbe ora essere compatibile con il Toolkit di Azure per IntelliJ. È possibile eseguirne il test facendo clic sul nome del progetto in Project Explorer di hello. menu a comparsa Hello include ora l'opzione hello **tooHDInsight inviare applicazione Spark**.

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a>Errore nell'esecuzione locale: *Usare dimensioni di heap maggiori*
Spark 1.6, se si utilizza un SDK per Java a 32 bit durante l'esecuzione locale, è possibile riscontrare hello gli errori seguenti:

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

Questi errori si verificano perché la dimensione dell'heap hello non è sufficientemente grande per toorun Spark. Spark richiede almeno 471 MB. Per altre informazioni, vedere [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081). Una soluzione semplice è toouse un SDK per Java a 64 bit. È inoltre possibile modificare le impostazioni di JVM hello in IntelliJ aggiungendo hello le opzioni seguenti:

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Aggiunta di opzioni toohello "Opzioni VM" casella in IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a>domande frequenti
Scegliere un'applicazione tooAzure archivio Data Lake, toosubmit **Interactive** modalità durante il processo di hello sign in Azure. Se si seleziona la modalità **Automated** (Automatico), viene visualizzato un errore.

![interative-signin](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

A questo punto, il problema è risolto. È possibile scegliere l'applicazione toosubmit un Cluster di Azure Data Lake con qualsiasi metodo di accesso.

## <a name="feedback-and-known-issues"></a>Commenti, suggerimenti e problemi noti
Il supporto della visualizzazione diretta degli output di Spark non è al momento disponibile.

Per eventuali commenti o suggerimenti oppure se si riscontrano problemi nell'uso di questo plug-in, inviare un messaggio di posta elettronica all'indirizzo hdivstool@microsoft.com.

## <a name="seealso"></a>Passaggi successivi
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demo
* Creare il progetto Scala (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (Creare applicazioni Spark Scala)
* Eseguire il debug remoto (video): [utilizzare Azure Toolkit per le applicazioni in modalità remota nel HDInsight Cluster Spark toodebug IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: usare Spark in HDInsight tooanalyze temperatura utilizzando dati impianto di compilazione](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming di Spark: Usare Spark in HDInsight toobuild in tempo reale lo streaming di applicazioni](hdinsight-apache-spark-eventhub-streaming.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Creazione ed esecuzione di applicazioni
* [Creare un'applicazione autonoma con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Eseguire processi in modalità remota in un cluster Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Strumenti ed estensioni
* [Utilizzare Azure Toolkit per le applicazioni in modalità remota tramite VPN Spark toodebug IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utilizzare Azure Toolkit per le applicazioni in modalità remota tramite SSH Spark toodebug IntelliJ](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Utilizzare gli strumenti di HDInsight in Azure Toolkit per le applicazioni di Spark toocreate Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Gestione delle risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)

