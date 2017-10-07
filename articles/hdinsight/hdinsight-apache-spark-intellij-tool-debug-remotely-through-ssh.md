---
title: "Azure Toolkit for IntelliJ: debug delle applicazioni Spark in modalità remota tramite SSH | Microsoft Docs"
description: "Istruzioni dettagliate su come toouse gli strumenti di HDInsight in Azure Toolkit per le applicazioni toodebug IntelliJ in modalità remota in HDInsight cluster tramite SSH"
keywords: eseguire debug remoto di intellij, debug remoto di intellij, ssh, intellij, hdinsight, debug di intellij, debug
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a>Eseguire il debug delle applicazioni Spark su un cluster HDInsight con Azure Toolkit for IntelliJ tramite SSH

In questo articolo vengono fornite istruzioni dettagliate su come toouse gli strumenti di HDInsight in Azure Toolkit per le applicazioni toodebug IntelliJ in modalità remota in un cluster HDInsight. toodebug il progetto, è inoltre possibile visualizzare hello [applicazioni di eseguire il Debug HDInsight Spark con Azure Toolkit per IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.

**Prerequisiti**

* **Strumenti HDInsight in Azure Toolkit per IntelliJ**. Questo strumento fa parte di Azure Toolkit for IntelliJ. Per altre informazioni, vedere [Installare Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).
* **Azure Toolkit per IntelliJ**. Utilizzare questa applicazione di Spark toocreate toolkit per un cluster HDInsight. Per ulteriori informazioni, seguire le istruzioni hello [utilizzare Azure Toolkit per le applicazioni per un cluster HDInsight Spark toocreate IntelliJ](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).
* **Servizio SSH di HDInsight con gestione di nome utente e password**. Per ulteriori informazioni, vedere [tooHDInsight (Hadoop) di connettersi tramite SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [uso di SSH tunneling tooaccess Ambari web dell'interfaccia utente, JobHistory, NameNode, Oozie e altre interfacce utente web](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel). 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a>Creare un'applicazione Scala Spark e configurarla per il debug remoto

1. Avviare IntelliJ IDEA e creare un progetto. In hello **nuovo progetto** finestra di dialogo casella, hello seguenti:

   a. Selezionare **HDInsight**. 

   b. Selezionare un modello Java o Scala in base alle preferenze. Selezionare tra hello le opzioni seguenti:

      - **Spark in HDInsight (Scala)**

      - **Spark in HDInsight (Java)**

      - **Esecuzione di esempio di Spark in un cluster HDInsight (Scala)**

      In questo esempio si usa un modello di **esempio per l'esecuzione di Spark in un cluster HDInsight (Scala)**.

   c. In hello **strumento di compilazione** selezionare uno dei hello seguenti, in base tooyour necessità:

      - **Maven**, per ottenere supporto per la creazione guidata di un progetto Scala

      -  **SBT**, per la gestione delle dipendenze hello e la compilazione per il progetto di Scala hello 

      ![Creare un progetto di debug](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   d. Selezionare **Avanti**.     
 
3. In hello Avanti **nuovo progetto** finestra hello seguenti:

   ![Selezionare hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   a. Specificare un nome per il progetto e il relativo percorso.

   b. In hello **Project SDK** elenco a discesa, seleziona **Java 1.8** per **nascita 2. x** cluster oppure selezionare **Java 1.7** per **Spark 1. x** cluster.

   c. In hello **versione Spark** elenco a discesa, creazione guidata progetto di Scala hello integra la versione corretta di hello per SDK Spark e SDK di Scala. Se la versione del cluster spark hello è precedente alla versione 2.0, selezionare **nascita 1. x**. In caso contrario, selezionare **Spark 2.x**. In questo esempio viene usata la versione **Spark 2.0.2 (Scala 2.11.8)**.

   d. Selezionare **Fine**.

4. Selezionare **src** > **principale** > **scala** tooopen il codice nel progetto hello. Questo esempio viene utilizzato hello **SparkCore_wasbloTest** script.

5. hello tooaccess **modificare configurazioni** icona selezionare hello nell'angolo superiore destro di hello del menu. Da questo menu, è possibile creare o modificare le configurazioni di hello per il debug remoto.

   ![Modifica configurazioni](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. In hello **le configurazioni di esecuzione/Debug** la finestra di dialogo, seleziona hello sul segno più (**+**). Selezionare quindi hello **inviare processo Spark** opzione.

   ![Aggiungere una nuova configurazione](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. Immettere le informazioni per **Nome**, **Cluster Spark**, e **Nome della classe principale**. Selezionare quindi **Configurazione avanzata**. 

   ![Eseguire configurazioni di debug](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. In hello **configurazione avanzata di Spark invio** nella finestra di dialogo **eseguire il debug remoto abilitare Spark**. Immettere nome utente SSH hello, quindi immettere una password o utilizzare un file di chiave privata. configurazione di hello toosave, selezionare **OK**.

   ![Abilitare il debug remoto di Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. configurazione di Hello ora viene salvata con il nome di hello specificato. dettagli di configurazione hello tooview, il nome di configurazione selezionare hello. Selezionare le modifiche toomake, **modificare configurazioni**. 

10. Dopo aver completato le impostazioni di configurazione hello, è possibile eseguire il progetto hello cluster remoto hello o eseguire il debug remoto.

## <a name="learn-how-tooperform-remote-debugging"></a>Informazioni su come tooperform il debug remoto
### <a name="scenario-1-perform-remote-run"></a>Scenario 1: Esecuzione remota

In questa sezione verrà illustrato come toodebug executor e driver.

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. Impostare i punti di interruzione e quindi selezionare hello **Debug** icona.

   ![Selezionare l'icona debug hello](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. Quando l'esecuzione del programma hello raggiunge il punto di interruzione hello, viene visualizzato un **Driver** scheda e due **esecutore** schede hello **Debugger** riquadro. Seleziona hello **programma Resume** toocontinue icona esegue codice hello, che quindi raggiunge hello successivo punto di interruzione e si concentra sulla corrispondente hello **esecutore** scheda. È possibile esaminare i log di esecuzione hello hello corrispondente **Console** scheda.

   ![Scheda di debug](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a>Scenario 2: eseguire il debug e la correzione di bug da remoto
In questa sezione viene illustrata la modalità toodynamically aggiornamento hello valore della variabile tramite hello IntelliJ funzionalità per la correzione semplice di debug. Nell'esempio di codice seguente di hello, viene generata un'eccezione perché il file di destinazione hello esiste già.
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a>debug remoto tooperform e la correzione dei bug
1. Impostare i due punti di interruzione e quindi selezionare hello **Debug** hello toostart sull'icona del processo di debug remoto.

2. codice Hello viene arrestata al primo punto di interruzione hello e parametro hello e informazioni sulle variabili sono espressi in hello **variabili** riquadro. 

3. Seleziona hello **programma Resume** toocontinue icona. codice Hello si arresta al secondo punto hello. Hello eccezione come previsto.

  ![Errore di generazione](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. Seleziona hello **programma Resume** sull'icona Nuovo. Hello **HDInsight Spark invio** finestra viene visualizzato un errore di "esecuzione processo non riuscita".

  ![Errore nell'invio](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. Valore variabile toodynamically aggiornamento hello tramite funzionalità di debug IntelliJ hello, selezionare **Debug** nuovamente. Hello **variabili** riquadro viene visualizzato nuovamente. 

6. Destinazione hello pulsante destro del mouse su hello **Debug** scheda e quindi selezionare **Imposta valore**. Quindi, immettere un nuovo valore per la variabile hello. Selezionare quindi **invio** valore hello toosave. 

  ![Impostare il valore](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. Seleziona hello **programma Resume** programma hello toorun toocontinue di icona. Questa volta, non viene rilevata alcuna eccezione. È possibile visualizzare che tale progetto hello viene eseguito correttamente senza le eccezioni.

  ![Debug senza eccezioni](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <a name="seealso"></a>Passaggi successivi
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demo
* Creare il progetto Scala (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (Creare applicazioni Spark Scala)
* Eseguire il debug remoto (video): [utilizzare Azure Toolkit per le applicazioni in modalità remota in un cluster HDInsight Spark toodebug IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: usare Spark in HDInsight tooanalyze temperatura utilizzando dati impianto di compilazione](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming di Spark: Usare Spark in HDInsight toobuild in tempo reale lo streaming di applicazioni](hdinsight-apache-spark-eventhub-streaming.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creare ed eseguire applicazioni
* [Creare un'applicazione autonoma con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Eseguire processi in modalità remota in un cluster Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Strumenti ed estensioni
* [Utilizzare Azure Toolkit per le applicazioni per un cluster HDInsight Spark toocreate IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizzare Azure Toolkit per le applicazioni in modalità remota tramite VPN Spark toodebug IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Utilizzare gli strumenti di HDInsight in Azure Toolkit per le applicazioni di Spark toocreate Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibile per i server Jupyter notebook nel cluster di hello Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)
