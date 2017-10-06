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
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="1e2e2-103">Ricevere eventi da Hub eventi di Azure usando Apache Storm</span><span class="sxs-lookup"><span data-stu-id="1e2e2-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="1e2e2-104">[Apache Storm](https://storm.incubator.apache.org) è un sistema distribuito di calcolo in tempo reale che semplifica l'elaborazione affidabile di flussi di dati non associati.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="1e2e2-105">In questa sezione viene illustrato come una tempesta di hub di eventi di Azure toouse spout tooreceive eventi dagli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-105">This section shows how toouse an Azure Event Hubs Storm spout tooreceive events from Event Hubs.</span></span> <span data-ttu-id="1e2e2-106">Usando Apache Storm, è possibile dividere gli eventi tra più processi ospitati in nodi diversi.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="1e2e2-107">Hello integrazione degli hub di eventi con Storm semplifica il consumo di eventi dal checkpoint in modo trasparente lo stato di avanzamento utilizzando Installazione Zookeeper elevato del numero, la gestione dei checkpoint persistente e parallelo riceve dagli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-107">hello Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="1e2e2-108">Per ulteriori informazioni sugli hub di eventi ricezione modelli, vedere hello [Panoramica di hub eventi][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="1e2e2-108">For more information about Event Hubs receive patterns, see hello [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="1e2e2-109">Creare il progetto e aggiungere il codice</span><span class="sxs-lookup"><span data-stu-id="1e2e2-109">Create project and add code</span></span>

<span data-ttu-id="1e2e2-110">Questa esercitazione viene utilizzato un [HDInsight Storm] [ HDInsight Storm] installazione, viene fornito con gli hub di eventi spout hello già disponibili.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with hello Event Hubs spout already available.</span></span>

1. <span data-ttu-id="1e2e2-111">Seguire hello [HDInsight Storm - Introduzione](../hdinsight/hdinsight-storm-overview.md) procedura toocreate HDInsight un nuovo cluster e connettere tooit tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-111">Follow hello [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure toocreate a new HDInsight cluster, and connect tooit via Remote Desktop.</span></span>
2. <span data-ttu-id="1e2e2-112">Hello copia `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` ambiente di sviluppo locale tooyour file.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-112">Copy hello `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file tooyour local development environment.</span></span> <span data-ttu-id="1e2e2-113">Contiene gli eventi-storm-beccuccio hello.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-113">This contains hello events-storm-spout.</span></span>
3. <span data-ttu-id="1e2e2-114">Comando che segue di hello utilizzare pacchetto hello tooinstall nell'archivio di Maven locale hello.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-114">Use hello following command tooinstall hello package into hello local Maven store.</span></span> <span data-ttu-id="1e2e2-115">In questo modo tooadd come riferimento nel hello tempesta di progetto in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-115">This enables you tooadd it as a reference in hello Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="1e2e2-116">In Eclipse creare un nuovo progetto Maven, fare clic su **File**, **New** (Nuovo) e infine su **Project** (Progetto).</span><span class="sxs-lookup"><span data-stu-id="1e2e2-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="1e2e2-117">Selezionare **Use default Workspace location** (Usa percorso predefinito dello spazio di lavoro) e quindi fare clic su **Next** (Avanti)</span><span class="sxs-lookup"><span data-stu-id="1e2e2-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="1e2e2-118">Seleziona hello **Guida rapida di sistema per maven** sistema per, quindi fare clic su **successivo**</span><span class="sxs-lookup"><span data-stu-id="1e2e2-118">Select hello **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="1e2e2-119">Inserire un valore per **GroupId** e **ArtifactId** e quindi fare clic su **Finish** (Fine)</span><span class="sxs-lookup"><span data-stu-id="1e2e2-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="1e2e2-120">In **pom.xml**, aggiungere hello seguendo le dipendenze in hello `<dependency>` nodo.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-120">In **pom.xml**, add hello following dependencies in hello `<dependency>` node.</span></span>

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

9. <span data-ttu-id="1e2e2-121">In hello **src** cartella, creare un file denominato **Config.properties** hello copia il contenuto seguente, sostituendo hello e `receive rule key` e `event hub name` valori:</span><span class="sxs-lookup"><span data-stu-id="1e2e2-121">In hello **src** folder, create a file called **Config.properties** and copy hello following content, substituting hello `receive rule key` and `event hub name` values:</span></span>

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
    <span data-ttu-id="1e2e2-122">valore per Hello **eventhub.receiver.credits** determina il numero di eventi viene eseguite in batch prima di rilasciarlo pipeline Storm toohello.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-122">hello value for **eventhub.receiver.credits** determines how many events are batched before releasing them toohello Storm pipeline.</span></span> <span data-ttu-id="1e2e2-123">Per i migliori risultati hello di semplicità, in questo esempio too10 questo valore.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-123">For hello sake of simplicity, this example sets this value too10.</span></span> <span data-ttu-id="1e2e2-124">Nell'ambiente di produzione, in genere deve essere impostato toohigher valori. ad esempio 1024.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-124">In production, it should usually be set toohigher values; for example, 1024.</span></span>
10. <span data-ttu-id="1e2e2-125">Creare una nuova classe denominata **LoggerBolt** con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="1e2e2-125">Create a new class called **LoggerBolt** with hello following code:</span></span>
    
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
    
    <span data-ttu-id="1e2e2-126">Questo fulmine Storm registra il contenuto di hello di eventi ricevuto hello.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-126">This Storm bolt logs hello content of hello received events.</span></span> <span data-ttu-id="1e2e2-127">Questo può essere esteso facilmente toostore tuple in un servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-127">This can easily be extended toostore tuples in a storage service.</span></span> <span data-ttu-id="1e2e2-128">Hello [esercitazioni su analysis sensore HDInsight] utilizzi gli stessi dati toostore approccio in HBase.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-128">hello [HDInsight sensor analysis tutorial] uses this same approach toostore data into HBase.</span></span>
11. <span data-ttu-id="1e2e2-129">Creare una classe denominata **LogTopology** con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="1e2e2-129">Create a class called **LogTopology** with hello following code:</span></span>
    
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

    <span data-ttu-id="1e2e2-130">Questa classe crea un nuovo beccuccio hub eventi, utilizzando le proprietà di hello in tooinstantiate file di configurazione hello è.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-130">This class creates a new Event Hubs spout, using hello properties in hello configuration file tooinstantiate it.</span></span> <span data-ttu-id="1e2e2-131">È importante toonote che questo esempio viene creata come molti spouts attività come il numero di hello di partizioni nell'hub di eventi hello, in ordine toouse hello massimo parallelismo consentito da hub eventi.</span><span class="sxs-lookup"><span data-stu-id="1e2e2-131">It is important toonote that this example creates as many spouts tasks as hello number of partitions in hello event hub, in order toouse hello maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e2e2-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e2e2-132">Next steps</span></span>
<span data-ttu-id="1e2e2-133">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="1e2e2-133">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="1e2e2-134">[Panoramica di Hub eventi][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="1e2e2-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="1e2e2-135">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="1e2e2-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="1e2e2-136">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="1e2e2-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[esercitazioni su analysis sensore HDInsight]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
