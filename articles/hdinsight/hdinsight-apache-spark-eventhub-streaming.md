---
title: aaaUse Apache Spark streaming con hub eventi in Azure HDInsight | Documenti Microsoft
description: "Compila un esempio di flusso Apache Spark in modalità toosend dati tooAzure Hub eventi del flusso e quindi ricevere gli eventi in cluster di HDInsight Spark con un'applicazione di scala."
keywords: streaming apache spark, streaming spark, esempio spark, esempio streaming spark apache, esempio azure hub eventi, esempio spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a>Streaming Apache Spark: elaborare i dati dall'Hub eventi di Azure con il cluster Spark in HDInsight

In questo articolo, si crea un Apache Spark lo streaming di esempio che coinvolge hello alla procedura seguente:

1. Utilizzare un messaggio di tooingest applicazione autonoma in un Hub di eventi di Azure.

2. I due diversi approcci, recuperare messaggi hello da Hub di eventi in tempo reale tramite un'applicazione in esecuzione nel cluster Spark in HDInsight di Azure.

3. È compilare pipeline di analisi flusso sistemi di archiviazione toopersist dati toodifferent o ottenere informazioni dettagliate dai dati in tempo reale di hello.

## <a name="prerequisites"></a>Prerequisiti

* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="spark-streaming-concepts"></a>Concetti relativi allo streaming Spark

Per una spiegazione dettagliata dello streaming Spark, vedere [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview) (Panoramica dello streaming in Apache Spark). HDInsight offre hello del cluster stesso flusso funzionalità tooa Spark in Azure.  

## <a name="what-does-this-solution-do"></a>Scopo di questa soluzione

In questo articolo, toocreate un esempio di flusso Spark, eseguire hello alla procedura seguente:

1. Creare un Hub eventi di Azure che riceve un flusso di eventi.

2. Eseguire un'applicazione autonoma locale che genera eventi e lo inserisce toohello Hub di eventi di Azure. applicazione di esempio Hello che questa sia pubblicata nel [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).

3. Eseguire un'applicazione di streaming in modalità remota in un cluster Spark che legge eventi di streaming provenienti dall'Hub di eventi di Azure ed eseguire varie analisi/elaborazioni di dati.

## <a name="create-an-azure-event-hub"></a>Creare un Hub di eventi di Azure

1. Accesso toohello [portale Azure](https://ms.portal.azure.com), fare clic su **New** in hello in alto a sinistra della schermata di hello.

2. Fare clic su **Internet delle cose** e quindi su **Hub eventi**.

    ![Creare un hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Creare un hub eventi per l'esempio di streaming Spark")

3. In hello **Crea spazio dei nomi** pannello, immettere un nome di spazio dei nomi. Scegliere hello tariffario (Standard o Basic). Inoltre, è possibile scegliere una sottoscrizione di Azure, un gruppo di risorse e una posizione nella quale risorsa hello toocreate. Fare clic su **crea** dello spazio dei nomi di toocreate hello.

      ![Fornire un nome di hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Fornire un nome di hub eventi per l'esempio di streaming Spark")

    > [!NOTE]
    > È consigliabile selezionare hello stesso **percorso** del cluster Apache Spark in HDInsight tooreduce latenza e i costi.
    >
    >

4. Nell'elenco dello spazio dei nomi di hello hub eventi, fare clic su hello nuovo spazio dei nomi.      


5. Nel Pannello di hello dello spazio dei nomi, fare clic su **hub eventi**, quindi fare clic su **+ Hub eventi** toocreate un nuovo Hub eventi.
   
    ![Creare un hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Creare un hub eventi per l'esempio di streaming Spark")

6. Digitare un nome per l'Hub eventi, set hello partizione conteggio too10 e too1 di memorizzazione di messaggi. Ci stiamo archiviazione messaggi hello in questa soluzione non in modo da lasciare rest hello come impostazione predefinita e quindi fare clic su **crea**.
   
    ![Fornire i dettagli dell'hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Fornire i dettagli dell'hub eventi per l'esempio di streaming Spark")

7. Hello appena creati Hub eventi è elencato nel Pannello di hello Hub eventi.
    
     ![Visualizzare l'Hub eventi, ad esempio di flusso Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "Hub di eventi di visualizzazione per hello nascita streaming di esempio")

8. Nel pannello dello spazio dei nomi hello (non hello specifico Hub eventi blade), fare clic su **criteri di accesso condiviso**, quindi fare clic su **RootManageSharedAccessKey**.
    
     ![Impostare i criteri di Hub eventi, ad esempio di flusso Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "criteri impostare Hub di eventi per hello nascita streaming di esempio")

9. Fare clic su hello toocopy pulsante Copia di hello **RootManageSharedAccessKey** primario chiave e connessione stringa toohello negli Appunti. Salvare queste toouse più avanti nell'esercitazione di hello.
    
     ![Visualizzare le chiavi di criterio Hub eventi, ad esempio di flusso Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "chiavi dei criteri di Hub di eventi di visualizzazione per hello nascita streaming di esempio")

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a>Inviare i messaggi tooAzure Hub di eventi tramite un'applicazione di esempio Scala

In questa sezione si utilizza un'applicazione locale autonomo di una Scala che genera un flusso di eventi e lo invia tooAzure Hub eventi creato in precedenza. Questa applicazione è disponibile in GitHub all'indirizzo [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer). Ecco i passaggi di Hello presuppongono che si è già duplicata questo repository GitHub.

1. Verificare che sia installato nel computer di hello in cui si esegue l'applicazione segue hello.

    * Oracle Java Development Kit. Per installarlo, fare clic [qui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
    * Apache Maven. È possibile scaricarlo [qui](https://maven.apache.org/download.cgi). Sono disponibili istruzioni tooinstall Maven [qui](https://maven.apache.org/install.html).

2. Aprire un prompt dei comandi e passare toohello percorso è stato clonato il repository GitHub hello per un'applicazione hello esempio Scala ed eseguire hello dopo l'applicazione hello toobuild di comando.

        mvn package

3. file jar di output di Hello per un'applicazione hello, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, viene creato in **/destinazione** directory. Utilizzare il file JAR più avanti in questa soluzione completa di articolo tootest hello.

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a>Creare i messaggi dell'applicazione tooreceive da Hub di eventi in un cluster Spark 

Sono disponibili due approcci tooconnect, Streaming Spark e hub di eventi di Azure, le connessioni basate su ricevitore e Direct DStream-connessione basata su. Basato su DStream diretta è stato introdotto in gennaio 2017 nella versione di hello 2.0.3. Si suppone che la connessione tooreplace hello originale basata su destinatario perché è più efficiente ed efficace a risorsa. Altre informazioni sono disponibili su [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs). DStream diretto supporta solo Spark 2.0 e versioni successive.

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a>Compilazione di applicazioni con connettore di hello dipendenza toospark eventhubs

Verranno inoltre pubblicate hello versione di Spark-EventHubs in GitHub di gestione temporanea. versione sosta hello di toouse di Spark EventHubs, hello primo passaggio consiste tooindicate GitHub come hello repository di origine mediante l'aggiunta di hello toopom.xml voce seguente:

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

È quindi possibile aggiungere hello seguente versione non definitiva di dipendenza tooyour progetto tootake hello.

Dipendenza Maven

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

Dipendenza SBT

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a>Connessione DStream diretto

È possibile scaricare da [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar) un file con estensione jar preesistente contenente esempi di uso di DStream diretto.

file jar Hello contiene tre esempi sono disponibili in cui il codice sorgente [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).

Prendere come esempio [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala):

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

In hello sopra riportato, `eventhubParameters` sono hello parametri specifici tooa singola EventHubs istanza e si dispone di toopass è toohello `createDirectStreams` API che costruisce mapping oggetto uno diretto DStream tooa spazio dei nomi degli hub di eventi. Oggetto di hello DStream diretto, è possibile chiamare qualsiasi API DStream fornita dal framework Spark Streaming API. In questo esempio, si calcola frequenza hello di ogni parola all'interno di intervalli di hello ultimo batch micro 3.

### <a name="receiver-based-connection"></a>Connessioni basate su ricevitore

Un Spark streaming scritto in Scala, che riceve gli eventi e destinazioni di route hello toodifferent, l'applicazione di esempio è disponibile all'indirizzo [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples). Seguire i passaggi hello sotto l'applicazione hello tooupdate per la configurazione di Hub eventi e creare file jar di output di hello.

1. Avviare IntelliJ IDEA e avviare schermata selezionare da hello **estrarre dal controllo della versione** e quindi fare clic su **Git**.
   
    ![Esempio di streaming Apache Spark - Ottenere origini da Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Esempio di streaming Apache Spark - Ottenere origini da Git")

2. In hello **Clone Repository** nella finestra di dialogo forniscono hello URL toohello Git repository tooclone da specificare hello directory tooclone per e quindi fare clic su **Clone**.
   
    ![Esempio di streaming Apache Spark - Clonare da Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Esempio di streaming Apache Spark - Clonare da Git")
3. Seguire i prompt di hello fino a quando progetto hello viene completamente duplicato. Premere **Alt + 1** tooopen hello **visualizzazione progetto**. Dovrebbe essere simile a seguito di hello.
   
    ![Esempio di streaming Apache Spark - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Esempio di streaming Apache Spark - Project View")
4. Verificare che il codice dell'applicazione hello viene compilato con Java8. tooensure, fare clic su **File**, fare clic su **struttura del progetto**e in hello **progetto** scheda, assicurarsi che il livello di linguaggio di progetto è stato impostato troppo**8 - espressioni lambda, tipo le annotazioni e così via.**.
   
    ![Esempio di streaming Apache Spark - Impostare il compilatore](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Esempio di streaming Apache Spark - Impostare il compilatore")
5. Aprire hello **pom.xml** e accertarsi che sia corretta versione di hello Spark. In `<properties>` nodo, cercare hello seguente frammento di codice e verificare la versione di hello Spark.

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. un'applicazione Hello richiede un file jar dipendenza chiamato **jar driver JDBC**. Si tratta di messaggi hello toowrite obbligatorio ricevuti da Hub di eventi in un database SQL di Azure. È possibile scaricare la versione 4.1 o successiva di questo file con estensione jar [qui](https://msdn.microsoft.com/sqlserver/aa937724.aspx). Aggiungi riferimento toothis jar nella libreria di progetto hello. Eseguire hello alla procedura seguente:
     
     1. Nella finestra in cui è aperta un'applicazione hello IDEA IntelliJ **File**, fare clic su **struttura del progetto**e quindi fare clic su **librerie**. 
     2. Fare clic su hello icona Aggiungi (![icona Aggiungi](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), fare clic su **Java**, quindi passare toohello percorso in cui sono stati scaricati file jar di driver JDBC hello. Seguire hello richieste tooadd hello jar file toohello libreria del progetto.

         ![aggiungere dipendenze mancanti](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Aggiungere file JAR di dipendenza mancanti")
     3. Fare clic su **Apply**.

7. Creare il file jar di hello output. Eseguire hello alla procedura seguente.

   1. In hello **struttura del progetto** la finestra di dialogo, fare clic su **elementi** e quindi fare clic su hello e simboli. Nella finestra di dialogo popup hello, fare clic su **JAR**, quindi fare clic su **dai moduli con dipendenze**.      
       
       ![Esempio di streaming Apache Spark - Creazione di un file con estensione jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Esempio di streaming Apache Spark - Creazione di un file con estensione jar")
   2. In hello **creare JAR dai moduli** finestra di dialogo, fare clic sui puntini di sospensione hello (![i puntini di sospensione](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) contro hello **classe Main**.
   3. In hello **Seleziona classe Main** finestra di dialogo selezionare una qualsiasi delle classi disponibili hello e quindi fare clic su **OK**.
      
       ![Esempio di streaming Apache Spark - Selezionare la classe per un file con estensione jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Esempio di streaming Apache Spark - Selezionare la classe per un file con estensione jar")
   4. In hello **creare JAR dai moduli** finestra di dialogo, accertarsi che l'opzione hello troppo**estrarre toohello destinazione JAR** sia selezionata e quindi fare clic su **OK**. Verrà creato un singolo file con estensione jar con tutte le dipendenze.
      
       ![Esempio di streaming Apache Spark - Creare un file con estensione jar dai moduli](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Esempio di streaming Apache Spark - Creare un file con estensione jar dai modul")
   5. Hello **Output Layout** scheda vengono elencati tutti JAR hello che sono inclusi come parte del progetto di Maven hello. È possibile selezionare e quelli in cui hello Scala applicazione hello di eliminazione non ha alcuna dipendenza diretta. Per un'applicazione hello viene creata in questo caso, è possibile rimuovere tutto tranne hello ultimo (**spark-streaming--persistenza-esempi di dati compilare output**). Selezionare toodelete JAR hello e quindi fare clic su hello **eliminare** icona (![icona Elimina](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).
      
       ![Esempio di streaming Apache Spark - Eliminare i file con estensione jar estratti](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Esempio di streaming Apache Spark - Eliminare i file con estensione jar estratti")
      
       Assicurarsi che **compilare su verificare** casella è selezionata, che assicura che jar hello viene creato ogni volta che il progetto hello viene compilato o aggiornato. Fare clic su **Apply**.
   6. In hello **Output Layout** scheda nella parte inferiore di hello di hello **elementi disponibili** casella, si dispone di jar SQL JDBC hello di libreria del progetto precedente toohello aggiunto. È necessario aggiungere questo toohello **Output Layout** scheda. Fare clic sul file jar hello e quindi fare clic su **estrarre nell'Output radice**.
      
       ![Esempio di streaming Apache Spark - Estrarre file con estensione jar di dipendenza](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Esempio di streaming Apache Spark - Estrarre file con estensione jar di dipendenza")  
      
       Hello **Output Layout** scheda dovrebbe essere simile al seguente.
      
       ![Esempio di streaming Apache Spark - Scheda output finale](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Esempio di streaming Apache Spark - Scheda output finale")        
      
       In hello **struttura del progetto** la finestra di dialogo, fare clic su **applica** e quindi fare clic su **OK**.    
   7. Dalla barra dei menu hello, fare clic su **compilare**, quindi fare clic su **Crea progetto**. È anche possibile fare clic su **artefatti di compilazione** jar hello toocreate. Hello jar output viene creato in **\classes\artifacts**.
      
       ![Esempio di streaming Apache Spark - Output dei file con estensione jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Esempio di streaming Apache Spark - Output dei file con estensione jar")

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a>Eseguire un'applicazione hello in modalità remota in un cluster Spark usando inserire il

In questo articolo è utilizzare applicazione flusso di inserire il toorun hello Apache Spark in modalità remota in un cluster Spark. Per informazioni dettagliate su come inserire il con HDInsight Spark toouse cluster, vedere [invia i processi in modalità remota tooan Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md). Prima di iniziare l'esecuzione di un'applicazione hello Spark streaming, sono disponibili un paio di operazioni che è necessario eseguire:

1. Avviare gli eventi di toogenerate hello autonomo locale dell'applicazione e inviati tooEvent Hub. Utilizzare hello successivo comando toodo pertanto:

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. Hello copia streaming jar (**spark-streaming-data-persistenza-examples.jar**) toohello associato hello cluster nell'archiviazione Blob di Azure. In questo modo hello jar accessibile tooLivy. È possibile utilizzare [ **AzCopy**](../storage/common/storage-use-azcopy.md), della riga di comando utilità, toodo così. Esistono molti degli altri client è possibile utilizzare dati tooupload. Altre informazioni in merito sono disponibili in [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).
3. Installare CURL computer hello in cui si eseguono tali applicazioni. Utilizziamo CURL tooinvoke hello hello toorun gli endpoint di inserire il processi in modalità remota.

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a>Eseguire hello Spark streaming tooreceive hello gli eventi dell'applicazione in un Blob di archiviazione di Azure come testo

Aprire un prompt dei comandi, passare toohello directory in cui è installato CURL ed eseguire hello comando (nome sostituire nome utente/password e cluster) seguente:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Hello parametri nel file hello **inputBlob.txt** sono definite come segue:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Segnalare il problema, comprendere quali sono i parametri di hello nel file di input hello:

* **file** file jar nell'account di archiviazione di Azure hello associato hello cluster hello percorso toohello dell'applicazione.
* **className** hello nome della classe hello in jar hello.
* **args** hello elenco di argomenti richiesto dalla classe hello
* **numExecutors** hello numero di core usati da hello toorun Spark streaming dell'applicazione. Deve essere sempre almeno due volte i numero di hello di partizioni di Hub eventi.
* **executorMemory**, **executorCores**, **driverMemory** vengono utilizzati parametri tooassign necessarie risorse applicazione streaming toohello.

> [!NOTE]
> Non è necessario cartelle di output di hello toocreate (EventCheckpoint, EventCount/EventCount10) che vengono utilizzate come parametri. lo streaming dell'applicazione Hello verranno creati automaticamente.
>
>

Quando si esegue il comando hello, verrà visualizzato un output simile hello seguente:

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

Prendere nota dell'ID batch hello nell'ultima riga di hello dell'output di hello (in questo esempio è '1'). tooverify che hello applicazione viene eseguita correttamente, è possibile esaminare l'account di archiviazione di Azure associato al cluster hello e dovrebbe essere hello **EventCount/EventCount10** cartella creato. Questa cartella deve contenere blob che acquisisce il numero di hello di eventi elaborati all'interno di hello periodo di tempo specificato per il parametro hello **batch intervallo in secondi**.

un'applicazione Hello Spark streaming continuerà toorun fino a quando non si terminarlo. toodo in tal caso, utilizzare hello comando seguente:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a>Eseguire applicazioni hello eventi hello tooreceive in un Blob di archiviazione di Azure come JSON
Aprire un prompt dei comandi, passare toohello directory in cui è installato CURL ed eseguire hello comando (nome sostituire nome utente/password e cluster) seguente:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Hello parametri nel file hello **inputJSON.txt** sono definite come segue:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

i parametri di Hello sono simili toowhat specificato per l'output di testo hello, nel passaggio precedente hello. Nuovamente, non è necessario cartelle di output di hello toocreate (EventCheckpoint, EventCount/EventCount10) che vengono utilizzate come parametri. lo streaming dell'applicazione Hello verranno creati automaticamente.

 Dopo l'esecuzione di comandi hello, è possibile esaminare l'account di archiviazione di Azure associato al cluster hello e dovrebbe essere hello **/EventStore10** cartella creato. Aprire qualsiasi file con prefisso **parte -** dovrebbe essere possibile visualizzare gli eventi di hello elaborati in un formato JSON.

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a>Eseguire applicazioni hello eventi hello tooreceive in una tabella Hive
hello toorun applicazione di streaming Spark che gli eventi di flussi in un Hive della tabella è necessario alcuni componenti aggiuntivi. Si tratta di:

* datanucleus-api-jdo-3.2.6.jar
* datanucleus-rdbms-3.2.9.jar
* datanucleus-core-3.2.10.jar
* hive-site.xml

Hello **JAR** file sono disponibili nel cluster HDInsight Spark in `/usr/hdp/current/spark-client/lib`. Hello **hive-Site.XML** è disponibile all'indirizzo `/usr/hdp/current/spark-client/conf`.

È possibile utilizzare [WinScp](http://winscp.net/eng/download.php) toocopy i file dal computer locale di hello cluster tooyour. Quindi, è possibile utilizzare strumenti toocopy questi file tramite l'account di archiviazione tooyour associati a cluster hello. Per ulteriori informazioni sulla modalità tooupload file toohello account di archiviazione, vedere [caricare dati per i processi di Hadoop in HDInsight](hdinsight-upload-data.md).

Dopo aver copiato i file di hello tooyour account di archiviazione di Azure, aprire un prompt dei comandi, passare toohello directory in cui è installato CURL ed eseguire hello comando (nome sostituire nome utente/password e cluster) seguente:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Hello parametri nel file hello **inputHive.txt** sono definite come segue:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

i parametri di Hello sono simili toowhat specificato per l'output di testo hello, nei passaggi precedenti hello. Nuovamente, non è necessario output di hello toocreate cartelle (EventCheckpoint, EventCount/EventCount10) o hello tabella Hive (EventHiveTable10) che vengono utilizzate come parametri di output. lo streaming dell'applicazione Hello verranno creati automaticamente. Si noti che hello **JAR** e **file** opzione include i file JAR di percorsi toohello e hello hive-Site.XML che si è copiato toohello account di archiviazione.

tooverify che hello tabella hive è stato creato correttamente, è possibile SSH in cluster hello e l'esecuzione di query Hive. Per istruzioni, vedere [Usare Hive con Hadoop in HDInsight tramite SSH](hdinsight-hadoop-use-hive-ssh.md). Quando si è connessi tramite SSH, è possibile eseguire hello successivo comando tooverify tabella Hive, hello **EventHiveTable10**, viene creato.

    show tables;

Verrà visualizzato un segue toohello simili di output:

    OK
    eventhivetable10
    hivesampletable

È anche possibile eseguire una query SELECT contenuto hello tooview della tabella hello.

    SELECT * FROM eventhivetable10 LIMIT 10;

Verrà visualizzato un output simile hello seguente:

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a>Eseguire applicazioni hello eventi hello tooreceive in una tabella di database SQL di Azure
Prima di eseguire questo passaggio, assicurarsi che sia stato creato un database SQL di Azure. Per istruzioni, vedere [Creare un database SQL in pochi minuti](../sql-database/sql-database-get-started.md). toocomplete in questa sezione, sono necessari i valori per nome del database, nome del server di database e le credenziali di amministratore di database hello come parametri. Tabella di database hello toocreate non è necessario tuttavia. che l'applicazione streaming Spark Hello creata.

Aprire un prompt dei comandi, passare toohello directory in cui è installato CURL ed eseguire hello comando seguente:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Hello parametri nel file hello **inputSQL.txt** sono definite come segue:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

tooverify che hello applicazione viene eseguita correttamente, è possibile connettersi a database SQL di Azure toohello utilizzando SQL Server Management Studio. Per istruzioni su come toodo che, vedere [connettersi tooSQL Database con SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md). Dopo avere connesso toohello database, è possibile passare toohello **EventContent** tabella in cui è stata creata da hello streaming dell'applicazione. È possibile eseguire dei dati di query rapida tooget hello dalla tabella hello. Eseguire hello seguente query:

    SELECT * FROM EventCount

Verrà visualizzato il seguente toohello simili di output:

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <a name="seealso"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)
* [Design of Receiver-based Connection and Direct DStream](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creare ed eseguire applicazioni
* [Creare un'applicazione autonoma con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Eseguire processi in modalità remota in un cluster Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Strumenti ed estensioni
* [Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
