---
title: 'Creare un''app Scala da eseguire nei cluster Spark: Azure HDInsight | Microsoft Docs'
description: Creare un'applicazione Spark scritta in Scala con Apache Maven come sistema di compilazione e un archetipo Maven esistente per Scala fornito da IntelliJ IDEA.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 95dba08744357f8800b05e3d4b892e3a363d5985
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-scala-maven-application-to-run-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="1368a-103">Creare un'applicazione Scala Maven da eseguire nei cluster Apache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1368a-103">Create a Scala Maven application to run on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="1368a-104">Informazioni su come creare un'applicazione Spark scritta in Scala usando Maven con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="1368a-104">Learn how to create a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="1368a-105">L'articolo usa Apache Maven come sistema di compilazione e inizia con un archetipo Maven esistente per Scala fornito da IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="1368a-105">The article uses Apache Maven as the build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="1368a-106">La creazione di un'applicazione Scala in IntelliJ IDEA comporta i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1368a-106">Creating a Scala application in IntelliJ IDEA involves the following steps:</span></span>

* <span data-ttu-id="1368a-107">Usare Maven come sistema di compilazione.</span><span class="sxs-lookup"><span data-stu-id="1368a-107">Use Maven as the build system.</span></span>
* <span data-ttu-id="1368a-108">Aggiornare il file del modello a oggetti dei progetti (POM) per risolvere le dipendenze del modulo Spark.</span><span class="sxs-lookup"><span data-stu-id="1368a-108">Update Project Object Model (POM) file to resolve Spark module dependencies.</span></span>
* <span data-ttu-id="1368a-109">Scrivere l'applicazione in Scala.</span><span class="sxs-lookup"><span data-stu-id="1368a-109">Write your application in Scala.</span></span>
* <span data-ttu-id="1368a-110">Generare un file con estensione jar che può essere inviato ai cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="1368a-110">Generate a jar file that can be submitted to HDInsight Spark clusters.</span></span>
* <span data-ttu-id="1368a-111">Eseguire l'applicazione in un cluster Spark usando Livy.</span><span class="sxs-lookup"><span data-stu-id="1368a-111">Run the application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="1368a-112">HDInsight offre inoltre un plug-in IntelliJ IDEA per semplificare il processo di creazione e di invio di applicazioni a un cluster HDInsight Spark basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="1368a-112">HDInsight also provides an IntelliJ IDEA plugin tool to ease the process of creating and submitting applications to an HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="1368a-113">Per altre informazioni, vedere [Utilizzare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="1368a-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1368a-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1368a-114">Prerequisites</span></span>

* <span data-ttu-id="1368a-115">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1368a-115">An Azure subscription.</span></span> <span data-ttu-id="1368a-116">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1368a-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="1368a-117">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1368a-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="1368a-118">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="1368a-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="1368a-119">Oracle Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="1368a-119">Oracle Java Development kit.</span></span> <span data-ttu-id="1368a-120">Per installarlo, fare clic [qui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="1368a-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="1368a-121">Ambiente IDE Java.</span><span class="sxs-lookup"><span data-stu-id="1368a-121">A Java IDE.</span></span> <span data-ttu-id="1368a-122">Questo articolo usa IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="1368a-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="1368a-123">Per installarlo, fare clic [qui](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="1368a-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="1368a-124">Installare il plug-in Scala per IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="1368a-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="1368a-125">Se durante l'installazione di IntelliJ IDEA non è stata richiesta l'abilitazione del plug-in Scala, avviare IntelliJ IDEA e completare i passaggi seguenti per installare il plug-in:</span><span class="sxs-lookup"><span data-stu-id="1368a-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through the following steps to install the plugin:</span></span>

1. <span data-ttu-id="1368a-126">Avviare IntelliJ IDEA e dalla schermata iniziale fare clic su **Configure** (Configura) e quindi fare clic su **Plugins** (Plugin).</span><span class="sxs-lookup"><span data-stu-id="1368a-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Abilitare i plug-in Scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="1368a-128">Nella schermata successiva fare clic su **Install JetBrains plugin** nell'angolo inferiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="1368a-128">In the next screen, click **Install JetBrains plugin** from the lower left corner.</span></span> <span data-ttu-id="1368a-129">Nella finestra di dialogo **Browse JetBrains Plugins** (Esplora plugin JetBrains) che si apre cercare Scala e quindi fare clic su **Install** (Installa).</span><span class="sxs-lookup"><span data-stu-id="1368a-129">In the **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Installare i plug-in Scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="1368a-131">Quando il plug-in è stato installato correttamente, fare clic sul pulsante **Restart IntelliJ IDEA** per riavviare l'IDE.</span><span class="sxs-lookup"><span data-stu-id="1368a-131">After the plugin installs successfully, click the **Restart IntelliJ IDEA button** to restart the IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="1368a-132">Creare un progetto Scala autonomo</span><span class="sxs-lookup"><span data-stu-id="1368a-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="1368a-133">Avviare IntelliJ IDEA e creare un nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="1368a-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="1368a-134">Nella finestra di dialogo del nuovo progetto selezionare le opzioni seguenti e quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="1368a-134">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![Creare un progetto Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="1368a-136">Selezionare **Maven** come tipo di progetto.</span><span class="sxs-lookup"><span data-stu-id="1368a-136">Select **Maven** as the project type.</span></span>
   * <span data-ttu-id="1368a-137">Specificare un valore per **Project SDK**.</span><span class="sxs-lookup"><span data-stu-id="1368a-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="1368a-138">Fare clic su New e passare alla directory di installazione Java, in genere `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="1368a-138">Click New and navigate to the Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="1368a-139">Selezionare l’opzione **Create from archetype** .</span><span class="sxs-lookup"><span data-stu-id="1368a-139">Select the **Create from archetype** option.</span></span>
   * <span data-ttu-id="1368a-140">Nell'elenco di archetipi selezionare **org.scala-tools.archetypes:scala-archetype-simple**.</span><span class="sxs-lookup"><span data-stu-id="1368a-140">From the list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="1368a-141">Verrà creata la struttura di directory appropriata e verranno scaricate le dipendenze predefinite necessarie per scrivere un programma Scala.</span><span class="sxs-lookup"><span data-stu-id="1368a-141">This will create the right directory structure and download the required default dependencies to write Scala program.</span></span>
2. <span data-ttu-id="1368a-142">Specificare i valori pertinenti per **GroupId** (ID gruppo), **ArtifactId** (ID elemento) e **Version** (Versione).</span><span class="sxs-lookup"><span data-stu-id="1368a-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="1368a-143">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1368a-143">Click **Next**.</span></span>
3. <span data-ttu-id="1368a-144">Nella finestra di dialogo successiva, in cui si specifica la home directory Maven e altre impostazioni utente, accettare le impostazioni predefinite e fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="1368a-144">In the next dialog box, where you specify Maven home directory and other user settings, accept the defaults and click **Next**.</span></span>
4. <span data-ttu-id="1368a-145">Nell'ultima finestra di dialogo specificare un nome di progetto e il percorso, quindi fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="1368a-145">In the last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="1368a-146">Eliminare il file **MySpec.Scala** nel percorso **src\test\scala\com\microsoft\spark\example**,</span><span class="sxs-lookup"><span data-stu-id="1368a-146">Delete the **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="1368a-147">poiché non è necessario per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1368a-147">You do not need this for the application.</span></span>
6. <span data-ttu-id="1368a-148">Se necessario, rinominare i file di origine e di test predefiniti.</span><span class="sxs-lookup"><span data-stu-id="1368a-148">If required, rename the default source and test files.</span></span> <span data-ttu-id="1368a-149">Nel riquadro sinistro di IntelliJ IDEA passare a **src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="1368a-149">From the left pane in the IntelliJ IDEA, navigate to **src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="1368a-150">Fare clic con il pulsante destro del mouse su **App.scala**, scegliere **Refactor** (Refactoring), fare clic su Rename file e nella finestra di dialogo specificare il nuovo nome per l'applicazione, quindi fare clic su **Refactor** (Refactoring).</span><span class="sxs-lookup"><span data-stu-id="1368a-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in the dialog box, provide the new name for the application and then click **Refactor**.</span></span>
   
    ![Rinominare file](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="1368a-152">Nei passaggi successivi si aggiornerà il file pom.xml per definire le dipendenze per l'applicazione Spark in Scala.</span><span class="sxs-lookup"><span data-stu-id="1368a-152">In the subsequent steps, you will update the pom.xml to define the dependencies for the Spark Scala application.</span></span> <span data-ttu-id="1368a-153">Affinché tali dipendenze vengano scaricate e risolte automaticamente, è necessario configurare Maven di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="1368a-153">For those dependencies to be downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Configurare Maven per i download automatici](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="1368a-155">Scegliere **Settings** (Impostazioni) dal menu **File**.</span><span class="sxs-lookup"><span data-stu-id="1368a-155">From the **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="1368a-156">Nella finestra di dialogo **Settings** (Impostazioni) passare a **Build, Execution, Deployment** (Compilazione, esecuzione, distribuzione)  > **Build Tools** (Strumenti di compilazione)  > **Maven** > **Importing** (Importazione).</span><span class="sxs-lookup"><span data-stu-id="1368a-156">In the **Settings** dialog box, navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="1368a-157">Selezionare l'opzione **Import Maven projects automatically**.</span><span class="sxs-lookup"><span data-stu-id="1368a-157">Select the option to **Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="1368a-158">Fare clic su **Apply** (Applica) e quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1368a-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="1368a-159">Aggiornare il file di origine Scala per includere il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1368a-159">Update the Scala source file to include your application code.</span></span> <span data-ttu-id="1368a-160">Aprire e sostituire il codice di esempio esistente con il codice seguente e salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="1368a-160">Open and replace the existing sample code with the following code and save the changes.</span></span> <span data-ttu-id="1368a-161">Questo codice legge i dati del file HVAC.csv, disponibile in tutti i cluster HDInsight Spark, recupera le righe che hanno solo una cifra nella sesta colonna e scrive l'output in **/HVACOut** nel contenitore di archiviazione predefinito per il cluster.</span><span class="sxs-lookup"><span data-stu-id="1368a-161">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the sixth column, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO to wasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows which have only one digit in the 7th column in the CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="1368a-162">Aggiornare il file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="1368a-162">Update the pom.xml.</span></span>
   
   1. <span data-ttu-id="1368a-163">Aggiungere il codice seguente in `<project>\<properties>`</span><span class="sxs-lookup"><span data-stu-id="1368a-163">Within `<project>\<properties>` add the following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="1368a-164">Aggiungere il codice seguente in `<project>\<dependencies>`</span><span class="sxs-lookup"><span data-stu-id="1368a-164">Within `<project>\<dependencies>` add the following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="1368a-165">Salvare le modifiche apportate a pom.xml.</span><span class="sxs-lookup"><span data-stu-id="1368a-165">Save changes to pom.xml.</span></span>
10. <span data-ttu-id="1368a-166">Creare il file con estensione jar.</span><span class="sxs-lookup"><span data-stu-id="1368a-166">Create the .jar file.</span></span> <span data-ttu-id="1368a-167">IntelliJ IDEA consente di creare un file con estensione jar come elemento di un progetto.</span><span class="sxs-lookup"><span data-stu-id="1368a-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="1368a-168">Eseguire i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="1368a-168">Perform the following steps.</span></span>
    
    1. <span data-ttu-id="1368a-169">Scegliere **Project Structure** (Struttura progetto) dal menu **File**.</span><span class="sxs-lookup"><span data-stu-id="1368a-169">From the **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="1368a-170">Nella finestra di dialogo **Project Structure** (Struttura progetto) fare clic su **Artifacts** (Elementi) e quindi sul segno più.</span><span class="sxs-lookup"><span data-stu-id="1368a-170">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="1368a-171">Nella finestra di dialogo popup fare clic su **JAR**, quindi fare clic su **From modules with dependencies** (Da moduli con dipendenze).</span><span class="sxs-lookup"><span data-stu-id="1368a-171">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="1368a-173">Nella finestra di dialogo **Create JAR from Modules** (Crea JAR da moduli) fare clic sui puntini di sospensione (![puntini di sospensione](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png)) relativi a **Main Class** (Classe principale).</span><span class="sxs-lookup"><span data-stu-id="1368a-173">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against the **Main Class**.</span></span>
    4. <span data-ttu-id="1368a-174">Nella finestra di dialogo **Select Main Class** (Seleziona classe principale) selezionare la classe visualizzata per impostazione predefinita e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1368a-174">In the **Select Main Class** dialog box, select the class that appears by default and then click **OK**.</span></span>
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="1368a-176">Nella finestra di dialogo **Create JAR from Modules** (Crea JAR da moduli) verificare che l'opzione per **estrarre nel file JAR di destinazione** sia selezionata e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1368a-176">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="1368a-177">Verrà creato un singolo file con estensione jar con tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="1368a-177">This creates a single JAR with all dependencies.</span></span>
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="1368a-179">Nella scheda del layout dell'output sono elencati tutti i file con estensione jar inclusi nel progetto Maven.</span><span class="sxs-lookup"><span data-stu-id="1368a-179">The output layout tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="1368a-180">È possibile selezionare ed eliminare quelli in cui l'applicazione Scala non ha dipendenze dirette.</span><span class="sxs-lookup"><span data-stu-id="1368a-180">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="1368a-181">Per l'applicazione creata in questo caso, è possibile rimuovere tutti i file tranne l'ultimo (**output di compilazione di SparkSimpleApp**).</span><span class="sxs-lookup"><span data-stu-id="1368a-181">For the application we are creating here, you can remove all but the last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="1368a-182">Selezionare i file JAR da eliminare e quindi fare clic sull’icona **Delete** .</span><span class="sxs-lookup"><span data-stu-id="1368a-182">Select the jars to delete and then click the **Delete** icon.</span></span>
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="1368a-184">Assicurarsi che la casella **Build on make** sia selezionata per garantire che il file jar venga creato ogni volta che il progetto viene creato o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="1368a-184">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="1368a-185">Fare clic su **Apply** (Applica) e quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1368a-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="1368a-186">Sulla barra dei menu fare clic su **Build** (Compila) e quindi su **Make Project** (Crea progetto).</span><span class="sxs-lookup"><span data-stu-id="1368a-186">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="1368a-187">È anche possibile fare clic su **Build Artifacts** per creare il file JAR.</span><span class="sxs-lookup"><span data-stu-id="1368a-187">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="1368a-188">Il file JAR di output viene creato in **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="1368a-188">The output jar is created under **\out\artifacts**.</span></span>
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-the-application-on-the-spark-cluster"></a><span data-ttu-id="1368a-190">Eseguire l'applicazione nel cluster Spark</span><span class="sxs-lookup"><span data-stu-id="1368a-190">Run the application on the Spark cluster</span></span>
<span data-ttu-id="1368a-191">Per eseguire l'applicazione nel cluster, è necessario eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1368a-191">To run the application on the cluster, you must do the following:</span></span>

* <span data-ttu-id="1368a-192">**Copiare il file jar dell’applicazione nel BLOB di archiviazione Azure** associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="1368a-192">**Copy the application jar to the Azure storage blob** associated with the cluster.</span></span> <span data-ttu-id="1368a-193">A tale scopo è possibile usare [**AzCopy**](../storage/common/storage-use-azcopy.md), un'utilità della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="1368a-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="1368a-194">È possibile usare molti altri client per caricare i dati.</span><span class="sxs-lookup"><span data-stu-id="1368a-194">There are a lot of other clients as well that you can use to upload data.</span></span> <span data-ttu-id="1368a-195">Ulteriori informazioni in merito sono disponibili in [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="1368a-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="1368a-196">**Usare Livy per inviare un processo dell’applicazione in modalità remota** al cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="1368a-196">**Use Livy to submit an application job remotely** to the Spark cluster.</span></span> <span data-ttu-id="1368a-197">I cluster Spark in HDInsight includono Livy che espone gli endpoint REST per inviare in modalità remota i processi Spark.</span><span class="sxs-lookup"><span data-stu-id="1368a-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints to remotely submit Spark jobs.</span></span> <span data-ttu-id="1368a-198">Per ulteriori informazioni, vedere [Inviare processi Spark in modalità remota utilizzando Livy con cluster Spark in HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="1368a-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="1368a-199">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="1368a-199">Next step</span></span>

<span data-ttu-id="1368a-200">In questo articolo è stato descritto come creare un'applicazione Scala di Spark.</span><span class="sxs-lookup"><span data-stu-id="1368a-200">In this article you learned how to create a Spark scala application.</span></span> <span data-ttu-id="1368a-201">Passare all'articolo successivo per informazioni su come eseguire questa applicazione in un cluster HDInsight Spark tramite Livy.</span><span class="sxs-lookup"><span data-stu-id="1368a-201">Advance to the next article to learn how to run this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="1368a-202">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="1368a-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

