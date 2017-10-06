---
title: eventi aaaReceive dall'hub di eventi di Azure usando Apache Storm | Documenti Microsoft
description: Avviare la ricezione da Hub eventi usando Apache Storm
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: java
ms.devlang: multiple
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a0ab860ee8d504a28aac380c504c928f0d6dbc1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a>Ricevere eventi da Hub eventi di Azure usando Apache Storm

[Apache Storm](https://storm.incubator.apache.org) è un sistema distribuito di calcolo in tempo reale che semplifica l'elaborazione affidabile di flussi di dati non associati. In questa sezione viene illustrato come una tempesta di hub di eventi di Azure toouse spout tooreceive eventi dagli hub eventi. Usando Apache Storm, è possibile dividere gli eventi tra più processi ospitati in nodi diversi. Hello integrazione degli hub di eventi con Storm semplifica il consumo di eventi dal checkpoint in modo trasparente lo stato di avanzamento utilizzando Installazione Zookeeper elevato del numero, la gestione dei checkpoint persistente e parallelo riceve dagli hub eventi.

Per ulteriori informazioni sugli hub di eventi ricezione modelli, vedere hello [Panoramica di hub eventi][Event Hubs overview].

## <a name="create-project-and-add-code"></a>Creare il progetto e aggiungere il codice

Questa esercitazione viene utilizzato un [HDInsight Storm] [ HDInsight Storm] installazione, viene fornito con gli hub di eventi spout hello già disponibili.

1. Seguire hello [HDInsight Storm - Introduzione](../hdinsight/hdinsight-storm-overview.md) procedura toocreate HDInsight un nuovo cluster e connettere tooit tramite Desktop remoto.
2. Hello copia `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` ambiente di sviluppo locale tooyour file. Contiene gli eventi-storm-beccuccio hello.
3. Comando che segue di hello utilizzare pacchetto hello tooinstall nell'archivio di Maven locale hello. In questo modo tooadd come riferimento nel hello tempesta di progetto in un passaggio successivo.

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. In Eclipse creare un nuovo progetto Maven, fare clic su **File**, **New** (Nuovo) e infine su **Project** (Progetto).
   
    ![][12]
5. Selezionare **Use default Workspace location** (Usa percorso predefinito dello spazio di lavoro) e quindi fare clic su **Next** (Avanti)
6. Seleziona hello **Guida rapida di sistema per maven** sistema per, quindi fare clic su **successivo**
7. Inserire un valore per **GroupId** e **ArtifactId** e quindi fare clic su **Finish** (Fine)
8. In **pom.xml**, aggiungere hello seguendo le dipendenze in hello `<dependency>` nodo.

    ```xml  
    <dependency>
        <groupId>org.apache.storm</groupId>
        <artifactId>storm-core</artifactId>
        <version>0.9.2-incubating</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.microsoft.eventhubs</groupId>
        <artifactId>eventhubs-storm-spout</artifactId>
        <version>0.9</version>
    </dependency>
    <dependency>
        <groupId>com.netflix.curator</groupId>
        <artifactId>curator-framework</artifactId>
        <version>1.3.3</version>
        <exclusions>
            <exclusion>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
            </exclusion>
            <exclusion>
                <groupId>org.slf4j</groupId>
                <artifactId>slf4j-log4j12</artifactId>
            </exclusion>
        </exclusions>
        <scope>provided</scope>
    </dependency>
    ```

9. In hello **src** cartella, creare un file denominato **Config.properties** hello copia il contenuto seguente, sostituendo hello e `receive rule key` e `event hub name` valori:

    ```java
    eventhubspout.username = ReceiveRule
    eventhubspout.password = {receive rule key}
    eventhubspout.namespace = ioteventhub-ns
    eventhubspout.entitypath = {event hub name}
    eventhubspout.partitions.count = 16
       
    # if not provided, will use storm's zookeeper settings
    # zookeeper.connectionstring=localhost:2181
       
    eventhubspout.checkpoint.interval = 10
    eventhub.receiver.credits = 10
    ```
    valore per Hello **eventhub.receiver.credits** determina il numero di eventi viene eseguite in batch prima di rilasciarlo pipeline Storm toohello. Per i migliori risultati hello di semplicità, in questo esempio too10 questo valore. Nell'ambiente di produzione, in genere deve essere impostato toohigher valori. ad esempio 1024.
10. Creare una nuova classe denominata **LoggerBolt** con hello seguente codice:
    
    ```java
    import java.util.Map;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import backtype.storm.task.OutputCollector;
    import backtype.storm.task.TopologyContext;
    import backtype.storm.topology.OutputFieldsDeclarer;
    import backtype.storm.topology.base.BaseRichBolt;
    import backtype.storm.tuple.Tuple;
    
    public class LoggerBolt extends BaseRichBolt {
        private OutputCollector collector;
        private static final Logger logger = LoggerFactory
                  .getLogger(LoggerBolt.class);
    
        @Override
        public void execute(Tuple tuple) {
            String value = tuple.getString(0);
            logger.info("Tuple value: " + value);
   
            collector.ack(tuple);
        }
   
        @Override
        public void prepare(Map map, TopologyContext context, OutputCollector collector) {
            this.collector = collector;
            this.count = 0;
        }
        
        @Override
        public void declareOutputFields(OutputFieldsDeclarer declarer) {
            // no output fields
        }
    
    }
    ```
    
    Questo fulmine Storm registra il contenuto di hello di eventi ricevuto hello. Questo può essere esteso facilmente toostore tuple in un servizio di archiviazione. Hello [esercitazioni su analysis sensore HDInsight] utilizzi gli stessi dati toostore approccio in HBase.
11. Creare una classe denominata **LogTopology** con hello seguente codice:
    
    ```java
    import java.io.FileReader;
    import java.util.Properties;
    import backtype.storm.Config;
    import backtype.storm.LocalCluster;
    import backtype.storm.StormSubmitter;
    import backtype.storm.generated.StormTopology;
    import backtype.storm.topology.TopologyBuilder;
    import com.microsoft.eventhubs.samples.EventCount;
    import com.microsoft.eventhubs.spout.EventHubSpout;
    import com.microsoft.eventhubs.spout.EventHubSpoutConfig;
        
    public class LogTopology {
        protected EventHubSpoutConfig spoutConfig;
        protected int numWorkers;
        
        protected void readEHConfig(String[] args) throws Exception {
            Properties properties = new Properties();
            if (args.length > 1) {
                properties.load(new FileReader(args[1]));
            } else {
                properties.load(EventCount.class.getClassLoader()
                        .getResourceAsStream("Config.properties"));
            }
        
            String username = properties.getProperty("eventhubspout.username");
            String password = properties.getProperty("eventhubspout.password");
            String namespaceName = properties
                    .getProperty("eventhubspout.namespace");
            String entityPath = properties.getProperty("eventhubspout.entitypath");
            String zkEndpointAddress = properties
                    .getProperty("zookeeper.connectionstring"); // opt
            int partitionCount = Integer.parseInt(properties
                    .getProperty("eventhubspout.partitions.count"));
            int checkpointIntervalInSeconds = Integer.parseInt(properties
                    .getProperty("eventhubspout.checkpoint.interval"));
            int receiverCredits = Integer.parseInt(properties
                    .getProperty("eventhub.receiver.credits")); // prefetch count
                                                                // (opt)
            System.out.println("Eventhub spout config: ");
            System.out.println("  partition count: " + partitionCount);
            System.out.println("  checkpoint interval: "
                    + checkpointIntervalInSeconds);
            System.out.println("  receiver credits: " + receiverCredits);
     
            spoutConfig = new EventHubSpoutConfig(username, password,
                    namespaceName, entityPath, partitionCount, zkEndpointAddress,
                    checkpointIntervalInSeconds, receiverCredits);
        
            // set hello number of workers toobe hello same as partition number.
            // hello idea is toohave a spout and a logger bolt co-exist in one
            // worker tooavoid shuffling messages across workers in storm cluster.
            numWorkers = spoutConfig.getPartitionCount();
        
            if (args.length > 0) {
                // set topology name so that sample Trident topology can use it as
                // stream name.
                spoutConfig.setTopologyName(args[0]);
            }
        }
        
        protected StormTopology buildTopology() {
            TopologyBuilder topologyBuilder = new TopologyBuilder();
       
            EventHubSpout eventHubSpout = new EventHubSpout(spoutConfig);
            topologyBuilder.setSpout("EventHubsSpout", eventHubSpout,
                    spoutConfig.getPartitionCount()).setNumTasks(
                    spoutConfig.getPartitionCount());
            topologyBuilder
                    .setBolt("LoggerBolt", new LoggerBolt(),
                            spoutConfig.getPartitionCount())
                    .localOrShuffleGrouping("EventHubsSpout")
                    .setNumTasks(spoutConfig.getPartitionCount());
            return topologyBuilder.createTopology();
        }
        
        protected void runScenario(String[] args) throws Exception {
            boolean runLocal = true;
            readEHConfig(args);
            StormTopology topology = buildTopology();
            Config config = new Config();
            config.setDebug(false);
        
            if (runLocal) {
                config.setMaxTaskParallelism(2);
                LocalCluster localCluster = new LocalCluster();
                localCluster.submitTopology("test", config, topology);
                Thread.sleep(5000000);
                localCluster.shutdown();
            } else {
                config.setNumWorkers(numWorkers);
                StormSubmitter.submitTopology(args[0], config, topology);
            }
        }
        
        public static void main(String[] args) throws Exception {
            LogTopology topology = new LogTopology();
            topology.runScenario(args);
        }
    }
    ```

    Questa classe crea un nuovo beccuccio hub eventi, utilizzando le proprietà di hello in tooinstantiate file di configurazione hello è. È importante toonote che questo esempio viene creata come molti spouts attività come il numero di hello di partizioni nell'hub di eventi hello, in ordine toouse hello massimo parallelismo consentito da hub eventi.

## <a name="next-steps"></a>Passaggi successivi
Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica di Hub eventi][Event Hubs overview]
* [Creare un hub eventi](event-hubs-create.md)
* [Domande frequenti su Hub eventi](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[esercitazioni su analysis sensore HDInsight]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
