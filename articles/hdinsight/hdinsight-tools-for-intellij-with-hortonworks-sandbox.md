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
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a>Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox

Questo articolo illustra come usare gli strumenti HDInsight per IntelliJ per sviluppare applicazioni Apache Scala e quindi testarle in [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) in esecuzione sulla workstation. 

[IntelliJ IDEA](https://www.jetbrains.com/idea/) è un ambiente di sviluppo integrato (IDE) Java per lo sviluppo di software per computer. Dopo aver sviluppato e testato le applicazioni in Hortonworks Sandbox, è possibile trasferirle in [Azure HDInsight](hdinsight-hadoop-introduction.md).

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questa esercitazione, è necessario avere:

- Hortonworks Data Platform (HDP) 2.4 in Hortonworks Sandbox in esecuzione nell'ambiente locale. Per configurare HDP, vedere l'[introduzione all'ecosistema Hadoop con un ambiente sandbox Hadoop in una macchina virtuale](hdinsight-hadoop-emulator-get-started.md). 
    >[!NOTE]
    >Gli strumenti HDInsight per IntelliJ sono stati testati solo con HDP 2.4. Per ottenere HDP 2.4, espandere [Archivio Hortonworks Sandbox](http://hortonworks.com/downloads/#sandbox) nel **sito di download di Hortonworks Sandbox**.

- [Java Developer Kit (JDK) versione 1.8 o successiva](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). JDK è richiesto da Azure Toolkit for IntelliJ.

- [IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/download) con i plug-in [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) e [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md). Gli strumenti HDInsight per IntelliJ sono disponibili nell'ambito di Azure Toolkit for IntelliJ. 

  Per installare i plug-in, seguire questa procedura:

  1. Aprire IntelliJ IDEA.
  2. Nella **schermata iniziale** selezionare **Configure** (Configura) e quindi **Plugins** (Plug-in).
  3. Selezionare **Install JetBrains plugin** (Installa plug-in JetBrains) nell'angolo inferiore sinistro.
  4. Usare la funzione di ricerca per cercare **Scala** e quindi selezionare **Install** (Installa).
  5. Selezionare **Restart IntelliJ IDEA** (Riavvia IntelliJ IDEA) per completare l'installazione.
  6. Ripetere i passaggi 4 e 5 per installare **Azure Toolkit for IntelliJ**. Per altre informazioni, vedere [Installare Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="create-a-spark-scala-application"></a>Creare un'applicazione Spark Scala

In questa sezione verrà creato un progetto Scala di esempio usando IntelliJ IDEA. Nella sezione successiva, IntelliJ IDEA verrà collegato a Hortonworks Sandbox (emulatore) prima di inviare il progetto.

1. Aprire IntelliJ IDEA dalla workstation. Nella finestra di dialogo **New Project** (Nuovo progetto) seguire questa procedura:

   a. Selezionare **HDInsight** > **Spark on HDInsight (Scala)** (Spark in HDInsight - Scala).

   b. Nell'elenco **Build tool** (Strumento di compilazione) selezionare uno degli strumenti seguenti, in base alla necessità:

    * **Maven**, per ottenere supporto per la creazione guidata di un progetto Scala
    * **SBT**, per la gestione delle dipendenze e la compilazione per il progetto Scala

   ![Finestra di dialogo del nuovo progetto](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. Selezionare **Avanti**.

3. Nella finestra di dialogo **New Project** (Nuovo progetto) successiva seguire questa procedura:

    ![Proprietà della creazione del progetto IntelliJ Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    a. Nella casella **Project name** (Nome progetto) immettere un nome per il progetto.

    b. Nella casella **Project location** (Percorso progetto) immettere un percorso per il progetto.

    c. Accanto all'elenco a discesa **Project SDK** (SDK progetto) selezionare **New** (Nuovo) e quindi **JDK** e infine specificare la cartella di Java JDK versione 1.7 o successiva. Selezionare **Java 1.8** per il cluster Spark 2.x oppure **Java 1.7** per il cluster Spark 1.x. Il percorso predefinito è C:\Programmi\Java\jdk1.8.x_xxx.

    d. Nell'elenco a discesa **Spark version** (Versione di Spark) la creazione guidata del progetto Scala inserisce la versione corretta per Spark SDK e Scala SDK. Se la versione del cluster Spark è precedente alla 2.0, selezionare **Spark 1.x**. In caso contrario, selezionare **Spark 2.x**. In questo esempio viene usata la versione Spark 1.6.2 (Scala 2.10.5). Assicurarsi di usare il repository contrassegnato come Scala 2.10.x. Non usare il repository contrassegnato come Scala 2.11.x.

4. Selezionare **Fine**.

5. Se la visualizzazione **Project** (Progetto) non è già aperta, premere **ALT+1** per aprirla.

6. In **Project Explorer** (Esplora progetti) espandere il progetto e quindi selezionare **src**.

7. Fare clic con il pulsante destro del mouse su **src**, scegliere **New** (Nuovo) e quindi fare clic su **Scala class** (Classe Scala).

8. Immettere un nome nella casella **Name** (Nome), selezionare **Object**, (Oggetto) nella casella **Kind** (Tipologia) e quindi selezionare **OK**.

    ![Finestra di dialogo Create New Scala Class (Crea nuova classe Scala)](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. Incollare il codice seguente nel file con estensione scala:

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

10. Dal menu **Build** (Compila) scegliere **Build project** (Compila progetto). Verificare che la compilazione sia stata completata correttamente.


## <a name="link-to-the-hortonworks-sandbox"></a>Eseguire il collegamento a Hortonworks Sandbox

Per poter eseguire il collegamento a Hortonworks Sandbox (emulatore), deve essere presente un'applicazione IntelliJ esistente.

Per il collegamento a un emulatore, seguire questa procedura:

1. Aprire il progetto in IntelliJ.

2. Dal menu **View** (Visualizza) scegliere **Tool Windows** (Finestre degli strumenti) e quindi selezionare **Azure Explorer**.

3. Espandere **Azure**, fare clic con il pulsante destro del mouse su **HDInsight** e quindi scegliere **Link an Emulator** (Collega un emulatore).

4. Nella finestra **Link A New Emulator** (Collega nuovo emulatore) immettere la password configurata per l'account radice di Hortonworks Sandbox e valori simili a quelli riportati nello screenshot seguente e quindi selezionare **OK**. 

   ![Finestra "Link a New Emulator" (Collega nuovo emulatore)](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. Per configurare l'emulatore, selezionare **Yes** (Sì).

Quando è connesso correttamente, l'emulatore (Hortonworks Sandbox) viene elencato nel nodo HDInsight.

## <a name="submit-the-spark-scala-application-to-the-hortonworks-sandbox"></a>Inviare l'applicazione Spark Scala a Hortonworks Sandbox

Dopo aver collegato IntelliJ IDEA all'emulatore è possibile inviare il progetto.

Per inviare un progetto a un emulatore, seguire questa procedura:

1. In **Project Explorer** (Esplora progetti) fare clic con il pulsante destro del mouse sul progetto e quindi scegliere **Submit Spark Application to HDInsight** (Invia applicazione Spark a HDInsight).

2. Eseguire le operazioni seguenti:

    a. Nell'elenco a discesa **Spark cluster (Linux only)** (Cluster Spark - solo Linux) selezionare l'ambiente Hortonworks Sandbox locale.

    b. Nella casella **Main class name** (Nome classe principale) scegliere o immettere il nome della classe principale. Per questa esercitazione, il nome è **GroupByTest**.

3. Selezionare **Submit** (Invia). I log di invio dei processi vengono visualizzati nella finestra degli strumenti di invio Spark.

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni su come creare applicazioni Spark per HDInsight con gli strumenti HDInsight per IntelliJ, vedere l'articolo su come [usare gli strumenti HDInsight in Azure Toolkit for IntelliJ per creare applicazioni Spark per un cluster HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md).

- Per un video sugli strumenti HDInsight per IntelliJ, vedere l'[introduzione agli strumenti HDInsight per IntelliJ per lo sviluppo Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).

- Per informazioni su come eseguire il debug di applicazioni Spark usando il toolkit in remoto in HDInsight tramite SSH, vedere [Eseguire il debug remoto delle applicazioni Spark su un cluster HDInsight con Azure Toolkit per IntelliJ tramite SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).

- Per informazioni su come eseguire il debug di applicazioni Spark usando il toolkit in remoto in HDInsight tramite VPN, vedere [Usare gli strumenti HDInsight in Azure Toolkit for IntelliJ per eseguire il debug di applicazioni Spark in remoto in cluster HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).

- Per informazioni su come usare gli strumenti HDInsight per Eclipse per creare un'applicazione Spark, vedere l'articolo su come [usare gli strumenti HDInsight in Azure Toolkit for Eclipse per creare applicazioni Spark](hdinsight-apache-spark-eclipse-tool-plugin.md).

- Per un video sugli strumenti HDInsight per Eclipse, vedere [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha) (Usare lo strumento HDInsight per Eclipse per creare applicazioni Spark).
