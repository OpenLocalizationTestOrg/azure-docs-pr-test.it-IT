---
title: argomenti di Apache Kafka aaaMirror - HDInsight di Azure | Documenti Microsoft
description: "Informazioni su come mirroring toouse Apache Kafka funzionalità toomaintain una replica di un Kafka nel cluster HDInsight dal mirroring del cluster secondario tooa di argomenti."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a>Utilizzare gli argomenti di Apache Kafka tooreplicate MirrorMaker con Kafka in HDInsight (anteprima)

Informazioni su come toouse Kafka Apache del mirroring del cluster secondario tooa funzionalità tooreplicate argomenti. Il mirroring può essere eseguito come un processo continuo o utilizzato in modo intermittente come metodo di migrazione dei dati da un cluster tooanother.

In questo esempio, il mirroring è tooreplicate utilizzati argomenti tra due cluster HDInsight. Entrambi i cluster sono in una rete virtuale di Azure in hello stessa area.

> [!WARNING]
> Il mirroring non deve essere considerato come una tolleranza di errore indica tooachieve. Hello tooitems offset all'interno di un argomento sono le differenze tra i cluster di origine e destinazione hello, pertanto i client non è possibile utilizzare hello due in modo intercambiabile.
>
> Se si teme la tolleranza di errore, è necessario impostare la replica per argomenti hello all'interno del cluster. Per altre informazioni, vedere [Introduzione a Kafka in HDInsight](hdinsight-apache-kafka-get-started.md).

## <a name="how-kafka-mirroring-works"></a>Funzionamento del mirroring di Kafka

Funzionamento del mirroring utilizzando hello MirrorMaker strumento (parte di Apache Kafka) tooconsume registra dagli argomenti su cluster di origine hello e quindi crea una copia locale nel cluster di destinazione hello. MirrorMaker utilizza (almeno) *consumer* che letti dal cluster di origine, hello e una *producer* che scrive cluster locale (destinazione) toohello.

Hello seguente diagramma illustra il processo di Mirroring hello:

![Diagramma del processo di mirroring hello](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

Apache Kafka in HDInsight non forniscono accesso toohello servizio Kafka hello rete internet pubblica. Produttori di Kafka o i consumer devono trovarsi nella hello stessa rete virtuale come nodi cluster Kafka hello hello. In questo esempio hello origine Kafka sia quelli di destinazione si trovano in una rete virtuale di Azure. Hello diagramma seguente illustra il flusso delle comunicazioni tra i cluster hello:

![Diagramma dei cluster Kafka di origine e destinazione in una rete virtuale di Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

cluster di origine e destinazione Hello può essere diverso in numero hello dei nodi e delle partizioni e offset all'interno degli argomenti hello sono diversi. Il mirroring gestisce valore hello chiave utilizzato per il partizionamento, in modo viene mantenuto l'ordine di record in una base per ogni chiave.

### <a name="mirroring-across-network-boundaries"></a>Mirroring tra i limiti di rete

Se è necessario toomirror tra cluster Kafka in reti diverse, esistono hello considerazioni aggiuntive seguenti:

* **Gateway**: reti hello devono essere in grado di toocommunicate in hello livello TCPIP.

* **Risoluzione dei nomi**: hello Kafka cluster in ogni rete deve essere in grado di tooconnect tooeach altri usando i nomi host. Tale operazione potrebbe richiedere un server di sistema DNS (Domain Name) in ogni rete che viene configurato tooforward richieste toohello altre reti.

    Quando si crea una rete virtuale di Azure, anziché utilizzare hello che automatica DNS fornito con la rete hello, è necessario specificare un personalizzato DNS server hello indirizzo IP e per server hello. Dopo aver hello che rete virtuale è stata creata, è necessario quindi creare una macchina virtuale di Azure che utilizza tale indirizzo IP, quindi installare e configurare software DNS su di esso.

    > [!WARNING]
    > Creare e configurare un server DNS personalizzato hello prima di installare HDInsight in hello rete virtuale. Non sussiste alcuna configurazione aggiuntiva necessaria per il server DNS di HDInsight toouse hello configurato per la rete virtuale hello.

Per altre informazioni sulla connessione di due reti virtuali di Azure, vedere [Configurare una connessione da rete virtuale a rete virtuale](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

## <a name="create-kafka-clusters"></a>Creare cluster Kafka

È possibile creare una rete virtuale di Azure e Kafka cluster manualmente, ma è più facile toouse un modello di gestione risorse di Azure. Utilizzare hello seguendo i passaggi toodeploy una rete virtuale di Azure e due Kafka cluster tooyour sottoscrizione di Azure.

1. Utilizzare hello seguente pulsante toosign in tooAzure e modello hello Apri nel portale di Azure hello.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello Azure Resource Manager modello si trova in **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > disponibilità tooguarantee Kafka in HDInsight, il cluster deve contenere almeno tre nodi di lavoro. Questo modello crea un cluster Kafka contenente tre nodi di lavoro.

2. Hello utilizzare seguendo le voci di informazioni toopopulate hello hello **distribuzione personalizzata** pannello:
    
    ![Distribuzione personalizzata di HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * **Gruppo di risorse**: creare un gruppo o selezionarne uno esistente. Questo gruppo contiene cluster HDInsight hello.

    * **Percorso**: selezionare un tooyou geograficamente Chiudi percorso.
     
    * **Nome del Cluster di base**: questo valore viene utilizzato come nome base hello hello Kafka cluster. Se ad esempio si immette **hdi** verranno creati cluster denominati **source-hdi** e **dest-hdi**.

    * **Nome utente di accesso del cluster**: nome utente amministratore di hello per hello origine e destinazione Kafka cluster.

    * **Password di account di accesso cluster**: cluster Kafka password dell'utente admin hello per hello origine e di destinazione.

    * **Nome utente SSH**: cluster Kafka hello SSH utente toocreate per hello origine e di destinazione.

    * **Password SSH**: cluster Kafka password hello per utente SSH hello hello origine e di destinazione.

3. Hello lettura **termini e condizioni**, quindi selezionare **accetto le condizioni indicate in precedenza toohello**.

4. Infine, controllare **Pin toodashboard** e quindi selezionare **acquisto**. Sono necessari circa 20 minuti toocreate cluster hello.

Dopo avere create le risorse di hello, verrà reindirizzato tooa pannello per gruppo di risorse hello che contiene i cluster hello e dashboard web.

![Pannello di gruppo di risorse per la rete virtuale hello e cluster](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> Si noti che sono nomi hello dei cluster HDInsight hello **origine BASENAME** e **dest BASENAME**, dove BASENAME è nome hello toohello modello specificato. Utilizzare questi nomi nei passaggi successivi per la connessione toohello cluster.

## <a name="create-topics"></a>Creare argomenti

1. Connettersi toohello **origine** cluster tramite SSH:

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    Sostituire **sshuser** con nome dell'utente SSH hello utilizzato durante la creazione di cluster hello. Sostituire **BASENAME** con il nome di base hello utilizzato durante la creazione di cluster hello.

    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Seguente hello utilizzare comandi toofind hello Zookeeper host del cluster di origine hello:

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. È stato creato hello utilizzare tooverify comando che hello argomento seguente:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    risposta Hello contiene `testtopic`.

4. Hello di utilizzare le seguenti informazioni di tooview hello Zookeeper host per questo (hello **origine**) cluster:

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    Restituisce toohello di informazioni simili seguente testo:

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    Salvare queste informazioni. Viene usato nella sezione successiva hello.

## <a name="configure-mirroring"></a>Configurare il mirroring

1. Connettersi toohello **destinazione** utilizzando una sessione SSH diversa del cluster:

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    Sostituire **sshuser** con nome dell'utente SSH hello utilizzato durante la creazione di cluster hello. Sostituire **BASENAME** con il nome di base hello utilizzato durante la creazione di cluster hello.

    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Comando che segue di hello utilizzare toocreate un `consumer.properties` file che descrive come toocommunicate con hello **origine** cluster:

    ```bash
    nano consumer.properties
    ```

    Hello utilizzo successivo di testo come contenuto di hello di hello `consumer.properties` file:

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    Sostituire **SOURCE_ZKHOSTS** con hello Zookeeper ospita informazioni da hello **origine** cluster.

    Questo file descrive hello consumer informazioni toouse durante la lettura dall'origine hello cluster Kafka. Per altre informazioni sulla configurazione dei consumer, vedere [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) (Configurazione di consumer) in kafka.apache.org.

    file hello toosave, usare **Ctrl + X**, **Y**e quindi **invio**.

3. Prima di configurare producer hello che comunica con i cluster di destinazione hello, deve trovare broker hello host per hello **destinazione** cluster. Utilizzare queste informazioni di hello tooretrieve i comandi seguenti:

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    Sostituire `$PASSWORD` con password di account (amministratore) hello account di accesso per il cluster hello.

    Sostituire `$CLUSTERNAME` con nome hello del cluster di destinazione hello.

    Questi comandi restituiscono informazioni simili che seguono di toohello:

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. Hello utilizzare seguente toocreate un `producer.properties` file che descrive come toocommunicate con hello **destinazione** cluster:

    ```bash
    nano producer.properties
    ```

    Hello utilizzo successivo di testo come contenuto di hello di hello `producer.properties` file:

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    Sostituire **DEST_BROKERS** con informazioni di Service broker hello del passaggio precedente hello.

    Per altre informazioni sulla configurazione dei producer, vedere [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) (Configurazione di producer) in kafka.apache.org.

## <a name="start-mirrormaker"></a>Avviare MirrorMaker

1. Da hello SSH connessione toohello **destinazione** cluster, utilizzare hello comando toostart hello MirrorMaker processo:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    Hello parametri in questo esempio vengono utilizzati:

    * **-consumer.config**: Specifica il file hello che contiene le proprietà di consumer. Queste proprietà sono utilizzate toocreate un consumer che legge da hello *origine* cluster Kafka.

    * **-producer.config**: Specifica il file hello che contiene le proprietà di producer. Queste proprietà sono utilizzate toocreate un produttore che scrive toohello *destinazione* cluster Kafka.

    * **-whitelist**: un elenco di argomenti che vengono replicate MirrorMaker hello origine cluster toohello destinazione.

    * **-num.streams**: hello svariate toocreate thread consumer.

 All'avvio, MirrorMaker restituisce toohello di informazioni simili seguente testo:

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. Da hello SSH connessione toohello **origine** cluster, utilizzare hello successivo comando toostart un produttore di inviare l'argomento toohello messaggi:

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    Sostituire `$PASSWORD` con password di accesso (amministrazione) hello per cluster di origine hello.

    Sostituire `$CLUSTERNAME` con nome hello del cluster di origine di hello.

     Quando si arriva a una riga vuota con un cursore, digitare alcuni messaggi di testo. Questi vengono inviati toohello argomento sul hello **origine** cluster. Al termine, utilizzare **Ctrl + C** processo producer di hello tooend.

3. Da hello SSH connessione toohello **destinazione** cluster, utilizzare **Ctrl + C** hello tooend MirrorMaker processo. Quindi seguito hello utilizzare i comandi che hello tooverify `testtopic` argomento è stato creato, e i dati di argomento hello è stata replicata toothis mirror:

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    Sostituire `$PASSWORD` con password di accesso (amministrazione) hello per cluster di destinazione hello.

    Sostituire `$CLUSTERNAME` con nome hello del cluster di destinazione hello.

    Hello elenco di argomenti include ora `testtopic`, che viene creato quando MirrorMaster rispecchia argomento hello hello origine cluster toohello destinazione. messaggi Hello recuperati dall'argomento hello sono hello identico a quello immesso nel cluster di origine hello.

## <a name="delete-hello-cluster"></a>Eliminare il cluster hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Poiché i passaggi di hello in questo documento crea entrambi i cluster in hello nello stesso gruppo di risorse di Azure, è possibile eliminare il gruppo di risorse hello in hello portale di Azure. Eliminazione gruppo di risorse hello rimuove tutte le risorse create eseguendo questo documento, hello rete virtuale di Azure e l'account di archiviazione utilizzato dal cluster hello.

## <a name="next-steps"></a>Passaggi successivi

In questo documento è stato descritto come toouse MirrorMaker toocreate una replica di un Kafka del cluster. Utilizzare hello seguendo i collegamenti toodiscover toowork altri modi con Kafka:

* [Documentazione su Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) in cwiki.apache.org.
* [Introduzione ad Apache Kafka (anteprima) in HDInsight](hdinsight-apache-kafka-get-started.md)
* [Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Usare Apache Spark con Kafka in HDInsight)
* [Usare Apache Storm (anteprima) con Kafka in HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Connettersi tooKafka tramite una rete virtuale di Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
