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
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a>Azure Cosmos DB: eseguire analisi dei grafi con Spark e Apache TinkerPop Gremlin

[Azure DB Cosmos](introduction.md) è hello del servizio di database distribuita a livello globale e più modelli da Microsoft. È possibile creare ed eseguire query di documento, chiave/valore e i database di grafico, ognuno dei quali vantaggio dalle funzionalità di distribuzione globale e della scala orizzontale hello base hello di Azure Cosmos DB. Azure Cosmos DB supporta carichi di lavoro di grafi OLTP (Online Transaction Processing) basati sul linguaggio [Apache TinkerPop Gremlin](graph-introduction.md).

[Spark](http://spark.apache.org/) è un progetto di Apache Software Foundation incentrato sull'elaborazione di dati OLAP (Online Analytical Processing) generici. Spark fornisce un in-memoria o basata su disco distribuita elaborazione modello ibrido che è simile toohello modello Hadoop MapReduce. È possibile distribuire Apache Spark in cloud hello utilizzando [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Combinando Azure Cosmos DB e Spark, è possibile eseguire carichi di lavoro sia OLTP che OLAP con Gremlin. Questo articolo Guida introduttiva illustra come toorun Gremlin le query eseguite su Azure Cosmos DB in un cluster Azure HDInsight Spark.

## <a name="prerequisites"></a>Prerequisiti

Prima di poter eseguire questo esempio, è necessario disporre di hello seguenti prerequisiti:
* Cluster Azure HDInsight Spark 2.0
* JDK 1.8+ (eseguire `apt-get install default-jdk` se JDK non è disponibile)
* Maven (eseguire `apt-get install maven` se Maven non è disponibile)
* Una sottoscrizione di Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])

Per informazioni su come tooset di un cluster Azure HDInsight Spark, vedere [cluster HDInsight Provisioning](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

## <a name="create-an-azure-cosmos-db-database-account"></a>Creare un account di database Azure Cosmos DB

Creare innanzitutto un account di database con l'API Graph hello eseguendo hello seguenti:

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Aggiungere una raccolta

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a>Ottenere Apache TinkerPop

Ottenere Apache TinkerPop eseguendo hello seguenti:

1. Toohello remoto nodo principale del cluster HDInsight hello `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.

2. Clonare il codice sorgente TinkerPop3 hello, compilarlo in locale e installarla tooMaven cache.

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. Installare hello Spark Gremlin plug-in 

    a. installazione di Hello di hello plug-in viene gestita da uve. Popolare le informazioni di repository hello per uve in modo da poter scaricare hello plug-in e le relative dipendenze. 

      Creare il file di configurazione uve hello se non è presente in `~/.groovy/grapeConfig.xml`. Utilizzare hello seguenti impostazioni:

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

    b. Avviare la console Gremlin `bin/gremlin.sh`.
        
    c. Installare hello Spark Gremlin plug-in con versione 3.3.0-SNAPSHOT, che è incorporato nei passaggi precedenti hello:

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

4. Controllare se toosee `Hadoop-Gremlin` viene attivata con `:plugin list`. Disabilita questo plug-in, in quanto potrebbe interferire con hello Spark Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.

## <a name="prepare-tinkerpop3-dependencies"></a>Preparare le dipendenze di TinkerPop3

Al momento della compilazione TinkerPop3 nel passaggio precedente hello, nella directory di destinazione hello processo hello spostate anche tutte le dipendenze di file jar per Spark e Hadoop. Utilizzare JAR hello pre-installati con HDI e inserire dipendenze aggiuntive solo in base alle esigenze.

1. Directory di destinazione passare toohello Console Gremlin in `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`. 

2. Spostare tutti JAR in `ext/` troppo`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.

3. Rimuovere tutti i file jar di librerie in `lib/` che è hello non è nel seguente elenco:

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

## <a name="get-hello-azure-cosmos-db-spark-connector"></a>Ottenere il connettore di Azure Cosmos DB Spark hello

1. Ottenere il connettore di Azure Cosmos DB Spark hello `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` e SDK per Java DB Cosmos `azure-documentdb-1.10.0.jar` da [connettore Spark di Azure Cosmos DB su GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).

2. In alternativa, è possibile eseguirne la compilazione in locale. Perché la versione più recente di hello di Spark Gremlin è stato compilato con Spark 1.6.1 e non è compatibile con Spark 2.0.2, attualmente utilizzata nel connettore di Azure Cosmos DB Spark hello, è possibile compilare il codice TinkerPop3 più recente di hello e installare manualmente JAR hello. Hello seguenti:

    a. Clonare il connettore di Azure Cosmos DB Spark hello.

    b. Compilare TinkerPop3 (operazione già eseguita nei passaggi precedenti) e installare tutti i file JAR di TinkerPop 3.3.0-SNAPSHOT in locale.

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    c. Aggiornamento `tinkerpop.version` `azure-documentdb-spark/pom.xml` troppo`3.3.0-SNAPSHOT`.
    
    d. Eseguire la compilazione con Maven. Hello JAR necessari vengono inseriti in `target` e `target/alternateLocation`.

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. Hello copia indicato in precedenza JAR tooa locale directory ~ / azure-documentdb-spark:

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a>Distribuire i nodi di lavoro di hello dipendenze toohello Spark 

1. Poiché TinkerPop3 dipende dalla trasformazione hello di dati del grafico, è necessario distribuire hello correlati i nodi di lavoro di dipendenze tooall Spark.

2. Hello copia indicato in precedenza Gremlin dipendenze, hello jar connettore CosmosDB Spark e nodi di lavoro di SDK per Java CosmosDB toohello eseguendo hello seguenti:

    a. Copiare tutti JAR hello in `~/azure-documentdb-spark`.

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    b. Ottenere l'elenco di hello di tutti i nodi di lavoro Spark, che sono disponibili nel Ambari Dashboard, hello `Spark2 Clients` elenco hello `Spark2` sezione.

    c. Copiare tale tooeach directory dei nodi di hello.

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a>Impostare le variabili di ambiente hello

1. Trovare la versione di hello HDP del cluster Spark hello. È il nome di directory hello in `/usr/hdp/` (ad esempio, 2.5.4.2-7).

2. Configurare hdp.version per tutti i nodi. Nel Ambari Dashboard andare troppo**sezione YARN** > **configurazioni** > **avanzate**e quindi hello seguenti: 
 
    a. In `Custom yarn-site`, aggiungere una nuova proprietà `hdp.version` con valore hello della versione di hello HDP sul nodo principale hello. 
     
    b. Salvare le configurazioni di hello. Verranno visualizzati avvisi che è possibile ignorare. 
     
    c. Riavviare i servizi YARN e Oozie hello come icone di notifica hello indicano.

3. Hello set seguenti variabili di ambiente nel nodo principale hello (sostituire i valori hello esigenze):

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a>Preparare hello grafico configurazione

1. Creare un file di configurazione con hello parametri di connessione di database di Azure Cosmos nascita impostazioni e inserirlo in `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.

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

2. Hello aggiornamento `spark.driver.extraClassPath` e `spark.executor.extraClassPath` tooinclude directory hello JAR hello distribuiti nel passaggio precedente hello, in questo caso `/home/sshuser/azure-documentdb-spark/*`.

3. Fornire i seguenti dettagli per il database di Azure Cosmos hello:

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a>Caricare hello TinkerPop grafico e salvarlo tooAzure Cosmos DB
toodemonstrate come un grafico in Azure Cosmos DB, in questo esempio utilizza hello TinkerPop toopersist predefiniti TinkerPop moderna grafico. grafico Hello viene archiviato in formato Kryo e viene fornito nel repository TinkerPop hello.

1. Poiché viene eseguito in modalità YARN Gremlin, è necessario rendere disponibile nel file system Hadoop hello dati del grafico hello. Utilizzare hello comandi che seguono toomake una directory e file di copia hello grafico locale al suo interno. 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. Aggiornare temporaneamente hello `gremlin-spark.properties` file toouse `GryoInputFormat` grafico hello tooread. Indicare anche `inputLocation` come directory di hello si crea, come illustrato di seguito hello:

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. Avviare Console Gremlin e quindi creare hello seguente calcolo passaggi toopersist dati toohello configurato Azure Cosmos DB raccolta:  

    a. Creare il grafico hello `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.

    b. Usare SparkGraphComputer per la scrittura `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.

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

4. Da Esplora dati, è possibile verificare tale hello dati sono stati resi persistenti tooAzure DB Cosmos.

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a>Caricare il grafico hello da DB Cosmos Azure ed eseguire query Gremlin

1. grafico hello tooload, modificare `gremlin-spark.properties` tooset `graphReader` troppo`DocumentDBInputRDD`:

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. Grafico hello del carico, leggere i dati di hello ed eseguire query di Gremlin con esso eseguendo hello seguenti:

    a. Avviare Console Gremlin hello `bin/gremlin.sh`.

    b. Creare il grafico hello con la configurazione di hello `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.

    c. Creare un attraversamento del grafo con SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.

    d. Eseguire hello query graph Gremlin seguenti:

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
> toosee più dettagliata di registrazione, imposta il livello di registrazione di hello in `conf/log4j-console.properties` tooa livello più dettagliato.
>

## <a name="next-steps"></a>Passaggi successivi

In questo articolo, avvio rapido appreso come creare un grafico toowork con combinando DB Cosmos Azure e Spark.

> [!div class="nextstepaction"]
