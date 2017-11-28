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
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="b6fba-104">Eseguire il debug delle applicazioni Spark su un cluster HDInsight con Azure Toolkit for IntelliJ tramite SSH</span><span class="sxs-lookup"><span data-stu-id="b6fba-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="b6fba-105">In questo articolo vengono fornite istruzioni dettagliate su come toouse gli strumenti di HDInsight in Azure Toolkit per le applicazioni toodebug IntelliJ in modalità remota in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b6fba-105">This article provides step-by-step guidance on how toouse HDInsight Tools in Azure Toolkit for IntelliJ toodebug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="b6fba-106">toodebug il progetto, è inoltre possibile visualizzare hello [applicazioni di eseguire il Debug HDInsight Spark con Azure Toolkit per IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span><span class="sxs-lookup"><span data-stu-id="b6fba-106">toodebug your project, you can also view hello [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="b6fba-107">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="b6fba-107">**Prerequisites**</span></span>

* <span data-ttu-id="b6fba-108">**Strumenti HDInsight in Azure Toolkit per IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="b6fba-109">Questo strumento fa parte di Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="b6fba-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="b6fba-110">Per altre informazioni, vedere [Installare Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="b6fba-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="b6fba-111">**Azure Toolkit per IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="b6fba-112">Utilizzare questa applicazione di Spark toocreate toolkit per un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b6fba-112">Use this toolkit toocreate Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="b6fba-113">Per ulteriori informazioni, seguire le istruzioni hello [utilizzare Azure Toolkit per le applicazioni per un cluster HDInsight Spark toocreate IntelliJ](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span><span class="sxs-lookup"><span data-stu-id="b6fba-113">For more information, follow hello instructions in [Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="b6fba-114">**Servizio SSH di HDInsight con gestione di nome utente e password**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="b6fba-115">Per ulteriori informazioni, vedere [tooHDInsight (Hadoop) di connettersi tramite SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [uso di SSH tunneling tooaccess Ambari web dell'interfaccia utente, JobHistory, NameNode, Oozie e altre interfacce utente web](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span><span class="sxs-lookup"><span data-stu-id="b6fba-115">For more information, see [Connect tooHDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="b6fba-116">Creare un'applicazione Scala Spark e configurarla per il debug remoto</span><span class="sxs-lookup"><span data-stu-id="b6fba-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="b6fba-117">Avviare IntelliJ IDEA e creare un progetto.</span><span class="sxs-lookup"><span data-stu-id="b6fba-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="b6fba-118">In hello **nuovo progetto** finestra di dialogo casella, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6fba-118">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="b6fba-119">a.</span><span class="sxs-lookup"><span data-stu-id="b6fba-119">a.</span></span> <span data-ttu-id="b6fba-120">Selezionare **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="b6fba-121">b.</span><span class="sxs-lookup"><span data-stu-id="b6fba-121">b.</span></span> <span data-ttu-id="b6fba-122">Selezionare un modello Java o Scala in base alle preferenze.</span><span class="sxs-lookup"><span data-stu-id="b6fba-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="b6fba-123">Selezionare tra hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6fba-123">Select between hello following options:</span></span>

      - <span data-ttu-id="b6fba-124">**Spark in HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="b6fba-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="b6fba-125">**Spark in HDInsight (Java)**</span><span class="sxs-lookup"><span data-stu-id="b6fba-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="b6fba-126">**Esecuzione di esempio di Spark in un cluster HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="b6fba-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="b6fba-127">In questo esempio si usa un modello di **esempio per l'esecuzione di Spark in un cluster HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="b6fba-128">c.</span><span class="sxs-lookup"><span data-stu-id="b6fba-128">c.</span></span> <span data-ttu-id="b6fba-129">In hello **strumento di compilazione** selezionare uno dei hello seguenti, in base tooyour necessità:</span><span class="sxs-lookup"><span data-stu-id="b6fba-129">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      - <span data-ttu-id="b6fba-130">**Maven**, per ottenere supporto per la creazione guidata di un progetto Scala</span><span class="sxs-lookup"><span data-stu-id="b6fba-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="b6fba-131">**SBT**, per la gestione delle dipendenze hello e la compilazione per il progetto di Scala hello</span><span class="sxs-lookup"><span data-stu-id="b6fba-131">**SBT**, for managing hello dependencies and building for hello Scala project</span></span> 

      ![Creare un progetto di debug](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="b6fba-133">d.</span><span class="sxs-lookup"><span data-stu-id="b6fba-133">d.</span></span> <span data-ttu-id="b6fba-134">Selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="b6fba-135">In hello Avanti **nuovo progetto** finestra hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6fba-135">In hello next **New Project** window, do hello following:</span></span>

   ![Selezionare hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="b6fba-137">a.</span><span class="sxs-lookup"><span data-stu-id="b6fba-137">a.</span></span> <span data-ttu-id="b6fba-138">Specificare un nome per il progetto e il relativo percorso.</span><span class="sxs-lookup"><span data-stu-id="b6fba-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="b6fba-139">b.</span><span class="sxs-lookup"><span data-stu-id="b6fba-139">b.</span></span> <span data-ttu-id="b6fba-140">In hello **Project SDK** elenco a discesa, seleziona **Java 1.8** per **nascita 2. x** cluster oppure selezionare **Java 1.7** per **Spark 1. x** cluster.</span><span class="sxs-lookup"><span data-stu-id="b6fba-140">In hello **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="b6fba-141">c.</span><span class="sxs-lookup"><span data-stu-id="b6fba-141">c.</span></span> <span data-ttu-id="b6fba-142">In hello **versione Spark** elenco a discesa, creazione guidata progetto di Scala hello integra la versione corretta di hello per SDK Spark e SDK di Scala.</span><span class="sxs-lookup"><span data-stu-id="b6fba-142">In hello **Spark Version** drop-down list, hello Scala project creation wizard integrates hello correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="b6fba-143">Se la versione del cluster spark hello è precedente alla versione 2.0, selezionare **nascita 1. x**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-143">If hello spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="b6fba-144">In caso contrario, selezionare **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="b6fba-145">In questo esempio viene usata la versione **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="b6fba-146">d.</span><span class="sxs-lookup"><span data-stu-id="b6fba-146">d.</span></span> <span data-ttu-id="b6fba-147">Selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-147">Select **Finish**.</span></span>

4. <span data-ttu-id="b6fba-148">Selezionare **src** > **principale** > **scala** tooopen il codice nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="b6fba-148">Select **src** > **main** > **scala** tooopen your code in hello project.</span></span> <span data-ttu-id="b6fba-149">Questo esempio viene utilizzato hello **SparkCore_wasbloTest** script.</span><span class="sxs-lookup"><span data-stu-id="b6fba-149">This example uses hello **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="b6fba-150">hello tooaccess **modificare configurazioni** icona selezionare hello nell'angolo superiore destro di hello del menu.</span><span class="sxs-lookup"><span data-stu-id="b6fba-150">tooaccess hello **Edit Configurations** menu, select hello icon in hello upper-right corner.</span></span> <span data-ttu-id="b6fba-151">Da questo menu, è possibile creare o modificare le configurazioni di hello per il debug remoto.</span><span class="sxs-lookup"><span data-stu-id="b6fba-151">From this menu, you can create or edit hello configurations for remote debugging.</span></span>

   ![Modifica configurazioni](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="b6fba-153">In hello **le configurazioni di esecuzione/Debug** la finestra di dialogo, seleziona hello sul segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="b6fba-153">In hello **Run/Debug Configurations** dialog box, select hello plus sign (**+**).</span></span> <span data-ttu-id="b6fba-154">Selezionare quindi hello **inviare processo Spark** opzione.</span><span class="sxs-lookup"><span data-stu-id="b6fba-154">Then select hello **Submit Spark Job** option.</span></span>

   ![Aggiungere una nuova configurazione](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="b6fba-156">Immettere le informazioni per **Nome**, **Cluster Spark**, e **Nome della classe principale**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="b6fba-157">Selezionare quindi **Configurazione avanzata**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-157">Then select **Advanced configuration**.</span></span> 

   ![Eseguire configurazioni di debug](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="b6fba-159">In hello **configurazione avanzata di Spark invio** nella finestra di dialogo **eseguire il debug remoto abilitare Spark**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-159">In hello **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="b6fba-160">Immettere nome utente SSH hello, quindi immettere una password o utilizzare un file di chiave privata.</span><span class="sxs-lookup"><span data-stu-id="b6fba-160">Enter hello SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="b6fba-161">configurazione di hello toosave, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-161">toosave hello configuration, select **OK**.</span></span>

   ![Abilitare il debug remoto di Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="b6fba-163">configurazione di Hello ora viene salvata con il nome di hello specificato.</span><span class="sxs-lookup"><span data-stu-id="b6fba-163">hello configuration is now saved with hello name you provided.</span></span> <span data-ttu-id="b6fba-164">dettagli di configurazione hello tooview, il nome di configurazione selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="b6fba-164">tooview hello configuration details, select hello configuration name.</span></span> <span data-ttu-id="b6fba-165">Selezionare le modifiche toomake, **modificare configurazioni**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-165">toomake changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="b6fba-166">Dopo aver completato le impostazioni di configurazione hello, è possibile eseguire il progetto hello cluster remoto hello o eseguire il debug remoto.</span><span class="sxs-lookup"><span data-stu-id="b6fba-166">After you complete hello configurations settings, you can run hello project against hello remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-tooperform-remote-debugging"></a><span data-ttu-id="b6fba-167">Informazioni su come tooperform il debug remoto</span><span class="sxs-lookup"><span data-stu-id="b6fba-167">Learn how tooperform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="b6fba-168">Scenario 1: Esecuzione remota</span><span class="sxs-lookup"><span data-stu-id="b6fba-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="b6fba-169">In questa sezione verrà illustrato come toodebug executor e driver.</span><span class="sxs-lookup"><span data-stu-id="b6fba-169">In this section, we show you how toodebug drivers and executors.</span></span>

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


1. <span data-ttu-id="b6fba-170">Impostare i punti di interruzione e quindi selezionare hello **Debug** icona.</span><span class="sxs-lookup"><span data-stu-id="b6fba-170">Set up breaking points, and then select hello **Debug** icon.</span></span>

   ![Selezionare l'icona debug hello](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="b6fba-172">Quando l'esecuzione del programma hello raggiunge il punto di interruzione hello, viene visualizzato un **Driver** scheda e due **esecutore** schede hello **Debugger** riquadro.</span><span class="sxs-lookup"><span data-stu-id="b6fba-172">When hello program execution reaches hello breaking point, you see a **Driver** tab and two **Executor** tabs in hello **Debugger** pane.</span></span> <span data-ttu-id="b6fba-173">Seleziona hello **programma Resume** toocontinue icona esegue codice hello, che quindi raggiunge hello successivo punto di interruzione e si concentra sulla corrispondente hello **esecutore** scheda. È possibile esaminare i log di esecuzione hello hello corrispondente **Console** scheda.</span><span class="sxs-lookup"><span data-stu-id="b6fba-173">Select hello **Resume Program** icon toocontinue running hello code, which then reaches hello next breakpoint and focuses on hello corresponding **Executor** tab. You can review hello execution logs on hello corresponding **Console** tab.</span></span>

   ![Scheda di debug](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="b6fba-175">Scenario 2: eseguire il debug e la correzione di bug da remoto</span><span class="sxs-lookup"><span data-stu-id="b6fba-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="b6fba-176">In questa sezione viene illustrata la modalità toodynamically aggiornamento hello valore della variabile tramite hello IntelliJ funzionalità per la correzione semplice di debug.</span><span class="sxs-lookup"><span data-stu-id="b6fba-176">In this section, we show you how toodynamically update hello variable value by using hello IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="b6fba-177">Nell'esempio di codice seguente di hello, viene generata un'eccezione perché il file di destinazione hello esiste già.</span><span class="sxs-lookup"><span data-stu-id="b6fba-177">In hello following code example, an exception is thrown because hello target file already exists.</span></span>
  
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


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="b6fba-178">debug remoto tooperform e la correzione dei bug</span><span class="sxs-lookup"><span data-stu-id="b6fba-178">tooperform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="b6fba-179">Impostare i due punti di interruzione e quindi selezionare hello **Debug** hello toostart sull'icona del processo di debug remoto.</span><span class="sxs-lookup"><span data-stu-id="b6fba-179">Set up two breaking points, and then select hello **Debug** icon toostart hello remote debugging process.</span></span>

2. <span data-ttu-id="b6fba-180">codice Hello viene arrestata al primo punto di interruzione hello e parametro hello e informazioni sulle variabili sono espressi in hello **variabili** riquadro.</span><span class="sxs-lookup"><span data-stu-id="b6fba-180">hello code stops at hello first breaking point, and hello parameter and variable information are shown in hello **Variables** pane.</span></span> 

3. <span data-ttu-id="b6fba-181">Seleziona hello **programma Resume** toocontinue icona.</span><span class="sxs-lookup"><span data-stu-id="b6fba-181">Select hello **Resume Program** icon toocontinue.</span></span> <span data-ttu-id="b6fba-182">codice Hello si arresta al secondo punto hello.</span><span class="sxs-lookup"><span data-stu-id="b6fba-182">hello code stops at hello second point.</span></span> <span data-ttu-id="b6fba-183">Hello eccezione come previsto.</span><span class="sxs-lookup"><span data-stu-id="b6fba-183">hello exception is caught as expected.</span></span>

  ![Errore di generazione](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="b6fba-185">Seleziona hello **programma Resume** sull'icona Nuovo.</span><span class="sxs-lookup"><span data-stu-id="b6fba-185">Select hello **Resume Program** icon again.</span></span> <span data-ttu-id="b6fba-186">Hello **HDInsight Spark invio** finestra viene visualizzato un errore di "esecuzione processo non riuscita".</span><span class="sxs-lookup"><span data-stu-id="b6fba-186">hello **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![Errore nell'invio](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="b6fba-188">Valore variabile toodynamically aggiornamento hello tramite funzionalità di debug IntelliJ hello, selezionare **Debug** nuovamente.</span><span class="sxs-lookup"><span data-stu-id="b6fba-188">toodynamically update hello variable value by using hello IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="b6fba-189">Hello **variabili** riquadro viene visualizzato nuovamente.</span><span class="sxs-lookup"><span data-stu-id="b6fba-189">hello **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="b6fba-190">Destinazione hello pulsante destro del mouse su hello **Debug** scheda e quindi selezionare **Imposta valore**.</span><span class="sxs-lookup"><span data-stu-id="b6fba-190">Right-click hello target on hello **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="b6fba-191">Quindi, immettere un nuovo valore per la variabile hello.</span><span class="sxs-lookup"><span data-stu-id="b6fba-191">Next, enter a new value for hello variable.</span></span> <span data-ttu-id="b6fba-192">Selezionare quindi **invio** valore hello toosave.</span><span class="sxs-lookup"><span data-stu-id="b6fba-192">Then select **Enter** toosave hello value.</span></span> 

  ![Impostare il valore](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="b6fba-194">Seleziona hello **programma Resume** programma hello toorun toocontinue di icona.</span><span class="sxs-lookup"><span data-stu-id="b6fba-194">Select hello **Resume Program** icon toocontinue toorun hello program.</span></span> <span data-ttu-id="b6fba-195">Questa volta, non viene rilevata alcuna eccezione.</span><span class="sxs-lookup"><span data-stu-id="b6fba-195">This time, no exception is caught.</span></span> <span data-ttu-id="b6fba-196">È possibile visualizzare che tale progetto hello viene eseguito correttamente senza le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="b6fba-196">You can see that hello project runs successfully without any exceptions.</span></span>

  ![Debug senza eccezioni](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="b6fba-198"><a name="seealso"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6fba-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="b6fba-199">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6fba-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="b6fba-200">Demo</span><span class="sxs-lookup"><span data-stu-id="b6fba-200">Demo</span></span>
* <span data-ttu-id="b6fba-201">Creare il progetto Scala (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (Creare applicazioni Spark Scala)</span><span class="sxs-lookup"><span data-stu-id="b6fba-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="b6fba-202">Eseguire il debug remoto (video): [utilizzare Azure Toolkit per le applicazioni in modalità remota in un cluster HDInsight Spark toodebug IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="b6fba-202">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="b6fba-203">Scenari</span><span class="sxs-lookup"><span data-stu-id="b6fba-203">Scenarios</span></span>
* [<span data-ttu-id="b6fba-204">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6fba-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b6fba-205">Spark con Machine Learning: usare Spark in HDInsight tooanalyze temperatura utilizzando dati impianto di compilazione</span><span class="sxs-lookup"><span data-stu-id="b6fba-205">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b6fba-206">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="b6fba-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b6fba-207">Streaming di Spark: Usare Spark in HDInsight toobuild in tempo reale lo streaming di applicazioni</span><span class="sxs-lookup"><span data-stu-id="b6fba-207">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b6fba-208">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6fba-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b6fba-209">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="b6fba-209">Create and run applications</span></span>
* [<span data-ttu-id="b6fba-210">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="b6fba-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b6fba-211">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="b6fba-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b6fba-212">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="b6fba-212">Tools and extensions</span></span>
* [<span data-ttu-id="b6fba-213">Utilizzare Azure Toolkit per le applicazioni per un cluster HDInsight Spark toocreate IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b6fba-213">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b6fba-214">Utilizzare Azure Toolkit per le applicazioni in modalità remota tramite VPN Spark toodebug IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b6fba-214">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b6fba-215">Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="b6fba-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="b6fba-216">Utilizzare gli strumenti di HDInsight in Azure Toolkit per le applicazioni di Spark toocreate Eclipse</span><span class="sxs-lookup"><span data-stu-id="b6fba-216">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="b6fba-217">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6fba-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b6fba-218">Kernel disponibile per i server Jupyter notebook nel cluster di hello Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6fba-218">Kernels available for Jupyter notebook in hello Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b6fba-219">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="b6fba-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b6fba-220">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="b6fba-220">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b6fba-221">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="b6fba-221">Manage resources</span></span>
* [<span data-ttu-id="b6fba-222">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="b6fba-222">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b6fba-223">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6fba-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
