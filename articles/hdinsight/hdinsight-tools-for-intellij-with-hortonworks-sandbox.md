---
title: Azure Toolkit per IntelliJ con Hortonworks Sandbox aaaUse | Documenti Microsoft
description: Informazioni su come gli strumenti HDInsight toouse in Azure Toolkit per IntelliJ con Hortonworks Sandbox.
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
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="25d17-104">Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="25d17-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="25d17-105">Informazioni su come gli strumenti di HDInsight toouse per applicazioni di Scala Apache toodevelop IntelliJ e quindi testare hello applicazioni su [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) esecuzione sulla workstation.</span><span class="sxs-lookup"><span data-stu-id="25d17-105">Learn how toouse HDInsight Tools for IntelliJ toodevelop Apache Scala applications and then test hello applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="25d17-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) è un ambiente di sviluppo integrato (IDE) Java per lo sviluppo di software per computer.</span><span class="sxs-lookup"><span data-stu-id="25d17-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="25d17-107">Dopo aver sviluppato e testare le applicazioni in Hortonworks Sandbox, è possibile spostarli troppo[Azure HDInsight](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="25d17-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them too[Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25d17-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="25d17-108">Prerequisites</span></span>

<span data-ttu-id="25d17-109">Prima di iniziare questa esercitazione, è necessario avere:</span><span class="sxs-lookup"><span data-stu-id="25d17-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="25d17-110">Hortonworks Data Platform (HDP) 2.4 in Hortonworks Sandbox in esecuzione nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="25d17-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="25d17-111">vedere tooconfigure HDP, [iniziare nell'ecosistema Hadoop hello con una sandbox di Hadoop in una macchina virtuale](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="25d17-111">tooconfigure HDP, see [Get started in hello Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="25d17-112">Gli strumenti HDInsight per IntelliJ sono stati testati solo con HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="25d17-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="25d17-113">Espandere tooget 2.4 HDP, **Hortonworks Sandbox archivio** su hello [Hortonworks Sandbox Scarica sito](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="25d17-113">tooget HDP 2.4, expand **Hortonworks Sandbox Archive** on hello [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="25d17-114">[Java Developer Kit (JDK) versione 1.8 o successiva](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="25d17-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="25d17-115">È necessario JDK hello Azure Toolkit per IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="25d17-115">JDK is required by hello Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="25d17-116">[Edizione community IDEA IntelliJ](https://www.jetbrains.com/idea/download) con hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in e hello [Azure Toolkit per IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span><span class="sxs-lookup"><span data-stu-id="25d17-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and hello [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="25d17-117">Strumenti HDInsight per IntelliJ è disponibili come parte di Azure Toolkit per IntelliJ hello.</span><span class="sxs-lookup"><span data-stu-id="25d17-117">HDInsight Tools for IntelliJ is available as a part of hello Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="25d17-118">tooinstall hello plug-in, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="25d17-118">tooinstall hello plug-ins, do hello following:</span></span>

  1. <span data-ttu-id="25d17-119">Aprire IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="25d17-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="25d17-120">In hello **iniziale** selezionare **configura**, quindi selezionare **plug-in**.</span><span class="sxs-lookup"><span data-stu-id="25d17-120">On hello **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="25d17-121">Selezionare **plug-in installa JetBrains** nell'angolo inferiore sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="25d17-121">Select **Install JetBrains plugin** in hello lower-left corner.</span></span>
  4. <span data-ttu-id="25d17-122">Utilizzare hello ricerca funzione toosearch per **Scala**, quindi selezionare **installare**.</span><span class="sxs-lookup"><span data-stu-id="25d17-122">Use hello search function toosearch for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="25d17-123">Selezionare **riavviare IDEA IntelliJ** installazione hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="25d17-123">Select **Restart IntelliJ IDEA** toocomplete hello installation.</span></span>
  6. <span data-ttu-id="25d17-124">Hello tooinstall ripetere il passaggio 4 e 5 **Azure Toolkit per IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="25d17-124">Repeat step 4 and 5 tooinstall hello **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="25d17-125">Per ulteriori informazioni, vedere [hello installare Azure Toolkit per IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="25d17-125">For more information, see [Install hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="25d17-126">Creare un'applicazione Spark Scala</span><span class="sxs-lookup"><span data-stu-id="25d17-126">Create a Spark Scala application</span></span>

<span data-ttu-id="25d17-127">In questa sezione verrà creato un progetto Scala di esempio usando IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="25d17-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="25d17-128">Nella sezione successiva hello, collegare IDEA IntelliJ toohello Hortonworks Sandbox (emulatore) prima di inviare il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="25d17-128">In hello next section, you link IntelliJ IDEA toohello Hortonworks Sandbox (emulator) before you submit hello project.</span></span>

1. <span data-ttu-id="25d17-129">Aprire IntelliJ IDEA dalla workstation.</span><span class="sxs-lookup"><span data-stu-id="25d17-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="25d17-130">In hello **nuovo progetto** finestra di dialogo casella, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="25d17-130">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="25d17-131">a.</span><span class="sxs-lookup"><span data-stu-id="25d17-131">a.</span></span> <span data-ttu-id="25d17-132">Selezionare **HDInsight** > **Spark on HDInsight (Scala)** (Spark in HDInsight - Scala).</span><span class="sxs-lookup"><span data-stu-id="25d17-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="25d17-133">b.</span><span class="sxs-lookup"><span data-stu-id="25d17-133">b.</span></span> <span data-ttu-id="25d17-134">In hello **strumento di compilazione** selezionare uno dei hello seguenti, in base tooyour necessità:</span><span class="sxs-lookup"><span data-stu-id="25d17-134">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

    * <span data-ttu-id="25d17-135">**Maven**, per ottenere supporto per la creazione guidata di un progetto Scala</span><span class="sxs-lookup"><span data-stu-id="25d17-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="25d17-136">**SBT**, per la gestione delle dipendenze hello e la compilazione per il progetto di Scala hello</span><span class="sxs-lookup"><span data-stu-id="25d17-136">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

   ![finestra di dialogo Nuovo progetto Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="25d17-138">Selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="25d17-138">Select **Next**.</span></span>

3. <span data-ttu-id="25d17-139">In hello Avanti **nuovo progetto** finestra di dialogo casella, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="25d17-139">In hello next **New Project** dialog box, do hello following:</span></span>

    ![Proprietà della creazione del progetto IntelliJ Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="25d17-141">a.</span><span class="sxs-lookup"><span data-stu-id="25d17-141">a.</span></span> <span data-ttu-id="25d17-142">In hello **nome progetto** , immettere un nome di progetto.</span><span class="sxs-lookup"><span data-stu-id="25d17-142">In hello **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="25d17-143">b.</span><span class="sxs-lookup"><span data-stu-id="25d17-143">b.</span></span> <span data-ttu-id="25d17-144">In hello **percorso progetto** , immettere un percorso del progetto.</span><span class="sxs-lookup"><span data-stu-id="25d17-144">In hello **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="25d17-145">c.</span><span class="sxs-lookup"><span data-stu-id="25d17-145">c.</span></span> <span data-ttu-id="25d17-146">Avanti toohello **Project SDK** elenco a discesa, seleziona **New**selezionare **JDK**, e quindi specificare la cartella hello di Java JDK versione 1.7 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="25d17-146">Next toohello **Project SDK** drop-down list, select **New**, select **JDK**, and then specify hello folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="25d17-147">Selezionare **Java 1.8** per cluster 2. x di Spark hello o selezionare **Java 1.7** per cluster 1. x di hello Spark.</span><span class="sxs-lookup"><span data-stu-id="25d17-147">Select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span> <span data-ttu-id="25d17-148">percorso predefinito di Hello è c:\Programmi\Microsoft Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="25d17-148">hello default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="25d17-149">d.</span><span class="sxs-lookup"><span data-stu-id="25d17-149">d.</span></span> <span data-ttu-id="25d17-150">In hello **versione Spark** elenco a discesa, creazione guidata nuovo progetto di Scala si integra la versione corretta di hello per SDK Spark e SDK di Scala.</span><span class="sxs-lookup"><span data-stu-id="25d17-150">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="25d17-151">Se la versione del cluster Spark hello è precedente alla versione 2.0, selezionare **nascita 1. x**.</span><span class="sxs-lookup"><span data-stu-id="25d17-151">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="25d17-152">In caso contrario, selezionare **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="25d17-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="25d17-153">In questo esempio viene usata la versione Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="25d17-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="25d17-154">Assicurarsi che si sta utilizzando repository hello contrassegnato Scala 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="25d17-154">Make sure that you are using hello repository marked Scala 2.10.x.</span></span> <span data-ttu-id="25d17-155">Non utilizzare repository hello contrassegnato Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="25d17-155">Do not use hello repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="25d17-156">Selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="25d17-156">Select **Finish**.</span></span>

5. <span data-ttu-id="25d17-157">Se hello **progetto** visualizzazione non è già aperta, premere **Alt + 1** tooopen è.</span><span class="sxs-lookup"><span data-stu-id="25d17-157">If hello **Project** view is not already open, press **Alt+1** tooopen it.</span></span>

6. <span data-ttu-id="25d17-158">In **Esplora progetti**, espandere il progetto hello e quindi selezionare **src**.</span><span class="sxs-lookup"><span data-stu-id="25d17-158">In **Project Explorer**, expand hello project, and then select **src**.</span></span>

7. <span data-ttu-id="25d17-159">Fare doppio clic su **src**, punto troppo**New**, quindi selezionare **Scala classe**.</span><span class="sxs-lookup"><span data-stu-id="25d17-159">Right-click **src**, point too**New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="25d17-160">In hello **nome** , immettere un nome, in hello **tipo** , quindi selezionare **oggetto**, quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="25d17-160">In hello **Name** box, enter a name, in hello **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![finestra Crea nuova classe Scala Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="25d17-162">Nel file .scala hello incollare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="25d17-162">In hello .scala file, paste hello following code:</span></span>

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

10. <span data-ttu-id="25d17-163">In hello **compilare** dal menu **compilazione progetto**.</span><span class="sxs-lookup"><span data-stu-id="25d17-163">On hello **Build** menu, select **Build project**.</span></span> <span data-ttu-id="25d17-164">Assicurarsi che la compilazione di hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="25d17-164">Make sure that hello compilation has been completed successfully.</span></span>


## <a name="link-toohello-hortonworks-sandbox"></a><span data-ttu-id="25d17-165">Collegamento toohello Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="25d17-165">Link toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="25d17-166">Prima di poter collegare tooa Hortonworks Sandbox (emulatore), è necessario disporre di un'applicazione IntelliJ esistente.</span><span class="sxs-lookup"><span data-stu-id="25d17-166">Before you can link tooa Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="25d17-167">emulatore tooan toolink, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="25d17-167">toolink tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="25d17-168">Progetto aperto hello in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="25d17-168">Open hello project in IntelliJ.</span></span>

2. <span data-ttu-id="25d17-169">In hello **vista** dal menu **strumenti di Windows**, quindi selezionare **Esplora Azure**.</span><span class="sxs-lookup"><span data-stu-id="25d17-169">On hello **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="25d17-170">Espandere **Azure**, fare clic con il pulsante destro del mouse su **HDInsight** e quindi scegliere **Link an Emulator** (Collega un emulatore).</span><span class="sxs-lookup"><span data-stu-id="25d17-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="25d17-171">In hello **collegamento A nuovo emulatore** finestra, immettere la password di hello configurati per l'account radice hello di hello Hortonworks Sandbox, immettere valori simili toothose nella seguente schermata hello e quindi selezionare **OK **.</span><span class="sxs-lookup"><span data-stu-id="25d17-171">In hello **Link A New Emulator** window, enter hello password that you've configured for hello root account of hello Hortonworks Sandbox, enter values similar toothose in hello following screenshot, and then select **OK**.</span></span> 

   ![finestra di "Collegamento a nuovo emulatore" Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="25d17-173">emulatore di hello tooconfigure, seleziona **Sì**.</span><span class="sxs-lookup"><span data-stu-id="25d17-173">tooconfigure hello emulator, select **Yes**.</span></span>

<span data-ttu-id="25d17-174">Quando l'emulatore hello è connesso correttamente, emulatore hello (Hortonworks Sandbox) viene elencata nel nodo HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="25d17-174">When hello emulator is connected successfully, hello emulator (Hortonworks Sandbox) is listed in hello HDInsight node.</span></span>

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a><span data-ttu-id="25d17-175">Inviare hello Spark Scala applicazione toohello Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="25d17-175">Submit hello Spark Scala application toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="25d17-176">Dopo aver collegato emulatore toohello IntelliJ IDEA, è possibile inviare il progetto.</span><span class="sxs-lookup"><span data-stu-id="25d17-176">After you have linked IntelliJ IDEA toohello emulator, you can submit your project.</span></span>

<span data-ttu-id="25d17-177">hello toosubmit un emulatore, tooan progetto seguente:</span><span class="sxs-lookup"><span data-stu-id="25d17-177">toosubmit a project tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="25d17-178">In **Esplora progetti**, fare clic sul progetto hello e quindi selezionare **Spark inviare applicazione tooHDInsight**.</span><span class="sxs-lookup"><span data-stu-id="25d17-178">In **Project Explorer**, right-click hello project, and then select **Submit Spark application tooHDInsight**.</span></span>

2. <span data-ttu-id="25d17-179">Hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="25d17-179">Do hello following:</span></span>

    <span data-ttu-id="25d17-180">a.</span><span class="sxs-lookup"><span data-stu-id="25d17-180">a.</span></span> <span data-ttu-id="25d17-181">In hello **cluster Spark (solo Linux)** elenco a discesa selezionare il Hortonworks Sandbox locale.</span><span class="sxs-lookup"><span data-stu-id="25d17-181">In hello **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="25d17-182">b.</span><span class="sxs-lookup"><span data-stu-id="25d17-182">b.</span></span> <span data-ttu-id="25d17-183">In hello **nome della classe principale** scegliere o immettere il nome di classe principale hello.</span><span class="sxs-lookup"><span data-stu-id="25d17-183">In hello **Main class name** box, choose or enter hello main class name.</span></span> <span data-ttu-id="25d17-184">Per questa esercitazione, è il nome di hello **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="25d17-184">For this tutorial, hello name is **GroupByTest**.</span></span>

3. <span data-ttu-id="25d17-185">Selezionare **Submit** (Invia).</span><span class="sxs-lookup"><span data-stu-id="25d17-185">Select **Submit**.</span></span> <span data-ttu-id="25d17-186">i log di invio processi Hello vengono visualizzati nella finestra degli strumenti di invio Spark hello.</span><span class="sxs-lookup"><span data-stu-id="25d17-186">hello job submission logs are shown in hello Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25d17-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25d17-187">Next steps</span></span>

- <span data-ttu-id="25d17-188">come le applicazioni toocreate Spark per HDInsight utilizzando gli strumenti HDInsight per IntelliJ, andare troppo toolearn[utilizza gli strumenti di HDInsight in Azure Toolkit per le applicazioni per il cluster HDInsight Spark Linux Spark toocreate IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="25d17-188">toolearn how toocreate Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="25d17-189">toowatch un video di strumenti HDInsight per IntelliJ, andare troppo[introdurre strumenti HDInsight per IntelliJ per lo sviluppo di Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).</span><span class="sxs-lookup"><span data-stu-id="25d17-189">toowatch a video of HDInsight Tools for IntelliJ, go too[Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="25d17-190">toolearn come applicazioni di Spark toodebug utilizzando hello toolkit in modalità remota in HDInsight tramite SSH, andare troppo[in remoto il debug di applicazioni di Spark in un cluster di HDInsight con Azure Toolkit per IntelliJ tramite SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="25d17-190">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through SSH, go too[Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="25d17-191">toolearn come applicazioni di Spark toodebug utilizzando hello toolkit in modalità remota in HDInsight tramite una VPN, andare troppo[utilizza gli strumenti di HDInsight in Azure Toolkit per le applicazioni in modalità remota in HDInsight Spark Linux cluster Spark toodebug IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="25d17-191">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through VPN, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="25d17-192">toolearn come toouse strumenti HDInsight per Eclipse toocreate un'applicazione di Spark, andare troppo[utilizza gli strumenti di HDInsight in Azure Toolkit per le applicazioni di Spark toocreate Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="25d17-192">toolearn how toouse HDInsight Tools for Eclipse toocreate a Spark application, go too[Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="25d17-193">toowatch un video di strumenti di HDInsight per Eclipse, andare troppo[utilizzare lo strumento di HDInsight per le applicazioni di Spark toocreate Eclipse](https://mix.office.com/watch/1rau2mopb6fha).</span><span class="sxs-lookup"><span data-stu-id="25d17-193">toowatch a video of HDInsight Tools for Eclipse, go too[Use HDInsight Tool for Eclipse toocreate Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
