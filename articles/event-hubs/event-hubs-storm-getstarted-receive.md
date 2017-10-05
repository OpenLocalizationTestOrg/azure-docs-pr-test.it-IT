---
title: Ricevere eventi da Hub eventi di Azure usando Apache Storm | Microsoft Docs
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
ms.openlocfilehash: 3e15370c7602276ef323708632b324fe05497f41
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="ad15b-103">Ricevere eventi da Hub eventi di Azure usando Apache Storm</span><span class="sxs-lookup"><span data-stu-id="ad15b-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="ad15b-104">[Apache Storm](https://storm.incubator.apache.org) è un sistema distribuito di calcolo in tempo reale che semplifica l'elaborazione affidabile di flussi di dati non associati.</span><span class="sxs-lookup"><span data-stu-id="ad15b-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="ad15b-105">Questa sezione illustra come usare uno Storm Spout di Hub eventi per ricevere eventi da Hub eventi stesso.</span><span class="sxs-lookup"><span data-stu-id="ad15b-105">This section shows how to use an Azure Event Hubs Storm spout to receive events from Event Hubs.</span></span> <span data-ttu-id="ad15b-106">Usando Apache Storm, è possibile dividere gli eventi tra più processi ospitati in nodi diversi.</span><span class="sxs-lookup"><span data-stu-id="ad15b-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="ad15b-107">L'integrazione di Hub eventi con Storm semplifica l'uso degli eventi eseguendo il checkpoint trasparente dello stato di avanzamento grazie all'installazione di Zookeeper di Storm e alla gestione dei checkpoint persistenti e delle ricezioni parallele dagli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="ad15b-107">The Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="ad15b-108">Per altre informazioni sui modelli di ricezione di Hub eventi, vedere [Panoramica di Hub eventi][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="ad15b-108">For more information about Event Hubs receive patterns, see the [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="ad15b-109">Creare il progetto e aggiungere il codice</span><span class="sxs-lookup"><span data-stu-id="ad15b-109">Create project and add code</span></span>

<span data-ttu-id="ad15b-110">Questa esercitazione usa un'installazione di [HDInsight Storm][HDInsight Storm] , fornita con lo Spout di Hub eventi già disponibile.</span><span class="sxs-lookup"><span data-stu-id="ad15b-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with the Event Hubs spout already available.</span></span>

1. <span data-ttu-id="ad15b-111">Seguire la procedura indicata nell' [introduzione a HDInsight Storm](../hdinsight/hdinsight-storm-overview.md) per creare un nuovo cluster HDInsight e quindi connettersi a quest'ultimo tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="ad15b-111">Follow the [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure to create a new HDInsight cluster, and connect to it via Remote Desktop.</span></span>
2. <span data-ttu-id="ad15b-112">Copiare il file `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` nell'ambiente di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="ad15b-112">Copy the `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file to your local development environment.</span></span> <span data-ttu-id="ad15b-113">Il file contiene il componente events-storm-spout.</span><span class="sxs-lookup"><span data-stu-id="ad15b-113">This contains the events-storm-spout.</span></span>
3. <span data-ttu-id="ad15b-114">Usare il comando seguente per installare il pacchetto nell'archivio Maven locale.</span><span class="sxs-lookup"><span data-stu-id="ad15b-114">Use the following command to install the package into the local Maven store.</span></span> <span data-ttu-id="ad15b-115">Ciò consentirà di aggiungerlo come riferimento nel progetto Storm in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="ad15b-115">This enables you to add it as a reference in the Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="ad15b-116">In Eclipse creare un nuovo progetto Maven, fare clic su **File**, **New** (Nuovo) e infine su **Project** (Progetto).</span><span class="sxs-lookup"><span data-stu-id="ad15b-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="ad15b-117">Selezionare **Use default Workspace location** (Usa percorso predefinito dello spazio di lavoro) e quindi fare clic su **Next** (Avanti)</span><span class="sxs-lookup"><span data-stu-id="ad15b-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="ad15b-118">Selezionare l'archetipo **maven-archetype-quickstart** e quindi fare clic su **Next** (Avanti)</span><span class="sxs-lookup"><span data-stu-id="ad15b-118">Select the **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="ad15b-119">Inserire un valore per **GroupId** e **ArtifactId** e quindi fare clic su **Finish** (Fine)</span><span class="sxs-lookup"><span data-stu-id="ad15b-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="ad15b-120">In **pom.xml** aggiungere le dipendenze seguenti nel nodo `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="ad15b-120">In **pom.xml**, add the following dependencies in the `<dependency>` node.</span></span>

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

9. <span data-ttu-id="ad15b-121">Nella cartella **src** creare un file denominato **Config.properties** e copiare il contenuto seguente, sostituendo i valori `receive rule key` e `event hub name`:</span><span class="sxs-lookup"><span data-stu-id="ad15b-121">In the **src** folder, create a file called **Config.properties** and copy the following content, substituting the `receive rule key` and `event hub name` values:</span></span>

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
    <span data-ttu-id="ad15b-122">Il valore per **eventhub.receiver.credits** determina quanti eventi vengono inseriti in batch prima del loro rilascio nella pipeline di Storm.</span><span class="sxs-lookup"><span data-stu-id="ad15b-122">The value for **eventhub.receiver.credits** determines how many events are batched before releasing them to the Storm pipeline.</span></span> <span data-ttu-id="ad15b-123">Per semplicità, questo esempio imposta il valore su 10.</span><span class="sxs-lookup"><span data-stu-id="ad15b-123">For the sake of simplicity, this example sets this value to 10.</span></span> <span data-ttu-id="ad15b-124">In produzione dovrebbe essere impostato su valori superiori, ad esempio 1024.</span><span class="sxs-lookup"><span data-stu-id="ad15b-124">In production, it should usually be set to higher values; for example, 1024.</span></span>
10. <span data-ttu-id="ad15b-125">Creare una nuova classe denominata **LoggerBolt** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="ad15b-125">Create a new class called **LoggerBolt** with the following code:</span></span>
    
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
    
    <span data-ttu-id="ad15b-126">Questo Bolt Storm registra il contenuto degli eventi ricevuti.</span><span class="sxs-lookup"><span data-stu-id="ad15b-126">This Storm bolt logs the content of the received events.</span></span> <span data-ttu-id="ad15b-127">Può essere facilmente esteso per archiviare tuple in un servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ad15b-127">This can easily be extended to store tuples in a storage service.</span></span> <span data-ttu-id="ad15b-128">L' [esercitazione di analisi dei sensori con HDInsight] usa lo stesso approccio per archiviare dati in HBase.</span><span class="sxs-lookup"><span data-stu-id="ad15b-128">The [HDInsight sensor analysis tutorial] uses this same approach to store data into HBase.</span></span>
11. <span data-ttu-id="ad15b-129">Creare una classe denominata **LogTopology** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="ad15b-129">Create a class called **LogTopology** with the following code:</span></span>
    
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
        
            // set the number of workers to be the same as partition number.
            // the idea is to have a spout and a logger bolt co-exist in one
            // worker to avoid shuffling messages across workers in storm cluster.
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

    <span data-ttu-id="ad15b-130">Questa classe crea un nuovo spout di Hub eventi, usando le proprietà contenute nel file di configurazione, per crearne un'istanza.</span><span class="sxs-lookup"><span data-stu-id="ad15b-130">This class creates a new Event Hubs spout, using the properties in the configuration file to instantiate it.</span></span> <span data-ttu-id="ad15b-131">È importante notare che questo esempio crea tante attività Spout quante sono le partizioni nell'hub eventi, in modo da usare il massimo parallelismo consentito dall'hub eventi stesso.</span><span class="sxs-lookup"><span data-stu-id="ad15b-131">It is important to note that this example creates as many spouts tasks as the number of partitions in the event hub, in order to use the maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad15b-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ad15b-132">Next steps</span></span>
<span data-ttu-id="ad15b-133">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad15b-133">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="ad15b-134">[Panoramica di Hub eventi][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="ad15b-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="ad15b-135">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="ad15b-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="ad15b-136">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="ad15b-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
<span data-ttu-id="ad15b-137">[esercitazione di analisi dei sensori con HDInsight]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md</span><span class="sxs-lookup"><span data-stu-id="ad15b-137">[HDInsight sensor analysis tutorial]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md</span></span>

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
