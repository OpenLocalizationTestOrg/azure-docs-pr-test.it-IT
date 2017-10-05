---
title: "Azure Toolkit for IntelliJ: debug delle applicazioni in modalità remota su HDInsight Spark | Microsoft Docs"
description: Informazioni su come usare gli Strumenti HDInsight nel Toolkit di Azure per IntelliJ per il debug remoto di applicazioni in esecuzione nei cluster HDInsight Spark tramite VPN.
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
ms.openlocfilehash: 5ce282aac94d0f22ea587cbe4005819310e23b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-debug-applications-remotely-on-hdinsight-spark-through-vpn"></a>Usare Azure Toolkit per IntelliJ per il debug remoto delle applicazioni su HDInsight Spark tramite VPN

È consigliabile usare la modalità di debug dell'applicazione Spark da remoto tramite SSH. Per istruzioni vedere [Eseguire il debug remoto delle applicazioni Spark su un cluster HDInsight con Azure Toolkit per IntelliJ tramite SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

Questo articolo offre indicazioni dettagliate su come usare gli strumenti HDInsight nel Toolkit di Azure per IntelliJ per inviare un processo Spark nel cluster HDInsight Spark e quindi eseguirne il debug remoto dal computer desktop. A tale scopo, è necessario seguire questa procedura generale:

1. Creare una rete virtuale di Azure da sito a sito o da punto a sito. Le procedure descritte in questo documento presuppongono che si usi una rete da sito a sito.
2. Creare un cluster Spark in Azure HDInsight incluso nella rete virtuale da sito a sito di Azure.
3. Verificare la connettività tra il nodo head del cluster e il PC desktop.
4. Creare un'applicazione Scala in IntelliJ IDEA e configurarla per il debug remoto.
5. Eseguire l'applicazione ed effettuarne il debug.

## <a name="prerequisites"></a>Prerequisiti
* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development Kit. Per installarlo, fare clic [qui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* IntelliJ IDEA. In questo articolo viene usata la versione 2017.1. Per installarlo, fare clic [qui](https://www.jetbrains.com/idea/download/).
* Strumenti HDInsight nel Toolkit di Azure per IntelliJ. Gli strumenti HDInsight per IntelliJ sono disponibili come parte di Azure Toolkit per IntelliJ. Per istruzioni su come installare Azure Toolkit, vedere [Installazione di Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).
* Accedere alla propria sottoscrizione di Azure da IntelliJ IDEA. Seguire le istruzioni riportate [qui](hdinsight-apache-spark-intellij-tool-plugin.md).
* Quando si esegue l'applicazione Spark in Scala per il debug remoto in un computer Windows, potrebbe essere restituita un'eccezione, come illustrato in [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) , causata da un file WinUtils.exe mancante in Windows. Per risolvere questo errore, è necessario [scaricare il file eseguibile da qui](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) in un percorso come **C:\WinUtils\bin**. È quindi necessario aggiungere una variabile di ambiente **HADOOP_HOME** e impostare il valore della variabile su **C\WinUtils**.

## <a name="step-1-create-an-azure-virtual-network"></a>Passaggio 1: Creare una rete virtuale di Azure
Seguire le istruzioni riportate nei collegamenti seguenti per creare una rete virtuale di Azure e quindi verificare la connettività tra il PC desktop e la rete virtuale di Azure.

* [Creare una rete virtuale con una connessione VPN da sito a sito tramite il portale di Azure e Azure Resource Manager](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Creare una rete virtuale con una connessione VPN da sito a sito usando PowerShell e Azure Resource Manager](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [Configurare una connessione da punto a sito a una rete virtuale con PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a>Passaggio 2: Creare un cluster HDInsight Spark
È consigliabile creare anche un cluster Apache Spark in Azure HDInsight incluso nella rete virtuale di Azure creata. Usare le informazioni disponibili in [Creare cluster Hadoop basati su Linux in HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Nell'ambito della configurazione facoltativa, selezionare la rete virtuale di Azure creata nel passaggio precedente.

## <a name="step-3-verify-the-connectivity-between-the-cluster-headnode-and-your-desktop"></a>Passaggio 3: Verificare la connettività tra il nodo head del cluster e il PC desktop
1. Ottenere l'indirizzo IP del nodo head. Aprire l'interfaccia utente di Ambari per il cluster. Dal pannello del cluster fare clic su **Dashboard**.

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. Nell'angolo superiore destro dell'interfaccia utente di Ambari fare clic su **Hosts**(Host).

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. Verrà visualizzato un elenco di nodi head, nodi del ruolo di lavoro e nodi zookeeper. I nodi head hanno il prefisso **hn***. Fare clic sul primo nodo head.

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. Nella parte inferiore della pagina visualizzata copiare l'indirizzo IP del nodo head e il nome host dalla casella **Summary** (Riepilogo).

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. Includere l'indirizzo IP e il nome host del nodo head nel file **hosts** nel computer in cui si vuole eseguire i processi Spark ed effettuarne il debug remoto. Sarà così possibile comunicare con il nodo head usando sia l'indirizzo IP che il nome host.

   1. Aprire un blocco note con autorizzazioni elevate. Scegliere **Apri** dal menu File e quindi passare al percorso del file hosts. In un computer Windows è `C:\Windows\System32\Drivers\etc\hosts`.
   2. Aggiungere quanto riportato di seguito al file **hosts** .

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. Nel computer che è stato connesso alla rete virtuale di Azure usata dal cluster HDInsight verificare che sia possibile effettuare il ping di entrambi i nodi head usando sia l'indirizzo IP che il nome host.
7. Connettersi con SSH al nodo head del cluster seguendo le istruzioni riportate in [Connettersi a un cluster HDInsight basato su Linux](hdinsight-hadoop-linux-use-ssh-unix.md). Dal nodo head del cluster effettuare il ping dell'indirizzo IP del computer desktop. È consigliabile testare la connettività per entrambi gli indirizzi IP assegnati al computer, uno per la connessione di rete e l'altro per la rete virtuale di Azure a cui il computer è connesso.
8. Ripetere questi passaggi anche per l'altro nodo head.

## <a name="step-4-create-a-spark-scala-application-using-the-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a>Passaggio 4: Creare un'applicazione Spark in Scala usando gli strumenti HDInsight nel Toolkit di Azure per IntelliJ e configurarla per il debug remoto
1. Avviare IntelliJ IDEA e creare un nuovo progetto. Nella finestra di dialogo del nuovo progetto selezionare le opzioni seguenti e quindi fare clic su **Next** (Avanti).

    ![Creazione di un'applicazione Spark in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * Selezionare **HDInsight** nel riquadro sinistro.
   * Selezionare **Spark on HDInsight (Scala)**(Spark in HDInsight - Scala) nel riquadro destro.
   * Fare clic su **Avanti**.
2. Nella finestra successiva inserire i dettagli di progetto seguenti e quindi fare clic su **Finish** (Fine).  
   - Specificare un nome per il progetto e il relativo percorso.
   - Per **Project SDK**, usare Java 1.8 per cluster Spark 2.x, Java 1.7 per cluster Spark 1.x.
   - Per la **Versione di Spark**, la creazione guidata del progetto Scala integra la versione corretta per Spark SDK e Scala SDK. Se la versione del cluster Spark è inferiore a 2.0, scegliere Spark 1.x. In caso contrario, selezionare Spark 2.x. In questo esempio viene usata la versione Spark 2.0.2 (Scala 2.11.8).
       ![Creare un'applicazione Spark in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)
  
3. Il progetto Spark creerà automaticamente un elemento. Per visualizzare l'elemento, seguire questa procedura.

   1. Scegliere **Project Structure** (Struttura progetto) dal menu **File**.
   2. Nella finestra di dialogo **Project Structure** (Struttura progetto) fare clic su **Artifacts** (Elementi) per visualizzare l'elemento predefinito creato.
   ![Creare un file con estensione jar](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)

      È anche possibile creare un elemento personalizzato facendo clic sull'icona **+** evidenziata nell'immagine precedente.

4. Aggiungere librerie al progetto. Per aggiungere una libreria, fare clic con il pulsante destro del mouse sul nome del progetto nell'albero del progetto e quindi scegliere **Open Module Settings**(Apri impostazioni modulo). Nella finestra di dialogo **Project Structure** (Struttura progetto) fare clic su **Libraries** (Librerie) nel riquadro sinistro, quindi sul simbolo (+) e infine su **From Maven** (Da Maven).

    ![Aggiunta di una libreria](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    Nella finestra di dialogo **Download Library from Maven Repository** (Scarica libreria da repository Maven) cercare e aggiungere le librerie seguenti.

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. Copiare `yarn-site.xml` e `core-site.xml` dal nodo head del cluster e aggiungerli al progetto. Per copiare i file, usare i comandi riportati di seguito. Per copiare i file dai nodi head del cluster è possibile usare [Cygwin](https://cygwin.com/install.html) per eseguire i comandi `scp` seguenti.

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    Poiché gli indirizzi IP e i nomi host dei nodi head del cluster sono già stati aggiunti al file hosts nel PC desktop, si possono usare i comandi **scp** nel modo seguente.

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    Aggiungere questi file al progetto copiandoli nella cartella **/src** dell'albero del progetto, ad esempio `<your project directory>\src`.
6. Aggiornare `core-site.xml` per apportare le modifiche seguenti.

   1. `core-site.xml` include la chiave crittografata per l'account di archiviazione associato al cluster. Nel file `core-site.xml` aggiunto al progetto, sostituire la chiave crittografata con la chiave di archiviazione effettiva associata all'account di archiviazione predefinito. Vedere la sezione [Gestire le chiavi di accesso alle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. Rimuovere le voci seguenti da `core-site.xml`.

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
   3. Salvare il file.
7. Aggiungere la classe principale per l'applicazione. In **Project Explorer** (Esplora progetti) fare clic con il pulsante destro del mouse su **src**, scegliere **New** (Nuovo) e quindi fare clic su **Scala class** (Classe Scala).

    ![Aggiunta di un codice sorgente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. Nella finestra di dialogo **Create New Scala Class** (Crea nuova classe Scala) immettere un nome, selezionare **Object** (Oggetto) per il campo **Kind** (Tipologia) e quindi fare clic su **OK**.

    ![Aggiunta di un codice sorgente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. Incollare il codice seguente nel file `MyClusterAppMain.scala` . Questo codice crea il contesto Spark e avvia un metodo `executeJob` dall'oggetto `SparkSample`.

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

10. Ripetere i precedenti passaggi 8 e 9 per aggiungere un nuovo oggetto Scala denominato `SparkSample`. Aggiungere il codice seguente a questa classe. Questo codice legge i dati dal file HVAC.csv, disponibile in tutti i cluster HDInsight Spark, recupera le righe con una sola cifra nella settima colonna del file CSV e scrive l'output in **/HVACOut** nel contenitore di archiviazione predefinito per il cluster.

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find the rows which have only one digit in the 7th column in the CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. Ripetere i precedenti passaggi 8 e 9 per aggiungere una nuova classe denominata `RemoteClusterDebugging`. Questa classe implementa il framework di test Spark usato per il debug delle applicazioni. Aggiungere il codice seguente alla classe `RemoteClusterDebugging` .

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

     Alcuni aspetti importanti da notare:

   * Per `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, verificare che il file JAR dell'assembly Spark sia disponibile nell'archiviazione cluster al percorso specificato.
   * Per `setJars`, specificare il percorso in cui verrà creato il file JAR dell'elemento. In genere è `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.
12. Nella classe `RemoteClusterDebugging` fare clic con il pulsante destro del mouse sulla parola chiave `test` e scegliere **Create RemoteClusterDebugging Configuration** (Crea configurazione RemoteClusterDebugging).

    ![Creazione della configurazione remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. Nella finestra di dialogo specificare un nome per la configurazione e selezionare **Test name** (Nome test) come **Test kind** (Tipologia test). Mantenere l'impostazione predefinita per tutti gli altri valori, fare clic su **Apply** (Applica) e quindi su **OK**.

    ![Creazione della configurazione remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. Nella barra dei menu verrà ora visualizzato un menu a discesa della configurazione **Remote Run** (Esecuzione remota).

    ![Creazione della configurazione remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-the-application-in-debug-mode"></a>Passaggio 5: Eseguire l'applicazione in modalità di debug
1. Nel progetto IntelliJ IDEA aprire `SparkSample.scala` e creare un punto di interruzione accanto a "val rdd1". Nel menu a comparsa per la creazione di un punto di interruzione selezionare **line in function executeJob**(riga in funzione executeJob).

    ![Aggiunta di un punto di interruzione](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. Fare clic sul pulsante **Debug Run** (Esecuzione debug) accanto al menu a discesa della configurazione **Remote Run** (Esecuzione remota) per avviare l'esecuzione dell'applicazione.

    ![Esecuzione del programma in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. Quando l'esecuzione del programma raggiunge il punto di interruzione, nel riquadro inferiore verrà visualizzata una scheda **Debugger** .

    ![Esecuzione del programma in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. Fare clic sull'icona (**+**) per aggiungere un'espressione di controllo come illustrato nell'immagine seguente.

    ![Esecuzione del programma in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    Poiché l'applicazione è stata interrotta prima della creazione della variabile `rdd1`, usando questa espressione di controllo si possono visualizzare le prime 5 righe nella variabile `rdd`. Premere **INVIO**.

    ![Esecuzione del programma in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    L'immagine precedente illustra che in fase di esecuzione è possibile eseguire query su terabyte di dati e il debug dell'avanzamento dell'applicazione. Nell'output illustrato nell'immagine precedente, ad esempio, si può osservare che la prima riga dell'output è un'intestazione. Sulla base di questo, è possibile modificare il codice dell'applicazione per ignorare la riga di intestazione, se necessario.
5. È ora possibile fare clic sull'icona **Resume Program** (Riprendi programma) per continuare l'esecuzione dell'applicazione.

    ![Esecuzione del programma in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. Se l'applicazione viene completata, verrà visualizzato un output simile al seguente.

    ![Esecuzione del programma in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <a name="seealso"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demo
* Creare il progetto Scala (video): [Creare applicazioni Spark in Scala](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Debug remoto (video): [Usare Azure Toolkit per IntelliJ per il debug remoto di applicazioni Spark nel cluster HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

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
* [Usare gli strumenti HDInsight nel Toolkit di Azure per IntelliJ per creare e inviare applicazioni Spark in Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usare Azure Toolkit per IntelliJ per il debug remoto di applicazioni Spark tramite SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications (Usare gli strumenti HDInsight nel Toolkit di Azure per Eclipse per creare applicazioni Spark)](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installare Jupyter Notebook nel computer e connetterlo a un cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse del cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)
