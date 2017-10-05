---
title: 'Azure Cosmos DB: eseguire analisi dei grafi con Spark e Apache TinkerPop Gremlin | Microsoft Docs'
description: Questo articolo fornisce le istruzioni necessarie per configurare ed eseguire l'analisi dei grafi e il calcolo parallelo in Azure Cosmos DB con Spark e TinkerPop SparkGraphComputer.
services: cosmosdb
documentationcenter: 
author: khdang
manager: shireest
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: gremlin
ms.topic: article
ms.date: 06/05/2017
ms.author: khdang
ms.openlocfilehash: 27c4d945e418b130c68cfde845571eb93658101e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="bd452-103">Azure Cosmos DB: eseguire analisi dei grafi con Spark e Apache TinkerPop Gremlin</span><span class="sxs-lookup"><span data-stu-id="bd452-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="bd452-104">[Azure Cosmos DB](introduction.md) è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bd452-104">[Azure Cosmos DB](introduction.md) is the globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="bd452-105">È possibile creare ed eseguire query su database di documenti, coppie chiave-valore e grafi sfruttando i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bd452-105">You can create and query document, key/value, and graph databases, all of which benefit from the global-distribution and horizontal-scale capabilities at the core of Azure Cosmos DB.</span></span> <span data-ttu-id="bd452-106">Azure Cosmos DB supporta carichi di lavoro di grafi OLTP (Online Transaction Processing) basati sul linguaggio [Apache TinkerPop Gremlin](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bd452-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="bd452-107">[Spark](http://spark.apache.org/) è un progetto di Apache Software Foundation incentrato sull'elaborazione di dati OLAP (Online Analytical Processing) generici.</span><span class="sxs-lookup"><span data-stu-id="bd452-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="bd452-108">Spark offre un modello di calcolo distribuito in memoria/su disco simile al modello MapReduce di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="bd452-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar to the Hadoop MapReduce model.</span></span> <span data-ttu-id="bd452-109">È possibile distribuire Apache Spark nel cloud con [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="bd452-109">You can deploy Apache Spark in the cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="bd452-110">Combinando Azure Cosmos DB e Spark, è possibile eseguire carichi di lavoro sia OLTP che OLAP con Gremlin.</span><span class="sxs-lookup"><span data-stu-id="bd452-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="bd452-111">Questa guida introduttiva illustra come eseguire query Gremlin su Azure Cosmos DB in un cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="bd452-111">This quick-start article demonstrates how to run Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd452-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bd452-112">Prerequisites</span></span>

<span data-ttu-id="bd452-113">Prima di poter eseguire questo esempio, è necessario soddisfare i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="bd452-113">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="bd452-114">Cluster Azure HDInsight Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="bd452-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="bd452-115">JDK 1.8+ (eseguire `apt-get install default-jdk` se JDK non è disponibile)</span><span class="sxs-lookup"><span data-stu-id="bd452-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="bd452-116">Maven (eseguire `apt-get install maven` se Maven non è disponibile)</span><span class="sxs-lookup"><span data-stu-id="bd452-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="bd452-117">Una sottoscrizione di Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="bd452-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="bd452-118">Per informazioni su come configurare un cluster Azure HDInsight Spark, vedere [Provisioning di cluster HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="bd452-118">For information about how to set up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="bd452-119">Creare un account di database Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bd452-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="bd452-120">Per prima cosa, si crea un account di database con l'API Graph seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd452-120">First, create a database account with the Graph API by doing the following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="bd452-121">Aggiungere una raccolta</span><span class="sxs-lookup"><span data-stu-id="bd452-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="bd452-122">Ottenere Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="bd452-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="bd452-123">Ottenere Apache TinkerPop seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd452-123">Get Apache TinkerPop by doing the following:</span></span>

1. <span data-ttu-id="bd452-124">Accedere in remoto al nodo master del cluster HDInsight `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="bd452-124">Remote to the master node of the HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="bd452-125">Clonare il codice sorgente di TinkerPop3, compilarlo in locale ed eseguirne l'installazione nella cache di Maven.</span><span class="sxs-lookup"><span data-stu-id="bd452-125">Clone the TinkerPop3 source code, build it locally, and install it to Maven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="bd452-126">Installare il plug-in Spark-Gremlin</span><span class="sxs-lookup"><span data-stu-id="bd452-126">Install the Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="bd452-127">a.</span><span class="sxs-lookup"><span data-stu-id="bd452-127">a.</span></span> <span data-ttu-id="bd452-128">L'installazione del plug-in viene gestita da Grape.</span><span class="sxs-lookup"><span data-stu-id="bd452-128">The installation of the plug-in is handled by Grape.</span></span> <span data-ttu-id="bd452-129">Inserire le informazioni relative ai repository per Grape in modo da consentire il download del plug-in e delle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="bd452-129">Populate the repositories information for Grape so it can download the plug-in and its dependencies.</span></span> 

      <span data-ttu-id="bd452-130">Creare il file di configurazione di Grape, se non è presente in `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="bd452-130">Create the grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="bd452-131">Usare le seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="bd452-131">Use the following settings:</span></span>

    ```xml
    <ivysettings>
    <settings defaultResolver="downloadGrapes"/>
    <resolvers>
        <chain name="downloadGrapes">
        <filesystem name="cachedGrapes">
            <ivy pattern="${user.home}/.groovy/grapes/[organisation]/[module]/ivy-[revision].xml"/>
            <artifact pattern="${user.home}/.groovy/grapes/[organisation]/[module]/[type]s/[artifact]-[revision].[ext]"/>
        </filesystem>
        <ibiblio name="codehaus" root="http://repository.codehaus.org/" m2compatible="true"/>
        <ibiblio name="central" root="http://central.maven.org/maven2/" m2compatible="true"/>
        <ibiblio name="jitpack" root="https://jitpack.io" m2compatible="true"/>
        <ibiblio name="java.net2" root="http://download.java.net/maven/2/" m2compatible="true"/>
        <ibiblio name="apache-snapshots" root="http://repository.apache.org/snapshots/" m2compatible="true"/>
        <ibiblio name="local" root="file:${user.home}/.m2/repository/" m2compatible="true"/>
        </chain>
    </resolvers>
    </ivysettings>
    ``` 

    <span data-ttu-id="bd452-132">b.</span><span class="sxs-lookup"><span data-stu-id="bd452-132">b.</span></span> <span data-ttu-id="bd452-133">Avviare la console Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="bd452-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="bd452-134">c.</span><span class="sxs-lookup"><span data-stu-id="bd452-134">c.</span></span> <span data-ttu-id="bd452-135">Installare il plug-in Spark-Gremlin con la versione 3.3.0-SNAPSHOT compilata nei passaggi precedenti:</span><span class="sxs-lookup"><span data-stu-id="bd452-135">Install the Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in the previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart the console to use [tinkerpop.spark]
    gremlin> :q
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :plugin use tinkerpop.spark
    ==>tinkerpop.spark activated
    ```

4. <span data-ttu-id="bd452-136">Controllare se `Hadoop-Gremlin` è attivato con `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="bd452-136">Check to see whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="bd452-137">Disabilitare questo plug-in perché potrebbe interferire con il plug-in Spark-Gremlin `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="bd452-137">Disable this plug-in, because it could interfere with the Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="bd452-138">Preparare le dipendenze di TinkerPop3</span><span class="sxs-lookup"><span data-stu-id="bd452-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="bd452-139">Durante la compilazione di TinkerPop3 nel passaggio precedente sono state estratte nella directory di destinazione anche tutte le dipendenze in formato JAR per Spark e Hadoop.</span><span class="sxs-lookup"><span data-stu-id="bd452-139">When you built TinkerPop3 in the previous step, the process also pulled all jar dependencies for Spark and Hadoop in the target directory.</span></span> <span data-ttu-id="bd452-140">Usare i file JAR preinstallati con HDI ed effettuare il pull delle dipendenze aggiuntive solo se necessario.</span><span class="sxs-lookup"><span data-stu-id="bd452-140">Use the jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="bd452-141">Passare alla directory di destinazione della console Gremlin in `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="bd452-141">Go to the Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="bd452-142">Spostare tutti i file JAR da `ext/` a `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="bd452-142">Move all jars under `ext/` to `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="bd452-143">Rimuovere tutte le librerie JAR in `lib/` che non sono incluse nell'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="bd452-143">Remove all jar libraries under `lib/` that are not in the following list:</span></span>

    ```bash
    # TinkerPop3
    gremlin-console-3.3.0-SNAPSHOT.jar
    gremlin-core-3.3.0-SNAPSHOT.jar       
    gremlin-groovy-3.3.0-SNAPSHOT.jar     
    gremlin-shaded-3.3.0-SNAPSHOT.jar     
    hadoop-gremlin-3.3.0-SNAPSHOT.jar     
    spark-gremlin-3.3.0-SNAPSHOT.jar      
    tinkergraph-gremlin-3.3.0-SNAPSHOT.jar

    # Gremlin depedencies
    asm-3.2.jar                                
    avro-1.7.4.jar                             
    caffeine-2.3.1.jar                         
    cglib-2.2.1-v20090111.jar                  
    gbench-0.4.3-groovy-2.4.jar                
    gprof-0.3.1-groovy-2.4.jar                 
    groovy-2.4.9-indy.jar                      
    groovy-2.4.9.jar                           
    groovy-console-2.4.9.jar                   
    groovy-groovysh-2.4.9-indy.jar             
    groovy-json-2.4.9-indy.jar                 
    groovy-jsr223-2.4.9-indy.jar               
    groovy-sql-2.4.9-indy.jar                  
    groovy-swing-2.4.9.jar                     
    groovy-templates-2.4.9.jar                 
    groovy-xml-2.4.9.jar                       
    hadoop-yarn-server-nodemanager-2.7.2.jar   
    hppc-0.7.1.jar                             
    javatuples-1.2.jar                         
    jaxb-impl-2.2.3-1.jar                      
    jbcrypt-0.4.jar                            
    jcabi-log-0.14.jar                         
    jcabi-manifests-1.1.jar                    
    jersey-core-1.9.jar                        
    jersey-guice-1.9.jar                       
    jersey-json-1.9.jar                        
    jettison-1.1.jar                           
    scalatest_2.11-2.2.6.jar                   
    servlet-api-2.5.jar                        
    snakeyaml-1.15.jar                         
    unused-1.0.0.jar                           
    xml-apis-1.3.04.jar                        
    ```

## <a name="get-the-azure-cosmos-db-spark-connector"></a><span data-ttu-id="bd452-144">Ottenere il connettore Spark per Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bd452-144">Get the Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="bd452-145">Ottenere il connettore Spark per Azure Cosmos DB `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` e Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` dalla relativa pagina in [Github](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="bd452-145">Get the Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="bd452-146">In alternativa, è possibile eseguirne la compilazione in locale.</span><span class="sxs-lookup"><span data-stu-id="bd452-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="bd452-147">Dato che l'ultima versione di Spark-Gremlin è stata compilata con Spark 1.6.1 e non è compatibile con la versione Spark 2.0.2 attualmente usata nel connettore Spark per Azure Cosmos DB, è possibile compilare il codice di TinkerPop3 più recente e installare i file JAR manualmente.</span><span class="sxs-lookup"><span data-stu-id="bd452-147">Because the latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in the Azure Cosmos DB Spark connector, you can build the latest TinkerPop3 code and install the jars manually.</span></span> <span data-ttu-id="bd452-148">Eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bd452-148">Do the following:</span></span>

    <span data-ttu-id="bd452-149">a.</span><span class="sxs-lookup"><span data-stu-id="bd452-149">a.</span></span> <span data-ttu-id="bd452-150">Clonare il connettore Spark per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bd452-150">Clone the Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="bd452-151">b.</span><span class="sxs-lookup"><span data-stu-id="bd452-151">b.</span></span> <span data-ttu-id="bd452-152">Compilare TinkerPop3 (operazione già eseguita nei passaggi precedenti)</span><span class="sxs-lookup"><span data-stu-id="bd452-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="bd452-153">e installare tutti i file JAR di TinkerPop 3.3.0-SNAPSHOT in locale.</span><span class="sxs-lookup"><span data-stu-id="bd452-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="bd452-154">c.</span><span class="sxs-lookup"><span data-stu-id="bd452-154">c.</span></span> <span data-ttu-id="bd452-155">Aggiornare `tinkerpop.version` `azure-documentdb-spark/pom.xml` a `3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="bd452-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` to `3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="bd452-156">d.</span><span class="sxs-lookup"><span data-stu-id="bd452-156">d.</span></span> <span data-ttu-id="bd452-157">Eseguire la compilazione con Maven.</span><span class="sxs-lookup"><span data-stu-id="bd452-157">Build with Maven.</span></span> <span data-ttu-id="bd452-158">I file JAR necessari vengono inseriti in `target` e `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="bd452-158">The needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="bd452-159">Copiare i file JAR elencati in precedenza in una directory locale in ~/azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="bd452-159">Copy the previously mentioned jars to a local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-the-dependencies-to-the-spark-worker-nodes"></a><span data-ttu-id="bd452-160">Distribuire le dipendenze nei nodi di lavoro Spark</span><span class="sxs-lookup"><span data-stu-id="bd452-160">Distribute the dependencies to the Spark worker nodes</span></span> 

1. <span data-ttu-id="bd452-161">Dato che la trasformazione dei dati dei grafi dipende da TinkerPop3, è necessario distribuire le relative dipendenze in tutti i nodi di lavoro Spark.</span><span class="sxs-lookup"><span data-stu-id="bd452-161">Because the transformation of graph data depends on TinkerPop3, you must distribute the related dependencies to all Spark worker nodes.</span></span>

2. <span data-ttu-id="bd452-162">Copiare le dipendenze Gremlin elencate in precedenza, il file JAR del connettore Spark per CosmosDB e CosmosDB Java SDK nei nodi di lavoro seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd452-162">Copy the previously mentioned Gremlin dependencies, the CosmosDB Spark connector jar, and CosmosDB Java SDK to the worker nodes by doing the following:</span></span>

    <span data-ttu-id="bd452-163">a.</span><span class="sxs-lookup"><span data-stu-id="bd452-163">a.</span></span> <span data-ttu-id="bd452-164">Copiare tutti i file JAR in `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="bd452-164">Copy all the jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="bd452-165">b.</span><span class="sxs-lookup"><span data-stu-id="bd452-165">b.</span></span> <span data-ttu-id="bd452-166">Ottenere l'elenco di tutti i nodi di lavoro Spark, disponibile nel dashboard Ambari, nell'elenco `Spark2 Clients` della sezione `Spark2`.</span><span class="sxs-lookup"><span data-stu-id="bd452-166">Get the list of all Spark worker nodes, which you can find on Ambari Dashboard, in the `Spark2 Clients` list in the `Spark2` section.</span></span>

    <span data-ttu-id="bd452-167">c.</span><span class="sxs-lookup"><span data-stu-id="bd452-167">c.</span></span> <span data-ttu-id="bd452-168">Copiare la directory in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="bd452-168">Copy that directory to each of the nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-the-environment-variables"></a><span data-ttu-id="bd452-169">Configurare le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="bd452-169">Set up the environment variables</span></span>

1. <span data-ttu-id="bd452-170">Trovare la versione HDP del cluster Spark,</span><span class="sxs-lookup"><span data-stu-id="bd452-170">Find the HDP version of the Spark cluster.</span></span> <span data-ttu-id="bd452-171">corrispondente al nome di directory in `/usr/hdp/` (ad esempio, 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="bd452-171">It is the directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="bd452-172">Configurare hdp.version per tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="bd452-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="bd452-173">Nel dashboard Ambari passare a **YARN section** > **Configs** > **Advanced** (Sezione YARN > Configurazioni > Avanzate) e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd452-173">In Ambari Dashboard, go to **YARN section** > **Configs** > **Advanced**, and then do the following:</span></span> 
 
    <span data-ttu-id="bd452-174">a.</span><span class="sxs-lookup"><span data-stu-id="bd452-174">a.</span></span> <span data-ttu-id="bd452-175">In `Custom yarn-site` aggiungere una nuova proprietà `hdp.version` con il valore della versione di HDP nel nodo master.</span><span class="sxs-lookup"><span data-stu-id="bd452-175">In `Custom yarn-site`, add a new property `hdp.version` with the value of the HDP version on the master node.</span></span> 
     
    <span data-ttu-id="bd452-176">b.</span><span class="sxs-lookup"><span data-stu-id="bd452-176">b.</span></span> <span data-ttu-id="bd452-177">Salvare le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="bd452-177">Save the configurations.</span></span> <span data-ttu-id="bd452-178">Verranno visualizzati avvisi che è possibile ignorare.</span><span class="sxs-lookup"><span data-stu-id="bd452-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="bd452-179">c.</span><span class="sxs-lookup"><span data-stu-id="bd452-179">c.</span></span> <span data-ttu-id="bd452-180">Riavviare i servizi Oozie e YARN come indicato dalle icone di notifica.</span><span class="sxs-lookup"><span data-stu-id="bd452-180">Restart the YARN and Oozie services as the notification icons indicate.</span></span>

3. <span data-ttu-id="bd452-181">Impostare le variabili di ambiente seguenti nel nodo master, sostituendo i valori in base alle esigenze:</span><span class="sxs-lookup"><span data-stu-id="bd452-181">Set the following environment variables on the master node (replace the values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-the-graph-configuration"></a><span data-ttu-id="bd452-182">Preparare la configurazione per i grafi</span><span class="sxs-lookup"><span data-stu-id="bd452-182">Prepare the graph configuration</span></span>

1. <span data-ttu-id="bd452-183">Creare un file di configurazione con i parametri di connessione di Azure Cosmos DB e le impostazioni di Spark e inserirlo in `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="bd452-183">Create a configuration file with the Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

    ```
    gremlin.graph=org.apache.tinkerpop.gremlin.hadoop.structure.HadoopGraph
    gremlin.hadoop.jarsInDistributedCache=true
    gremlin.hadoop.defaultGraphComputer=org.apache.tinkerpop.gremlin.spark.process.computer.SparkGraphComputer

    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    gremlin.hadoop.graphWriter=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBOutputRDD

    ####################################
    # SparkGraphComputer Configuration #
    ####################################
    spark.master=yarn
    spark.executor.memory=3g
    spark.executor.instances=6
    spark.serializer=org.apache.spark.serializer.KryoSerializer
    spark.kryo.registrator=org.apache.tinkerpop.gremlin.spark.structure.io.gryo.GryoRegistrator
    gremlin.spark.persistContext=true

    # Classpath for the driver and executors
    spark.driver.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    spark.executor.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    
    ######################################
    # DocumentDB Spark connector         #
    ######################################
    spark.documentdb.connectionMode=Gateway
    spark.documentdb.schema_samplingratio=1.0
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    spark.documentdb.preferredRegions=FILLIN
    ```

2. <span data-ttu-id="bd452-184">Aggiornare `spark.driver.extraClassPath` e `spark.executor.extraClassPath` in modo da includere la directory dei file JAR distribuiti nel passaggio precedente, in questo caso `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="bd452-184">Update the `spark.driver.extraClassPath` and `spark.executor.extraClassPath` to include the directory of the jars that you distributed in the previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="bd452-185">Specificare i dettagli seguenti per Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="bd452-185">Provide the following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-the-tinkerpop-graph-and-save-it-to-azure-cosmos-db"></a><span data-ttu-id="bd452-186">Caricare il grafo TinkerPop e salvarlo in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bd452-186">Load the TinkerPop graph, and save it to Azure Cosmos DB</span></span>
<span data-ttu-id="bd452-187">Per illustrare come è possibile salvare in modo permanente un grafo in Azure Cosmos DB, si usa come esempio il grafo modern predefinito di TinkerPop.</span><span class="sxs-lookup"><span data-stu-id="bd452-187">To demonstrate how to persist a graph into Azure Cosmos DB, this example uses the TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="bd452-188">Il grafo è stato archiviato in formato Kryo ed è disponibile nel repository TinkerPop.</span><span class="sxs-lookup"><span data-stu-id="bd452-188">The graph is stored in Kryo format, and it's provided in the TinkerPop repository.</span></span>

1. <span data-ttu-id="bd452-189">Dato che si esegue Gremlin in modalità YARN, è necessario rendere disponibili i dati del grafo nel file system Hadoop.</span><span class="sxs-lookup"><span data-stu-id="bd452-189">Because you are running Gremlin in YARN mode, you must make the graph data available in the Hadoop file system.</span></span> <span data-ttu-id="bd452-190">Usare i comandi seguenti per creare una directory e copiare al suo interno il file del grafo locale.</span><span class="sxs-lookup"><span data-stu-id="bd452-190">Use the following commands to make a directory and copy the local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="bd452-191">Aggiornare temporaneamente il file `gremlin-spark.properties` in modo da usare `GryoInputFormat` per la lettura del grafo.</span><span class="sxs-lookup"><span data-stu-id="bd452-191">Temporarily update the `gremlin-spark.properties` file to use `GryoInputFormat` to read the graph.</span></span> <span data-ttu-id="bd452-192">Indicare anche `inputLocation` come directory creata, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="bd452-192">Also indicate `inputLocation` as the directory you create, as in the following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="bd452-193">Avviare la console Gremlin e creare questi passaggi di calcolo per salvare in modo permanente i dati nella raccolta Azure Cosmos DB configurata:</span><span class="sxs-lookup"><span data-stu-id="bd452-193">Start Gremlin Console, and then create the following computation steps to persist data to the configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="bd452-194">a.</span><span class="sxs-lookup"><span data-stu-id="bd452-194">a.</span></span> <span data-ttu-id="bd452-195">Creare il grafo: `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="bd452-195">Create the graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="bd452-196">b.</span><span class="sxs-lookup"><span data-stu-id="bd452-196">b.</span></span> <span data-ttu-id="bd452-197">Usare SparkGraphComputer per la scrittura `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="bd452-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[gryoinputformat->documentdboutputrdd]
    gremlin> hg = graph.
                compute(SparkGraphComputer.class).
                result(GraphComputer.ResultGraph.NEW).
                persist(GraphComputer.Persist.EDGES).
                program(TraversalVertexProgram.build().
                    traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)), "gremlin-groovy", "g.V()").
                    create(graph)).
                submit().
                get() 
    ==>result[hadoopgraph[documentdbinputrdd->documentdboutputrdd],memory[size:1]]
    ```

4. <span data-ttu-id="bd452-198">In Esplora dati è possibile verificare che i dati siano stati salvati in modo permanente in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bd452-198">From Data Explorer, you can verify that the data has been persisted to Azure Cosmos DB.</span></span>

## <a name="load-the-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="bd452-199">Caricare il grafo da Azure Cosmos DB ed eseguire query Gremlin.</span><span class="sxs-lookup"><span data-stu-id="bd452-199">Load the graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="bd452-200">Per caricare il grafo, modificare `gremlin-spark.properties` per impostare `graphReader` su `DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="bd452-200">To load the graph, edit `gremlin-spark.properties` to set `graphReader` to `DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="bd452-201">Caricare il grafo, attraversare i dati ed eseguire query Gremlin seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd452-201">Load the graph, traverse the data, and run Gremlin queries with it by doing the following:</span></span>

    <span data-ttu-id="bd452-202">a.</span><span class="sxs-lookup"><span data-stu-id="bd452-202">a.</span></span> <span data-ttu-id="bd452-203">Avviare la console Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="bd452-203">Start the Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="bd452-204">b.</span><span class="sxs-lookup"><span data-stu-id="bd452-204">b.</span></span> <span data-ttu-id="bd452-205">Creare il grafo con la configurazione `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="bd452-205">Create the graph with the configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="bd452-206">c.</span><span class="sxs-lookup"><span data-stu-id="bd452-206">c.</span></span> <span data-ttu-id="bd452-207">Creare un attraversamento del grafo con SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="bd452-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="bd452-208">d.</span><span class="sxs-lookup"><span data-stu-id="bd452-208">d.</span></span> <span data-ttu-id="bd452-209">Eseguire le query Gremlin seguenti sul grafo:</span><span class="sxs-lookup"><span data-stu-id="bd452-209">Run the following Gremlin graph queries:</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[documentdbinputrdd->documentdboutputrdd]
    gremlin> g = graph.traversal().withComputer(SparkGraphComputer)
    ==>graphtraversalsource[hadoopgraph[documentdbinputrdd->documentdboutputrdd], sparkgraphcomputer]
    gremlin> g.V().count()
    ==>6
    gremlin> g.E().count()
    ==>6
    gremlin> g.V(1).out().values('name')
    ==>josh
    ==>vadas
    ==>lop
    gremlin> g.V().hasLabel('person').coalesce(values('nickname'), values('name'))
    ==>josh
    ==>peter
    ==>vadas
    ==>marko
    gremlin> g.V().hasLabel('person').
            choose(values('name')).
                option('marko', values('age')).
                option('josh', values('name')).
                option('vadas', valueMap()).
                option('peter', label())
    ==>josh
    ==>person
    ==>[name:[vadas],age:[27]]
    ==>29
    ```

> [!NOTE]
> <span data-ttu-id="bd452-210">Per visualizzare una registrazione più dettagliata, impostare un livello di log più dettagliato in `conf/log4j-console.properties`.</span><span class="sxs-lookup"><span data-stu-id="bd452-210">To see more detailed logging, set the log level in `conf/log4j-console.properties` to a more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="bd452-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd452-211">Next steps</span></span>

<span data-ttu-id="bd452-212">In questa guida introduttiva si è appreso come usare i grafi combinando Azure Cosmos DB e Spark.</span><span class="sxs-lookup"><span data-stu-id="bd452-212">In this quick-start article, you've learned how to work with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
