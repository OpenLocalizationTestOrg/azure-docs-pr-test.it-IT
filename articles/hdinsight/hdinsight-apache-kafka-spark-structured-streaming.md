---
title: aaaApache Spark Streaming strutturati con Kafka - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come Apache Spark streaming (DStream) tooget dati in o da Apache Kafka toouse. In questo esempio i dati vengono trasmessi in streaming tramite un notebook Jupyter da Spark in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a>Usare lo streaming strutturato Spark con Kafka (anteprima) in HDInsight

Informazioni su come toouse Spark strutturati Streaming dati tooread Kafka Apache in Azure HDInsight.

Lo streaming strutturato Spark è un motore di elaborazione del flusso basato su Spark SQL. Consente di calcoli di streaming tooexpress hello stesso come il calcolo di batch in dati statici. Per ulteriori informazioni sui flussi strutturati, vedere hello [strutturati Streaming Guida per programmatori [alfa]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) in Apache.org.

> [!IMPORTANT]
> In questo esempio viene usato Spark 2.1 in HDInsight 3.6. Lo streaming strutturato è considerato __alfa__ in Spark 2.1.
>
> procedura di Hello in questo documento consente di creare un gruppo di risorse di Azure che contiene sia un Spark in HDInsight e un Kafka nel cluster HDInsight. Questi cluster sono entrambi contenuti all'interno di una rete virtuale di Azure, che consente di hello toodirectly cluster Spark comunicare hello cluster Kafka.
>
> Al termine con i passaggi di hello in questo documento, tenere presente toodelete hello cluster tooavoid in eccesso addebiti.

## <a name="create-hello-clusters"></a>Creare il cluster hello

Apache Kafka in HDInsight non forniscono accesso toohello Kafka Broker hello rete internet pubblica. Tutto ciò che deve essere tooKafka discussioni hello stessa rete virtuale come nodi di hello hello cluster Kafka. In questo esempio hello Kafka sia cluster Spark si trovano in una rete virtuale di Azure. Hello diagramma seguente illustra il flusso delle comunicazioni tra i cluster hello:

![Diagramma dei cluster Spark e Kafka in una rete virtuale di Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> servizio Kafka Hello è limitato toocommunication all'interno di rete virtuale hello. Altri servizi in cluster hello, ad esempio SSH e Ambari, accessibile tramite internet hello. Per ulteriori informazioni sulle porte pubbliche hello disponibili con HDInsight, vedere [porte e gli URI utilizzato da HDInsight](hdinsight-hadoop-port-settings-for-services.md).

È possibile creare una rete virtuale di Azure, Kafka e Spark cluster manualmente, ma è più facile toouse un modello di gestione risorse di Azure. Utilizzare hello seguenti passaggi viene toodeploy una rete virtuale di Azure, Kafka, e Spark cluster tooyour sottoscrizione di Azure.

1. Utilizzare hello seguente pulsante toosign in tooAzure e modello hello Apri nel portale di Azure hello.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello Azure Resource Manager modello si trova in **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.

    Questo modello consente di creare hello seguenti risorse:

    * Kafka nel cluster HDInsight 3.5.
    * Spark nel cluster HDInsight 3.6.
    * Una rete virtuale di Azure che contiene il cluster di HDInsight hello.

    > [!IMPORTANT]
    > Hello strutturati streaming blocco appunti utilizzato in questo esempio richiede Spark in HDInsight 3.6. Se si utilizza una versione precedente di Spark in HDInsight, si ricevono errori quando si utilizza notebook hello.

2. Hello utilizzare seguendo le voci di informazioni toopopulate hello hello **distribuzione personalizzata** pannello:
   
    ![Distribuzione personalizzata di HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Gruppo di risorse**: creare un gruppo o selezionarne uno esistente. Questo gruppo contiene cluster HDInsight hello.

    * **Percorso**: selezionare un tooyou geograficamente Chiudi percorso.

    * **Nome del Cluster di base**: questo valore viene utilizzato come nome di base per i cluster Spark e Kafka hello hello. Ad esempio, se si immette **hdi** viene creato un cluster Spark denominato spark-hdi e un cluster Kafka denominato **kafka-hdi**.

    * **Nome utente di accesso del cluster**: nome utente amministratore di hello per i cluster Spark e Kafka hello.

    * **Password di account di accesso cluster**: password dell'utente per i cluster Spark e Kafka hello hello admin.

    * **Nome utente SSH**: hello toocreate utente SSH per i cluster Spark e Kafka hello.

    * **Password SSH**: password hello per utente SSH hello per i cluster Spark e Kafka hello.

3. Hello lettura **termini e condizioni**, quindi selezionare **accetto le condizioni indicate in precedenza toohello**.

4. Infine, controllare **Pin toodashboard** e quindi selezionare **acquisto**. Sono necessari circa 20 minuti toocreate cluster hello.

Dopo avere create le risorse di hello, verrà reindirizzato toohello pannello gruppo della risorsa.

![Pannello di gruppo di risorse per la rete virtuale hello e cluster](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Si noti che sono nomi hello dei cluster HDInsight hello **spark BASENAME** e **kafka BASENAME**, dove BASENAME è nome hello toohello modello specificato. Utilizzare questi nomi nei passaggi successivi per la connessione toohello cluster.

## <a name="get-hello-kafka-brokers"></a>Ottenere hello Kafka Broker

codice in questo esempio Hello connette toohello Kafka gli host in cluster Kafka hello di Service broker. toofind hello host di Service broker Kafka, usare hello esempio PowerShell o Bash seguente:

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> In questo esempio prevede `$PASSWORD` password hello toocontain per account di accesso cluster hello e `$CLUSTERNAME` nome hello toocontain di hello cluster Kafka.
>
> Questo esempio viene utilizzato hello [jq](https://stedolan.github.io/jq/) dati tooparse utilità fuori documento JSON hello.

Hello l'output è simile toohello seguente testo:

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

Salvare queste informazioni, viene utilizzato in hello le sezioni seguenti di questo documento.

## <a name="get-hello-notebooks"></a>Ottenere notebook hello

codice Hello ad esempio hello descritta in questo documento è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).

## <a name="upload-hello-notebooks"></a>Caricare i notebook hello

Utilizzare hello seguenti passaggi viene notebook hello tooupload da tooyour progetto hello Spark nel cluster HDInsight:

1. Nel web browser, connettersi toohello server Jupyter notebook nel cluster di Spark. In hello seguente URL, sostituire `CLUSTERNAME` con nome hello del cluster Kafka:

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    Quando richiesto, immettere l'account di accesso cluster hello (amministrazione) e la password utilizzata per la creazione di cluster hello.

2. Da hello parte superiore destra della pagina hello, utilizzare hello __caricare__ hello tooupload pulsante __flusso-Tweets-To_Kafka.ipynb__ cluster toohello di file. Selezionare __aprire__ caricamento hello toostart.

    ![Utilizzare hello caricamento pulsante tooselect e caricare un blocco per Appunti](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Selezionare file KafkaStreaming.ipynb hello](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. Trovare hello __flusso-Tweets-To_Kafka.ipynb__ voce nell'elenco di hello di blocchi appunti e selezionare __caricare__ pulsante accanto a esso.

    ![Caricamento di hello utilizzare accanto a tooupload di voce KafkaStreaming.ipynb hello è server notebook toohello](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. Ripetere i passaggi da 1 a 3 hello di tooload __Spark-struttura-Streaming-da-Kafka.ipynb__ notebook.

## <a name="load-tweets-into-kafka"></a>Caricamento di tweet in Kafka

Una volta caricati i file hello, selezionare hello __flusso-Tweets-To_Kafka.ipynb__ notebook hello tooopen di voce. Seguire i passaggi hello hello notebook tooload tweets in Kafka.

## <a name="process-tweets-using-spark-structured-streaming"></a>Elaborazione dei tweet con lo streaming strutturato Spark

Home page di server Jupyter Notebook hello, selezionare hello __Spark-struttura-Streaming-da-Kafka.ipynb__ voce. Seguire i passaggi hello hello notebook tooload TWEET da Kafka tramite flusso strutturati Spark.

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come toouse Spark strutturata di flusso, vedere hello seguenti documenti toolearn ulteriori informazioni sull'utilizzo di Spark e Kafka:

* [La modalità di nascita streaming (DStream) con Kafka toouse](hdinsight-apache-spark-with-kafka.md).
* [Iniziare a usare un notebook Jupyter e Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md)