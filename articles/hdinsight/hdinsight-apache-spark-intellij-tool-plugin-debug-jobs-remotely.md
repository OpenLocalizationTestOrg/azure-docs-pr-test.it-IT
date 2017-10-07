---
title: "Toolkit per IntelliJ - il Debug delle applicazioni in modalità remota in HDInsight Spark aaaAzure | Documenti Microsoft"
description: Informazioni su come utilizzare gli strumenti di HDInsight in Azure Toolkit per IntelliJ tooremotely debug applicazioni in esecuzione nel cluster HDInsight Spark tramite vpn.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a>Utilizzare Azure Toolkit per le applicazioni di toodebug IntelliJ in modalità remota in HDInsight Spark tramite VPN

Si consiglia di hello modalità di debug di spark applicaltion in remoto tramite ssh. Per istruzioni vedere [Eseguire il debug remoto delle applicazioni Spark su un cluster HDInsight con Azure Toolkit per IntelliJ tramite SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

In questo articolo vengono fornite istruzioni dettagliate su come toouse hello gli strumenti di HDInsight in Azure Toolkit per IntelliJ toosubmit un processo di Spark nel cluster HDInsight Spark e quindi eseguire il debug in modalità remota dal computer desktop. toodo in tal caso, è necessario eseguire hello seguendo i passaggi generali:

1. Creare una rete virtuale di Azure da sito a sito o da punto a sito. passaggi di Hello in questo documento presuppongono l'utilizzo di una rete da sito a sito.
2. Creare un cluster Spark in HDInsight di Azure che fa parte di hello site-to-site rete virtuale di Azure.
3. Verificare la connettività di hello tra nodo head cluster hello e desktop.
4. Creare un'applicazione Scala in IntelliJ IDEA e configurarla per il debug remoto.
5. Esecuzione e il debug di un'applicazione hello.

## <a name="prerequisites"></a>Prerequisiti
* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development Kit. Per installarlo, fare clic [qui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* IntelliJ IDEA. In questo articolo viene usata la versione 2017.1. Per installarlo, fare clic [qui](https://www.jetbrains.com/idea/download/).
* Strumenti HDInsight nel Toolkit di Azure per IntelliJ. Strumenti HDInsight per IntelliJ sono disponibili come parte di Azure Toolkit per IntelliJ hello. Per istruzioni su come tooinstall hello Azure Toolkit, vedere [installazione hello Azure Toolkit per IntelliJ](../azure-toolkit-for-intellij-installation.md).
* Accedere alla propria sottoscrizione di Azure da IntelliJ IDEA. Seguire le istruzioni di hello [qui](hdinsight-apache-spark-intellij-tool-plugin.md).
* Durante l'esecuzione dell'applicazione di Spark Scala per il debug remoto in un computer Windows, è possibile ricevere un'eccezione, come illustrato in [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) che si verifica a causa di tooa mancante WinUtils.exe in Windows. toowork intorno a questo errore, è necessario [scaricare qui hello eseguibile](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa percorso **C:\WinUtils\bin**. È quindi necessario aggiungere una variabile di ambiente **HADOOP_HOME** e impostare il valore di hello della variabile hello troppo**C\WinUtils**.

## <a name="step-1-create-an-azure-virtual-network"></a>Passaggio 1: Creare una rete virtuale di Azure
Seguire le istruzioni di hello da hello seguito collegamenti toocreate una rete virtuale di Azure e quindi verificare la connettività di hello tra desktop hello e rete virtuale di Azure.

* [Creare una rete virtuale con una connessione VPN da sito a sito tramite il portale di Azure e Azure Resource Manager](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Creare una rete virtuale con una connessione VPN da sito a sito usando PowerShell e Azure Resource Manager](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [Configurare una rete virtuale tooa connessione point-to-site tramite PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a>Passaggio 2: Creare un cluster HDInsight Spark
Inoltre, è necessario creare un cluster Apache Spark in HDInsight di Azure che fa parte di hello rete virtuale di Azure che è stato creato. Utilizzare le informazioni di hello disponibile all'indirizzo [basati su Linux creare cluster HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Come parte della configurazione facoltativa, selezionare hello rete virtuale di Azure creato nel passaggio precedente hello.

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a>Passaggio 3: Verificare la connettività di hello tra nodo head cluster hello e desktop
1. Ottenere l'indirizzo IP hello del nodo head hello. Aprire Ambari UI per cluster hello. Dal Pannello di hello cluster, fare clic su **Dashboard**.

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. Hello Ambari UI, nell'angolo superiore destro di hello, fare clic su **host**.

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. Verrà visualizzato un elenco di nodi head, nodi del ruolo di lavoro e nodi zookeeper. Hello headnodes hanno hello **hn*** prefisso. Fare clic su nodo head prima hello.

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. Nella parte inferiore di hello della pagina hello che viene aperta, da hello **riepilogo** casella Indirizzo IP di hello copia del nodo head hello e il nome host hello.

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. Includere l'indirizzo IP hello e il nome host di hello di hello nodo head toohello **host** file nel computer hello in cui si desidera toorun e debug in modalità remota i processi di Spark hello. Ciò consentirà toocommunicate con il nodo head hello utilizzando l'indirizzo IP hello nonché hostname hello.

   1. Aprire un blocco note con autorizzazioni elevate. Scegliere dal menu file hello **aprire** e quindi passare toohello percorso del file host hello. In un computer Windows è `C:\Windows\System32\Drivers\etc\hosts`.
   2. Aggiungere hello seguente toohello **host** file.

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. Dal computer hello che si è connessi toohello rete virtuale di Azure che viene utilizzato dal cluster HDInsight hello, verificare che è possibile effettuare il ping entrambi headnodes hello utilizzando l'indirizzo IP hello nonché hostname hello.
7. SSH nel nodo head del cluster di hello utilizzando istruzioni hello in [cluster di HDInsight tooan Connetti tramite SSH](hdinsight-hadoop-linux-use-ssh-unix.md). Dal nodo head del cluster di hello, eseguire il ping hello di indirizzo IP del computer desktop hello. È necessario testare la connettività tooboth hello assegnati indirizzi IP computer toohello, uno per la connessione di rete hello e hello altri per hello rete virtuale di Azure che hello computer è connesso.
8. Ripetere i passaggi di hello per hello altri nodo head anche.

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a>Passaggio 4: Creare un'applicazione di Scala Spark usando gli strumenti di HDInsight hello in Azure Toolkit per IntelliJ e configurarlo per il debug remoto
1. Avviare IntelliJ IDEA e creare un nuovo progetto. In hello dialogo Nuovo progetto, rendere hello opzioni seguenti e quindi fare clic su **Avanti**.

    ![Creazione di un'applicazione Spark in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * Nel riquadro sinistro hello selezionare **HDInsight**.
   * Nel riquadro destro hello selezionare **Spark in HDInsight (Scala)**.
   * Fare clic su **Avanti**.
2. Nella finestra successiva hello forniscono hello seguenti dettagli di progetto e quindi fare clic su **fine**.  
   - Specificare un nome per il progetto e il relativo percorso.
   - Per **Project SDK**, usare Java 1.8 per cluster Spark 2.x, Java 1.7 per cluster Spark 1.x.
   - Per la **Versione di Spark**, la creazione guidata del progetto Scala integra la versione corretta per Spark SDK e Scala SDK. Se la versione del cluster spark hello è 2.0 inferiore, scegliere nascita 1. x. In caso contrario, selezionare Spark 2.x. In questo esempio viene usata la versione Spark 2.0.2 (Scala 2.11.8).
       ![Creare un'applicazione Spark in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)
  
3. progetto Spark Hello creerà automaticamente un elemento per l'utente. elemento hello toosee, seguire questi passaggi.

   1. Da hello **File** menu, fare clic su **struttura del progetto**.
   2. In hello **struttura del progetto** la finestra di dialogo, fare clic su **elementi** toosee hello predefinito l'elemento viene creato.
   ![Creare un file con estensione jar](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)

      È inoltre possibile creare la propria artefatto bly facendo clic su hello  **+**  icona, evidenziata nell'immagine di hello precedente.

4. Aggiungere le librerie tooyour progetto. tooadd una libreria, fare doppio clic su nome progetto hello nella struttura di progetto hello e quindi fare clic su **aprire le impostazioni del modulo**. In hello **struttura del progetto** la finestra di dialogo, nel riquadro di sinistra hello, fare clic su **librerie**, fare clic sul simbolo hello (+) e quindi fare clic su **da Maven**.

    ![Aggiunta di una libreria](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    In hello **Download Library dal Repository di Maven** finestra di dialogo, cercare e aggiungere hello seguenti librerie.

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. Copia `yarn-site.xml` e `core-site.xml` da hello nodo head del cluster e aggiungerla toohello progetto. Utilizzare i seguenti comandi toocopy hello file hello. È possibile utilizzare [Cygwin](https://cygwin.com/install.html) seguente hello toorun `scp` comandi file hello toocopy headnodes cluster hello.

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    Poiché è stata già aggiunta hello cluster nodo head IP indirizzo e i nomi host fo hello file hosts sul desktop di hello, possiamo utilizzare hello **scp** comandi nel seguente modo hello.

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    Aggiungere questi file di progetto tooyour copiandoli in hello **/src** cartella nella struttura del progetto, ad esempio `<your project directory>\src`.
6. Hello aggiornamento `core-site.xml` hello toomake dopo le modifiche.

   1. `core-site.xml`include l'account di archiviazione chiavi toohello crittografato hello associato hello cluster. In hello `core-site.xml` che è stato aggiunto progetto toohello, chiave di crittografato hello sostituire con la chiave di archiviazione effettivo hello associata con l'account di archiviazione predefinito hello. Vedere la sezione [Gestire le chiavi di accesso alle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. Rimuovere hello seguendo le voci dalla hello `core-site.xml`.

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. Salvare il file hello.
7. Aggiungere classe di hello principale per l'applicazione. Da hello **Esplora progetti**, fare doppio clic su **src**, punto troppo**New**, quindi fare clic su **Scala classe**.

    ![Aggiunta di un codice sorgente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. In hello **Crea nuova classe Scala** finestra di dialogo immettere un nome, per **tipo** selezionare **oggetto**, quindi fare clic su **OK**.

    ![Aggiunta di un codice sorgente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. In hello `MyClusterAppMain.scala` file, incollare hello seguente codice. Questo codice crea il contesto di Spark hello e avvia un `executeJob` metodo hello `SparkSample` oggetto.

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. Ripetere i passaggi 8 e 9 di sopra di un nuovo oggetto di Scala denominato tooadd `SparkSample`. classe toothis aggiungere hello seguente codice. Questo codice legge i dati di hello da hello HVAC.csv (disponibile in tutti i cluster HDInsight Spark), recupera le righe hello solo con una cifra nella colonna settimo hello hello CSV e scrive l'output di hello troppo**/HVACOut** in predefinito hello contenitore di archiviazione per cluster hello.

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. Ripetere i passaggi 8 e 9 di sopra di una nuova classe denominata tooadd `RemoteClusterDebugging`. Questa classe implementa framework di test di Spark hello che viene utilizzato per il debug di applicazioni. Aggiungere i seguenti toohello codice hello `RemoteClusterDebugging` classe.

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     Alcuni aspetti importanti toonote qui:

   * Per `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, assicurarsi che sia disponibile nell'archiviazione cluster hello nel percorso specificato hello hello assembly Spark JAR.
   * Per `setJars`, specificare il percorso di hello in cui verranno creati file jar di elemento di hello. In genere è `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.
12. In hello `RemoteClusterDebugging` classe destro del mouse su hello `test` (parola chiave) e selezionare **Crea configurazione RemoteClusterDebugging**.

    ![Creazione della configurazione remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. Nella finestra di dialogo hello, specificare un nome per la configurazione di hello e selezionare hello **Test tipo** come **nome Test**. Mantenere l'impostazione predefinita per tutti gli altri valori, fare clic su **Apply** (Applica) e quindi su **OK**.

    ![Creazione della configurazione remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. Verrà visualizzato un **remoto eseguire** configurazione elenco a discesa nella barra dei menu hello.

    ![Creazione della configurazione remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a>Passaggio 5: Esecuzione di un'applicazione hello in modalità debug
1. Nel progetto IntelliJ IDEA, aprire `SparkSample.scala` e creare un rdd1 too'val successivo punto di interruzione '. Nel menu a comparsa hello per la creazione di un punto di interruzione, selezionare **riga nella funzione executeJob**.

    ![Aggiunta di un punto di interruzione](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. Fare clic su hello **Debug eseguire** pulsante Avanti toohello **remoto eseguire** toostart elenco a discesa configurazione in esecuzione un'applicazione hello.

    ![Eseguire il programma di hello in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. Quando l'esecuzione del programma hello raggiunge il punto di interruzione hello, vedrai un **Debugger** scheda nel riquadro inferiore hello.

    ![Eseguire il programma di hello in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. Fare clic su hello (**+**) tooadd icona un'espressione di controllo come illustrato nell'immagine di hello riportata di seguito.

    ![Eseguire il programma di hello in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    In questo caso, perché si è interrotta un'applicazione hello prima variabile hello `rdd1` è stato creato, utilizzando questa espressione di controllo è possibile vedere quali sono hello prime 5 righe nella variabile hello `rdd`. Premere **INVIO**.

    ![Eseguire il programma di hello in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    Ciò che viene visualizzato nell'immagine di hello sopra è in fase di esecuzione, è possibile eseguire una query terrabytes dei dati e di debug come l'avanzamento dell'applicazione. Ad esempio, nell'output di hello illustrato nell'immagine di hello precedente, si noterà che hello prima riga dell'output di hello è un'intestazione. In base a ciò, è possibile modificare la riga di intestazione hello tooskip codice di applicazione se necessario.
5. È ora possibile fare clic su hello **programma Resume** tooproceed icona con l'applicazione di eseguire.

    ![Eseguire il programma di hello in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. Se un'applicazione hello viene completata correttamente, verrà visualizzato un output simile hello seguente.

    ![Eseguire il programma di hello in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <a name="seealso"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demo
* Creare il progetto Scala (video): [Creare applicazioni Spark in Scala](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Eseguire il Debug remoto (Video): [utilizzare Azure Toolkit per le applicazioni in modalità remota nel HDInsight Cluster Spark toodebug IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

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
* [Utilizzare gli strumenti di HDInsight in Azure Toolkit per IntelliJ toocreate e inviare applicazioni Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizzare Azure Toolkit per le applicazioni in modalità remota tramite SSH Spark toodebug IntelliJ](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Utilizzare gli strumenti di HDInsight in Azure Toolkit per le applicazioni di Spark toocreate Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)
