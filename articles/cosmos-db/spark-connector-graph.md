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
ms.openlocfilehash: 0be5c9b12cdba4a428c809d00e1e68785a9ec1ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="f2786-103">Azure Cosmos DB: eseguire analisi dei grafi con Spark e Apache TinkerPop Gremlin</span><span class="sxs-lookup"><span data-stu-id="f2786-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="f2786-104">[Azure DB Cosmos](introduction.md) è hello del servizio di database distribuita a livello globale e più modelli da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f2786-104">[Azure Cosmos DB](introduction.md) is hello globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="f2786-105">È possibile creare ed eseguire query di documento, chiave/valore e i database di grafico, ognuno dei quali vantaggio dalle funzionalità di distribuzione globale e della scala orizzontale hello base hello di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f2786-105">You can create and query document, key/value, and graph databases, all of which benefit from hello global-distribution and horizontal-scale capabilities at hello core of Azure Cosmos DB.</span></span> <span data-ttu-id="f2786-106">Azure Cosmos DB supporta carichi di lavoro di grafi OLTP (Online Transaction Processing) basati sul linguaggio [Apache TinkerPop Gremlin](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f2786-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="f2786-107">[Spark](http://spark.apache.org/) è un progetto di Apache Software Foundation incentrato sull'elaborazione di dati OLAP (Online Analytical Processing) generici.</span><span class="sxs-lookup"><span data-stu-id="f2786-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="f2786-108">Spark fornisce un in-memoria o basata su disco distribuita elaborazione modello ibrido che è simile toohello modello Hadoop MapReduce.</span><span class="sxs-lookup"><span data-stu-id="f2786-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar toohello Hadoop MapReduce model.</span></span> <span data-ttu-id="f2786-109">È possibile distribuire Apache Spark in cloud hello utilizzando [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="f2786-109">You can deploy Apache Spark in hello cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="f2786-110">Combinando Azure Cosmos DB e Spark, è possibile eseguire carichi di lavoro sia OLTP che OLAP con Gremlin.</span><span class="sxs-lookup"><span data-stu-id="f2786-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="f2786-111">Questo articolo Guida introduttiva illustra come toorun Gremlin le query eseguite su Azure Cosmos DB in un cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f2786-111">This quick-start article demonstrates how toorun Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2786-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f2786-112">Prerequisites</span></span>

<span data-ttu-id="f2786-113">Prima di poter eseguire questo esempio, è necessario disporre di hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="f2786-113">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="f2786-114">Cluster Azure HDInsight Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="f2786-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="f2786-115">JDK 1.8+ (eseguire `apt-get install default-jdk` se JDK non è disponibile)</span><span class="sxs-lookup"><span data-stu-id="f2786-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="f2786-116">Maven (eseguire `apt-get install maven` se Maven non è disponibile)</span><span class="sxs-lookup"><span data-stu-id="f2786-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="f2786-117">Una sottoscrizione di Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="f2786-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="f2786-118">Per informazioni su come tooset di un cluster Azure HDInsight Spark, vedere [cluster HDInsight Provisioning](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="f2786-118">For information about how tooset up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="f2786-119">Creare un account di database Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f2786-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="f2786-120">Creare innanzitutto un account di database con l'API Graph hello eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2786-120">First, create a database account with hello Graph API by doing hello following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="f2786-121">Aggiungere una raccolta</span><span class="sxs-lookup"><span data-stu-id="f2786-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="f2786-122">Ottenere Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="f2786-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="f2786-123">Ottenere Apache TinkerPop eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2786-123">Get Apache TinkerPop by doing hello following:</span></span>

1. <span data-ttu-id="f2786-124">Toohello remoto nodo principale del cluster HDInsight hello `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="f2786-124">Remote toohello master node of hello HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="f2786-125">Clonare il codice sorgente TinkerPop3 hello, compilarlo in locale e installarla tooMaven cache.</span><span class="sxs-lookup"><span data-stu-id="f2786-125">Clone hello TinkerPop3 source code, build it locally, and install it tooMaven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="f2786-126">Installare hello Spark Gremlin plug-in</span><span class="sxs-lookup"><span data-stu-id="f2786-126">Install hello Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="f2786-127">a.</span><span class="sxs-lookup"><span data-stu-id="f2786-127">a.</span></span> <span data-ttu-id="f2786-128">installazione di Hello di hello plug-in viene gestita da uve.</span><span class="sxs-lookup"><span data-stu-id="f2786-128">hello installation of hello plug-in is handled by Grape.</span></span> <span data-ttu-id="f2786-129">Popolare le informazioni di repository hello per uve in modo da poter scaricare hello plug-in e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="f2786-129">Populate hello repositories information for Grape so it can download hello plug-in and its dependencies.</span></span> 

      <span data-ttu-id="f2786-130">Creare il file di configurazione uve hello se non è presente in `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="f2786-130">Create hello grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="f2786-131">Utilizzare hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="f2786-131">Use hello following settings:</span></span>

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

    <span data-ttu-id="f2786-132">b.</span><span class="sxs-lookup"><span data-stu-id="f2786-132">b.</span></span> <span data-ttu-id="f2786-133">Avviare la console Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="f2786-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="f2786-134">c.</span><span class="sxs-lookup"><span data-stu-id="f2786-134">c.</span></span> <span data-ttu-id="f2786-135">Installare hello Spark Gremlin plug-in con versione 3.3.0-SNAPSHOT, che è incorporato nei passaggi precedenti hello:</span><span class="sxs-lookup"><span data-stu-id="f2786-135">Install hello Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in hello previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart hello console toouse [tinkerpop.spark]
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

4. <span data-ttu-id="f2786-136">Controllare se toosee `Hadoop-Gremlin` viene attivata con `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="f2786-136">Check toosee whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="f2786-137">Disabilita questo plug-in, in quanto potrebbe interferire con hello Spark Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="f2786-137">Disable this plug-in, because it could interfere with hello Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="f2786-138">Preparare le dipendenze di TinkerPop3</span><span class="sxs-lookup"><span data-stu-id="f2786-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="f2786-139">Al momento della compilazione TinkerPop3 nel passaggio precedente hello, nella directory di destinazione hello processo hello spostate anche tutte le dipendenze di file jar per Spark e Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f2786-139">When you built TinkerPop3 in hello previous step, hello process also pulled all jar dependencies for Spark and Hadoop in hello target directory.</span></span> <span data-ttu-id="f2786-140">Utilizzare JAR hello pre-installati con HDI e inserire dipendenze aggiuntive solo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="f2786-140">Use hello jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="f2786-141">Directory di destinazione passare toohello Console Gremlin in `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="f2786-141">Go toohello Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="f2786-142">Spostare tutti JAR in `ext/` troppo`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="f2786-142">Move all jars under `ext/` too`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="f2786-143">Rimuovere tutti i file jar di librerie in `lib/` che è hello non è nel seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="f2786-143">Remove all jar libraries under `lib/` that are not in hello following list:</span></span>

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

## <a name="get-hello-azure-cosmos-db-spark-connector"></a><span data-ttu-id="f2786-144">Ottenere il connettore di Azure Cosmos DB Spark hello</span><span class="sxs-lookup"><span data-stu-id="f2786-144">Get hello Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="f2786-145">Ottenere il connettore di Azure Cosmos DB Spark hello `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` e SDK per Java DB Cosmos `azure-documentdb-1.10.0.jar` da [connettore Spark di Azure Cosmos DB su GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="f2786-145">Get hello Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="f2786-146">In alternativa, è possibile eseguirne la compilazione in locale.</span><span class="sxs-lookup"><span data-stu-id="f2786-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="f2786-147">Perché la versione più recente di hello di Spark Gremlin è stato compilato con Spark 1.6.1 e non è compatibile con Spark 2.0.2, attualmente utilizzata nel connettore di Azure Cosmos DB Spark hello, è possibile compilare il codice TinkerPop3 più recente di hello e installare manualmente JAR hello.</span><span class="sxs-lookup"><span data-stu-id="f2786-147">Because hello latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in hello Azure Cosmos DB Spark connector, you can build hello latest TinkerPop3 code and install hello jars manually.</span></span> <span data-ttu-id="f2786-148">Hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2786-148">Do hello following:</span></span>

    <span data-ttu-id="f2786-149">a.</span><span class="sxs-lookup"><span data-stu-id="f2786-149">a.</span></span> <span data-ttu-id="f2786-150">Clonare il connettore di Azure Cosmos DB Spark hello.</span><span class="sxs-lookup"><span data-stu-id="f2786-150">Clone hello Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="f2786-151">b.</span><span class="sxs-lookup"><span data-stu-id="f2786-151">b.</span></span> <span data-ttu-id="f2786-152">Compilare TinkerPop3 (operazione già eseguita nei passaggi precedenti)</span><span class="sxs-lookup"><span data-stu-id="f2786-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="f2786-153">e installare tutti i file JAR di TinkerPop 3.3.0-SNAPSHOT in locale.</span><span class="sxs-lookup"><span data-stu-id="f2786-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="f2786-154">c.</span><span class="sxs-lookup"><span data-stu-id="f2786-154">c.</span></span> <span data-ttu-id="f2786-155">Aggiornamento `tinkerpop.version` `azure-documentdb-spark/pom.xml` troppo`3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="f2786-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` too`3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="f2786-156">d.</span><span class="sxs-lookup"><span data-stu-id="f2786-156">d.</span></span> <span data-ttu-id="f2786-157">Eseguire la compilazione con Maven.</span><span class="sxs-lookup"><span data-stu-id="f2786-157">Build with Maven.</span></span> <span data-ttu-id="f2786-158">Hello JAR necessari vengono inseriti in `target` e `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="f2786-158">hello needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="f2786-159">Hello copia indicato in precedenza JAR tooa locale directory ~ / azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="f2786-159">Copy hello previously mentioned jars tooa local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a><span data-ttu-id="f2786-160">Distribuire i nodi di lavoro di hello dipendenze toohello Spark</span><span class="sxs-lookup"><span data-stu-id="f2786-160">Distribute hello dependencies toohello Spark worker nodes</span></span> 

1. <span data-ttu-id="f2786-161">Poiché TinkerPop3 dipende dalla trasformazione hello di dati del grafico, è necessario distribuire hello correlati i nodi di lavoro di dipendenze tooall Spark.</span><span class="sxs-lookup"><span data-stu-id="f2786-161">Because hello transformation of graph data depends on TinkerPop3, you must distribute hello related dependencies tooall Spark worker nodes.</span></span>

2. <span data-ttu-id="f2786-162">Hello copia indicato in precedenza Gremlin dipendenze, hello jar connettore CosmosDB Spark e nodi di lavoro di SDK per Java CosmosDB toohello eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2786-162">Copy hello previously mentioned Gremlin dependencies, hello CosmosDB Spark connector jar, and CosmosDB Java SDK toohello worker nodes by doing hello following:</span></span>

    <span data-ttu-id="f2786-163">a.</span><span class="sxs-lookup"><span data-stu-id="f2786-163">a.</span></span> <span data-ttu-id="f2786-164">Copiare tutti JAR hello in `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="f2786-164">Copy all hello jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="f2786-165">b.</span><span class="sxs-lookup"><span data-stu-id="f2786-165">b.</span></span> <span data-ttu-id="f2786-166">Ottenere l'elenco di hello di tutti i nodi di lavoro Spark, che sono disponibili nel Ambari Dashboard, hello `Spark2 Clients` elenco hello `Spark2` sezione.</span><span class="sxs-lookup"><span data-stu-id="f2786-166">Get hello list of all Spark worker nodes, which you can find on Ambari Dashboard, in hello `Spark2 Clients` list in hello `Spark2` section.</span></span>

    <span data-ttu-id="f2786-167">c.</span><span class="sxs-lookup"><span data-stu-id="f2786-167">c.</span></span> <span data-ttu-id="f2786-168">Copiare tale tooeach directory dei nodi di hello.</span><span class="sxs-lookup"><span data-stu-id="f2786-168">Copy that directory tooeach of hello nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a><span data-ttu-id="f2786-169">Impostare le variabili di ambiente hello</span><span class="sxs-lookup"><span data-stu-id="f2786-169">Set up hello environment variables</span></span>

1. <span data-ttu-id="f2786-170">Trovare la versione di hello HDP del cluster Spark hello.</span><span class="sxs-lookup"><span data-stu-id="f2786-170">Find hello HDP version of hello Spark cluster.</span></span> <span data-ttu-id="f2786-171">È il nome di directory hello in `/usr/hdp/` (ad esempio, 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="f2786-171">It is hello directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="f2786-172">Configurare hdp.version per tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="f2786-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="f2786-173">Nel Ambari Dashboard andare troppo**sezione YARN** > **configurazioni** > **avanzate**e quindi hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2786-173">In Ambari Dashboard, go too**YARN section** > **Configs** > **Advanced**, and then do hello following:</span></span> 
 
    <span data-ttu-id="f2786-174">a.</span><span class="sxs-lookup"><span data-stu-id="f2786-174">a.</span></span> <span data-ttu-id="f2786-175">In `Custom yarn-site`, aggiungere una nuova proprietà `hdp.version` con valore hello della versione di hello HDP sul nodo principale hello.</span><span class="sxs-lookup"><span data-stu-id="f2786-175">In `Custom yarn-site`, add a new property `hdp.version` with hello value of hello HDP version on hello master node.</span></span> 
     
    <span data-ttu-id="f2786-176">b.</span><span class="sxs-lookup"><span data-stu-id="f2786-176">b.</span></span> <span data-ttu-id="f2786-177">Salvare le configurazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="f2786-177">Save hello configurations.</span></span> <span data-ttu-id="f2786-178">Verranno visualizzati avvisi che è possibile ignorare.</span><span class="sxs-lookup"><span data-stu-id="f2786-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="f2786-179">c.</span><span class="sxs-lookup"><span data-stu-id="f2786-179">c.</span></span> <span data-ttu-id="f2786-180">Riavviare i servizi YARN e Oozie hello come icone di notifica hello indicano.</span><span class="sxs-lookup"><span data-stu-id="f2786-180">Restart hello YARN and Oozie services as hello notification icons indicate.</span></span>

3. <span data-ttu-id="f2786-181">Hello set seguenti variabili di ambiente nel nodo principale hello (sostituire i valori hello esigenze):</span><span class="sxs-lookup"><span data-stu-id="f2786-181">Set hello following environment variables on hello master node (replace hello values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a><span data-ttu-id="f2786-182">Preparare hello grafico configurazione</span><span class="sxs-lookup"><span data-stu-id="f2786-182">Prepare hello graph configuration</span></span>

1. <span data-ttu-id="f2786-183">Creare un file di configurazione con hello parametri di connessione di database di Azure Cosmos nascita impostazioni e inserirlo in `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="f2786-183">Create a configuration file with hello Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

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

    # Classpath for hello driver and executors
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

2. <span data-ttu-id="f2786-184">Hello aggiornamento `spark.driver.extraClassPath` e `spark.executor.extraClassPath` tooinclude directory hello JAR hello distribuiti nel passaggio precedente hello, in questo caso `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="f2786-184">Update hello `spark.driver.extraClassPath` and `spark.executor.extraClassPath` tooinclude hello directory of hello jars that you distributed in hello previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="f2786-185">Fornire i seguenti dettagli per il database di Azure Cosmos hello:</span><span class="sxs-lookup"><span data-stu-id="f2786-185">Provide hello following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a><span data-ttu-id="f2786-186">Caricare hello TinkerPop grafico e salvarlo tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f2786-186">Load hello TinkerPop graph, and save it tooAzure Cosmos DB</span></span>
<span data-ttu-id="f2786-187">toodemonstrate come un grafico in Azure Cosmos DB, in questo esempio utilizza hello TinkerPop toopersist predefiniti TinkerPop moderna grafico.</span><span class="sxs-lookup"><span data-stu-id="f2786-187">toodemonstrate how toopersist a graph into Azure Cosmos DB, this example uses hello TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="f2786-188">grafico Hello viene archiviato in formato Kryo e viene fornito nel repository TinkerPop hello.</span><span class="sxs-lookup"><span data-stu-id="f2786-188">hello graph is stored in Kryo format, and it's provided in hello TinkerPop repository.</span></span>

1. <span data-ttu-id="f2786-189">Poiché viene eseguito in modalità YARN Gremlin, è necessario rendere disponibile nel file system Hadoop hello dati del grafico hello.</span><span class="sxs-lookup"><span data-stu-id="f2786-189">Because you are running Gremlin in YARN mode, you must make hello graph data available in hello Hadoop file system.</span></span> <span data-ttu-id="f2786-190">Utilizzare hello comandi che seguono toomake una directory e file di copia hello grafico locale al suo interno.</span><span class="sxs-lookup"><span data-stu-id="f2786-190">Use hello following commands toomake a directory and copy hello local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="f2786-191">Aggiornare temporaneamente hello `gremlin-spark.properties` file toouse `GryoInputFormat` grafico hello tooread.</span><span class="sxs-lookup"><span data-stu-id="f2786-191">Temporarily update hello `gremlin-spark.properties` file toouse `GryoInputFormat` tooread hello graph.</span></span> <span data-ttu-id="f2786-192">Indicare anche `inputLocation` come directory di hello si crea, come illustrato di seguito hello:</span><span class="sxs-lookup"><span data-stu-id="f2786-192">Also indicate `inputLocation` as hello directory you create, as in hello following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="f2786-193">Avviare Console Gremlin e quindi creare hello seguente calcolo passaggi toopersist dati toohello configurato Azure Cosmos DB raccolta:</span><span class="sxs-lookup"><span data-stu-id="f2786-193">Start Gremlin Console, and then create hello following computation steps toopersist data toohello configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="f2786-194">a.</span><span class="sxs-lookup"><span data-stu-id="f2786-194">a.</span></span> <span data-ttu-id="f2786-195">Creare il grafico hello `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="f2786-195">Create hello graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="f2786-196">b.</span><span class="sxs-lookup"><span data-stu-id="f2786-196">b.</span></span> <span data-ttu-id="f2786-197">Usare SparkGraphComputer per la scrittura `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="f2786-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

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

4. <span data-ttu-id="f2786-198">Da Esplora dati, è possibile verificare tale hello dati sono stati resi persistenti tooAzure DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f2786-198">From Data Explorer, you can verify that hello data has been persisted tooAzure Cosmos DB.</span></span>

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="f2786-199">Caricare il grafico hello da DB Cosmos Azure ed eseguire query Gremlin</span><span class="sxs-lookup"><span data-stu-id="f2786-199">Load hello graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="f2786-200">grafico hello tooload, modificare `gremlin-spark.properties` tooset `graphReader` troppo`DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="f2786-200">tooload hello graph, edit `gremlin-spark.properties` tooset `graphReader` too`DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="f2786-201">Grafico hello del carico, leggere i dati di hello ed eseguire query di Gremlin con esso eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2786-201">Load hello graph, traverse hello data, and run Gremlin queries with it by doing hello following:</span></span>

    <span data-ttu-id="f2786-202">a.</span><span class="sxs-lookup"><span data-stu-id="f2786-202">a.</span></span> <span data-ttu-id="f2786-203">Avviare Console Gremlin hello `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="f2786-203">Start hello Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="f2786-204">b.</span><span class="sxs-lookup"><span data-stu-id="f2786-204">b.</span></span> <span data-ttu-id="f2786-205">Creare il grafico hello con la configurazione di hello `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="f2786-205">Create hello graph with hello configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="f2786-206">c.</span><span class="sxs-lookup"><span data-stu-id="f2786-206">c.</span></span> <span data-ttu-id="f2786-207">Creare un attraversamento del grafo con SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="f2786-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="f2786-208">d.</span><span class="sxs-lookup"><span data-stu-id="f2786-208">d.</span></span> <span data-ttu-id="f2786-209">Eseguire hello query graph Gremlin seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2786-209">Run hello following Gremlin graph queries:</span></span>

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
> <span data-ttu-id="f2786-210">toosee più dettagliata di registrazione, imposta il livello di registrazione di hello in `conf/log4j-console.properties` tooa livello più dettagliato.</span><span class="sxs-lookup"><span data-stu-id="f2786-210">toosee more detailed logging, set hello log level in `conf/log4j-console.properties` tooa more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="f2786-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f2786-211">Next steps</span></span>

<span data-ttu-id="f2786-212">In questo articolo, avvio rapido appreso come creare un grafico toowork con combinando DB Cosmos Azure e Spark.</span><span class="sxs-lookup"><span data-stu-id="f2786-212">In this quick-start article, you've learned how toowork with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
