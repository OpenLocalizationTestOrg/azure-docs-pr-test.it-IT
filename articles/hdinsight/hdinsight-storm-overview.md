---
title: "aaaWhat è Apache Storm - HDInsight di Azure | Documenti Microsoft"
description: "Apache Storm consente tooprocess flussi di dati in tempo reale. Azure HDInsight consente tooeasily creare cluster Storm in hello cloud di Azure. Con Visual Studio, è possibile creare soluzioni Storm in c# e quindi distribuire tooyour che cluster HDInsight Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: casi d'uso di Apache Storm,cluster Storm,informazioni su Apache Storm
ms.assetid: 72d54080-1e48-4a5e-aa50-cce4ffc85077
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6c6b2925ef3e5666dfecc3fb3c835bb362902c51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a>Che cos'è Apache Storm in Azure HDInsight?

[Apache Storm](http://storm.apache.org/) è un sistema di calcolo distribuito, a tolleranza di errore e open source. È possibile utilizzare i flussi di dati in tempo reale tooprocess di Storm con Hadoop. Soluzioni di Storm possono anche fornire garantita l'elaborazione dei dati, con hello possibilità tooreplay dati che non sono stato elaborato hello prima volta.

Storm in HDInsight offre hello seguenti vantaggi chiave:

* Viene eseguito come servizio gestito con un contratto di servizio con tempo di attività del 99,9%.

* Può essere personalizzato facilmente eseguendo script nel cluster Storm durante o dopo la creazione. Per altre informazioni, vedere [Personalizzare cluster HDInsight mediante l'azione script](hdinsight-hadoop-customize-cluster-linux.md).

* Usa diversi linguaggi. È possibile scrivere componenti Storm in linguaggio hello di propria scelta, ad esempio Java, c# e Python.

    * Integra Visual Studio con HDInsight per lo sviluppo di hello, gestione e monitoraggio delle topologie di c#. Per ulteriori informazioni, vedere [topologie c# Storm sviluppare con gli strumenti HDInsight per Visual Studio hello](hdinsight-storm-develop-csharp-visual-studio-topology.md).

    * Supporta hello Trident Java interface. È possibile creare topologie Storm che supportano l'elaborazione di tipo exactly-once dei messaggi, la persistenza transazionale del datastore e un insieme di operazioni di analisi di flusso di uso comune.

*  È possibile aumentare o ridurre facilmente le prestazioni dei cluster Storm. È possibile aggiungere o rimuovere i nodi di lavoro con le topologie Storm toorunning alcun impatto.

* Si integra con hello seguenti servizi di Azure:

    * Hub eventi di Azure

    * Rete virtuale di Azure

    * Database SQL di Azure

    * Archiviazione di Azure

    * Azure Cosmos DB

* Combina in modo sicuro funzionalità hello di più cluster HDInsight tramite una rete virtuale. È possibile creare pipeline di analisi che usano cluster Storm, Kafka, Spark, HBase o Hadoop.

Per un elenco delle società che usano Apache Storm per le loro soluzioni di analisi in tempo reale, vedere l'articolo relativo alle [società che usano Apache Storm](https://storm.apache.org/documentation/Powered-By.html).

tooget avviato utilizzando Storm, vedere [introduzione Storm in HDInsight][gettingstarted].

## <a name="how-does-storm-work"></a>Funzionamento di Storm

Storm esegue i processi di MapReduce che potrebbe acquisire familiarità con le topologie anziché hello. Le topologie Storm sono costituite da più componenti disposti in un grafo aciclico diretto (DAG). Flussi di dati tra i componenti di hello nel grafico hello. Ogni componente utilizza uno o più flussi di dati e, facoltativamente, trasmette uno o più flussi. Hello seguente diagramma viene illustrato il flusso dei dati tra i componenti in una topologia di base del numero di parole:

![Esempio di disposizione dei componenti in una topologia Storm](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* I componenti spout inseriscono i dati in una topologia Uno o più flussi generano topologia hello.

* I componenti bolt usano i flussi trasmessi dagli spout o da altri bolt. Bulloni potrebbero facoltativamente generare flussi topologia hello. Bulloni sono inoltre responsabili per la scrittura di servizi tooexternal dati o archiviazione, ad esempio HDFS, Kafka o HBase.

## <a name="ease-of-creation"></a>Facilità di creazione

Il provisioning di un nuovo cluster Storm in HDInsight richiede solo alcuni minuti. Per altre informazioni sulla creazione di un cluster Storm, vedere [Introduzione a Storm in un HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

## <a name="ease-of-use"></a>Semplicità d'uso

* __Secure Shell (SSH) connettività__: È possibile accedere ai nodi head del cluster Storm del hello su hello Internet utilizzando SSH. È possibile eseguire comandi direttamente nel cluster tramite SSH.

  Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* __Connettività Web__: hello Ambari web dell'interfaccia utente di fornire i cluster HDInsight tutti. È facilmente possibile monitorare, configurare e gestire i servizi nel cluster utilizzando hello Ambari web dell'interfaccia utente. I cluster di Storm includono inoltre hello Storm UI. È possibile monitorare e gestire topologie Storm in esecuzione dal browser utilizzando hello Storm UI.

  Per ulteriori informazioni, vedere hello [gestire HDInsight utilizzando hello dell'interfaccia utente Web Ambari](hdinsight-hadoop-manage-ambari.md) e [Monitor e gestire l'utilizzo dell'interfaccia utente Storm hello](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) documenti.

* __Azure PowerShell e CLI di Azure__: PowerShell e CLI forniscono entrambi l'utilità della riga di comando che è possibile utilizzare il toowork sistema client e altri servizi di Azure HDInsight.

* __Integrazione di Visual Studio__: Azure Data Lake Tools per Visual Studio includono modelli di progetto per la creazione di topologie di c# Storm tramite hello SCP.Net framework. Data Lake Tools fornisce anche strumenti toodeploy, monitorare e gestire soluzioni con Storm in HDInsight.

  Per ulteriori informazioni, vedere [topologie c# Storm sviluppare con gli strumenti HDInsight per Visual Studio hello](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="integration-with-other-azure-services"></a>Integrazione con altri servizi di Azure

* __Azure Data Lake Store__: per un esempio dell'uso di Data Lake Store con un cluster Storm, vedere [Usare Azure Data Lake Store con Apache Storm in HDInsight](hdinsight-storm-write-data-lake-store.md).

* __Hub eventi__: per un esempio di utilizzo degli hub di eventi con un cluster Storm, vedere hello seguenti documenti:

    * [Sviluppare una topologia di conteggio parole per Storm in HDInsight](hdinsight-storm-develop-java-topology.md)

    * [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (C#)](hdinsight-storm-develop-csharp-event-hub-topology.md)

* __Database SQL__, __DB Cosmos__, __hub eventi__, e __HBase__: sono inclusi esempi di modello in hello Data Lake Tools per Visual Studio. Per altre informazioni, vedere [Sviluppare una topologia C# per Storm in HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="reliability"></a>Affidabilità

Apache Storm garantisce che ogni messaggio in arrivo è sempre completamente elaborata, anche quando l'analisi dei dati hello sono distribuito in centinaia di nodi.

nodo Nimbus Hello fornisce funzionalità simili toohello Hadoop JobTracker e assegna alle attività tooother i nodi del cluster tramite Zookeeper. I nodi di zookeeper coordinare per un cluster e facilitano la comunicazione tra Nimbus e hello processo Supervisore in nodi di lavoro hello. Se un nodo di elaborazione viene interrotto, viene informato nodo Nimbus hello e assegna attività hello e nodo tooanother dati associati.

configurazione di Hello predefinita per i cluster Apache Storm è solo un nodo di Nimbus toohave. Storm in HDInsight prevede invece due nodi Nimbus. Se si verifica un errore sul nodo primario hello, cluster Storm hello passa nodo secondario toohello mentre viene recuperato nodo primario hello. Hello seguente diagramma illustra configurazione del flusso attività hello per Storm in HDInsight:

![Diagramma di Nimbus, Zookeeper e Supervisor](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a>Scalabilità

È possibile ridimensionare in modo dinamico i cluster HDInsight aggiungendo o rimuovendo nodi del ruolo di lavoro. L'operazione può essere eseguita durante l'elaborazione dei dati.

> [!IMPORTANT]
> tootake sfruttare nuovi nodi aggiunti tramite la scalabilità, è necessario topologie Storm toorebalance avviate prima dimensione del cluster hello è stato aumentato.

## <a name="support"></a>Supporto

Storm in HDInsight viene fornito con supporto continuo di livello aziendale. Storm in HDInsight offre anche un contratto di servizio con disponibilità del 99,9%. Pertanto, che si garantisce che un cluster Storm disponga di connettività esterna almeno il 99,9% del tempo di hello.

Per altre informazioni, vedere il [supporto di Azure](https://azure.microsoft.com/support/options/).

## <a name="apache-storm-use-cases"></a>Casi d'uso di Apache Storm

Hello di seguito è illustrati alcuni scenari comuni per cui è possibile utilizzare Storm in HDInsight:

* Internet delle cose
* Rilevamento delle frodi
* Analisi di social media
* Estrazione, trasformazione e caricamento (ETL)
* Monitoraggio della rete
* Search
* Mobile Engagement

Per informazioni su scenari reali, vedere hello [modo le aziende utilizzano Storm](https://storm.apache.org/documentation/Powered-By.html) documento.

## <a name="development"></a>Sviluppo.

Gli sviluppatori .NET possono progettare e implementare topologie in C# usando Strumenti Azure Data Lake per Visual Studio. È inoltre possibile creare topologie ibride che usano componenti Java e C#.

Per altre informazioni, vedere [Sviluppare topologie C# per Storm in HDInsight tramite Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

È inoltre possibile sviluppare soluzioni di Java utilizzando hello IDE di propria scelta. Per altre informazioni, vedere [Sviluppare topologie Java per Storm in HDInsight](hdinsight-storm-develop-java-topology.md).

Python può inoltre essere utilizzati toodevelop Storm componenti. Per altre informazioni, vedere [Sviluppare topologie Storm usando Python in HDInsight](hdinsight-storm-develop-python-topology.md).

## <a name="common-development-patterns"></a>Modelli di sviluppo comuni

### <a name="guaranteed-message-processing"></a>Elaborazione garantita dei messaggi

Apache Storm può offrire diversi livelli di elaborazione garantita dei messaggi. Un'applicazione Storm di base può ad esempio garantire un'elaborazione at-least-once, mentre Trident può garantire un'elaborazione exactly-once.

Per altre informazioni, vedere la sezione sulle [garanzie relative all'elaborazione dati](https://storm.apache.org/about/guarantees-data-processing.html) nel sito Web apache.org.

### <a name="ibasicbolt"></a>IBasicBolt

modello di leggere una tupla di input, la creazione di zero o più tuple, Hello e tupla di input hello acking immediatamente alla fine hello hello eseguire quindi il metodo è comune. Storm fornisce hello [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) interfaccia tooautomate questo modello.

### <a name="joins"></a>Join

La modalità di unione dei flussi di dati varia a seconda delle applicazioni. È possibile, ad esempio, creare un join di ogni tupla da più flussi in un unico nuovo flusso oppure è possibile creare un solo join di più batch di tuple per una specifica finestra. In entrambi i casi è possibile creare un join tramite [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Campo di raggruppamento è un modo per definire come tuple sono toobolts indirizzato.

Nel seguente esempio Java di hello, fieldsGrouping è usato tooroute tuple che provengono da componenti "1", "2" e "3" toohello MyJoiner fulmine:

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a>Batch

Apache Storm include un meccanismo a tempo interno noto come "tupla tick". È possibile impostare la frequenza con cui viene trasmessa una tupla tick nella topologia.

Per un esempio dell'uso di una tupla tick da un componente C#, vedere [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).

### <a name="caches"></a>Cache

La memorizzazione nella cache viene spesso usata come meccanismo per velocizzare l'elaborazione perché conserva in memoria le risorse usate di frequente. Poiché una topologia viene distribuita in più nodi e in più processi all'interno di ogni nodo, è consigliabile usare [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Utilizzare `fieldsGrouping` tooensure tuple contenenti campi hello che vengono utilizzati per la ricerca nella cache sono sempre toohello indirizzato stessa procedura. Questa funzionalità di raggruppamento evita la duplicazione delle voci della cache nei processi.

### <a name="stream-top-n"></a>Flusso di "primi N"

Quando la topologia dipende dal calcolo di un valore di primi N, calcolare il valore di primi N hello in parallelo. Quindi unione output di hello da tali calcoli in un valore globale. Questa operazione può essere eseguita tramite [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) tooroute dal campo per l'elaborazione parallela. È quindi possibile instradare fulmine tooa che a livello globale determina il valore di primi N hello.

Per un esempio di calcolare un valore di primi N, vedere hello [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) esempio.

## <a name="logging"></a>Registrazione

Storm Usa Log4j Apache toolog informazioni. Per impostazione predefinita, una grande quantità di dati viene registrata e può essere difficile toosort mediante le informazioni di hello. È possibile includere un file di configurazione della registrazione durante il comportamento della registrazione della topologia toocontrol Storm.

Per una topologia di esempio che illustra come tooconfigure registrazione, vedere [basati su Java WordCount](hdinsight-storm-develop-java-topology.md) esempio per Storm in HDInsight.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle soluzioni di analisi in tempo reale con Storm in HDInsight:

* [Introduzione ad Apache Storm in HDInsight][gettingstarted]
* [Topologie di esempio per Apache Storm in HDInsight](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
