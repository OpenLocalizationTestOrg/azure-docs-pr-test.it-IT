---
title: aaaStart con Apache Kafka - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toocreate un Kafka Apache cluster in Azure HDInsight. Informazioni su come toocreate argomenti, i sottoscrittori e i consumer.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a>Iniziare a usare Apache Kafka (anteprima) in HDInsight

Informazioni su come toocreate e utilizzare un [Kafka Apache](https://kafka.apache.org) cluster in Azure HDInsight. Kafka è una piattaforma di streaming distribuita open source disponibile con HDInsight. Viene spesso usato come broker di messaggi, che fornisce funzionalità simili tooa pubblicazione-sottoscrizione coda di messaggi.

> [!NOTE]
> Con HDInsight sono attualmente disponibili due versioni di Kafka: 0.9.0 (HDInsight 3.4) e 0.10.0 (HDInsight 3.5 e 3.6). passaggi di Hello in questo documento si presuppongono che si stanno utilizzando Kafka 3.6 di HDInsight.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a>Creare un cluster Kafka

Utilizzare hello seguendo i passaggi toocreate un Kafka cluster HDInsight:

1. Da hello [portale di Azure](https://portal.azure.com)selezionare **+ nuovo**, **Intelligence + Analitica**, quindi selezionare **HDInsight**.
   
    ![Creazione di un cluster HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. Da **nozioni di base**, immettere hello le seguenti informazioni:

    * **Nome del cluster**: nome hello del cluster HDInsight hello.
    * **Sottoscrizione**: selezionare hello toouse di sottoscrizione.
    * **Nome utente account di accesso del cluster** e **password dell'account di accesso Cluster**: accesso hello quando si accede a cluster hello tramite HTTPS. Usare questi servizi tooaccess credenziali, ad esempio hello dell'interfaccia utente Web Ambari o l'API REST.
    * **Secure Shell (SSH) username**: hello account di accesso quando si accede a cluster hello su SSH. Per impostazione predefinita la password di hello è hello come password di accesso cluster hello.
    * **Gruppo di risorse**: hello gruppo toocreate hello cluster della risorsa in.
    * **Percorso**: hello Azure area toocreate hello cluster.
   
 ![Selezionare la sottoscrizione](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. Selezionare **Cluster tipo**, e quindi set hello seguendo i valori da **configurazione Cluster**:
   
    * **Tipo di cluster**: Kafka

    * **Versione**: Kafka 0.10.0 (HDI 3.6)

    * **Livello cluster**: Standard
     
 Infine, utilizzare hello **selezionare** pulsante toosave impostazioni.
     
 ![Selezionare il tipo di cluster](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. Dopo aver selezionato il tipo di cluster hello, utilizzare hello __selezionare__ tooset hello cluster tipo di pulsante. Successivamente, utilizzare hello __Avanti__ configurazione di base toofinish pulsante.

5. In **Archiviazione** selezionare o creare un account di archiviazione. Per i passaggi hello in questo documento, lasciare hello altri campi valori predefiniti di hello. Hello utilizzare __Avanti__ configurazione dell'archiviazione toosave pulsante.

    ![Configurare le impostazioni di account di archiviazione hello per HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. Da __applicazioni (facoltative)__selezionare __Avanti__ toocontinue. Non sono richieste applicazioni per questo esempio.

7. Da __dimensioni del Cluster__selezionare __Avanti__ toocontinue.

    > [!WARNING]
    > disponibilità tooguarantee Kafka in HDInsight, il cluster deve contenere almeno tre nodi di lavoro.

    ![Set hello dimensione del cluster Kafka](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > Hello **dischi per ogni nodo del lavoro** controlli voce hello scalabilità di Kafka in HDInsight. Per altre informazioni, vedere [Configurare l'archiviazione e la scalabilità per Apache Kafka in HDInsight](hdinsight-apache-kafka-scalability.md).

8. Da __impostazioni avanzate__selezionare __Avanti__ toocontinue.

9. Da hello **riepilogo**, esaminare la configurazione hello per cluster hello. Hello utilizzare __modifica__ collegamenti toochange eventuali impostazioni non sono corrette. Infine, utilizzare the__Create__ pulsante toocreate hello cluster.
   
    ![Riepilogo della configurazione del cluster](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > Può richiedere di cluster hello toocreate di too20 minuti.

## <a name="connect-toohello-cluster"></a>Connettere il cluster toohello

> [!IMPORTANT]
> Quando si esegue hello alla procedura seguente, è necessario utilizzare un client SSH. Per ulteriori informazioni, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

Dal client, usare SSH tooconnect toohello cluster:

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

Sostituire **SSHUSER** con il nome utente SSH hello fornito durante la creazione del cluster. Sostituire **CLUSTERNAME** con nome hello del cluster di hello.

Quando richiesto, immettere la password di hello utilizzati per hello account SSH.

Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="getkafkainfo"></a>Ottenere informazioni di host hello Zookeeper e Service Broker

Quando si lavora con Kafka, è necessario conoscere i due valori di host. Hello *Zookeeper* host e hello *Broker* host. Questi host vengono utilizzati con l'API Kafka hello e molte delle utilità hello forniti con Kafka.

Utilizzare hello seguenti variabili di ambiente toocreate passaggi che contengono informazioni sull'host hello. Queste variabili di ambiente vengono utilizzate nei passaggi hello in questo documento.

1. Da un cluster di toohello connessione SSH, seguente hello utilizzare comandi hello tooinstall `jq` utilità. Questa utilità è tooparse utilizzati documenti JSON ed è utile per il recupero di informazioni sull'host di Service broker hello:
   
    ```bash
    sudo apt -y install jq
    ```

2. le variabili di ambiente hello tooset con le informazioni recuperate dai Ambari, hello di utilizzare i comandi seguenti:

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > Impostare `CLUSTERNAME=` toohello nome di cluster Kafka hello. Impostare `PASSWORD=` password di accesso (amministrazione) toohello utilizzato per la creazione di cluster hello.

    testo Hello è riportato un esempio del contenuto di hello di `$KAFKAZKHOSTS`:
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    testo Hello è riportato un esempio del contenuto di hello di `$KAFKABROKERS`:
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > Hello `cut` comando è elenco hello tootrim utilizzato di voci di host tootwo host. Elenco completo di hello tooprovide degli host non è necessario quando si crea un consumer Kafka o il produttore.
   
    > [!WARNING]
    > Non fare affidamento su hello le informazioni restituite da questa sessione tooalways sia accurato. Se si modifica la scala cluster hello, nuovo Broker vengono aggiunti o rimossi. Se si verifica un errore e viene sostituito un nodo, il nome host hello per nodo hello potrebbe cambiare.
    >
    > È necessario recuperare informazioni di host Zookeeper e broker hello poco prima di utilizzare tooensure si dispone di informazioni valide.

## <a name="create-a-topic"></a>Creare un argomento

Kafka archivia i flussi di dati in categorie denominate *argomenti*. Da un SSH connessione tooa nodo head cluster, utilizzare uno script fornito con Kafka toocreate un argomento:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

Questo comando si connette utilizzando hello host informazioni archiviate in tooZookeeper `$KAFKAZKHOSTS`e quindi creare l'argomento Kafka denominato **test**. È possibile verificare che tale argomento hello è stato creato utilizzando i seguenti argomenti toolist script hello:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

Hello output di questo comando Elenca argomenti Kafka, che contiene hello **test** argomento.

## <a name="produce-and-consume-records"></a>Produrre e utilizzare record

Kafka archivia i *record* negli argomenti. I record vengono prodotti da *producer* e usati da *consumer*. I producer recuperano i record da *broker* di Kafka. Ogni nodo del ruolo di lavoro nel cluster HDInsight è un broker Kafka.

Utilizzare i seguenti record di toostore passaggi nell'argomento di prova hello creato in precedenza e quindi leggerli utilizzando un consumer hello:

1. Dalla sessione SSH hello, usare uno script fornito con l'argomento di toohello Kafka toowrite record:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    Non vengono restituiti toohello prompt dei comandi dopo questo comando. Digitare alcuni messaggi di testo e quindi utilizzare **Ctrl + C** toostop invio toohello argomento. Ogni riga viene inviata come record distinto.

2. Utilizzare uno script fornito con i record di tooread Kafka dall'argomento hello:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    Questo comando recupera i record di hello dall'argomento hello e li visualizza. Utilizzando `--from-beginning` indica hello consumer toostart dall'inizio di hello del flusso di hello, pertanto vengono recuperati tutti i record.

3. Utilizzare __Ctrl + C__ consumer hello toostop.

## <a name="producer-and-consumer-api"></a>API per producer e consumer

È possibile anche a livello di codice producono e utilizzano i record mediante hello [Kafka API](http://kafka.apache.org/documentation#api). toobuild un produttore di Java e i consumer, utilizzare hello seguendo i passaggi nell'ambiente di sviluppo.

> [!IMPORTANT]
> È necessario che i seguenti componenti installati nell'ambiente di sviluppo hello:
>
> * [Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o equivalente, ad esempio OpenJDK.
>
> * [Apache Maven](http://maven.apache.org/)
>
> * Un client SSH e hello `scp` comando. Per ulteriori informazioni, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

1. Scaricare esempi hello da [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started). Ad esempio di tipo produttore/consumer hello, utilizzare il progetto di hello in hello `Producer-Consumer` directory. In questo esempio contiene hello le seguenti classi:
   
    * **Eseguire** -avvia consumer hello o produttori.

    * **Producer** -archivi 1.000.000 record toohello argomento.

    * **Consumer** -legge i record da un argomento di hello.

2. un pacchetto, jar toocreate posizionarsi directory toohello di hello `Producer-Consumer` directory e utilizzare hello comando seguente:

    ```
    mvn clean package
    ```

    Questo comando crea una directory denominata `target`, che contiene un file denominato `kafka-producer-consumer-1.0-SNAPSHOT.jar`.

3. Seguente hello utilizzare comandi hello toocopy `kafka-producer-consumer-1.0-SNAPSHOT.jar` cluster HDInsight tooyour di file:
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    Sostituire **SSHUSER** con utente SSH hello per il cluster, quindi sostituire **CLUSTERNAME** con nome hello del cluster. Quando richiesto immettere la password di hello hello SSH utente.

4. Una volta hello `scp` comando al termine della copia del file hello, connettere il cluster toohello tramite SSH. Utilizzare hello comando toowrite record toohello test argomento:

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. Al termine il processo di hello, utilizzare hello successivo comando tooread dall'argomento hello:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    record di Hello letti, insieme a un conteggio di record, viene visualizzato. È possibile visualizzare alcuni maggiore di 1.000.000 registrati come argomento di toohello record diversi tramite uno script in un passaggio precedente è stata inviata.

6. Utilizzare __Ctrl + C__ consumer hello tooexit.

### <a name="multiple-consumers"></a>Consumer multipli

I consumer Kafka usano un gruppo di consumer durante la lettura dei record. Utilizzo hello stessa raggruppamento con più consumer risultati carico bilanciato legge da un argomento. Nel gruppo hello ogni consumer riceve una parte del record di hello. toosee il processo, utilizzare hello seguendo i passaggi:

1. Aprire un nuovo SSH sessione toohello cluster, in modo da disporre di due di essi. In ogni sessione, utilizzare hello seguenti toostart un consumer con hello stesso ID di gruppo di consumer:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    Questo comando avvia un consumer con ID gruppo hello `mygroup`.

    > [!NOTE]
    > Utilizzare i comandi di hello in hello [informazioni hello Zookeeper e Broker host](#getkafkainfo) tooset sezione `$KAFKABROKERS` per questa sessione SSH.

2. Osservare come i record di hello conteggi ogni sessione ricevuti da un argomento di hello. Totale Hello di entrambe le sessioni deve hello stesso come ricevuto in precedenza da un consumer.

Consumo client all'interno dello stesso gruppo viene gestito tramite le partizioni di hello per argomento hello hello. Per hello `test` argomento creato in precedenza, include otto partizioni. Se si apre otto sessioni SSH e avvia un consumer in tutte le sessioni, ogni consumer legge i record da una singola partizione per l'argomento hello.

> [!IMPORTANT]
> Un gruppo di consumer non può contenere un numero di istanze di consumer maggiore del numero di partizioni. In questo esempio, un gruppo di consumer può contenere i consumatori tooeight poiché questo è il numero di hello di partizioni nell'argomento hello. In alternativa è possibile avere più gruppi di consumer, ognuno con al massimo otto consumer.

Record archiviati in Kafka vengono archiviati in ordine di hello che vengono ricevuti all'interno di una partizione. tooachieve nell'ordine di recapito per i record *all'interno di una partizione*, creare un gruppo di consumer in cui il numero di hello di istanze di consumer corrisponde numero hello di partizioni. tooachieve nell'ordine di recapito per i record *in argomento hello*, creare un gruppo di consumer con l'istanza di un solo consumer.

## <a name="streaming-api"></a>API di streaming

Hello streaming API tooKafka è stato aggiunto nella versione 0.10.0; le versioni precedenti si basano su Apache Spark o Storm per l'elaborazione del flusso.

1. Se non già stato fatto, scaricare gli esempi di hello da [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour ambiente di sviluppo. Per hello lo streaming di esempio, utilizzare il progetto di hello in hello `streaming` directory.
   
    Questo progetto contiene solo una classe, `Stream`, che legge i record da hello `test` argomento creato in precedenza. Conteggi parole hello leggere e genera ogni argomento tooa conteggio delle parole e denominato `wordcounts`. Hello `wordcounts` argomento viene creato in un passaggio successivo in questa sezione.

2. Dalla riga di comando hello nell'ambiente di sviluppo, modificare il percorso di directory toohello di hello `Streaming` directory, quindi utilizzare hello comando toocreate un pacchetto di file jar seguenti:

    ```bash
    mvn clean package
    ```

    Questo comando crea una directory denominata `target`, che contiene un file denominato `kafka-streaming-1.0-SNAPSHOT.jar`.

3. Seguente hello utilizzare comandi hello toocopy `kafka-streaming-1.0-SNAPSHOT.jar` cluster HDInsight tooyour di file:
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    Sostituire **SSHUSER** con utente SSH hello per il cluster, quindi sostituire **CLUSTERNAME** con nome hello del cluster. Quando richiesto immettere la password di hello hello SSH utente.

4. Una volta hello `scp` comando al termine della copia del file hello, connettere il cluster toohello tramite SSH e quindi usare hello successivo comando toocreate hello `wordcounts` argomento:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. Successivamente, avviare hello streaming processo utilizzando hello comando seguente:
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    Questo comando avvia il flusso di processo in background hello hello.

6. Comando che segue di hello utilizzare toosend messaggi toohello `test` argomento. Questi messaggi vengono elaborati da hello lo streaming di esempio:
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. Hello Usa seguenti output di hello tooview comando che viene scritto toohello `wordcounts` argomento dal processo di streaming hello:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > dati hello tooview, è necessario indicare hello consumer tooprint hello chiave e hello deserializzatore toouse per hello chiave e il valore. nome della chiave Hello è parola hello e valore di chiave hello contiene il conteggio di hello.
   
    Hello l'output è simile toohello seguente testo:
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > conteggio Hello viene incrementato ogni volta che viene rilevata una parola.

7. Utilizzare hello __Ctrl + C__ tooexit hello consumer, quindi utilizzare hello `fg` comando toobring hello streaming in primo piano toohello indietro delle attività in background. Utilizzare __Ctrl + C__ tooexit viene anche.

## <a name="delete-hello-cluster"></a>Eliminare il cluster hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Risoluzione dei problemi

Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Passaggi successivi

In questo documento, si sono appreso hello nozioni fondamentali sulle operazioni con Apache Kafka in HDInsight. Utilizzare hello toolearn più informazioni sull'utilizzo di Kafka seguenti:

* [Garantire la disponibilità elevata dei dati con Kafka in HDInsight](hdinsight-apache-kafka-high-availability.md)
* [Aumentare la scalabilità configurando dischi gestiti con Kafka in HDInsight](hdinsight-apache-kafka-scalability.md)
* [Documentazione di Apache Kafka](http://kafka.apache.org/documentation.html) in kafka.apache.org.
* [Utilizzare MirrorMaker toocreate una replica di Kafka in HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Usare Apache Storm (anteprima) con Kafka in HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Usare Apache Spark con Kafka in HDInsight)
* [Connettersi tooKafka tramite una rete virtuale di Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
