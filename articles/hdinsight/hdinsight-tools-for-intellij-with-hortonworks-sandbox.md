---
title: Usare Azure Toolkit for IntelliJ con Hortonworks Sandbox | Microsoft Docs
description: Informazioni su come usare gli strumenti HDInsight in Azure Toolkit for IntelliJ con Hortonworks Sandbox.
keywords: strumenti hadoop,query hive,intellij,hortonworks sandbox,azure toolkit for intellij
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c49f185db5a035f70a711bf309b973182d94a2b0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="16c2b-104">Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="16c2b-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="16c2b-105">Questo articolo illustra come usare gli strumenti HDInsight per IntelliJ per sviluppare applicazioni Apache Scala e quindi testarle in [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) in esecuzione sulla workstation.</span><span class="sxs-lookup"><span data-stu-id="16c2b-105">Learn how to use HDInsight Tools for IntelliJ to develop Apache Scala applications and then test the applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="16c2b-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) è un ambiente di sviluppo integrato (IDE) Java per lo sviluppo di software per computer.</span><span class="sxs-lookup"><span data-stu-id="16c2b-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="16c2b-107">Dopo aver sviluppato e testato le applicazioni in Hortonworks Sandbox, è possibile trasferirle in [Azure HDInsight](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="16c2b-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them to [Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16c2b-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="16c2b-108">Prerequisites</span></span>

<span data-ttu-id="16c2b-109">Prima di iniziare questa esercitazione, è necessario avere:</span><span class="sxs-lookup"><span data-stu-id="16c2b-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="16c2b-110">Hortonworks Data Platform (HDP) 2.4 in Hortonworks Sandbox in esecuzione nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="16c2b-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="16c2b-111">Per configurare HDP, vedere l'[introduzione all'ecosistema Hadoop con un ambiente sandbox Hadoop in una macchina virtuale](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="16c2b-111">To configure HDP, see [Get started in the Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="16c2b-112">Gli strumenti HDInsight per IntelliJ sono stati testati solo con HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="16c2b-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="16c2b-113">Per ottenere HDP 2.4, espandere [Archivio Hortonworks Sandbox](http://hortonworks.com/downloads/#sandbox) nel **sito di download di Hortonworks Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="16c2b-113">To get HDP 2.4, expand **Hortonworks Sandbox Archive** on the [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="16c2b-114">[Java Developer Kit (JDK) versione 1.8 o successiva](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="16c2b-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="16c2b-115">JDK è richiesto da Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="16c2b-115">JDK is required by the Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="16c2b-116">[IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/download) con i plug-in [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) e [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md).</span><span class="sxs-lookup"><span data-stu-id="16c2b-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with the [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and the [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="16c2b-117">Gli strumenti HDInsight per IntelliJ sono disponibili nell'ambito di Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="16c2b-117">HDInsight Tools for IntelliJ is available as a part of the Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="16c2b-118">Per installare i plug-in, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16c2b-118">To install the plug-ins, do the following:</span></span>

  1. <span data-ttu-id="16c2b-119">Aprire IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="16c2b-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="16c2b-120">Nella **schermata iniziale** selezionare **Configure** (Configura) e quindi **Plugins** (Plug-in).</span><span class="sxs-lookup"><span data-stu-id="16c2b-120">On the **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="16c2b-121">Selezionare **Install JetBrains plugin** (Installa plug-in JetBrains) nell'angolo inferiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="16c2b-121">Select **Install JetBrains plugin** in the lower-left corner.</span></span>
  4. <span data-ttu-id="16c2b-122">Usare la funzione di ricerca per cercare **Scala** e quindi selezionare **Install** (Installa).</span><span class="sxs-lookup"><span data-stu-id="16c2b-122">Use the search function to search for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="16c2b-123">Selezionare **Restart IntelliJ IDEA** (Riavvia IntelliJ IDEA) per completare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="16c2b-123">Select **Restart IntelliJ IDEA** to complete the installation.</span></span>
  6. <span data-ttu-id="16c2b-124">Ripetere i passaggi 4 e 5 per installare **Azure Toolkit for IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="16c2b-124">Repeat step 4 and 5 to install the **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="16c2b-125">Per altre informazioni, vedere [Installare Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="16c2b-125">For more information, see [Install the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="16c2b-126">Creare un'applicazione Spark Scala</span><span class="sxs-lookup"><span data-stu-id="16c2b-126">Create a Spark Scala application</span></span>

<span data-ttu-id="16c2b-127">In questa sezione verrà creato un progetto Scala di esempio usando IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="16c2b-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="16c2b-128">Nella sezione successiva, IntelliJ IDEA verrà collegato a Hortonworks Sandbox (emulatore) prima di inviare il progetto.</span><span class="sxs-lookup"><span data-stu-id="16c2b-128">In the next section, you link IntelliJ IDEA to the Hortonworks Sandbox (emulator) before you submit the project.</span></span>

1. <span data-ttu-id="16c2b-129">Aprire IntelliJ IDEA dalla workstation.</span><span class="sxs-lookup"><span data-stu-id="16c2b-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="16c2b-130">Nella finestra di dialogo **New Project** (Nuovo progetto) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16c2b-130">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="16c2b-131">a.</span><span class="sxs-lookup"><span data-stu-id="16c2b-131">a.</span></span> <span data-ttu-id="16c2b-132">Selezionare **HDInsight** > **Spark on HDInsight (Scala)** (Spark in HDInsight - Scala).</span><span class="sxs-lookup"><span data-stu-id="16c2b-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="16c2b-133">b.</span><span class="sxs-lookup"><span data-stu-id="16c2b-133">b.</span></span> <span data-ttu-id="16c2b-134">Nell'elenco **Build tool** (Strumento di compilazione) selezionare uno degli strumenti seguenti, in base alla necessità:</span><span class="sxs-lookup"><span data-stu-id="16c2b-134">In the **Build tool** list, select either of the following, according to your need:</span></span>

    * <span data-ttu-id="16c2b-135">**Maven**, per ottenere supporto per la creazione guidata di un progetto Scala</span><span class="sxs-lookup"><span data-stu-id="16c2b-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="16c2b-136">**SBT**, per la gestione delle dipendenze e la compilazione per il progetto Scala</span><span class="sxs-lookup"><span data-stu-id="16c2b-136">**SBT**, for managing the dependencies and building for the Scala project</span></span>

   ![Finestra di dialogo del nuovo progetto](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="16c2b-138">Selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16c2b-138">Select **Next**.</span></span>

3. <span data-ttu-id="16c2b-139">Nella finestra di dialogo **New Project** (Nuovo progetto) successiva seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16c2b-139">In the next **New Project** dialog box, do the following:</span></span>

    ![Proprietà della creazione del progetto IntelliJ Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="16c2b-141">a.</span><span class="sxs-lookup"><span data-stu-id="16c2b-141">a.</span></span> <span data-ttu-id="16c2b-142">Nella casella **Project name** (Nome progetto) immettere un nome per il progetto.</span><span class="sxs-lookup"><span data-stu-id="16c2b-142">In the **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="16c2b-143">b.</span><span class="sxs-lookup"><span data-stu-id="16c2b-143">b.</span></span> <span data-ttu-id="16c2b-144">Nella casella **Project location** (Percorso progetto) immettere un percorso per il progetto.</span><span class="sxs-lookup"><span data-stu-id="16c2b-144">In the **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="16c2b-145">c.</span><span class="sxs-lookup"><span data-stu-id="16c2b-145">c.</span></span> <span data-ttu-id="16c2b-146">Accanto all'elenco a discesa **Project SDK** (SDK progetto) selezionare **New** (Nuovo) e quindi **JDK** e infine specificare la cartella di Java JDK versione 1.7 o successiva.</span><span class="sxs-lookup"><span data-stu-id="16c2b-146">Next to the **Project SDK** drop-down list, select **New**, select **JDK**, and then specify the folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="16c2b-147">Selezionare **Java 1.8** per il cluster Spark 2.x oppure **Java 1.7** per il cluster Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="16c2b-147">Select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span> <span data-ttu-id="16c2b-148">Il percorso predefinito è C:\Programmi\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="16c2b-148">The default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="16c2b-149">d.</span><span class="sxs-lookup"><span data-stu-id="16c2b-149">d.</span></span> <span data-ttu-id="16c2b-150">Nell'elenco a discesa **Spark version** (Versione di Spark) la creazione guidata del progetto Scala inserisce la versione corretta per Spark SDK e Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="16c2b-150">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="16c2b-151">Se la versione del cluster Spark è precedente alla 2.0, selezionare **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="16c2b-151">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="16c2b-152">In caso contrario, selezionare **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="16c2b-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="16c2b-153">In questo esempio viene usata la versione Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="16c2b-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="16c2b-154">Assicurarsi di usare il repository contrassegnato come Scala 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="16c2b-154">Make sure that you are using the repository marked Scala 2.10.x.</span></span> <span data-ttu-id="16c2b-155">Non usare il repository contrassegnato come Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="16c2b-155">Do not use the repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="16c2b-156">Selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="16c2b-156">Select **Finish**.</span></span>

5. <span data-ttu-id="16c2b-157">Se la visualizzazione **Project** (Progetto) non è già aperta, premere **ALT+1** per aprirla.</span><span class="sxs-lookup"><span data-stu-id="16c2b-157">If the **Project** view is not already open, press **Alt+1** to open it.</span></span>

6. <span data-ttu-id="16c2b-158">In **Project Explorer** (Esplora progetti) espandere il progetto e quindi selezionare **src**.</span><span class="sxs-lookup"><span data-stu-id="16c2b-158">In **Project Explorer**, expand the project, and then select **src**.</span></span>

7. <span data-ttu-id="16c2b-159">Fare clic con il pulsante destro del mouse su **src**, scegliere **New** (Nuovo) e quindi fare clic su **Scala class** (Classe Scala).</span><span class="sxs-lookup"><span data-stu-id="16c2b-159">Right-click **src**, point to **New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="16c2b-160">Immettere un nome nella casella **Name** (Nome), selezionare **Object**, (Oggetto) nella casella **Kind** (Tipologia) e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="16c2b-160">In the **Name** box, enter a name, in the **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![Finestra di dialogo Create New Scala Class (Crea nuova classe Scala)](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="16c2b-162">Incollare il codice seguente nel file con estensione scala:</span><span class="sxs-lookup"><span data-stu-id="16c2b-162">In the .scala file, paste the following code:</span></span>

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. <span data-ttu-id="16c2b-163">Dal menu **Build** (Compila) scegliere **Build project** (Compila progetto).</span><span class="sxs-lookup"><span data-stu-id="16c2b-163">On the **Build** menu, select **Build project**.</span></span> <span data-ttu-id="16c2b-164">Verificare che la compilazione sia stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="16c2b-164">Make sure that the compilation has been completed successfully.</span></span>


## <a name="link-to-the-hortonworks-sandbox"></a><span data-ttu-id="16c2b-165">Eseguire il collegamento a Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="16c2b-165">Link to the Hortonworks Sandbox</span></span>

<span data-ttu-id="16c2b-166">Per poter eseguire il collegamento a Hortonworks Sandbox (emulatore), deve essere presente un'applicazione IntelliJ esistente.</span><span class="sxs-lookup"><span data-stu-id="16c2b-166">Before you can link to a Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="16c2b-167">Per il collegamento a un emulatore, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16c2b-167">To link to an emulator, do the following:</span></span>

1. <span data-ttu-id="16c2b-168">Aprire il progetto in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="16c2b-168">Open the project in IntelliJ.</span></span>

2. <span data-ttu-id="16c2b-169">Dal menu **View** (Visualizza) scegliere **Tool Windows** (Finestre degli strumenti) e quindi selezionare **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="16c2b-169">On the **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="16c2b-170">Espandere **Azure**, fare clic con il pulsante destro del mouse su **HDInsight** e quindi scegliere **Link an Emulator** (Collega un emulatore).</span><span class="sxs-lookup"><span data-stu-id="16c2b-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="16c2b-171">Nella finestra **Link A New Emulator** (Collega nuovo emulatore) immettere la password configurata per l'account radice di Hortonworks Sandbox e valori simili a quelli riportati nello screenshot seguente e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="16c2b-171">In the **Link A New Emulator** window, enter the password that you've configured for the root account of the Hortonworks Sandbox, enter values similar to those in the following screenshot, and then select **OK**.</span></span> 

   ![Finestra "Link a New Emulator" (Collega nuovo emulatore)](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="16c2b-173">Per configurare l'emulatore, selezionare **Yes** (Sì).</span><span class="sxs-lookup"><span data-stu-id="16c2b-173">To configure the emulator, select **Yes**.</span></span>

<span data-ttu-id="16c2b-174">Quando è connesso correttamente, l'emulatore (Hortonworks Sandbox) viene elencato nel nodo HDInsight.</span><span class="sxs-lookup"><span data-stu-id="16c2b-174">When the emulator is connected successfully, the emulator (Hortonworks Sandbox) is listed in the HDInsight node.</span></span>

## <a name="submit-the-spark-scala-application-to-the-hortonworks-sandbox"></a><span data-ttu-id="16c2b-175">Inviare l'applicazione Spark Scala a Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="16c2b-175">Submit the Spark Scala application to the Hortonworks Sandbox</span></span>

<span data-ttu-id="16c2b-176">Dopo aver collegato IntelliJ IDEA all'emulatore è possibile inviare il progetto.</span><span class="sxs-lookup"><span data-stu-id="16c2b-176">After you have linked IntelliJ IDEA to the emulator, you can submit your project.</span></span>

<span data-ttu-id="16c2b-177">Per inviare un progetto a un emulatore, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16c2b-177">To submit a project to an emulator, do the following:</span></span>

1. <span data-ttu-id="16c2b-178">In **Project Explorer** (Esplora progetti) fare clic con il pulsante destro del mouse sul progetto e quindi scegliere **Submit Spark Application to HDInsight** (Invia applicazione Spark a HDInsight).</span><span class="sxs-lookup"><span data-stu-id="16c2b-178">In **Project Explorer**, right-click the project, and then select **Submit Spark application to HDInsight**.</span></span>

2. <span data-ttu-id="16c2b-179">Eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="16c2b-179">Do the following:</span></span>

    <span data-ttu-id="16c2b-180">a.</span><span class="sxs-lookup"><span data-stu-id="16c2b-180">a.</span></span> <span data-ttu-id="16c2b-181">Nell'elenco a discesa **Spark cluster (Linux only)** (Cluster Spark - solo Linux) selezionare l'ambiente Hortonworks Sandbox locale.</span><span class="sxs-lookup"><span data-stu-id="16c2b-181">In the **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="16c2b-182">b.</span><span class="sxs-lookup"><span data-stu-id="16c2b-182">b.</span></span> <span data-ttu-id="16c2b-183">Nella casella **Main class name** (Nome classe principale) scegliere o immettere il nome della classe principale.</span><span class="sxs-lookup"><span data-stu-id="16c2b-183">In the **Main class name** box, choose or enter the main class name.</span></span> <span data-ttu-id="16c2b-184">Per questa esercitazione, il nome è **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="16c2b-184">For this tutorial, the name is **GroupByTest**.</span></span>

3. <span data-ttu-id="16c2b-185">Selezionare **Submit** (Invia).</span><span class="sxs-lookup"><span data-stu-id="16c2b-185">Select **Submit**.</span></span> <span data-ttu-id="16c2b-186">I log di invio dei processi vengono visualizzati nella finestra degli strumenti di invio Spark.</span><span class="sxs-lookup"><span data-stu-id="16c2b-186">The job submission logs are shown in the Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16c2b-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16c2b-187">Next steps</span></span>

- <span data-ttu-id="16c2b-188">Per informazioni su come creare applicazioni Spark per HDInsight con gli strumenti HDInsight per IntelliJ, vedere l'articolo su come [usare gli strumenti HDInsight in Azure Toolkit for IntelliJ per creare applicazioni Spark per un cluster HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="16c2b-188">To learn how to create Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="16c2b-189">Per un video sugli strumenti HDInsight per IntelliJ, vedere l'[introduzione agli strumenti HDInsight per IntelliJ per lo sviluppo Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).</span><span class="sxs-lookup"><span data-stu-id="16c2b-189">To watch a video of HDInsight Tools for IntelliJ, go to [Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="16c2b-190">Per informazioni su come eseguire il debug di applicazioni Spark usando il toolkit in remoto in HDInsight tramite SSH, vedere [Eseguire il debug remoto delle applicazioni Spark su un cluster HDInsight con Azure Toolkit per IntelliJ tramite SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="16c2b-190">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through SSH, go to [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="16c2b-191">Per informazioni su come eseguire il debug di applicazioni Spark usando il toolkit in remoto in HDInsight tramite VPN, vedere [Usare gli strumenti HDInsight in Azure Toolkit for IntelliJ per eseguire il debug di applicazioni Spark in remoto in cluster HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="16c2b-191">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through VPN, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="16c2b-192">Per informazioni su come usare gli strumenti HDInsight per Eclipse per creare un'applicazione Spark, vedere l'articolo su come [usare gli strumenti HDInsight in Azure Toolkit for Eclipse per creare applicazioni Spark](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="16c2b-192">To learn how to use HDInsight Tools for Eclipse to create a Spark application, go to [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="16c2b-193">Per un video sugli strumenti HDInsight per Eclipse, vedere [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha) (Usare lo strumento HDInsight per Eclipse per creare applicazioni Spark).</span><span class="sxs-lookup"><span data-stu-id="16c2b-193">To watch a video of HDInsight Tools for Eclipse, go to [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
