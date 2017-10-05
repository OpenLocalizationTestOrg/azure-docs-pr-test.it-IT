---
title: 'Azure Toolkit for IntelliJ: Creare applicazioni Spark per un cluster HDInsight | Microsoft Docs'
description: Usare il Toolkit di Azure per IntelliJ per sviluppare applicazioni Spark scritte in Scala e inoltrarle a un cluster HDInsight Spark.
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
ms.openlocfilehash: 19cb8f436fa4d86f323013a5d4b3b50bf6c80a1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="3938e-103">Usare Azure Toolkit for IntelliJ per creare applicazioni Spark per un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="3938e-103">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="3938e-104">Usare il plug-in Azure Toolkit for IntelliJ per sviluppare applicazioni Spark scritte in Scala e quindi inoltrarle a un cluster HDInsight Spark direttamente dall'ambiente di sviluppo integrato (IDE) IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3938e-104">Use the Azure Toolkit for IntelliJ plug-in to develop Spark applications written in Scala, and then submit them to an HDInsight Spark cluster directly from the IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="3938e-105">È possibile usare il plug-in in vari modi:</span><span class="sxs-lookup"><span data-stu-id="3938e-105">You can use the plug-in in a few ways:</span></span>

* <span data-ttu-id="3938e-106">Sviluppare e inviare un'applicazione Spark in Scala in un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="3938e-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="3938e-107">Accedere alle risorse cluster HDInsight Spark di Azure.</span><span class="sxs-lookup"><span data-stu-id="3938e-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="3938e-108">Sviluppare ed eseguire un'applicazione Spark in Scala localmente.</span><span class="sxs-lookup"><span data-stu-id="3938e-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="3938e-109">Per creare il progetto, guardare il video [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (Creare applicazioni Spark con Azure Toolkit for IntelliJ).</span><span class="sxs-lookup"><span data-stu-id="3938e-109">To create your project, view the [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3938e-110">È possibile usare questo plug-in per creare e inviare applicazioni solo per cluster HDInsight Spark in Linux.</span><span class="sxs-lookup"><span data-stu-id="3938e-110">You can use this plug-in to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="3938e-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3938e-111">Prerequisites</span></span>

- <span data-ttu-id="3938e-112">Un cluster Apache Spark in HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="3938e-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="3938e-113">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="3938e-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="3938e-114">Kit di sviluppo di Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="3938e-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="3938e-115">È possibile installarlo dal [sito Web di Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="3938e-115">You can install it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="3938e-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="3938e-116">IntelliJ IDEA.</span></span> <span data-ttu-id="3938e-117">In questo articolo viene usata la versione 2017.1.</span><span class="sxs-lookup"><span data-stu-id="3938e-117">This article uses version 2017.1.</span></span> <span data-ttu-id="3938e-118">È possibile installarlo dal [sito Web di JetBrains](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="3938e-118">You can install it from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="3938e-119">Installare il Toolkit di Azure per IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3938e-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="3938e-120">Per le istruzioni di installazione vedere [Installare Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="3938e-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="3938e-121">Accedere alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3938e-121">Sign in to your Azure subscription</span></span>

1. <span data-ttu-id="3938e-122">Avviare l'IDE IntelliJ e aprire Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="3938e-122">Start the IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="3938e-123">Nel menu **Visualizza** selezionare **Finestre degli strumenti** e quindi **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="3938e-123">On the **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![Collegamento di Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="3938e-125">Fare clic con il pulsante destro del mouse sul nodo **Azure** e quindi scegliere **Sign In** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="3938e-125">Right-click the **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="3938e-126">Nella finestra di dialogo di **Azure Sign In** (Accesso ad Azure) fare clic su **Sign-in** (Accedi) e immettere le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="3938e-126">In the **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Finestra di dialogo di accesso di Azure](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="3938e-128">Dopo l'accesso, la finestra di dialogo **Selezionare le sottoscrizioni** elenca tutte le sottoscrizioni di Azure associate alle credenziali.</span><span class="sxs-lookup"><span data-stu-id="3938e-128">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions that are associated with the credentials.</span></span> <span data-ttu-id="3938e-129">Fare clic sul pulsante **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="3938e-129">Select the **Select** button.</span></span>

    ![Finestra di dialogo Seleziona sottoscrizioni](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="3938e-131">Nella scheda **Azure Explorer** espandere **HDInsight** per visualizzare i cluster HDInsight Spark disponibili nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3938e-131">On the **Azure Explorer** tab, expand **HDInsight** to view the HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Cluster HDInsight Spark in Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="3938e-133">Per visualizzare le risorse, ad esempio gli account di archiviazione, associate al cluster, è possibile espandere ancora un nodo di tipo nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="3938e-133">To view the resources (for example, storage accounts) that are associated with the cluster, you can further expand a cluster-name node.</span></span>
   
    ![Nodo di tipo nome del cluster espanso](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="3938e-135">Eseguire un'applicazione Spark in Scala in un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="3938e-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="3938e-136">Avviare IntelliJ IDEA e creare un progetto.</span><span class="sxs-lookup"><span data-stu-id="3938e-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="3938e-137">Nella finestra di dialogo **New Project** (Nuovo progetto) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3938e-137">In the **New Project** dialog box, do the following:</span></span> 

   <span data-ttu-id="3938e-138">a.</span><span class="sxs-lookup"><span data-stu-id="3938e-138">a.</span></span> <span data-ttu-id="3938e-139">Selezionare **HDInsight** > **Spark on HDInsight (Scala)** (Spark in HDInsight - Scala).</span><span class="sxs-lookup"><span data-stu-id="3938e-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="3938e-140">b.</span><span class="sxs-lookup"><span data-stu-id="3938e-140">b.</span></span> <span data-ttu-id="3938e-141">Nell'elenco **Build tool** (Strumento di compilazione) selezionare uno degli strumenti seguenti, in base alla necessità:</span><span class="sxs-lookup"><span data-stu-id="3938e-141">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="3938e-142">**Maven**, per ottenere supporto per la creazione guidata di un progetto Scala</span><span class="sxs-lookup"><span data-stu-id="3938e-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="3938e-143">**SBT**, per la gestione delle dipendenze e la compilazione per il progetto Scala</span><span class="sxs-lookup"><span data-stu-id="3938e-143">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![Finestra di dialogo del nuovo progetto](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="3938e-145">Selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3938e-145">Select **Next**.</span></span>

3. <span data-ttu-id="3938e-146">La creazione guidata del progetto Scala rileva automaticamente se è installato il plug-in Scala.</span><span class="sxs-lookup"><span data-stu-id="3938e-146">The Scala project-creation wizard automatically detects whether you've installed the Scala plug-in.</span></span> <span data-ttu-id="3938e-147">Selezionare **Installa**.</span><span class="sxs-lookup"><span data-stu-id="3938e-147">Select **Install**.</span></span>

   ![Verifica del plug-in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="3938e-149">Per scaricare il plug-in Scala, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="3938e-149">To download the Scala plug-in, select **OK**.</span></span> <span data-ttu-id="3938e-150">Seguire le istruzioni per riavviare IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3938e-150">Follow the instructions to restart IntelliJ.</span></span> 

   ![Finestra di dialogo di installazione del plug-in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="3938e-152">Nella finestra **New Project** (Nuovo progetto) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3938e-152">In the **New Project** window, do the following:</span></span>  

    ![Selezione di Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="3938e-154">a.</span><span class="sxs-lookup"><span data-stu-id="3938e-154">a.</span></span> <span data-ttu-id="3938e-155">Immettere un nome e un percorso per il progetto.</span><span class="sxs-lookup"><span data-stu-id="3938e-155">Enter a project name and location.</span></span>

   <span data-ttu-id="3938e-156">b.</span><span class="sxs-lookup"><span data-stu-id="3938e-156">b.</span></span> <span data-ttu-id="3938e-157">Nell'elenco a discesa **Project SDK** (SDK progetto) selezionare **Java 1.8** per il cluster Spark 2.x oppure **Java 1.7** per il cluster Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="3938e-157">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span>

   <span data-ttu-id="3938e-158">c.</span><span class="sxs-lookup"><span data-stu-id="3938e-158">c.</span></span> <span data-ttu-id="3938e-159">Nell'elenco a discesa **Spark version** (Versione di Spark) la creazione guidata del progetto Scala inserisce la versione corretta per Spark SDK e Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="3938e-159">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="3938e-160">Se la versione del cluster Spark è precedente alla 2.0, selezionare **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="3938e-160">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="3938e-161">In caso contrario, selezionare **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="3938e-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="3938e-162">In questo esempio viene usata la versione **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="3938e-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="3938e-163">Selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="3938e-163">Select **Finish**.</span></span>

7. <span data-ttu-id="3938e-164">Il progetto Spark crea automaticamente un elemento.</span><span class="sxs-lookup"><span data-stu-id="3938e-164">The Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="3938e-165">Per visualizzare l'elemento, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3938e-165">To view the artifact, do the following:</span></span>

   <span data-ttu-id="3938e-166">a.</span><span class="sxs-lookup"><span data-stu-id="3938e-166">a.</span></span> <span data-ttu-id="3938e-167">Dal menu **File** selezionare **Project Structure** (Struttura progetto).</span><span class="sxs-lookup"><span data-stu-id="3938e-167">On the **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="3938e-168">b.</span><span class="sxs-lookup"><span data-stu-id="3938e-168">b.</span></span> <span data-ttu-id="3938e-169">Nella finestra di dialogo **Project Structure** (Struttura progetto) selezionare **Artifacts** (Elementi) per visualizzare l'elemento predefinito creato.</span><span class="sxs-lookup"><span data-stu-id="3938e-169">In the **Project Structure** dialog box, select **Artifacts** to view the default artifact that is created.</span></span> <span data-ttu-id="3938e-170">È anche possibile creare un elemento personalizzato selezionando il segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="3938e-170">You can also create your own artifact by selecting the plus sign (**+**).</span></span>

      ![Informazioni sull'elemento nella finestra di dialogo](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="3938e-172">Aggiungere il codice sorgente dell'applicazione seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3938e-172">Add your application source code by doing the following:</span></span>

   <span data-ttu-id="3938e-173">a.</span><span class="sxs-lookup"><span data-stu-id="3938e-173">a.</span></span> <span data-ttu-id="3938e-174">In Project Explorer (Esplora progetti) fare clic con il pulsante destro del mouse su **src**, selezionare **New** (Nuovo) e quindi selezionare **Scala class** (Classe Scala).</span><span class="sxs-lookup"><span data-stu-id="3938e-174">In Project Explorer, right-click **src**, point to **New**, and then select **Scala Class**.</span></span>
      
      ![Comandi per la creazione di una classe Scala in Project Explorer (Esplora progetti)](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="3938e-176">b.</span><span class="sxs-lookup"><span data-stu-id="3938e-176">b.</span></span> <span data-ttu-id="3938e-177">Nella finestra di dialogo **Create New Scala Class** (Crea nuova classe Scala) immettere un nome, selezionare **Object** (Oggetto) per il campo **Kind** (Tipologia) e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="3938e-177">In the **Create New Scala Class** dialog box, provide a name, select **Object** in the **Kind** box, and then select **OK**.</span></span>
      
      ![Finestra di dialogo Create New Scala Class (Crea nuova classe Scala)](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="3938e-179">c.</span><span class="sxs-lookup"><span data-stu-id="3938e-179">c.</span></span> <span data-ttu-id="3938e-180">Nel file **MyClusterApp.scala** incollare il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="3938e-180">In the **MyClusterApp.scala** file, paste the following code.</span></span> <span data-ttu-id="3938e-181">Il codice legge i dati dal file HVAC.csv, disponibile in tutti i cluster HDInsight Spark, recupera le righe con una sola cifra nella settima colonna del file CSV e scrive l'output in **/HVACOut** nel contenitore di archiviazione predefinito per il cluster.</span><span class="sxs-lookup"><span data-stu-id="3938e-181">The code reads the data from HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that have only one digit in the seventh column in the CSV file, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find the rows that have only one digit in the seventh column in the CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="3938e-182">Eseguire l'applicazione in un cluster HDInsight Spark seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3938e-182">Run the application on an HDInsight Spark cluster by doing the following:</span></span>

   <span data-ttu-id="3938e-183">a.</span><span class="sxs-lookup"><span data-stu-id="3938e-183">a.</span></span> <span data-ttu-id="3938e-184">In Project Explorer (Esplora progetti) fare clic con il pulsante destro del mouse sul nome del progetto e quindi scegliere **Submit Spark Application to HDInsight** (Invia applicazione Spark a HDInsight).</span><span class="sxs-lookup"><span data-stu-id="3938e-184">In Project Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>
      
      ![Comando di invio dell'applicazione Spark a HDInsight](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="3938e-186">b.</span><span class="sxs-lookup"><span data-stu-id="3938e-186">b.</span></span> <span data-ttu-id="3938e-187">Viene richiesto di immettere le credenziali della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3938e-187">You are prompted to enter your Azure subscription credentials.</span></span> <span data-ttu-id="3938e-188">Nella finestra di dialogo **Spark Submission** (Invio Spark) specificare i valori seguenti e selezionare **Submit** (Invia).</span><span class="sxs-lookup"><span data-stu-id="3938e-188">In the **Spark Submission** dialog box, provide the following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="3938e-189">Per **Spark clusters (Linux only)**(Cluster Spark - solo Linux) selezionare il cluster Spark HDInsight in cui eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3938e-189">For **Spark clusters (Linux only)**, select the HDInsight Spark cluster on which you want to run your application.</span></span>

      * <span data-ttu-id="3938e-190">Selezionare un elemento nel progetto IntelliJ oppure selezionarne uno dal disco rigido.</span><span class="sxs-lookup"><span data-stu-id="3938e-190">Select an artifact from the IntelliJ project, or select one from the hard drive.</span></span>

      * <span data-ttu-id="3938e-191">Nella casella **Main class name** (Nome classe principale) selezionare i puntini di sospensione (**...**), selezionare la classe principale nel codice sorgente dell'applicazione e quindi **OK**.</span><span class="sxs-lookup"><span data-stu-id="3938e-191">In the **Main class name** box, select the ellipsis (**...**), select the main class in your application source code, and then select **OK**.</span></span>

        ![Finestra di dialogo di selezione della classe principale](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="3938e-193">Poiché il codice dell'applicazione in questo esempio non richiede argomenti della riga di comando e non fa riferimento a JAR o altri file, è possibile lasciare vuote le rimanenti caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="3938e-193">Because the application code in this example does not require command-line arguments or reference JARs or files, you can leave the remaining boxes empty.</span></span> <span data-ttu-id="3938e-194">Quando sono state fornite tutte le informazioni, la finestra di dialogo sarà simile all'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="3938e-194">After you provide all the information, the dialog box should resemble the following image.</span></span>
        
        ![Finestra di dialogo Spark Submission (Invio Spark)](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="3938e-196">c.</span><span class="sxs-lookup"><span data-stu-id="3938e-196">c.</span></span> <span data-ttu-id="3938e-197">Nella scheda **Spark Submission** (Invio Spark) nella parte inferiore della finestra verrà visualizzato lo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="3938e-197">The **Spark Submission** tab at the bottom of the window should start displaying the progress.</span></span> <span data-ttu-id="3938e-198">È anche possibile arrestare l'applicazione selezionando il pulsante rosso nella finestra **Spark Submission** (Invio Spark).</span><span class="sxs-lookup"><span data-stu-id="3938e-198">You can also stop the application by selecting the red button in the **Spark Submission** window.</span></span>
      
      ![Finestra Spark Submission (Invio Spark)](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="3938e-200">Per informazioni su come accedere all'output dei processi, vedere la sezione "Accedere e gestire i cluster HDInsight Spark tramite il Toolkit di Azure per IntelliJ" più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3938e-200">To learn how to access the job output, see the "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="3938e-201">Eseguire o eseguire il debug di un'applicazione Spark Scala in un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="3938e-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="3938e-202">Si consiglia anche di usare un altro modo per inviare l'applicazione Spark al cluster.</span><span class="sxs-lookup"><span data-stu-id="3938e-202">We also recommend another way of submitting the Spark application to the cluster.</span></span> <span data-ttu-id="3938e-203">È ad esempio possibile configurare i parametri nell'IDE **Run/Debug configurations** (Esegui/Esegui il debug delle configurazioni).</span><span class="sxs-lookup"><span data-stu-id="3938e-203">You can do so by setting the parameters in the **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="3938e-204">Per altre informazioni vedere [Eseguire il debug remoto delle applicazioni Spark su un cluster HDInsight con Azure Toolkit for IntelliJ tramite SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="3938e-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="3938e-205">Accedere e gestire i cluster HDInsight Spark tramite il Toolkit di Azure per IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3938e-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="3938e-206">È possibile eseguire diverse operazioni mediante il Toolkit Azure per IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3938e-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="3938e-207">Accedere alla visualizzazione del processo</span><span class="sxs-lookup"><span data-stu-id="3938e-207">Access the job view</span></span>
1. <span data-ttu-id="3938e-208">In Azure Explorer espandere **HDInsight**, espandere il nome del cluster Spark e quindi selezionare **Processi**.</span><span class="sxs-lookup"><span data-stu-id="3938e-208">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then select **Jobs**.</span></span>  

    ![Nodo di visualizzazione dei processi](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="3938e-210">Nel riquadro destro la scheda **Spark Job View** (Visualizzazione processi Spark) visualizza tutte le applicazioni eseguite nel cluster.</span><span class="sxs-lookup"><span data-stu-id="3938e-210">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="3938e-211">Selezionare il nome dell'applicazione per cui si vogliono visualizzare altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="3938e-211">Select the name of the application for which you want to see more details.</span></span>

    ![Dettagli applicazione](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="3938e-213">Per visualizzare le informazioni di base sui processi in esecuzione, passare il mouse sopra il grafico relativo al processo.</span><span class="sxs-lookup"><span data-stu-id="3938e-213">To display basic running job information, hover over the job graph.</span></span> <span data-ttu-id="3938e-214">Per visualizzare i grafici sulle fasi e le informazioni generate da ogni processo, selezionare un nodo nel grafico relativo al processo.</span><span class="sxs-lookup"><span data-stu-id="3938e-214">To view the stages graph and information that every job generates, select a node on the job graph.</span></span>

    ![Dettagli delle fasi dei processi](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="3938e-216">Per visualizzare i log di uso più frequente, ad esempio *Driver Stderr*, *Driver Stdout* e *Directory Info*, selezionare la scheda **Log**.</span><span class="sxs-lookup"><span data-stu-id="3938e-216">To view frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select the **Log** tab.</span></span>

    ![Dettagli del log](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="3938e-218">È anche possibile visualizzare l'interfaccia utente della cronologia di Spark e l'interfaccia utente di YARN, a livello di applicazione, selezionando i rispettivi collegamenti nella parte superiore della finestra.</span><span class="sxs-lookup"><span data-stu-id="3938e-218">You can also view the Spark history UI and the YARN UI (at the application level) by selecting a link at the top of the window.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="3938e-219">Accedere al Server cronologia Spark</span><span class="sxs-lookup"><span data-stu-id="3938e-219">Access the Spark history server</span></span>
1. <span data-ttu-id="3938e-220">In Azure Explorer espandere **HDInsight**, fare clic con il pulsante destro del mouse sul nome del cluster Spark e quindi scegliere **Open Spark History UI** (Apri UI cronologia Spark).</span><span class="sxs-lookup"><span data-stu-id="3938e-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="3938e-221">Quando richiesto, immettere le credenziali dell'amministratore del cluster, specificate durante la configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="3938e-221">When you're prompted, enter the cluster's admin credentials, which you specified when you set up the cluster.</span></span>

3. <span data-ttu-id="3938e-222">Nel dashboard del server della cronologia di Spark è possibile usare il nome dell'applicazione per cercare l'applicazione di cui è appena stata completata l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3938e-222">On the Spark history server dashboard, you can use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="3938e-223">Nel codice precedente impostare il nome dell'applicazione usando `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="3938e-223">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="3938e-224">Il nome dell'applicazione Spark è quindi **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="3938e-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="3938e-225">Avviare il portale di Ambari</span><span class="sxs-lookup"><span data-stu-id="3938e-225">Start the Ambari portal</span></span>
1. <span data-ttu-id="3938e-226">In Azure Explorer espandere **HDInsight**, fare clic con il pulsante destro del mouse sul nome del cluster Spark e quindi scegliere **Open Cluster Management Portal (Ambari)** (Apri il portale di gestione cluster - Ambari).</span><span class="sxs-lookup"><span data-stu-id="3938e-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="3938e-227">Quando richiesto, immettere le credenziali dell'amministratore per il cluster.</span><span class="sxs-lookup"><span data-stu-id="3938e-227">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="3938e-228">Queste credenziali sono state specificate durante il processo di configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="3938e-228">You specified these credentials during the cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="3938e-229">Gestire le sottoscrizioni di Azure</span><span class="sxs-lookup"><span data-stu-id="3938e-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="3938e-230">Per impostazione predefinita, il Toolkit di Azure per IntelliJ elenca i cluster Spark di tutte le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="3938e-230">By default, Azure Toolkit for IntelliJ lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="3938e-231">Se necessario, è possibile specificare le sottoscrizioni a cui si vuole accedere.</span><span class="sxs-lookup"><span data-stu-id="3938e-231">If necessary, you can specify the subscriptions that you want to access.</span></span> 

1. <span data-ttu-id="3938e-232">In Azure Explorer fare clic con il pulsante destro del mouse sul nodo radice **Azure** e quindi scegliere **Gestisci sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="3938e-232">In Azure Explorer, right-click the **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="3938e-233">Nella finestra di dialogo deselezionare le caselle di controllo accanto alla sottoscrizione alla quale non si vuole accedere e quindi selezionare **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="3938e-233">In the dialog box, clear the check boxes next to the subscriptions that you don't want to access, and then select **Close**.</span></span> <span data-ttu-id="3938e-234">È anche possibile selezionare **Esci** per uscire dalla sessione di sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3938e-234">You can also select **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="3938e-235">Eseguire un'applicazione Spark in Scala localmente</span><span class="sxs-lookup"><span data-stu-id="3938e-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="3938e-236">È possibile usare il Toolkit di Azure per IntelliJ per eseguire applicazioni Spark Scala localmente nella workstation.</span><span class="sxs-lookup"><span data-stu-id="3938e-236">You can use Azure Toolkit for IntelliJ to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="3938e-237">Le applicazioni in genere non richiedono l'accesso a risorse del cluster quali il contenitore di archiviazione e possono essere eseguite e testate localmente.</span><span class="sxs-lookup"><span data-stu-id="3938e-237">The applications usually don't need access to cluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="3938e-238">Prerequisito</span><span class="sxs-lookup"><span data-stu-id="3938e-238">Prerequisite</span></span>
<span data-ttu-id="3938e-239">Quando si esegue l'applicazione Spark Scala locale in un computer Windows, potrebbe essere restituita un'eccezione, come spiegato in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356),</span><span class="sxs-lookup"><span data-stu-id="3938e-239">While you're running the local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="3938e-240">che si verifica a causa di un file WinUtils.exe mancante in Windows.</span><span class="sxs-lookup"><span data-stu-id="3938e-240">The exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="3938e-241">Per risolvere questo errore, [scaricare il file eseguibile](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) in un percorso come **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="3938e-241">To resolve this error, [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="3938e-242">È quindi necessario aggiungere una variabile di ambiente **HADOOP_HOME** e impostare il valore della variabile su **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="3938e-242">Then, add the environment variable **HADOOP_HOME**, and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="3938e-243">Eseguire un'applicazione Spark in Scala locale</span><span class="sxs-lookup"><span data-stu-id="3938e-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="3938e-244">Avviare IntelliJ IDEA e creare un progetto.</span><span class="sxs-lookup"><span data-stu-id="3938e-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="3938e-245">Nella finestra di dialogo **New Project** (Nuovo progetto) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3938e-245">In the **New Project** dialog box, do the following:</span></span>
   
    <span data-ttu-id="3938e-246">a.</span><span class="sxs-lookup"><span data-stu-id="3938e-246">a.</span></span> <span data-ttu-id="3938e-247">Selezionare **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)** (Spark su esecuzione di esempio locale HDInsight - Scala).</span><span class="sxs-lookup"><span data-stu-id="3938e-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="3938e-248">b.</span><span class="sxs-lookup"><span data-stu-id="3938e-248">b.</span></span> <span data-ttu-id="3938e-249">Nell'elenco **Build tool** (Strumento di compilazione) selezionare uno degli strumenti seguenti, in base alla necessità:</span><span class="sxs-lookup"><span data-stu-id="3938e-249">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="3938e-250">**Maven**, per ottenere supporto per la creazione guidata di un progetto Scala</span><span class="sxs-lookup"><span data-stu-id="3938e-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="3938e-251">**SBT**, per la gestione delle dipendenze e la compilazione per il progetto Scala</span><span class="sxs-lookup"><span data-stu-id="3938e-251">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![Finestra di dialogo del nuovo progetto](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="3938e-253">Selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3938e-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="3938e-254">Nella finestra successiva seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3938e-254">In the next window, do the following:</span></span>
   
    <span data-ttu-id="3938e-255">a.</span><span class="sxs-lookup"><span data-stu-id="3938e-255">a.</span></span> <span data-ttu-id="3938e-256">Immettere un nome e un percorso per il progetto.</span><span class="sxs-lookup"><span data-stu-id="3938e-256">Enter a project name and location.</span></span>

    <span data-ttu-id="3938e-257">b.</span><span class="sxs-lookup"><span data-stu-id="3938e-257">b.</span></span> <span data-ttu-id="3938e-258">Nell'elenco a discesa **Project SDK** (SDK progetto) selezionare una versione di Java successiva alla versione 1.7.</span><span class="sxs-lookup"><span data-stu-id="3938e-258">In the **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="3938e-259">c.</span><span class="sxs-lookup"><span data-stu-id="3938e-259">c.</span></span> <span data-ttu-id="3938e-260">Nell'elenco a discesa **Spark Version** (Versione di Spark) selezionare la versione di Scala da usare: Scala 2.11.x per Spark 2.0 o Scala 2.10.x per Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="3938e-260">In the **Spark Version** drop-down list, select the version of Scala that you want to use: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![Finestra di dialogo del nuovo progetto](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="3938e-262">Selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="3938e-262">Select **Finish**.</span></span>

6. <span data-ttu-id="3938e-263">Il modello aggiunge un codice di esempio (**LogQuery**) sotto la cartella **src** eseguibile in locale nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="3938e-263">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![Percorso di LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="3938e-265">Fare clic con il pulsante destro del mouse sull'applicazione **LogQuery** e quindi selezionare **Run 'LogQuery'** (Esegui "LogQuery").</span><span class="sxs-lookup"><span data-stu-id="3938e-265">Right-click the **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="3938e-266">Viene visualizzato un output simile al seguente nella scheda **Run** (Esegui) in basso:</span><span class="sxs-lookup"><span data-stu-id="3938e-266">On the **Run** tab at the bottom, you see an output like the following:</span></span>
   
   ![Risultato dell'esecuzione locale dell'applicazione Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-to-use-azure-toolkit-for-intellij"></a><span data-ttu-id="3938e-268">Convertire le applicazioni IntelliJ IDEA esistenti per usare il Toolkit di Azure per IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3938e-268">Convert existing IntelliJ IDEA applications to use Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="3938e-269">È possibile convertire le applicazioni Spark Scala esistenti create in IntelliJ IDEA per renderle compatibili con Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3938e-269">You can convert the existing Spark Scala applications that you created in IntelliJ IDEA to be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="3938e-270">È possibile usare il plug-in per inviare le applicazioni a un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="3938e-270">You can then use the plug-in to submit the applications to an HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="3938e-271">Per un'applicazione Spark Scala esistente creata tramite IntelliJ IDEA, aprire il file con estensione IML associato.</span><span class="sxs-lookup"><span data-stu-id="3938e-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open the associated .iml file.</span></span>

2. <span data-ttu-id="3938e-272">A livello di radice viene visualizzato un elemento **module** simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3938e-272">At the root level is a **module** element like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="3938e-273">Modificare l'elemento per aggiungere `UniqueKey="HDInsightTool"` in modo che l'elemento **module** sia simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3938e-273">Edit the element to add `UniqueKey="HDInsightTool"` so that the **module** element looks like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="3938e-274">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="3938e-274">Save the changes.</span></span> <span data-ttu-id="3938e-275">L'applicazione dovrebbe ora essere compatibile con il Toolkit di Azure per IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3938e-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="3938e-276">È possibile verificarlo facendo clic con il pulsante destro del mouse sul nome del progetto in Project Explorer (Esplora progetti).</span><span class="sxs-lookup"><span data-stu-id="3938e-276">You can test it by right-clicking the project name in Project Explorer.</span></span> <span data-ttu-id="3938e-277">Nel menu a comparsa viene ora visualizzata l'opzione **Submit Spark Application to HDInsight**(Invia applicazione Spark a HDInsight).</span><span class="sxs-lookup"><span data-stu-id="3938e-277">The pop-up menu now has the option **Submit Spark Application to HDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3938e-278">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="3938e-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="3938e-279">Errore nell'esecuzione locale: *Usare dimensioni di heap maggiori*</span><span class="sxs-lookup"><span data-stu-id="3938e-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="3938e-280">Se in Spark 1.6 si usa un SDK per Java a 32 bit durante l'esecuzione locale, è possibile riscontrare gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="3938e-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter the following errors:</span></span>

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

<span data-ttu-id="3938e-281">Questi errori si verificano perché le dimensioni heap non sono sufficientemente grandi da consentire l'esecuzione di Spark.</span><span class="sxs-lookup"><span data-stu-id="3938e-281">These errors happen because the heap size is not large enough for Spark to run.</span></span> <span data-ttu-id="3938e-282">Spark richiede almeno 471 MB.</span><span class="sxs-lookup"><span data-stu-id="3938e-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="3938e-283">Per altre informazioni, vedere [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081). Una soluzione semplice consiste nell'uso di un SDK per Java a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="3938e-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is to use a 64-bit Java SDK.</span></span> <span data-ttu-id="3938e-284">È anche possibile modificare le impostazioni JVM in IntelliJ aggiungendo le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3938e-284">You can also change the JVM settings in IntelliJ by adding the following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Aggiunta di opzioni alla casella "VM options" (Opzioni della macchina virtuale) in IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="3938e-286">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="3938e-286">FAQ</span></span>
<span data-ttu-id="3938e-287">Per inviare un'applicazione ad Azure Data Lake Store, selezionare la modalità **Interactive** (Interattivo) durante l'accesso ad Azure.</span><span class="sxs-lookup"><span data-stu-id="3938e-287">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="3938e-288">Se si seleziona la modalità **Automated** (Automatico), viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="3938e-288">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="3938e-290">A questo punto, il problema è risolto.</span><span class="sxs-lookup"><span data-stu-id="3938e-290">Now, we resolved it.</span></span> <span data-ttu-id="3938e-291">È possibile scegliere un cluster di Azure Data Lake per inviare l'applicazione con qualsiasi metodo di accesso.</span><span class="sxs-lookup"><span data-stu-id="3938e-291">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="3938e-292">Commenti, suggerimenti e problemi noti</span><span class="sxs-lookup"><span data-stu-id="3938e-292">Feedback and known issues</span></span>
<span data-ttu-id="3938e-293">Il supporto della visualizzazione diretta degli output di Spark non è al momento disponibile.</span><span class="sxs-lookup"><span data-stu-id="3938e-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="3938e-294">Per eventuali commenti o suggerimenti oppure se si riscontrano problemi nell'uso di questo plug-in, inviare un messaggio di posta elettronica all'indirizzo hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="3938e-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="3938e-295"><a name="seealso"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3938e-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="3938e-296">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3938e-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="3938e-297">Demo</span><span class="sxs-lookup"><span data-stu-id="3938e-297">Demo</span></span>
* <span data-ttu-id="3938e-298">Creare il progetto Scala (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (Creare applicazioni Spark Scala)</span><span class="sxs-lookup"><span data-stu-id="3938e-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="3938e-299">Debug remoto (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) (Usare Azure Toolkit for IntelliJ per il debug remoto di applicazioni Spark nel cluster HDInsight)</span><span class="sxs-lookup"><span data-stu-id="3938e-299">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="3938e-300">Scenari</span><span class="sxs-lookup"><span data-stu-id="3938e-300">Scenarios</span></span>
* [<span data-ttu-id="3938e-301">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3938e-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="3938e-302">Spark con Machine Learning: usare Spark in HDInsight per l'analisi della temperatura di compilazione usando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="3938e-302">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="3938e-303">Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="3938e-303">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="3938e-304">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="3938e-304">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="3938e-305">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3938e-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="3938e-306">Creazione ed esecuzione di applicazioni</span><span class="sxs-lookup"><span data-stu-id="3938e-306">Creating and running applications</span></span>
* [<span data-ttu-id="3938e-307">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="3938e-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="3938e-308">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="3938e-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="3938e-309">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="3938e-309">Tools and extensions</span></span>
* [<span data-ttu-id="3938e-310">Usare Azure Toolkit per IntelliJ per il debug remoto di applicazioni Spark tramite VPN</span><span class="sxs-lookup"><span data-stu-id="3938e-310">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="3938e-311">Usare Azure Toolkit per IntelliJ per il debug remoto di applicazioni Spark tramite SSH</span><span class="sxs-lookup"><span data-stu-id="3938e-311">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="3938e-312">Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="3938e-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="3938e-313">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications (Usare gli strumenti HDInsight nel Toolkit di Azure per Eclipse per creare applicazioni Spark)</span><span class="sxs-lookup"><span data-stu-id="3938e-313">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="3938e-314">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3938e-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="3938e-315">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="3938e-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="3938e-316">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="3938e-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="3938e-317">Installare Jupyter Notebook nel computer e connetterlo a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="3938e-317">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="3938e-318">Gestione delle risorse</span><span class="sxs-lookup"><span data-stu-id="3938e-318">Managing resources</span></span>
* [<span data-ttu-id="3938e-319">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3938e-319">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="3938e-320">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3938e-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

