---
title: aaaCreate Scala app toorun nei cluster Spark - HDInsight di Azure | Documenti Microsoft
description: Creare un'applicazione di Spark scritta in Scala con Apache Maven come hello compilazione system e un sistema di rilevazione di Maven esistente per la Scala fornito da IntelliJ IDEA.
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
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="b628a-103">Creare un toorun applicazione Scala Maven nel cluster di Apache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b628a-103">Create a Scala Maven application toorun on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="b628a-104">Informazioni su come un'applicazione di Spark scritta in Scala con Maven IDEA IntelliJ toocreate.</span><span class="sxs-lookup"><span data-stu-id="b628a-104">Learn how toocreate a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="b628a-105">articolo Hello utilizza Apache Maven come sistema di compilazione e inizia con un sistema di rilevazione di Maven esistente per la Scala fornito da IntelliJ IDEA di hello.</span><span class="sxs-lookup"><span data-stu-id="b628a-105">hello article uses Apache Maven as hello build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="b628a-106">La creazione di un'applicazione di Scala in IntelliJ IDEA prevede hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b628a-106">Creating a Scala application in IntelliJ IDEA involves hello following steps:</span></span>

* <span data-ttu-id="b628a-107">Utilizzare Maven come sistema di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="b628a-107">Use Maven as hello build system.</span></span>
* <span data-ttu-id="b628a-108">Aggiornare le dipendenze del modulo modello oggetto di progetto (POM) file tooresolve Spark.</span><span class="sxs-lookup"><span data-stu-id="b628a-108">Update Project Object Model (POM) file tooresolve Spark module dependencies.</span></span>
* <span data-ttu-id="b628a-109">Scrivere l'applicazione in Scala.</span><span class="sxs-lookup"><span data-stu-id="b628a-109">Write your application in Scala.</span></span>
* <span data-ttu-id="b628a-110">Generare un file jar che può essere cluster Spark tooHDInsight inviato.</span><span class="sxs-lookup"><span data-stu-id="b628a-110">Generate a jar file that can be submitted tooHDInsight Spark clusters.</span></span>
* <span data-ttu-id="b628a-111">Eseguire un'applicazione hello in cluster Spark usando inserire il.</span><span class="sxs-lookup"><span data-stu-id="b628a-111">Run hello application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="b628a-112">HDInsight fornisce inoltre un processo hello di tooease dello strumento di plug-in IntelliJ IDEA di creazione e invio tooan applicazioni cluster HDInsight Spark in Linux.</span><span class="sxs-lookup"><span data-stu-id="b628a-112">HDInsight also provides an IntelliJ IDEA plugin tool tooease hello process of creating and submitting applications tooan HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="b628a-113">Per ulteriori informazioni, vedere [plug-in strumenti di HDInsight di utilizzo per toocreate IntelliJ IDEA e inviare le applicazioni di Spark](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="b628a-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b628a-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b628a-114">Prerequisites</span></span>

* <span data-ttu-id="b628a-115">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b628a-115">An Azure subscription.</span></span> <span data-ttu-id="b628a-116">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b628a-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b628a-117">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b628a-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b628a-118">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b628a-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="b628a-119">Oracle Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="b628a-119">Oracle Java Development kit.</span></span> <span data-ttu-id="b628a-120">Per installarlo, fare clic [qui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="b628a-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="b628a-121">Ambiente IDE Java.</span><span class="sxs-lookup"><span data-stu-id="b628a-121">A Java IDE.</span></span> <span data-ttu-id="b628a-122">Questo articolo usa IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="b628a-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="b628a-123">Per installarlo, fare clic [qui](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="b628a-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="b628a-124">Installare il plug-in Scala per IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="b628a-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="b628a-125">Se installazione IDEA IntelliJ non non richiesta per l'abilitazione di plug-in di Scala, avviare IntelliJ IDEA e passare a hello plug-in hello tooinstall di passaggi seguente:</span><span class="sxs-lookup"><span data-stu-id="b628a-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through hello following steps tooinstall hello plugin:</span></span>

1. <span data-ttu-id="b628a-126">Avviare IntelliJ IDEA e dalla schermata iniziale fare clic su **Configure** (Configura) e quindi fare clic su **Plugins** (Plugin).</span><span class="sxs-lookup"><span data-stu-id="b628a-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Abilitare i plug-in Scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="b628a-128">Nella schermata successiva hello, fare clic su **plug-in installa JetBrains** dall'angolo inferiore sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="b628a-128">In hello next screen, click **Install JetBrains plugin** from hello lower left corner.</span></span> <span data-ttu-id="b628a-129">In hello **Sfoglia i plug-in JetBrains** la finestra di dialogo che viene aperto, eseguire la ricerca di Scala e quindi fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="b628a-129">In hello **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Installare i plug-in Scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="b628a-131">Dopo l'installazione di plug-in hello correttamente, fare clic su hello **pulsante riavviare IDEA IntelliJ** toorestart hello IDE.</span><span class="sxs-lookup"><span data-stu-id="b628a-131">After hello plugin installs successfully, click hello **Restart IntelliJ IDEA button** toorestart hello IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="b628a-132">Creare un progetto Scala autonomo</span><span class="sxs-lookup"><span data-stu-id="b628a-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="b628a-133">Avviare IntelliJ IDEA e creare un nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="b628a-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="b628a-134">In hello dialogo Nuovo progetto, rendere hello opzioni seguenti e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b628a-134">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>
   
    ![Creare un progetto Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="b628a-136">Selezionare **Maven** come tipo di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="b628a-136">Select **Maven** as hello project type.</span></span>
   * <span data-ttu-id="b628a-137">Specificare un valore per **Project SDK**.</span><span class="sxs-lookup"><span data-stu-id="b628a-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="b628a-138">Fare clic su Nuovo e passare toohello directory di installazione Java, in genere `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="b628a-138">Click New and navigate toohello Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="b628a-139">Seleziona hello **Create dal sistema per** opzione.</span><span class="sxs-lookup"><span data-stu-id="b628a-139">Select hello **Create from archetype** option.</span></span>
   * <span data-ttu-id="b628a-140">Selezionare nell'elenco di archetipi hello **semplice sistema di rilevazione di tools.archetypes:scala org.scala**.</span><span class="sxs-lookup"><span data-stu-id="b628a-140">From hello list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="b628a-141">Verrà creata una struttura di directory destra hello e scaricare hello necessario predefinito dipendenze toowrite Scala programma.</span><span class="sxs-lookup"><span data-stu-id="b628a-141">This will create hello right directory structure and download hello required default dependencies toowrite Scala program.</span></span>
2. <span data-ttu-id="b628a-142">Specificare i valori pertinenti per **GroupId** (ID gruppo), **ArtifactId** (ID elemento) e **Version** (Versione).</span><span class="sxs-lookup"><span data-stu-id="b628a-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="b628a-143">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b628a-143">Click **Next**.</span></span>
3. <span data-ttu-id="b628a-144">In hello successiva finestra di dialogo in cui si specifica Maven home directory e altre impostazioni utente, accettare le impostazioni predefinite hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b628a-144">In hello next dialog box, where you specify Maven home directory and other user settings, accept hello defaults and click **Next**.</span></span>
4. <span data-ttu-id="b628a-145">In hello ultima finestra di dialogo, specificare un nome di progetto e il percorso e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="b628a-145">In hello last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="b628a-146">Eliminare hello **MySpec.Scala** file in **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="b628a-146">Delete hello **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="b628a-147">Non è necessario questo per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b628a-147">You do not need this for hello application.</span></span>
6. <span data-ttu-id="b628a-148">Se necessario, rinominare i file di origine e di test predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="b628a-148">If required, rename hello default source and test files.</span></span> <span data-ttu-id="b628a-149">Dal riquadro sinistro di hello in IntelliJ IDEA hello, passare troppo**src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="b628a-149">From hello left pane in hello IntelliJ IDEA, navigate too**src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="b628a-150">Fare doppio clic su **App.scala**, fare clic su **refactoring**, fare clic su Rinomina file, nella finestra di dialogo hello specificare hello nuovo nome per un'applicazione hello e quindi fare clic su **refactoring**.</span><span class="sxs-lookup"><span data-stu-id="b628a-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in hello dialog box, provide hello new name for hello application and then click **Refactor**.</span></span>
   
    ![Rinominare file](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="b628a-152">Nei passaggi successivi hello, si aggiornerà hello pom.xml toodefine hello le dipendenze per hello applicazione Spark Scala.</span><span class="sxs-lookup"><span data-stu-id="b628a-152">In hello subsequent steps, you will update hello pom.xml toodefine hello dependencies for hello Spark Scala application.</span></span> <span data-ttu-id="b628a-153">Per tali dipendenze toobe scaricato e risolti automaticamente, che è necessario configurare Maven di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="b628a-153">For those dependencies toobe downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Configurare Maven per i download automatici](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="b628a-155">Da hello **File** menu, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="b628a-155">From hello **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="b628a-156">In hello **impostazioni** finestra di dialogo passare troppo**distribuzione della compilazione, esecuzione,** > **gli strumenti di generazione** > **Maven**  >  **Importazione**.</span><span class="sxs-lookup"><span data-stu-id="b628a-156">In hello **Settings** dialog box, navigate too**Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="b628a-157">L'opzione hello troppo**automaticamente i progetti Maven importazione**.</span><span class="sxs-lookup"><span data-stu-id="b628a-157">Select hello option too**Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="b628a-158">Fare clic su **Apply** (Applica) e quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b628a-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="b628a-159">Aggiornare hello Scala origine file tooinclude il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b628a-159">Update hello Scala source file tooinclude your application code.</span></span> <span data-ttu-id="b628a-160">Aprire e sostituire hello esistente codice di esempio con hello seguente di codice e salvare le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="b628a-160">Open and replace hello existing sample code with hello following code and save hello changes.</span></span> <span data-ttu-id="b628a-161">Questo codice legge i dati di hello da hello HVAC.csv (disponibile in tutti i cluster HDInsight Spark), recupera righe hello solo con una cifra nella sesta colonna hello e scrive l'output di hello troppo**/HVACOut** in spazio di archiviazione predefinito hello contenitore per i cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="b628a-161">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello sixth column, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="b628a-162">Aggiornare pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="b628a-162">Update hello pom.xml.</span></span>
   
   1. <span data-ttu-id="b628a-163">All'interno di `<project>\<properties>` aggiungere hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b628a-163">Within `<project>\<properties>` add hello following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="b628a-164">All'interno di `<project>\<dependencies>` aggiungere hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b628a-164">Within `<project>\<dependencies>` add hello following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="b628a-165">Salvare le modifiche toopom.xml.</span><span class="sxs-lookup"><span data-stu-id="b628a-165">Save changes toopom.xml.</span></span>
10. <span data-ttu-id="b628a-166">Creare il file JAR hello.</span><span class="sxs-lookup"><span data-stu-id="b628a-166">Create hello .jar file.</span></span> <span data-ttu-id="b628a-167">IntelliJ IDEA consente di creare un file con estensione jar come elemento di un progetto.</span><span class="sxs-lookup"><span data-stu-id="b628a-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="b628a-168">Eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="b628a-168">Perform hello following steps.</span></span>
    
    1. <span data-ttu-id="b628a-169">Da hello **File** menu, fare clic su **struttura del progetto**.</span><span class="sxs-lookup"><span data-stu-id="b628a-169">From hello **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="b628a-170">In hello **struttura del progetto** la finestra di dialogo, fare clic su **elementi** e quindi fare clic su hello e simboli.</span><span class="sxs-lookup"><span data-stu-id="b628a-170">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="b628a-171">Nella finestra di dialogo popup hello, fare clic su **JAR**, quindi fare clic su **dai moduli con dipendenze**.</span><span class="sxs-lookup"><span data-stu-id="b628a-171">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="b628a-173">In hello **creare JAR dai moduli** finestra di dialogo, fare clic sui puntini di sospensione hello (![i puntini di sospensione](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) contro hello **classe Main**.</span><span class="sxs-lookup"><span data-stu-id="b628a-173">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against hello **Main Class**.</span></span>
    4. <span data-ttu-id="b628a-174">In hello **Seleziona classe Main** della finestra di dialogo classe hello select che viene visualizzato per impostazione predefinita e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b628a-174">In hello **Select Main Class** dialog box, select hello class that appears by default and then click **OK**.</span></span>
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="b628a-176">In hello **creare JAR dai moduli** finestra di dialogo, accertarsi che l'opzione hello troppo**estrarre toohello destinazione JAR** sia selezionata e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b628a-176">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="b628a-177">Verrà creato un singolo file con estensione jar con tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="b628a-177">This creates a single JAR with all dependencies.</span></span>
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="b628a-179">scheda layout di Hello output elenca tutti JAR hello che sono inclusi come parte del progetto di Maven hello.</span><span class="sxs-lookup"><span data-stu-id="b628a-179">hello output layout tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="b628a-180">È possibile selezionare e quelli in cui hello Scala applicazione hello di eliminazione non ha alcuna dipendenza diretta.</span><span class="sxs-lookup"><span data-stu-id="b628a-180">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="b628a-181">Per un'applicazione hello viene creata in questo caso, è possibile rimuovere tutto tranne hello ultimo (**output di compilazione SparkSimpleApp**).</span><span class="sxs-lookup"><span data-stu-id="b628a-181">For hello application we are creating here, you can remove all but hello last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="b628a-182">Selezionare toodelete JAR hello e quindi fare clic su hello **eliminare** icona.</span><span class="sxs-lookup"><span data-stu-id="b628a-182">Select hello jars toodelete and then click hello **Delete** icon.</span></span>
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="b628a-184">Assicurarsi che **compilare su verificare** casella è selezionata, che assicura che jar hello viene creato ogni volta che il progetto hello viene compilato o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="b628a-184">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="b628a-185">Fare clic su **Apply** (Applica) e quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b628a-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="b628a-186">Dalla barra dei menu hello, fare clic su **compilare**, quindi fare clic su **Crea progetto**.</span><span class="sxs-lookup"><span data-stu-id="b628a-186">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="b628a-187">È anche possibile fare clic su **artefatti di compilazione** jar hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b628a-187">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="b628a-188">Hello jar output viene creato in **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="b628a-188">hello output jar is created under **\out\artifacts**.</span></span>
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a><span data-ttu-id="b628a-190">Eseguire un'applicazione hello in cluster Spark hello</span><span class="sxs-lookup"><span data-stu-id="b628a-190">Run hello application on hello Spark cluster</span></span>
<span data-ttu-id="b628a-191">un'applicazione hello toorun nel cluster hello, è necessario eseguire il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b628a-191">toorun hello application on hello cluster, you must do hello following:</span></span>

* <span data-ttu-id="b628a-192">**Il blob di archiviazione Azure toohello copia hello applicazione jar** associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="b628a-192">**Copy hello application jar toohello Azure storage blob** associated with hello cluster.</span></span> <span data-ttu-id="b628a-193">È possibile utilizzare [ **AzCopy**](../storage/common/storage-use-azcopy.md), della riga di comando utilità, toodo così.</span><span class="sxs-lookup"><span data-stu-id="b628a-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="b628a-194">Esistono molti degli altri client anche che è possibile utilizzare dati tooupload.</span><span class="sxs-lookup"><span data-stu-id="b628a-194">There are a lot of other clients as well that you can use tooupload data.</span></span> <span data-ttu-id="b628a-195">Altre informazioni in merito sono disponibili in [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="b628a-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="b628a-196">**Utilizzare toosubmit inserire il processo di un'applicazione in modalità remota** cluster Spark toohello.</span><span class="sxs-lookup"><span data-stu-id="b628a-196">**Use Livy toosubmit an application job remotely** toohello Spark cluster.</span></span> <span data-ttu-id="b628a-197">Il cluster Spark in HDInsight include inserire il che espone REST endpoint tooremotely invia i processi di Spark.</span><span class="sxs-lookup"><span data-stu-id="b628a-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints tooremotely submit Spark jobs.</span></span> <span data-ttu-id="b628a-198">Per ulteriori informazioni, vedere [Inviare processi Spark in modalità remota utilizzando Livy con cluster Spark in HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="b628a-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="b628a-199">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="b628a-199">Next step</span></span>

<span data-ttu-id="b628a-200">In questo articolo si è appreso come toocreate un'applicazione di scala di Spark.</span><span class="sxs-lookup"><span data-stu-id="b628a-200">In this article you learned how toocreate a Spark scala application.</span></span> <span data-ttu-id="b628a-201">Avanzamento toohello Avanti articolo toolearn come toorun questa applicazione su un HDInsight Spark cluster utilizzando inserire il.</span><span class="sxs-lookup"><span data-stu-id="b628a-201">Advance toohello next article toolearn how toorun this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="b628a-202">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="b628a-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

