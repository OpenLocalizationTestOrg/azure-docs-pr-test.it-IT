---
title: Toolkit per Eclipse - Scala creare applicazioni per HDInsight Spark aaaAzure | Documenti Microsoft
description: Utilizzare gli strumenti HDInsight in Azure Toolkit per le applicazioni di Spark toodevelop Eclipse scritte in Scala e inviarli tooan cluster HDInsight Spark, direttamente da essi hello Eclipse IDE.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Utilizzare Azure Toolkit per le applicazioni per un cluster HDInsight Spark toocreate Eclipse

Utilizzare gli strumenti di HDInsight in Azure Toolkit per Eclipse toodevelop applicazioni scritte in Scala di nascita e inviarli cluster Azure HDInsight Spark tooan, direttamente da Eclipse IDE hello. È possibile utilizzare gli strumenti di HDInsight hello plug-in diversi modi:

* toodevelop e presentare una domanda Scala Spark in un cluster HDInsight Spark
* tooaccess le risorse del cluster Azure HDInsight Spark
* toodevelop ed eseguire un'applicazione di Scala Spark in locale

> [!IMPORTANT]
> Questo strumento può essere utilizzato toocreate e inviare le applicazioni solo per un cluster HDInsight Spark in Linux.
> 
> 

## <a name="prerequisites"></a>Prerequisiti

* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development Kit versione 8, che viene utilizzato per il runtime di Eclipse IDE hello. È possibile scaricarlo da hello [sito Web Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Ambiente IDE Eclipse. Questo articolo usa Eclipse Neon. È possibile installarlo dal hello [sito Web di Eclipse](https://www.eclipse.org/downloads/).   
* Spark SDK. È possibile scaricarlo da [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a>Installare gli strumenti di HDInsight in Azure Toolkit per Eclipse e plug-in Scala
### <a name="install-hdinsight-tools"></a>Installare gli strumenti di HDInsight
Gli strumenti HDInsight per Eclipse sono disponibili come parte di Azure Toolkit for Eclipse. Le istruzioni di installazione sono disponibili in [Installazione di Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse-installation.md).
### <a name="install-scala-plugin"></a>Installazione di plug-in Scala
Quando si apre hello Intellij, hello strumenti HDInsight automaticamente rileva se plug-in di Scala non è installato o non. Fare clic su **OK** tooinstall toocontinue e seguire le istruzioni hello da hello Eclipse Marketplace.

 ![Plug-in Scala di installazione automatica](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a>Accedi tooyour sottoscrizione di Azure
1. Avviare Eclipse IDE hello e aprire Esplora Azure. In hello **finestra** menu, fare clic su **Mostra visualizzazione**, quindi fare clic su **altri**. Nella finestra di dialogo di hello visualizzata, espandere **Azure**, fare clic su **Esplora Azure**, quindi fare clic su **OK**.

    ![Finestra di dialogo Show View (Mostra visualizzazione)](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. Pulsante destro del mouse hello **Azure** nodo e quindi fare clic su **Accedi**.
3. In hello **Azure Accedi** finestra di dialogo selezionare il metodo di autenticazione hello, fare clic su **Accedi**, immettere le credenziali di Azure.
   
    ![Finestra di dialogo di accesso di Azure](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. Dopo avere effettuato, hello **sottoscrizioni selezionare** elenchi della finestra di dialogo casella tutte le sottoscrizioni di Azure associate a credenziali hello di hello. Fare clic su **selezionare** tooclose hello finestra di dialogo.

    ![Finestra di dialogo Selezionare le sottoscrizioni](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. In hello **Esplora Azure** espandere **HDInsight** toosee hello cluster HDInsight Spark nella sottoscrizione.
   
    ![Cluster HDInsight Spark in Azure Explorer](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. È inoltre possibile espandere un nome nodo toosee hello risorse cluster (ad esempio, gli account di archiviazione) associato hello cluster.
   
    ![Espansione di risorse toosee del nome di un cluster](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a>Configurare un progetto Spark in Scala per un cluster HDInsight Spark

1. Nell'area di lavoro di hello IDE di Eclipse, fare clic su **File**, fare clic su **New**, quindi fare clic su **progetto**. 
2. Nella creazione guidata nuovo progetto di hello, espandere **HDInsight**selezionare **Spark in HDInsight (Scala)**, quindi fare clic su **Avanti**.

    ![Selezione di hello Spark in HDInsight (Scala) progetto](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. auto di Hello Scala progetto Creazione guidata rileva se plug-in di Scala non è installato o non. Fare clic su **OK** toocontinue download plug-in Scala di hello, quindi seguire hello istruzioni toorestart Eclipse.

    ![Controllo di Scala](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. In hello **nuovo progetto di Scala HDInsight** fornire hello seguente i valori nella finestra di dialogo e quindi fare clic su **Avanti**:
   * Immettere un nome per il progetto hello.
   * In hello **JRE** area, verificare che l'opzione **utilizzare un ambiente di esecuzione JRE** è troppo**JavaSE 1.7** o versione successiva.
   * Assicurarsi che il SDK di Spark sia set toohello percorso in cui sono stati scaricati hello SDK. Hello collegamento toohello download percorso sia incluso in hello [prerequisiti](#prerequisites) più indietro in questo articolo. È inoltre possibile scaricare hello SDK da hello collegamento disponibile nella finestra di dialogo hello.

    ![Finestra di dialogo New HDInsight Scala Project (Nuovo progetto HDInsight Scala)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  In hello successiva finestra di dialogo, fare clic su hello **librerie** scheda e mantenere i valori predefiniti di hello e quindi fare clic su **fine**. 
   
    ![Scheda Libraries (Librerie)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a>Creare un'applicazione Scala per un cluster HDInsight Spark

1. Nell'IDE di Eclipse, da Esplora pacchetti, hello espandere progetto hello creato in precedenza, fare doppio clic su **src**, punto troppo**New**, quindi fare clic su **altri**.
2. In hello **selezionare una procedura guidata** finestra di dialogo espandere **procedure guidate di Scala**, fare clic su **oggetto Scala**, quindi fare clic su **Avanti**.
   
    ![Finestra di dialogo Select a wizard (Seleziona una procedura guidata)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. In hello **Crea nuovo File** nella finestra di dialogo immettere un nome per l'oggetto hello e quindi fare clic su **fine**.
   
    ![Finestra di dialogo Create New File (Crea nuovo file)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. Incollare hello seguente di codice nell'editor di testo hello:
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. Eseguire un'applicazione hello in un cluster HDInsight Spark:
   
   1. Da Esplora pacchetti, nome del progetto hello e quindi scegliere **tooHDInsight inviare applicazione Spark**.        
   2. In hello **invio Spark** fornire hello seguente i valori nella finestra di dialogo e quindi fare clic su **Invia**:
      
      * Per **nome Cluster**, selezionare l'applicazione di cluster di HDInsight Spark in cui si desidera toorun hello.
      * Selezionare un elemento dal progetto Eclipse hello o selezionarne una da un disco rigido. valore predefinito di Hello dipende dall'elemento hello facendo clic su da Esplora pacchetti.
      * In hello **nome della classe principale** dropdownlist, presentazione guidata consente di visualizzare i nomi degli oggetti dal progetto selezionato. Selezionare o immettere uno che si desidera toorun. Se si seleziona l'elemento dal disco rigido, è necessario inserire il nome della classe principale manualmente. 
      * Poiché il codice dell'applicazione hello in questo esempio non richiedono alcun argomento della riga di comando o fare riferimento a contenitori o file, è possibile lasciare hello rimanenti caselle di testo vuote.
        
       ![Finestra di dialogo Spark Submission (Invio Spark)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. Hello **invio Spark** scheda deve iniziare la visualizzazione di stato di avanzamento hello. È possibile arrestare l'applicazione hello facendo clic sul pulsante rosso hello in hello **invio Spark** finestra. È inoltre possibile visualizzare i registri di hello per questa applicazione specifica esecuzione facendo clic sull'icona globo hello (indicato da una casella blu hello nell'immagine hello).
      
       ![Finestra Spark Submission (Invio Spark)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a>Accedere e gestire i cluster HDInsight Spark con gli strumenti HDInsight in Azure Toolkit for Eclipse
È possibile eseguire diverse operazioni con strumenti di HDInsight, incluso l'output di hello processo di accesso.

### <a name="access-hello-job-view"></a>Visualizzazione processo hello di accesso
1. In Esplora Azure espandere **HDInsight**, espandere il nome del cluster Spark hello e quindi fare clic su **processi**. 

    ![Nodo di visualizzazione dei processi](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Fare clic su hello **processi** nodo. gli strumenti di HDInsight Hello consente di rilevare automaticamente se plug-in clipse di hello (fx) E non è installato o non. Fare clic su **OK** toocontinue e seguire istruzioni hello tooinstall hello Eclipse Marketplace e riavviare Eclipse.

    ![Installare E(fx)clipse](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. Aprire hello visualizzazione dei processi da hello **processi** nodo. Nel riquadro di destra hello, hello **Visualizza processo Spark** scheda vengono visualizzate tutte le applicazioni che sono state eseguite nel cluster hello hello. Fare clic su hello nome dell'applicazione hello per cui si desiderano toosee ulteriori dettagli.

    ![Dettagli applicazione](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. Se si passa il mouse sul grafico processi hello, vengono visualizzate informazioni di base per processo in esecuzione. Fare clic sul grafico processi hello Mostra grafico fasi hello e informazioni che ogni processo viene generato l'errore.

    ![Dettagli delle fasi dei processi](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. Registri usati di frequente, tra cui Stderr Driver, Driver Stdout e informazioni di Directory, sono elencati nel hello **Log** scheda.

    ![Dettagli del log](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. È anche possibile aprire hello cronologia Spark dell'interfaccia utente e hello dell'interfaccia utente di YARN (a livello di applicazione hello) facendo clic sul collegamento ipertestuale rispettivi hello nella parte superiore di hello della finestra hello.

### <a name="access-hello-storage-container-for-hello-cluster"></a>Contenitore di archiviazione di hello di accesso per il cluster hello
1. In Esplora Azure espandere hello **HDInsight** toosee nodo radice un elenco di cluster di HDInsight Spark disponibili.
2. Espandere l'account di archiviazione hello toosee nome cluster hello e contenitore di archiviazione predefinito hello per cluster hello.
   
    ![Account di archiviazione e contenitore di archiviazione predefinito](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. Fare clic su nome del contenitore di archiviazione hello associato hello cluster. Nel riquadro di destra hello, fare doppio clic su hello **HVACOut** cartella. Aprire uno dei hello **parte -** i file di output di hello toosee di un'applicazione hello.

### <a name="access-hello-spark-history-server"></a>Server di accesso hello Spark cronologia
1. In Azure Explorer fare clic con il pulsante destro del mouse sul nome del cluster Spark e quindi scegliere **Open Spark History UI** (Apri UI cronologia Spark). Quando richiesto, immettere le credenziali di amministratore hello per cluster hello. È necessario specificare queste durante il provisioning del cluster di hello.
2. Nel dashboard di server cronologia Spark hello, utilizzare toolook nome di applicazione hello per un'applicazione hello appena finita in esecuzione. In hello codice precedente, impostare il nome di applicazione hello utilizzando `val conf = new SparkConf().setAppName("MyClusterApp")`. Il nome dell'applicazione Spark è **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Avviare il portale di Ambari hello
1. In Azure Explorer fare clic con il pulsante destro del mouse sul nome del cluster Spark e quindi scegliere **Open Cluster Management Portal (Ambari)** (Apri portale di gestione cluster - Ambari). 
2. Quando richiesto, immettere le credenziali di amministratore hello per cluster hello. È necessario specificare queste durante il provisioning del cluster di hello.

### <a name="manage-azure-subscriptions"></a>Gestire le sottoscrizioni di Azure
Per impostazione predefinita, gli strumenti di HDInsight in Azure Toolkit per Eclipse sono elencati i cluster Spark hello da tutte le sottoscrizioni di Azure. Se necessario, è possibile specificare per il quale si desidera che il cluster di hello tooaccess le sottoscrizioni di hello. 

1. In soluzioni di Azure, fare clic hello **Azure** nodo radice e quindi fare clic su **Gestisci sottoscrizioni**. 
2. Nella finestra di dialogo hello, deselezionare le caselle di controllo hello per sottoscrizione hello non desidera tooaccess e quindi fare clic su **Chiudi**. È anche possibile fare clic su **Sign Out** se si desidera toosign fuori la sottoscrizione di Azure.

## <a name="run-a-spark-scala-application-locally"></a>Eseguire un'applicazione Spark in Scala localmente
È possibile utilizzare gli strumenti di HDInsight in Azure Toolkit per le applicazioni di Scala Spark toorun Eclipse in locale nella workstation. In genere, queste applicazioni non è necessario accedere alle risorse toocluster, ad esempio un contenitore di archiviazione, ed è possibile eseguire e testarle in locale.

### <a name="prerequisite"></a>Prerequisito
Mentre si esegue un'applicazione hello locale Spark Scala in un computer Windows, è possibile ricevere un'eccezione, come illustrato in [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). che si verifica a causa di un file **WinUtils.exe** mancante in Windows. 

tooresolve questo errore, è necessario [scaricare hello eseguibile](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa percorso **C:\WinUtils\bin**. È quindi necessario aggiungere la variabile di ambiente hello **HADOOP_HOME** e impostare il valore di hello della variabile hello troppo**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Eseguire un'applicazione Spark in Scala locale
1. Avviare Eclipse e creare un progetto. In hello **nuovo progetto** rendere hello opzioni seguenti nella finestra di dialogo e quindi fare clic su **Avanti**.
   
   * Nel riquadro sinistro hello selezionare **HDInsight**.
   * Nel riquadro di destra hello, selezionare **Spark in HDInsight locale eseguire esempio (Scala)**.

    ![Finestra di dialogo Nuovo progetto](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. dettagli di progetto hello tooprovide, seguire i passaggi da 3 a 6 dalla sezione precedente di hello [impostare un progetto di Spark Scala per un cluster HDInsight Spark](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).
3. modello di Hello aggiunge un codice di esempio (**LogQuery**) in hello **src** cartella che è possibile eseguire in locale nel computer in uso.
   
    ![Percorso di LogQuery](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. Hello rapida **LogQuery** applicazione, scegliere troppo**runas**e quindi fare clic su **1 applicazione Scala**. Verrà visualizzato un output simile al seguente in hello **Console** scheda nella parte inferiore di hello:
   
   ![Risultato dell'esecuzione locale dell'applicazione Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a>domande frequenti
Scegliere un'applicazione tooAzure archivio Data Lake, toosubmit **Interactive** modalità durante il processo di hello sign in Azure. Se si seleziona la modalità **Automated** (Automatico), viene visualizzato un errore.

![interative-signin](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

A questo punto, il problema è risolto. È possibile scegliere l'applicazione toosubmit un Cluster di Azure Data Lake con qualsiasi metodo di accesso.

## <a name="feedback-and-known-issues"></a>Commenti, suggerimenti e problemi noti
Il supporto della visualizzazione diretta degli output di Spark non è al momento disponibile.

Se si dispone dei suggerimenti o commenti e suggerimenti o se si verificano problemi quando si utilizza questo strumento, è possibile toosend gratuita noi un'e-mail all'indirizzo hdivstool@microsoft.com.

## <a name="seealso"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale](hdinsight-apache-spark-eventhub-streaming.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Creazione ed esecuzione di applicazioni
* [Creare un'applicazione autonoma con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Eseguire processi in modalità remota in un cluster Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Strumenti ed estensioni
* [Utilizzare Azure Toolkit per IntelliJ toocreate e inviare le applicazioni di Scala di Spark](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizzare Azure Toolkit per le applicazioni in modalità remota tramite VPN Spark toodebug IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utilizzare Azure Toolkit per le applicazioni in modalità remota tramite SSH Spark toodebug IntelliJ](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Gestione delle risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)

