---
title: aaaUse Kafka Apache con Storm in HDInsight - Azure | Documenti Microsoft
description: Apache Kafka viene installato con Apache Storm in HDInsight. Informazioni su come toowrite tooKafka e quindi leggere da essa, utilizzando hello KafkaBolt e KafkaSpout componenti forniti Storm. E inoltre come toouse hello luminoso framework toodefine e inviare le topologie di Storm.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a>Usare Apache Kafka (anteprima) con Storm in HDInsight

Informazioni su come toouse Apache Storm tooread da e scrittura tooApache Kafka. Questo esempio viene illustrato come toosave di dati da un toohello topologia Storm compatibile HDFS file di sistema utilizzate da HDInsight.

> [!NOTE]
> procedura di Hello in questo documento consente di creare un gruppo di risorse di Azure che contiene sia una tempesta di HDInsight e un Kafka nel cluster HDInsight. Questi cluster sono entrambi contenuti all'interno di una rete virtuale di Azure, che consente di hello toodirectly cluster Storm comunicare hello cluster Kafka.
> 
> Al termine con i passaggi di hello in questo documento, tenere presente toodelete hello cluster tooavoid in eccesso addebiti.

## <a name="get-hello-code"></a>Ottenere il codice hello

codice Hello ad esempio hello utilizzato in questo documento è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).

toocompile questo progetto, è necessario hello seguente configurazione per l'ambiente di sviluppo:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versione successiva. Per HDInsight 3.5 o una versione successiva è necessario Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

* Un client SSH (è necessario hello `ssh` e `scp` comandi): per informazioni, vedere [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Un editor di testo o ambiente IDE.

Hello seguenti variabili di ambiente possono essere impostate durante l'installazione di Java e hello JDK nella workstation di sviluppo. Tuttavia, è necessario verificare che esistano e che contengono i valori corretti di hello per il sistema.

* `JAVA_HOME`-deve puntare toohello directory in cui hello JDK è installato.
* `PATH`-deve contenere hello seguenti percorsi:
  
    * `JAVA_HOME`(o percorso equivalente hello).
    * `JAVA_HOME\bin`(o percorso equivalente hello).
    * directory di Hello in cui è installato Maven.

## <a name="create-hello-clusters"></a>Creare il cluster hello

Apache Kafka in HDInsight non forniscono accesso toohello Kafka Broker hello rete internet pubblica. Tutto ciò che deve essere tooKafka discussioni hello stessa rete virtuale come nodi di hello hello cluster Kafka. In questo esempio hello Kafka sia cluster Storm si trovano in una rete virtuale di Azure. Hello diagramma seguente illustra il flusso delle comunicazioni tra i cluster hello:

![Diagramma dei cluster Storm e Kafka in una rete virtuale di Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> Ad esempio SSH e Ambari sia accessibile tramite altri servizi in cluster hello hello internet. Per ulteriori informazioni sulle porte pubbliche hello disponibili con HDInsight, vedere [porte e gli URI utilizzato da HDInsight](hdinsight-hadoop-port-settings-for-services.md).

È possibile creare una rete virtuale di Azure, Kafka, e Storm cluster manualmente, ma è più facile toouse un modello di gestione risorse di Azure. Utilizzare hello seguenti passaggi viene toodeploy una rete virtuale di Azure, Kafka, e Storm cluster tooyour sottoscrizione di Azure.

1. Utilizzare hello seguente pulsante toosign in tooAzure e modello hello Apri nel portale di Azure hello.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello Azure Resource Manager modello si trova in **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**. Crea hello seguenti risorse:
    
    * Gruppo di risorse di Azure
    * Rete virtuale di Azure
    * Account di archiviazione di Azure
    * Kafka in HDInsight versione 3.6 con tre nodi di lavoro
    * Storm in HDInsight versione 3.6 con tre nodi di lavoro

  > [!WARNING]
  > disponibilità tooguarantee Kafka in HDInsight, il cluster deve contenere almeno tre nodi di lavoro. Questo modello crea un cluster Kafka contenente tre nodi di lavoro.

2. Hello utilizzare seguendo le voci di informazioni aggiuntive toopopulate hello hello **distribuzione personalizzata** pannello:
   
    ![Distribuzione personalizzata di HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * **Gruppo di risorse**: creare un gruppo o selezionarne uno esistente. Questo gruppo contiene cluster HDInsight hello.
   
    * **Percorso**: selezionare un tooyou geograficamente Chiudi percorso.

    * **Nome del Cluster di base**: questo valore viene utilizzato come nome di base per i cluster Storm e Kafka hello hello. Ad esempio, se si immette **hdi** viene creato un cluster Storm denominato **storm-hdi** e un cluster Kafka denominato **kafka-hdi**.
   
    * **Nome utente di accesso del cluster**: nome utente amministratore di hello per i cluster Storm e Kafka hello.
   
    * **Password di account di accesso cluster**: password dell'utente per i cluster Storm e Kafka hello hello admin.
    
    * **Nome utente SSH**: hello toocreate utente SSH per i cluster Storm e Kafka hello.
    
    * **Password SSH**: password hello per utente SSH hello per i cluster Storm e Kafka hello.

3. Hello lettura **termini e condizioni**, quindi selezionare **accetto le condizioni indicate in precedenza toohello**.

4. Infine, controllare **Pin toodashboard** e quindi selezionare **acquisto**. Sono necessari circa 20 minuti toocreate cluster hello.

Dopo avere create le risorse di hello, viene visualizzato il pannello hello per il gruppo di risorse hello.

![Pannello di gruppo di risorse per la rete virtuale hello e cluster](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> Si noti che sono nomi hello dei cluster HDInsight hello **storm BASENAME** e **kafka BASENAME**, dove BASENAME è nome hello toohello modello specificato. Utilizzare questi nomi nei passaggi successivi per la connessione toohello cluster.

## <a name="understanding-hello-code"></a>Informazioni sul codice hello

Questo progetto contiene due topologie:

* **KafkaWriter**: definito da hello **writer.yaml** file, questa topologia scrive tooKafka frasi casuale usando hello KafkaBolt fornito con Apache Storm.

    Questa topologia viene utilizzato un oggetto personalizzato **SentenceSpout** frasi casuale toogenerate di componente.

* **KafkaReader**: definito da hello **reader.yaml** file, questa topologia legge i dati da Kafka utilizzando hello KafkaSpout fornito con Apache Storm quindi registri hello toostdout di dati.

    Questa topologia utilizza l'archiviazione toodefault hello Storm HdfsBolt toowrite dati per i cluster Storm hello.
### <a name="flux"></a>Flux

topologie di Hello vengono definite utilizzando [flusso](https://storm.apache.org/releases/1.1.0/flux.html). Flusso è stato introdotto in Storm 0.10 e consente di configurazione della topologia hello tooseparate dal codice hello. Per le topologie che usano framework luminoso hello, topologia hello è definita in un file YAML. file YAML Hello può essere incluso come parte della topologia hello. Può essere anche un file autonomo utilizzato quando si invia la topologia hello. Flux supporta anche la sostituzione delle variabili in fase di esecuzione, caratteristica che viene usata in questo esempio.

i seguenti parametri Hello vengono impostati in fase di esecuzione per queste topologie:

* `${kafka.topic}`: nome hello di hello Kafka argomento topologie hello lettura/scrittura a.

* `${kafka.broker.hosts}`: hello ospita tale hello Kafka di connessione eseguito. informazioni di Service broker Hello viene utilizzate dalle hello KafkaBolt tooKafka di scrittura.

* `${kafka.zookeeper.hosts}`: host hello in esecuzione Zookeeper in hello cluster Kafka.

Per altre informazioni sulle topologie di Flux, vedere [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="download-and-compile-hello-project"></a>Scaricare e compilare il progetto hello

1. In ambiente di sviluppo, scaricare il progetto hello da [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), aprire una riga di comando e modificare le directory toohello percorso sia stato scaricato il progetto hello.

2. Da hello **hdinsight-storm-java-kafka** directory seguenti hello utilizzare comandi progetto hello toocompile e creare un pacchetto per la distribuzione:

  ```bash
  mvn clean package
  ```

    processo del pacchetto Hello crea un file denominato `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.

3. Utilizzare hello seguenti comandi toocopy hello pacchetto tooyour Storm nel cluster HDInsight. Sostituire **USERNAME** con nome utente di hello SSH per il cluster hello. Sostituire **BASENAME** con nome base hello utilizzato per la creazione di cluster hello.

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    Quando richiesto, immettere la password di hello utilizzati durante la creazione di cluster hello.

## <a name="configure-hello-topology"></a>Configurare la topologia di hello

1. Utilizzare uno dei seguenti metodi toodiscover hello hello host di Service broker Kafka:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Hello Bash esempio si presuppone che `$CLUSTERNAME` contiene il nome di hello del cluster HDInsight hello. Presuppone anche che [jq](https://stedolan.github.io/jq/) sia installato. Quando richiesto, immettere la password di hello per account di accesso cluster hello.

    il valore di Hello restituito è simile toohello seguente testo:

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > Anche se possono essere presenti più di due host di Service broker per il cluster, non è necessario un elenco completo di tutti gli host tooclients tooprovide. È sufficiente specificarne uno o due.

2. Utilizzare uno dei seguenti host Kafka Zookeeper di metodi toodiscover hello hello:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Hello Bash esempio si presuppone che `$CLUSTERNAME` contiene il nome di hello del cluster HDInsight hello. Presuppone anche che [jq](https://stedolan.github.io/jq/) sia installato. Quando richiesto, immettere la password di hello per account di accesso cluster hello.

    il valore di Hello restituito è simile toohello seguente testo:

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > Anche se sono presenti più di due nodi Zookeeper, non è necessario un elenco completo di tutti gli host tooclients tooprovide. È sufficiente specificarne uno o due.

    Salvare questo valore, che verrà usato in un secondo momento.

3. Modifica hello `dev.properties` file nella directory radice del progetto hello hello. Aggiungere hello Broker e righe corrispondenti toohello Zookeeper host informazioni in questo file. Hello esempio seguente viene configurata utilizzando i valori di esempio hello nei passaggi precedenti hello:

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. Salvare hello `dev.properties` file, quindi utilizzare hello seguenti comando tooupload il cluster Storm toohello:

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    Sostituire **USERNAME** con nome utente di hello SSH per il cluster hello. Sostituire **BASENAME** con nome base hello utilizzato per la creazione di cluster hello.

## <a name="start-hello-writer"></a>Avvio del writer hello

1. Utilizzare hello seguente cluster Storm di toohello tooconnect tramite SSH. Sostituire **USERNAME** con nome dell'utente SSH hello utilizzato durante la creazione di cluster hello. Sostituire **BASENAME** con il nome di base hello utilizzato durante la creazione di cluster hello.

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    Quando richiesto, immettere la password di hello utilizzati durante la creazione di cluster hello.
   
    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Da hello connessione SSH, utilizzare hello comando toocreate hello argomento Kafka utilizzato dalla topologia hello seguente:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    Sostituire `$KAFKAZKHOSTS` con hello Zookeeper recuperato nella sezione precedente hello informazioni sull'host.

2. Da cluster Storm toohello di connessione SSH di hello, utilizzare hello topologia writer hello toostart di comando seguente:

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    Hello parametri utilizzati con questo comando sono:

    * `org.apache.storm.flux.Flux`: Utilizzare luminoso tooconfigure ed eseguire questa topologia.

    * `--remote`: Inviare tooNimbus topologia hello. topologia Hello viene distribuita tra i nodi di lavoro hello cluster hello.

    * `-R /writer.yaml`: Hello utilizzare `writer.yaml` topologia hello tooconfigure del file. `-R`indica che la risorsa è incluso nel file jar hello. È pertanto nella directory radice del file jar hello, hello `/writer.yaml` è tooit percorso hello.

    * `--filter`: Consente di popolare i hello `writer.yaml` topologia utilizzando valori hello `dev.properties` file. Ad esempio, hello valore hello `kafka.topic` voce nel file hello è hello tooreplace utilizzati `${kafka.topic}` voce nella definizione della topologia hello.

5. Una volta avviata la topologia hello, utilizzare hello tooverify comando scrive dati toohello argomento Kafka seguenti:

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    Sostituire `$KAFKAZKHOSTS` con hello Zookeeper recuperato nella sezione precedente hello informazioni sull'host.

    Questo comando Usa uno script fornito con l'argomento di hello toomonitor Kafka. Dopo qualche istante, deve iniziare restituzione casuale frasi che sono stati scritti toohello argomento. Hello l'output è simile toohello seguente esempio:

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    Utilizzare Ctrl + script hello toostop c.

## <a name="start-hello-reader"></a>Avviare il lettore hello

1. Da cluster hello SSH sessione toohello Storm utilizzare hello topologia lettore hello toostart di comando seguente:

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. Una volta avviata la topologia hello, aprire hello Storm UI. Questa interfaccia utente Web è disponibile all'indirizzo https://storm-BASENAME.azurehdinsight.net/stormui. Sostituire __BASENAME__ con il nome di base hello utilizzato al momento della creazione di cluster hello. 

    Quando richiesto, utilizzare nome account di accesso di amministratore hello (impostazione predefinita, `admin`) e la password utilizzati quando è stato creato il cluster di hello. Viene visualizzato un toohello simile a pagina web seguente immagine:

    ![Interfaccia utente di Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. Dall'interfaccia utente di Storm hello, selezionare hello __kafka lettore__ collegamento hello __topologia riepilogo__ sezione toodisplay informazioni hello __kafka lettore__ topologia.

    ![Nella sezione Riepilogo della topologia dell'interfaccia utente web di Storm hello](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. toodisplay informazioni sulle istanze di hello del componente di logger fulmine hello, seleziona hello __logger fulmine__ collegamento hello __bulloni (tutto il tempo)__ sezione.

    ![Logger fulmine collegamento nella sezione bulloni hello](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. In hello __executor__ , selezionare un collegamento in hello __porta__ registrazione toodisplay colonna informazioni su questa istanza del componente hello.

    ![Collegamento esecutori](./media/hdinsight-apache-storm-with-kafka/executors.png)

    log Hello contiene un registro dei dati di hello letti da hello argomento Kafka. informazioni Hello nel registro hello sono simile toohello seguente testo:

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a>Arrestare le topologie di hello

Da un cluster Storm toohello sessione SSH, utilizzare hello topologie di Storm hello toostop i comandi seguenti:

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a>Eliminare il cluster hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Poiché i passaggi di hello in questo documento crea entrambi i cluster in hello nello stesso gruppo di risorse di Azure, è possibile eliminare il gruppo di risorse hello in hello portale di Azure. Eliminazione gruppo di risorse hello rimuove tutte le risorse create seguendo questo documento.

## <a name="next-steps"></a>Passaggi successivi

Per altri esempi di topologie che possono essere usate con Storm in HDInsight, vedere [Esempi di topologie e componenti Storm per Apache Storm in HDInsight](hdinsight-storm-example-topology.md).

Per informazioni sulla distribuzione e sul monitoraggio di topologie in HDInsight basato su Linux, vedere [Distribuzione e gestione di topologie Apache Storm in HDInsight basato su Linux](hdinsight-storm-deploy-monitor-topology-linux.md).