---
title: aaaApache Spark streaming con Kafka - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come dati di toostream Spark Apache Spark in o da Apache Kafka utilizzando DStreams toouse. In questo esempio i dati vengono trasmessi in streaming tramite un notebook Jupyter da Spark in HDInsight.
keywords: esempio kafka,kafka zookeeper,spark streaming kafka,esempio spark streaming kafka
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a>Esempio dello streaming Apache Spark (DStream) con Kafka (anteprima) in HDInsight

Informazioni su come dati di toostream Spark Apache Spark in o da Apache Kafka in HDInsight mediante DStreams toouse. Questo esempio viene utilizzato un server Jupyter notebook esecuzione nel cluster Spark hello.
> [!NOTE]
> procedura di Hello in questo documento consente di creare un gruppo di risorse di Azure che contiene sia un Spark in HDInsight e un Kafka nel cluster HDInsight. Questi cluster sono entrambi contenuti all'interno di una rete virtuale di Azure, che consente di hello toodirectly cluster Spark comunicare hello cluster Kafka.
>
> Al termine con i passaggi di hello in questo documento, tenere presente toodelete hello cluster tooavoid in eccesso addebiti.

## <a name="create-hello-clusters"></a>Creare il cluster hello

Apache Kafka in HDInsight non forniscono accesso toohello Kafka Broker hello rete internet pubblica. Tutto ciò che deve essere tooKafka discussioni hello stessa rete virtuale come nodi di hello hello cluster Kafka. In questo esempio hello Kafka sia cluster Spark si trovano in una rete virtuale di Azure. Hello diagramma seguente illustra il flusso delle comunicazioni tra i cluster hello:

![Diagramma dei cluster Spark e Kafka in una rete virtuale di Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Anche se Kafka stesso toocommunication limitato all'interno di rete virtuale hello, altri servizi in cluster hello, ad esempio possibile accedere tramite SSH e Ambari hello internet. Per ulteriori informazioni sulle porte pubbliche hello disponibili con HDInsight, vedere [porte e gli URI utilizzato da HDInsight](hdinsight-hadoop-port-settings-for-services.md).

È possibile creare una rete virtuale di Azure, Kafka e Spark cluster manualmente, ma è più facile toouse un modello di gestione risorse di Azure. Utilizzare hello seguenti passaggi viene toodeploy una rete virtuale di Azure, Kafka, e Spark cluster tooyour sottoscrizione di Azure.

1. Utilizzare hello seguente pulsante toosign in tooAzure e modello hello Apri nel portale di Azure hello.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello Azure Resource Manager modello si trova in **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > disponibilità tooguarantee Kafka in HDInsight, il cluster deve contenere almeno tre nodi di lavoro. Questo modello crea un cluster Kafka contenente tre nodi di lavoro.

    Questo modello crea un cluster HDInsight 3.6 sia per Kafka che per Spark.

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

Dopo avere create le risorse di hello, verrà reindirizzato tooa pannello per gruppo di risorse hello che contiene i cluster hello e dashboard web.

![Pannello di gruppo di risorse per la rete virtuale hello e cluster](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Si noti che sono nomi hello dei cluster HDInsight hello **spark BASENAME** e **kafka BASENAME**, dove BASENAME è nome hello toohello modello specificato. Utilizzare questi nomi nei passaggi successivi per la connessione toohello cluster.

## <a name="use-hello-notebooks"></a>Utilizzare i blocchi appunti hello

codice Hello ad esempio hello descritta in questo documento è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).

Seguire i passaggi hello hello `README.md` file toocomplete in questo esempio.

## <a name="delete-hello-cluster"></a>Eliminare il cluster hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Poiché i passaggi di hello in questo documento crea entrambi i cluster in hello nello stesso gruppo di risorse di Azure, è possibile eliminare il gruppo di risorse hello in hello portale di Azure. Eliminazione gruppo hello rimuove tutte le risorse create eseguendo questo documento, hello rete virtuale di Azure e l'account di archiviazione utilizzato dal cluster hello.

## <a name="next-steps"></a>Passaggi successivi

In questo esempio è stato descritto come toouse nascita tooread e scrivere tooKafka. Utilizzare hello seguendo i collegamenti toodiscover toowork altri modi con Kafka:

* [Introduzione ad Apache Kafka (anteprima) in HDInsight](hdinsight-apache-kafka-get-started.md)
* [Utilizzare MirrorMaker toocreate una replica di Kafka in HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Usare Apache Storm (anteprima) con Kafka in HDInsight](hdinsight-apache-storm-with-kafka.md)

