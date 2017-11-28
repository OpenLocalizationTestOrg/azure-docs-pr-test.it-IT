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
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="ac3f2-103">Utilizzare Azure Toolkit per le applicazioni per un cluster HDInsight Spark toocreate IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ac3f2-103">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="ac3f2-104">Utilizzare hello Azure Toolkit per le applicazioni di Spark toodevelop plug-in IntelliJ scritte in Scala e quindi inviarli tooan cluster HDInsight Spark direttamente dall'ambiente di sviluppo integrato (IDE) di hello IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-104">Use hello Azure Toolkit for IntelliJ plug-in toodevelop Spark applications written in Scala, and then submit them tooan HDInsight Spark cluster directly from hello IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="ac3f2-105">È possibile utilizzare hello plug-in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-105">You can use hello plug-in in a few ways:</span></span>

* <span data-ttu-id="ac3f2-106">Sviluppare e inviare un'applicazione Spark in Scala in un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="ac3f2-107">Accedere alle risorse cluster HDInsight Spark di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="ac3f2-108">Sviluppare ed eseguire un'applicazione Spark in Scala localmente.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="ac3f2-109">toocreate il progetto, hello vista [creare applicazioni Spark con hello Azure Toolkit per IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-109">toocreate your project, view hello [Create Spark Applications with hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac3f2-110">È possibile utilizzare questo plug-in toocreate e inviare le applicazioni solo per un cluster HDInsight Spark in Linux.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-110">You can use this plug-in toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="ac3f2-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ac3f2-111">Prerequisites</span></span>

- <span data-ttu-id="ac3f2-112">Un cluster Apache Spark in HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="ac3f2-113">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="ac3f2-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="ac3f2-114">Kit di sviluppo di Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="ac3f2-115">È possibile installarlo dal hello [sito Web Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="ac3f2-115">You can install it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="ac3f2-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-116">IntelliJ IDEA.</span></span> <span data-ttu-id="ac3f2-117">In questo articolo viene usata la versione 2017.1.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-117">This article uses version 2017.1.</span></span> <span data-ttu-id="ac3f2-118">È possibile installarlo dal hello [sito Web JetBrains](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="ac3f2-118">You can install it from hello [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="ac3f2-119">Installare il Toolkit di Azure per IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ac3f2-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="ac3f2-120">Per le istruzioni di installazione vedere [Installare Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="ac3f2-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="ac3f2-121">Accedi tooyour sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="ac3f2-121">Sign in tooyour Azure subscription</span></span>

1. <span data-ttu-id="ac3f2-122">Avviare hello IntelliJ IDE, quindi aprire Esplora Azure.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-122">Start hello IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="ac3f2-123">In hello **vista** dal menu **finestre degli strumenti**, quindi selezionare **Esplora Azure**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-123">On hello **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![collegamento Esplora Azure Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="ac3f2-125">Pulsante destro del mouse hello **Azure** nodo e quindi selezionare **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-125">Right-click hello **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="ac3f2-126">In hello **Azure Accedi** nella finestra di dialogo **Accedi**, quindi immettere le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-126">In hello **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Hello Azure Sign nella finestra di dialogo](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="ac3f2-128">Dopo avere effettuato, hello **sottoscrizioni selezionare** tutti hello sottoscrizioni Azure in cui sono associate elenchi di finestra di dialogo casella hello credenziali.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-128">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions that are associated with hello credentials.</span></span> <span data-ttu-id="ac3f2-129">Seleziona hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-129">Select hello **Select** button.</span></span>

    ![la finestra di dialogo selezionare le sottoscrizioni di Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="ac3f2-131">In hello **Esplora Azure** espandere **HDInsight** hello tooview cluster HDInsight Spark presenti nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-131">On hello **Azure Explorer** tab, expand **HDInsight** tooview hello HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Cluster HDInsight Spark in Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="ac3f2-133">tooview hello risorse (ad esempio, gli account di archiviazione) che sono associate ai cluster hello, è possibile espandere ulteriormente un nodo del nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-133">tooview hello resources (for example, storage accounts) that are associated with hello cluster, you can further expand a cluster-name node.</span></span>
   
    ![Nodo di tipo nome del cluster espanso](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="ac3f2-135">Eseguire un'applicazione Spark in Scala in un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="ac3f2-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="ac3f2-136">Avviare IntelliJ IDEA e creare un progetto.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="ac3f2-137">In hello **nuovo progetto** finestra di dialogo casella, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-137">In hello **New Project** dialog box, do hello following:</span></span> 

   <span data-ttu-id="ac3f2-138">a.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-138">a.</span></span> <span data-ttu-id="ac3f2-139">Selezionare **HDInsight** > **Spark on HDInsight (Scala)** (Spark in HDInsight - Scala).</span><span class="sxs-lookup"><span data-stu-id="ac3f2-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="ac3f2-140">b.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-140">b.</span></span> <span data-ttu-id="ac3f2-141">In hello **strumento di compilazione** selezionare uno dei hello seguenti, in base tooyour necessità:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-141">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="ac3f2-142">**Maven**, per ottenere supporto per la creazione guidata di un progetto Scala</span><span class="sxs-lookup"><span data-stu-id="ac3f2-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="ac3f2-143">**SBT**, per la gestione delle dipendenze hello e la compilazione per il progetto di Scala hello</span><span class="sxs-lookup"><span data-stu-id="ac3f2-143">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![finestra di dialogo Nuovo progetto Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="ac3f2-145">Selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-145">Select **Next**.</span></span>

3. <span data-ttu-id="ac3f2-146">Hello Scala-creazione del progetto verrà rilevato automaticamente se è stato installato hello Scala plug-in.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-146">hello Scala project-creation wizard automatically detects whether you've installed hello Scala plug-in.</span></span> <span data-ttu-id="ac3f2-147">Selezionare **Installa**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-147">Select **Install**.</span></span>

   ![Verifica del plug-in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="ac3f2-149">hello toodownload Scala plug-in, seleziona **OK**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-149">toodownload hello Scala plug-in, select **OK**.</span></span> <span data-ttu-id="ac3f2-150">Seguire le istruzioni di hello toorestart IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-150">Follow hello instructions toorestart IntelliJ.</span></span> 

   ![finestra di dialogo dell'installazione di plug-in Scala Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="ac3f2-152">In hello **nuovo progetto** finestra hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-152">In hello **New Project** window, do hello following:</span></span>  

    ![Selezione di hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="ac3f2-154">a.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-154">a.</span></span> <span data-ttu-id="ac3f2-155">Immettere un nome e un percorso per il progetto.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-155">Enter a project name and location.</span></span>

   <span data-ttu-id="ac3f2-156">b.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-156">b.</span></span> <span data-ttu-id="ac3f2-157">In hello **Project SDK** elenco a discesa, seleziona **Java 1.8** per cluster 2. x di Spark hello o selezionare **Java 1.7** per cluster 1. x di hello Spark.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-157">In hello **Project SDK** drop-down list, select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span>

   <span data-ttu-id="ac3f2-158">c.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-158">c.</span></span> <span data-ttu-id="ac3f2-159">In hello **versione Spark** elenco a discesa, creazione guidata nuovo progetto di Scala si integra la versione corretta di hello per SDK Spark e SDK di Scala.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-159">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="ac3f2-160">Se la versione del cluster Spark hello è precedente alla versione 2.0, selezionare **nascita 1. x**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-160">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="ac3f2-161">In caso contrario, selezionare **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="ac3f2-162">In questo esempio viene usata la versione **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="ac3f2-163">Selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-163">Select **Finish**.</span></span>

7. <span data-ttu-id="ac3f2-164">progetto Spark Hello crea automaticamente un elemento.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-164">hello Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="ac3f2-165">elemento hello tooview, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-165">tooview hello artifact, do hello following:</span></span>

   <span data-ttu-id="ac3f2-166">a.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-166">a.</span></span> <span data-ttu-id="ac3f2-167">In hello **File** dal menu **struttura del progetto**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-167">On hello **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="ac3f2-168">b.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-168">b.</span></span> <span data-ttu-id="ac3f2-169">In hello **struttura del progetto** nella finestra di dialogo **elementi** tooview hello predefinito l'elemento viene creato.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-169">In hello **Project Structure** dialog box, select **Artifacts** tooview hello default artifact that is created.</span></span> <span data-ttu-id="ac3f2-170">È inoltre possibile creare la propria artefatto selezionando hello sul segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="ac3f2-170">You can also create your own artifact by selecting hello plus sign (**+**).</span></span>

      ![Informazioni di elementi nella finestra di dialogo hello](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="ac3f2-172">Aggiungere il codice sorgente dell'applicazione eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-172">Add your application source code by doing hello following:</span></span>

   <span data-ttu-id="ac3f2-173">a.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-173">a.</span></span> <span data-ttu-id="ac3f2-174">In Esplora progetti, fare doppio clic su **src**, punto troppo**New**, quindi selezionare **Scala classe**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-174">In Project Explorer, right-click **src**, point too**New**, and then select **Scala Class**.</span></span>
      
      ![Comandi per la creazione di una classe Scala in Project Explorer (Esplora progetti)](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="ac3f2-176">b.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-176">b.</span></span> <span data-ttu-id="ac3f2-177">In hello **Crea nuova classe Scala** finestra di dialogo, specificare un nome, selezionare **oggetto** in hello **tipo** e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-177">In hello **Create New Scala Class** dialog box, provide a name, select **Object** in hello **Kind** box, and then select **OK**.</span></span>
      
      ![Finestra di dialogo Create New Scala Class (Crea nuova classe Scala)](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="ac3f2-179">c.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-179">c.</span></span> <span data-ttu-id="ac3f2-180">In hello **MyClusterApp.scala** file, incollare hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-180">In hello **MyClusterApp.scala** file, paste hello following code.</span></span> <span data-ttu-id="ac3f2-181">Hello codice legge i dati di hello da HVAC.csv (disponibile in tutti i cluster HDInsight Spark), recupera le righe di hello che contengono solo una cifra nella colonna di settimo hello nel file CSV hello e scrive l'output di hello troppo**/HVACOut** in predefinito hello contenitore di archiviazione per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-181">hello code reads hello data from HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that have only one digit in hello seventh column in hello CSV file, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

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

9. <span data-ttu-id="ac3f2-182">Eseguire un'applicazione hello in un cluster HDInsight Spark eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-182">Run hello application on an HDInsight Spark cluster by doing hello following:</span></span>

   <span data-ttu-id="ac3f2-183">a.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-183">a.</span></span> <span data-ttu-id="ac3f2-184">In Esplora progetti, nome del progetto hello e quindi scegliere **tooHDInsight inviare applicazione Spark**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-184">In Project Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>
      
      ![comando tooHDInsight inviare Spark applicazione Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="ac3f2-186">b.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-186">b.</span></span> <span data-ttu-id="ac3f2-187">Si sono tooenter richieste le credenziali di sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-187">You are prompted tooenter your Azure subscription credentials.</span></span> <span data-ttu-id="ac3f2-188">In hello **invio Spark** fornire hello seguente i valori nella finestra di dialogo e quindi selezionare **Invia**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-188">In hello **Spark Submission** dialog box, provide hello following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="ac3f2-189">Per **nascita cluster (solo Linux)**, selezionare l'applicazione di cluster di HDInsight Spark in cui si desidera toorun hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-189">For **Spark clusters (Linux only)**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>

      * <span data-ttu-id="ac3f2-190">Selezionare un elemento dal progetto IntelliJ hello o selezionarne uno dall'unità disco rigido hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-190">Select an artifact from hello IntelliJ project, or select one from hello hard drive.</span></span>

      * <span data-ttu-id="ac3f2-191">In hello **nome della classe principale** casella, i puntini di sospensione selezionare hello (**...** ), selezionare la classe principale hello nel codice sorgente dell'applicazione, quindi **OK**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-191">In hello **Main class name** box, select hello ellipsis (**...**), select hello main class in your application source code, and then select **OK**.</span></span>

        ![finestra di dialogo Seleziona classe Main Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="ac3f2-193">Poiché il codice dell'applicazione hello in questo esempio non richiede argomenti della riga di comando o fare riferimento a contenitori o file, è possibile lasciare hello rimanenti caselle vuote.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-193">Because hello application code in this example does not require command-line arguments or reference JARs or files, you can leave hello remaining boxes empty.</span></span> <span data-ttu-id="ac3f2-194">Dopo aver fornito tutte le informazioni di hello, la finestra di dialogo hello dovrebbe essere simile a hello seguente immagine.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-194">After you provide all hello information, hello dialog box should resemble hello following image.</span></span>
        
        ![la finestra di dialogo di invio Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="ac3f2-196">c.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-196">c.</span></span> <span data-ttu-id="ac3f2-197">Hello **invio Spark** scheda nella parte inferiore di hello della finestra hello deve iniziare la visualizzazione di stato di avanzamento hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-197">hello **Spark Submission** tab at hello bottom of hello window should start displaying hello progress.</span></span> <span data-ttu-id="ac3f2-198">È anche possibile arrestare un'applicazione hello selezionando pulsante rosso hello hello **invio Spark** finestra.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-198">You can also stop hello application by selecting hello red button in hello **Spark Submission** window.</span></span>
      
      ![finestra di invio Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="ac3f2-200">toolearn come tooaccess hello output del processo, vedere hello "accesso e gestire i cluster di HDInsight Spark usando Azure Toolkit per IntelliJ" più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-200">toolearn how tooaccess hello job output, see hello "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="ac3f2-201">Eseguire o eseguire il debug di un'applicazione Spark Scala in un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="ac3f2-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="ac3f2-202">Si consiglia inoltre di un altro modo per cluster di toohello hello Spark applicazione di invio.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-202">We also recommend another way of submitting hello Spark application toohello cluster.</span></span> <span data-ttu-id="ac3f2-203">È possibile farlo impostando i parametri di hello in hello **le configurazioni di esecuzione/Debug** IDE.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-203">You can do so by setting hello parameters in hello **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="ac3f2-204">Per altre informazioni vedere [Eseguire il debug remoto delle applicazioni Spark su un cluster HDInsight con Azure Toolkit for IntelliJ tramite SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="ac3f2-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="ac3f2-205">Accedere e gestire i cluster HDInsight Spark tramite il Toolkit di Azure per IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ac3f2-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="ac3f2-206">È possibile eseguire diverse operazioni mediante il Toolkit Azure per IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="ac3f2-207">Visualizzazione processo hello di accesso</span><span class="sxs-lookup"><span data-stu-id="ac3f2-207">Access hello job view</span></span>
1. <span data-ttu-id="ac3f2-208">In Esplora Azure espandere **HDInsight**, espandere il nome del cluster Spark hello e quindi selezionare **processi**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-208">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then select **Jobs**.</span></span>  

    ![Nodo di visualizzazione dei processi](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="ac3f2-210">Nel riquadro di destra hello, hello **Visualizza processo Spark** scheda vengono visualizzate tutte le applicazioni che sono state eseguite nel cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-210">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="ac3f2-211">Selezionare il nome di hello di un'applicazione hello per cui si desiderano toosee ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-211">Select hello name of hello application for which you want toosee more details.</span></span>

    ![Dettagli applicazione](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="ac3f2-213">toodisplay esecuzione processo informazioni di base, passare il mouse sul grafico processi hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-213">toodisplay basic running job information, hover over hello job graph.</span></span> <span data-ttu-id="ac3f2-214">grafico di fasi tooview hello e le informazioni che ogni processo viene generato l'errore, selezionare un nodo nel grafico processi hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-214">tooview hello stages graph and information that every job generates, select a node on hello job graph.</span></span>

    ![Dettagli delle fasi dei processi](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="ac3f2-216">tooview utilizzati di frequente i log, ad esempio *Driver Stderr*, *Driver Stdout*, e *informazioni di Directory*selezionare hello **Log** scheda.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-216">tooview frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select hello **Log** tab.</span></span>

    ![Dettagli del log](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="ac3f2-218">È anche possibile visualizzare hello cronologia Spark dell'interfaccia utente e dell'interfaccia utente di YARN (a livello di applicazione hello) hello selezionando un collegamento nella parte superiore di hello della finestra hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-218">You can also view hello Spark history UI and hello YARN UI (at hello application level) by selecting a link at hello top of hello window.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="ac3f2-219">Server di accesso hello Spark cronologia</span><span class="sxs-lookup"><span data-stu-id="ac3f2-219">Access hello Spark history server</span></span>
1. <span data-ttu-id="ac3f2-220">In Azure Explorer espandere **HDInsight**, fare clic con il pulsante destro del mouse sul nome del cluster Spark e quindi scegliere **Open Spark History UI** (Apri UI cronologia Spark).</span><span class="sxs-lookup"><span data-stu-id="ac3f2-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="ac3f2-221">Quando richiesto, immettere le credenziali di amministratore del cluster di hello, specificata durante la configurazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-221">When you're prompted, enter hello cluster's admin credentials, which you specified when you set up hello cluster.</span></span>

3. <span data-ttu-id="ac3f2-222">Nel dashboard di server hello Spark cronologia, è possibile utilizzare hello applicazione nome toolook per un'applicazione hello appena finita in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-222">On hello Spark history server dashboard, you can use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="ac3f2-223">In hello codice precedente, impostare il nome di applicazione hello utilizzando `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-223">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="ac3f2-224">Il nome dell'applicazione Spark è quindi **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="ac3f2-225">Avviare il portale di Ambari hello</span><span class="sxs-lookup"><span data-stu-id="ac3f2-225">Start hello Ambari portal</span></span>
1. <span data-ttu-id="ac3f2-226">In Azure Explorer espandere **HDInsight**, fare clic con il pulsante destro del mouse sul nome del cluster Spark e quindi scegliere **Open Cluster Management Portal (Ambari)** (Apri il portale di gestione cluster - Ambari).</span><span class="sxs-lookup"><span data-stu-id="ac3f2-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="ac3f2-227">Quando richiesto, immettere le credenziali di amministratore hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-227">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="ac3f2-228">Queste credenziali è stato specificato durante l'installazione del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-228">You specified these credentials during hello cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="ac3f2-229">Gestire le sottoscrizioni di Azure</span><span class="sxs-lookup"><span data-stu-id="ac3f2-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="ac3f2-230">Per impostazione predefinita, Azure Toolkit per IntelliJ sono elencati i cluster Spark hello da tutte le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-230">By default, Azure Toolkit for IntelliJ lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="ac3f2-231">Se necessario, è possibile specificare che si desidera tooaccess le sottoscrizioni di hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-231">If necessary, you can specify hello subscriptions that you want tooaccess.</span></span> 

1. <span data-ttu-id="ac3f2-232">In soluzioni di Azure, fare clic hello **Azure** nodo radice e quindi selezionare **Gestisci sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-232">In Azure Explorer, right-click hello **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="ac3f2-233">Nella finestra di dialogo hello cancellare hello caselle di controllo successive toohello sottoscrizioni che non desidera tooaccess e quindi selezionare **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-233">In hello dialog box, clear hello check boxes next toohello subscriptions that you don't want tooaccess, and then select **Close**.</span></span> <span data-ttu-id="ac3f2-234">È inoltre possibile selezionare **Sign Out** se si desidera toosign fuori la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-234">You can also select **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="ac3f2-235">Eseguire un'applicazione Spark in Scala localmente</span><span class="sxs-lookup"><span data-stu-id="ac3f2-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="ac3f2-236">È possibile utilizzare Azure Toolkit per le applicazioni di Scala Spark toorun IntelliJ in locale nella workstation.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-236">You can use Azure Toolkit for IntelliJ toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="ac3f2-237">applicazioni Hello in genere non è necessario accedere toocluster alle risorse, ad esempio i contenitori di archiviazione, ed è possibile eseguire tali test in locale.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-237">hello applications usually don't need access toocluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="ac3f2-238">Prerequisito</span><span class="sxs-lookup"><span data-stu-id="ac3f2-238">Prerequisite</span></span>
<span data-ttu-id="ac3f2-239">Mentre si esegue un'applicazione hello locale Spark Scala in un computer Windows, è possibile ricevere un'eccezione, come illustrato in [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="ac3f2-239">While you're running hello local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="ac3f2-240">perché WinUtils.exe manca in Windows, si verifica un'eccezione di Hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-240">hello exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="ac3f2-241">tooresolve questo errore, [scaricare hello eseguibile](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa percorso, ad esempio **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-241">tooresolve this error, [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="ac3f2-242">Quindi, aggiungere la variabile di ambiente hello **HADOOP_HOME**e impostare il valore di hello della variabile hello troppo**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-242">Then, add hello environment variable **HADOOP_HOME**, and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="ac3f2-243">Eseguire un'applicazione Spark in Scala locale</span><span class="sxs-lookup"><span data-stu-id="ac3f2-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="ac3f2-244">Avviare IntelliJ IDEA e creare un progetto.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="ac3f2-245">In hello **nuovo progetto** finestra di dialogo casella, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-245">In hello **New Project** dialog box, do hello following:</span></span>
   
    <span data-ttu-id="ac3f2-246">a.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-246">a.</span></span> <span data-ttu-id="ac3f2-247">Selezionare **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)** (Spark su esecuzione di esempio locale HDInsight - Scala).</span><span class="sxs-lookup"><span data-stu-id="ac3f2-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="ac3f2-248">b.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-248">b.</span></span> <span data-ttu-id="ac3f2-249">In hello **strumento di compilazione** selezionare uno dei hello seguenti, in base tooyour necessità:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-249">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="ac3f2-250">**Maven**, per ottenere supporto per la creazione guidata di un progetto Scala</span><span class="sxs-lookup"><span data-stu-id="ac3f2-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="ac3f2-251">**SBT**, per la gestione delle dipendenze hello e la compilazione per il progetto di Scala hello</span><span class="sxs-lookup"><span data-stu-id="ac3f2-251">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![finestra di dialogo Nuovo progetto Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="ac3f2-253">Selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="ac3f2-254">Nella finestra successiva hello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-254">In hello next window, do hello following:</span></span>
   
    <span data-ttu-id="ac3f2-255">a.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-255">a.</span></span> <span data-ttu-id="ac3f2-256">Immettere un nome e un percorso per il progetto.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-256">Enter a project name and location.</span></span>

    <span data-ttu-id="ac3f2-257">b.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-257">b.</span></span> <span data-ttu-id="ac3f2-258">In hello **Project SDK** elenco a discesa selezionare una versione di Java che è successiva alla versione 1.7.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-258">In hello **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="ac3f2-259">c.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-259">c.</span></span> <span data-ttu-id="ac3f2-260">In hello **versione Spark** elenco a discesa, la versione di hello selezionare di Scala che si desidera toouse: Scala 2.11.x per Spark 2.0 o Scala 2.10.x per Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-260">In hello **Spark Version** drop-down list, select hello version of Scala that you want toouse: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![finestra di dialogo Nuovo progetto Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="ac3f2-262">Selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-262">Select **Finish**.</span></span>

6. <span data-ttu-id="ac3f2-263">modello di Hello aggiunge un codice di esempio (**LogQuery**) in hello **src** cartella che è possibile eseguire in locale nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-263">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![Percorso di LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="ac3f2-265">Pulsante destro del mouse hello **LogQuery** dell'applicazione e quindi selezionare **esecuzione 'LogQuery'**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-265">Right-click hello **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="ac3f2-266">In hello **eseguire** scheda nella parte inferiore di hello, viene visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-266">On hello **Run** tab at hello bottom, you see an output like hello following:</span></span>
   
   ![Risultato dell'esecuzione locale dell'applicazione Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a><span data-ttu-id="ac3f2-268">Converti esistente IntelliJ IDEA applicazioni toouse Azure Toolkit per IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ac3f2-268">Convert existing IntelliJ IDEA applications toouse Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="ac3f2-269">È possibile convertire hello Spark Scala le applicazioni esistenti create in IntelliJ IDEA toobe compatibili con Azure Toolkit per IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-269">You can convert hello existing Spark Scala applications that you created in IntelliJ IDEA toobe compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="ac3f2-270">È quindi possibile utilizzare hello toosubmit plug-in hello applicazioni tooan cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-270">You can then use hello plug-in toosubmit hello applications tooan HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="ac3f2-271">Per un'applicazione di Scala Spark esistente che è stata creata tramite IntelliJ IDEA, aprire il file di .iml associato hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open hello associated .iml file.</span></span>

2. <span data-ttu-id="ac3f2-272">Livello di radice hello è un **modulo** elemento hello seguente:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-272">At hello root level is a **module** element like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="ac3f2-273">Modifica hello elemento tooadd `UniqueKey="HDInsightTool"` così che hello **modulo** elemento simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-273">Edit hello element tooadd `UniqueKey="HDInsightTool"` so that hello **module** element looks like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="ac3f2-274">Salvare le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-274">Save hello changes.</span></span> <span data-ttu-id="ac3f2-275">L'applicazione dovrebbe ora essere compatibile con il Toolkit di Azure per IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="ac3f2-276">È possibile eseguirne il test facendo clic sul nome del progetto in Project Explorer di hello.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-276">You can test it by right-clicking hello project name in Project Explorer.</span></span> <span data-ttu-id="ac3f2-277">menu a comparsa Hello include ora l'opzione hello **tooHDInsight inviare applicazione Spark**.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-277">hello pop-up menu now has hello option **Submit Spark Application tooHDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ac3f2-278">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ac3f2-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="ac3f2-279">Errore nell'esecuzione locale: *Usare dimensioni di heap maggiori*</span><span class="sxs-lookup"><span data-stu-id="ac3f2-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="ac3f2-280">Spark 1.6, se si utilizza un SDK per Java a 32 bit durante l'esecuzione locale, è possibile riscontrare hello gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter hello following errors:</span></span>

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

<span data-ttu-id="ac3f2-281">Questi errori si verificano perché la dimensione dell'heap hello non è sufficientemente grande per toorun Spark.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-281">These errors happen because hello heap size is not large enough for Spark toorun.</span></span> <span data-ttu-id="ac3f2-282">Spark richiede almeno 471 MB.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="ac3f2-283">Per altre informazioni, vedere [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081). Una soluzione semplice è toouse un SDK per Java a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is toouse a 64-bit Java SDK.</span></span> <span data-ttu-id="ac3f2-284">È inoltre possibile modificare le impostazioni di JVM hello in IntelliJ aggiungendo hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac3f2-284">You can also change hello JVM settings in IntelliJ by adding hello following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Aggiunta di opzioni toohello "Opzioni VM" casella in IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="ac3f2-286">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="ac3f2-286">FAQ</span></span>
<span data-ttu-id="ac3f2-287">Scegliere un'applicazione tooAzure archivio Data Lake, toosubmit **Interactive** modalità durante il processo di hello sign in Azure.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-287">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="ac3f2-288">Se si seleziona la modalità **Automated** (Automatico), viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-288">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="ac3f2-290">A questo punto, il problema è risolto.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-290">Now, we resolved it.</span></span> <span data-ttu-id="ac3f2-291">È possibile scegliere l'applicazione toosubmit un Cluster di Azure Data Lake con qualsiasi metodo di accesso.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-291">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="ac3f2-292">Commenti, suggerimenti e problemi noti</span><span class="sxs-lookup"><span data-stu-id="ac3f2-292">Feedback and known issues</span></span>
<span data-ttu-id="ac3f2-293">Il supporto della visualizzazione diretta degli output di Spark non è al momento disponibile.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="ac3f2-294">Per eventuali commenti o suggerimenti oppure se si riscontrano problemi nell'uso di questo plug-in, inviare un messaggio di posta elettronica all'indirizzo hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="ac3f2-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="ac3f2-295"><a name="seealso"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ac3f2-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="ac3f2-296">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ac3f2-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="ac3f2-297">Demo</span><span class="sxs-lookup"><span data-stu-id="ac3f2-297">Demo</span></span>
* <span data-ttu-id="ac3f2-298">Creare il progetto Scala (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (Creare applicazioni Spark Scala)</span><span class="sxs-lookup"><span data-stu-id="ac3f2-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="ac3f2-299">Eseguire il debug remoto (video): [utilizzare Azure Toolkit per le applicazioni in modalità remota nel HDInsight Cluster Spark toodebug IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="ac3f2-299">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="ac3f2-300">Scenari</span><span class="sxs-lookup"><span data-stu-id="ac3f2-300">Scenarios</span></span>
* [<span data-ttu-id="ac3f2-301">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ac3f2-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="ac3f2-302">Spark con Machine Learning: usare Spark in HDInsight tooanalyze temperatura utilizzando dati impianto di compilazione</span><span class="sxs-lookup"><span data-stu-id="ac3f2-302">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="ac3f2-303">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="ac3f2-303">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="ac3f2-304">Streaming di Spark: Usare Spark in HDInsight toobuild in tempo reale lo streaming di applicazioni</span><span class="sxs-lookup"><span data-stu-id="ac3f2-304">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="ac3f2-305">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ac3f2-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="ac3f2-306">Creazione ed esecuzione di applicazioni</span><span class="sxs-lookup"><span data-stu-id="ac3f2-306">Creating and running applications</span></span>
* [<span data-ttu-id="ac3f2-307">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="ac3f2-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ac3f2-308">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="ac3f2-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="ac3f2-309">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="ac3f2-309">Tools and extensions</span></span>
* [<span data-ttu-id="ac3f2-310">Utilizzare Azure Toolkit per le applicazioni in modalità remota tramite VPN Spark toodebug IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ac3f2-310">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="ac3f2-311">Utilizzare Azure Toolkit per le applicazioni in modalità remota tramite SSH Spark toodebug IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ac3f2-311">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="ac3f2-312">Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="ac3f2-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="ac3f2-313">Utilizzare gli strumenti di HDInsight in Azure Toolkit per le applicazioni di Spark toocreate Eclipse</span><span class="sxs-lookup"><span data-stu-id="ac3f2-313">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="ac3f2-314">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ac3f2-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="ac3f2-315">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="ac3f2-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="ac3f2-316">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="ac3f2-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="ac3f2-317">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="ac3f2-317">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="ac3f2-318">Gestione delle risorse</span><span class="sxs-lookup"><span data-stu-id="ac3f2-318">Managing resources</span></span>
* [<span data-ttu-id="ac3f2-319">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="ac3f2-319">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="ac3f2-320">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ac3f2-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

