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
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a>Creare un toorun applicazione Scala Maven nel cluster di Apache Spark in HDInsight

Informazioni su come un'applicazione di Spark scritta in Scala con Maven IDEA IntelliJ toocreate. articolo Hello utilizza Apache Maven come sistema di compilazione e inizia con un sistema di rilevazione di Maven esistente per la Scala fornito da IntelliJ IDEA di hello.  La creazione di un'applicazione di Scala in IntelliJ IDEA prevede hello alla procedura seguente:

* Utilizzare Maven come sistema di compilazione hello.
* Aggiornare le dipendenze del modulo modello oggetto di progetto (POM) file tooresolve Spark.
* Scrivere l'applicazione in Scala.
* Generare un file jar che può essere cluster Spark tooHDInsight inviato.
* Eseguire un'applicazione hello in cluster Spark usando inserire il.

> [!NOTE]
> HDInsight fornisce inoltre un processo hello di tooease dello strumento di plug-in IntelliJ IDEA di creazione e invio tooan applicazioni cluster HDInsight Spark in Linux. Per ulteriori informazioni, vedere [plug-in strumenti di HDInsight di utilizzo per toocreate IntelliJ IDEA e inviare le applicazioni di Spark](hdinsight-apache-spark-intellij-tool-plugin.md).
> 
> 

## <a name="prerequisites"></a>Prerequisiti

* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development Kit. Per installarlo, fare clic [qui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Ambiente IDE Java. Questo articolo usa IntelliJ IDEA 15.0.1. Per installarlo, fare clic [qui](https://www.jetbrains.com/idea/download/).

## <a name="install-scala-plugin-for-intellij-idea"></a>Installare il plug-in Scala per IntelliJ IDEA
Se installazione IDEA IntelliJ non non richiesta per l'abilitazione di plug-in di Scala, avviare IntelliJ IDEA e passare a hello plug-in hello tooinstall di passaggi seguente:

1. Avviare IntelliJ IDEA e dalla schermata iniziale fare clic su **Configure** (Configura) e quindi fare clic su **Plugins** (Plugin).
   
    ![Abilitare i plug-in Scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. Nella schermata successiva hello, fare clic su **plug-in installa JetBrains** dall'angolo inferiore sinistro di hello. In hello **Sfoglia i plug-in JetBrains** la finestra di dialogo che viene aperto, eseguire la ricerca di Scala e quindi fare clic su **installare**.
   
    ![Installare i plug-in Scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. Dopo l'installazione di plug-in hello correttamente, fare clic su hello **pulsante riavviare IDEA IntelliJ** toorestart hello IDE.

## <a name="create-a-standalone-scala-project"></a>Creare un progetto Scala autonomo
1. Avviare IntelliJ IDEA e creare un nuovo progetto. In hello dialogo Nuovo progetto, rendere hello opzioni seguenti e quindi fare clic su **Avanti**.
   
    ![Creare un progetto Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * Selezionare **Maven** come tipo di progetto hello.
   * Specificare un valore per **Project SDK**. Fare clic su Nuovo e passare toohello directory di installazione Java, in genere `C:\Program Files\Java\jdk1.8.0_66`.
   * Seleziona hello **Create dal sistema per** opzione.
   * Selezionare nell'elenco di archetipi hello **semplice sistema di rilevazione di tools.archetypes:scala org.scala**. Verrà creata una struttura di directory destra hello e scaricare hello necessario predefinito dipendenze toowrite Scala programma.
2. Specificare i valori pertinenti per **GroupId** (ID gruppo), **ArtifactId** (ID elemento) e **Version** (Versione). Fare clic su **Avanti**.
3. In hello successiva finestra di dialogo in cui si specifica Maven home directory e altre impostazioni utente, accettare le impostazioni predefinite hello e fare clic su **Avanti**.
4. In hello ultima finestra di dialogo, specificare un nome di progetto e il percorso e quindi fare clic su **fine**.
5. Eliminare hello **MySpec.Scala** file in **src\test\scala\com\microsoft\spark\example**. Non è necessario questo per un'applicazione hello.
6. Se necessario, rinominare i file di origine e di test predefinito hello. Dal riquadro sinistro di hello in IntelliJ IDEA hello, passare troppo**src\main\scala\com.microsoft.spark.example**. Fare doppio clic su **App.scala**, fare clic su **refactoring**, fare clic su Rinomina file, nella finestra di dialogo hello specificare hello nuovo nome per un'applicazione hello e quindi fare clic su **refactoring**.
   
    ![Rinominare file](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. Nei passaggi successivi hello, si aggiornerà hello pom.xml toodefine hello le dipendenze per hello applicazione Spark Scala. Per tali dipendenze toobe scaricato e risolti automaticamente, che è necessario configurare Maven di conseguenza.
   
    ![Configurare Maven per i download automatici](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. Da hello **File** menu, fare clic su **impostazioni**.
   2. In hello **impostazioni** finestra di dialogo passare troppo**distribuzione della compilazione, esecuzione,** > **gli strumenti di generazione** > **Maven**  >  **Importazione**.
   3. L'opzione hello troppo**automaticamente i progetti Maven importazione**.
   4. Fare clic su **Apply** (Applica) e quindi su **OK**.
8. Aggiornare hello Scala origine file tooinclude il codice dell'applicazione. Aprire e sostituire hello esistente codice di esempio con hello seguente di codice e salvare le modifiche di hello. Questo codice legge i dati di hello da hello HVAC.csv (disponibile in tutti i cluster HDInsight Spark), recupera righe hello solo con una cifra nella sesta colonna hello e scrive l'output di hello troppo**/HVACOut** in spazio di archiviazione predefinito hello contenitore per i cluster di hello.
   
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
9. Aggiornare pom.xml hello.
   
   1. All'interno di `<project>\<properties>` aggiungere hello seguenti:
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. All'interno di `<project>\<dependencies>` aggiungere hello seguenti:
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      Salvare le modifiche toopom.xml.
10. Creare il file JAR hello. IntelliJ IDEA consente di creare un file con estensione jar come elemento di un progetto. Eseguire hello alla procedura seguente.
    
    1. Da hello **File** menu, fare clic su **struttura del progetto**.
    2. In hello **struttura del progetto** la finestra di dialogo, fare clic su **elementi** e quindi fare clic su hello e simboli. Nella finestra di dialogo popup hello, fare clic su **JAR**, quindi fare clic su **dai moduli con dipendenze**.
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. In hello **creare JAR dai moduli** finestra di dialogo, fare clic sui puntini di sospensione hello (![i puntini di sospensione](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) contro hello **classe Main**.
    4. In hello **Seleziona classe Main** della finestra di dialogo classe hello select che viene visualizzato per impostazione predefinita e quindi fare clic su **OK**.
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. In hello **creare JAR dai moduli** finestra di dialogo, accertarsi che l'opzione hello troppo**estrarre toohello destinazione JAR** sia selezionata e quindi fare clic su **OK**. Verrà creato un singolo file con estensione jar con tutte le dipendenze.
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. scheda layout di Hello output elenca tutti JAR hello che sono inclusi come parte del progetto di Maven hello. È possibile selezionare e quelli in cui hello Scala applicazione hello di eliminazione non ha alcuna dipendenza diretta. Per un'applicazione hello viene creata in questo caso, è possibile rimuovere tutto tranne hello ultimo (**output di compilazione SparkSimpleApp**). Selezionare toodelete JAR hello e quindi fare clic su hello **eliminare** icona.
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        Assicurarsi che **compilare su verificare** casella è selezionata, che assicura che jar hello viene creato ogni volta che il progetto hello viene compilato o aggiornato. Fare clic su **Apply** (Applica) e quindi su **OK**.
    7. Dalla barra dei menu hello, fare clic su **compilare**, quindi fare clic su **Crea progetto**. È anche possibile fare clic su **artefatti di compilazione** jar hello toocreate. Hello jar output viene creato in **\out\artifacts**.
       
        ![Creazione di un file con estensione jar](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a>Eseguire un'applicazione hello in cluster Spark hello
un'applicazione hello toorun nel cluster hello, è necessario eseguire il seguente hello:

* **Il blob di archiviazione Azure toohello copia hello applicazione jar** associato hello cluster. È possibile utilizzare [ **AzCopy**](../storage/common/storage-use-azcopy.md), della riga di comando utilità, toodo così. Esistono molti degli altri client anche che è possibile utilizzare dati tooupload. Altre informazioni in merito sono disponibili in [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).
* **Utilizzare toosubmit inserire il processo di un'applicazione in modalità remota** cluster Spark toohello. Il cluster Spark in HDInsight include inserire il che espone REST endpoint tooremotely invia i processi di Spark. Per ulteriori informazioni, vedere [Inviare processi Spark in modalità remota utilizzando Livy con cluster Spark in HDInsight](hdinsight-apache-spark-livy-rest-interface.md).

## <a name="next-step"></a>Passaggio successivo

In questo articolo si è appreso come toocreate un'applicazione di scala di Spark. Avanzamento toohello Avanti articolo toolearn come toorun questa applicazione su un HDInsight Spark cluster utilizzando inserire il.

> [!div class="nextstepaction"]
>[Eseguire processi in modalità remota in un cluster Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

