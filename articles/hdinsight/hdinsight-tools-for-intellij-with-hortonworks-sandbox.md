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
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a>Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox

Informazioni su come gli strumenti di HDInsight toouse per applicazioni di Scala Apache toodevelop IntelliJ e quindi testare hello applicazioni su [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) esecuzione sulla workstation. 

[IntelliJ IDEA](https://www.jetbrains.com/idea/) è un ambiente di sviluppo integrato (IDE) Java per lo sviluppo di software per computer. Dopo aver sviluppato e testare le applicazioni in Hortonworks Sandbox, è possibile spostarli troppo[Azure HDInsight](hdinsight-hadoop-introduction.md).

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questa esercitazione, è necessario avere:

- Hortonworks Data Platform (HDP) 2.4 in Hortonworks Sandbox in esecuzione nell'ambiente locale. vedere tooconfigure HDP, [iniziare nell'ecosistema Hadoop hello con una sandbox di Hadoop in una macchina virtuale](hdinsight-hadoop-emulator-get-started.md). 
    >[!NOTE]
    >Gli strumenti HDInsight per IntelliJ sono stati testati solo con HDP 2.4. Espandere tooget 2.4 HDP, **Hortonworks Sandbox archivio** su hello [Hortonworks Sandbox Scarica sito](http://hortonworks.com/downloads/#sandbox).

- [Java Developer Kit (JDK) versione 1.8 o successiva](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). È necessario JDK hello Azure Toolkit per IntelliJ.

- [Edizione community IDEA IntelliJ](https://www.jetbrains.com/idea/download) con hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in e hello [Azure Toolkit per IntelliJ](../azure-toolkit-for-intellij.md) plug-in. Strumenti HDInsight per IntelliJ è disponibili come parte di Azure Toolkit per IntelliJ hello. 

  tooinstall hello plug-in, hello seguenti:

  1. Aprire IntelliJ IDEA.
  2. In hello **iniziale** selezionare **configura**, quindi selezionare **plug-in**.
  3. Selezionare **plug-in installa JetBrains** nell'angolo inferiore sinistro hello.
  4. Utilizzare hello ricerca funzione toosearch per **Scala**, quindi selezionare **installare**.
  5. Selezionare **riavviare IDEA IntelliJ** installazione hello toocomplete.
  6. Hello tooinstall ripetere il passaggio 4 e 5 **Azure Toolkit per IntelliJ**. Per ulteriori informazioni, vedere [hello installare Azure Toolkit per IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="create-a-spark-scala-application"></a>Creare un'applicazione Spark Scala

In questa sezione verrà creato un progetto Scala di esempio usando IntelliJ IDEA. Nella sezione successiva hello, collegare IDEA IntelliJ toohello Hortonworks Sandbox (emulatore) prima di inviare il progetto hello.

1. Aprire IntelliJ IDEA dalla workstation. In hello **nuovo progetto** finestra di dialogo casella, hello seguenti:

   a. Selezionare **HDInsight** > **Spark on HDInsight (Scala)** (Spark in HDInsight - Scala).

   b. In hello **strumento di compilazione** selezionare uno dei hello seguenti, in base tooyour necessità:

    * **Maven**, per ottenere supporto per la creazione guidata di un progetto Scala
    * **SBT**, per la gestione delle dipendenze hello e la compilazione per il progetto di Scala hello

   ![finestra di dialogo Nuovo progetto Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. Selezionare **Avanti**.

3. In hello Avanti **nuovo progetto** finestra di dialogo casella, hello seguenti:

    ![Proprietà della creazione del progetto IntelliJ Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    a. In hello **nome progetto** , immettere un nome di progetto.

    b. In hello **percorso progetto** , immettere un percorso del progetto.

    c. Avanti toohello **Project SDK** elenco a discesa, seleziona **New**selezionare **JDK**, e quindi specificare la cartella hello di Java JDK versione 1.7 o versione successiva. Selezionare **Java 1.8** per cluster 2. x di Spark hello o selezionare **Java 1.7** per cluster 1. x di hello Spark. percorso predefinito di Hello è c:\Programmi\Microsoft Files\Java\jdk1.8.x_xxx.

    d. In hello **versione Spark** elenco a discesa, creazione guidata nuovo progetto di Scala si integra la versione corretta di hello per SDK Spark e SDK di Scala. Se la versione del cluster Spark hello è precedente alla versione 2.0, selezionare **nascita 1. x**. In caso contrario, selezionare **Spark 2.x**. In questo esempio viene usata la versione Spark 1.6.2 (Scala 2.10.5). Assicurarsi che si sta utilizzando repository hello contrassegnato Scala 2.10.x. Non utilizzare repository hello contrassegnato Scala 2.11.x.

4. Selezionare **Fine**.

5. Se hello **progetto** visualizzazione non è già aperta, premere **Alt + 1** tooopen è.

6. In **Esplora progetti**, espandere il progetto hello e quindi selezionare **src**.

7. Fare doppio clic su **src**, punto troppo**New**, quindi selezionare **Scala classe**.

8. In hello **nome** , immettere un nome, in hello **tipo** , quindi selezionare **oggetto**, quindi selezionare **OK**.

    ![finestra Crea nuova classe Scala Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. Nel file .scala hello incollare hello seguente codice:

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

10. In hello **compilare** dal menu **compilazione progetto**. Assicurarsi che la compilazione di hello è stata completata.


## <a name="link-toohello-hortonworks-sandbox"></a>Collegamento toohello Hortonworks Sandbox

Prima di poter collegare tooa Hortonworks Sandbox (emulatore), è necessario disporre di un'applicazione IntelliJ esistente.

emulatore tooan toolink, hello seguenti:

1. Progetto aperto hello in IntelliJ.

2. In hello **vista** dal menu **strumenti di Windows**, quindi selezionare **Esplora Azure**.

3. Espandere **Azure**, fare clic con il pulsante destro del mouse su **HDInsight** e quindi scegliere **Link an Emulator** (Collega un emulatore).

4. In hello **collegamento A nuovo emulatore** finestra, immettere la password di hello configurati per l'account radice hello di hello Hortonworks Sandbox, immettere valori simili toothose nella seguente schermata hello e quindi selezionare **OK **. 

   ![finestra di "Collegamento a nuovo emulatore" Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. emulatore di hello tooconfigure, seleziona **Sì**.

Quando l'emulatore hello è connesso correttamente, emulatore hello (Hortonworks Sandbox) viene elencata nel nodo HDInsight hello.

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a>Inviare hello Spark Scala applicazione toohello Hortonworks Sandbox

Dopo aver collegato emulatore toohello IntelliJ IDEA, è possibile inviare il progetto.

hello toosubmit un emulatore, tooan progetto seguente:

1. In **Esplora progetti**, fare clic sul progetto hello e quindi selezionare **Spark inviare applicazione tooHDInsight**.

2. Hello seguenti:

    a. In hello **cluster Spark (solo Linux)** elenco a discesa selezionare il Hortonworks Sandbox locale.

    b. In hello **nome della classe principale** scegliere o immettere il nome di classe principale hello. Per questa esercitazione, è il nome di hello **GroupByTest**.

3. Selezionare **Submit** (Invia). i log di invio processi Hello vengono visualizzati nella finestra degli strumenti di invio Spark hello.

## <a name="next-steps"></a>Passaggi successivi

- come le applicazioni toocreate Spark per HDInsight utilizzando gli strumenti HDInsight per IntelliJ, andare troppo toolearn[utilizza gli strumenti di HDInsight in Azure Toolkit per le applicazioni per il cluster HDInsight Spark Linux Spark toocreate IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md).

- toowatch un video di strumenti HDInsight per IntelliJ, andare troppo[introdurre strumenti HDInsight per IntelliJ per lo sviluppo di Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).

- toolearn come applicazioni di Spark toodebug utilizzando hello toolkit in modalità remota in HDInsight tramite SSH, andare troppo[in remoto il debug di applicazioni di Spark in un cluster di HDInsight con Azure Toolkit per IntelliJ tramite SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).

- toolearn come applicazioni di Spark toodebug utilizzando hello toolkit in modalità remota in HDInsight tramite una VPN, andare troppo[utilizza gli strumenti di HDInsight in Azure Toolkit per le applicazioni in modalità remota in HDInsight Spark Linux cluster Spark toodebug IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).

- toolearn come toouse strumenti HDInsight per Eclipse toocreate un'applicazione di Spark, andare troppo[utilizza gli strumenti di HDInsight in Azure Toolkit per le applicazioni di Spark toocreate Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md).

- toowatch un video di strumenti di HDInsight per Eclipse, andare troppo[utilizzare lo strumento di HDInsight per le applicazioni di Spark toocreate Eclipse](https://mix.office.com/watch/1rau2mopb6fha).
