---
title: aaaApache Storm topologia di esempio Java - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toocreate Apache Storm topologie Java mediante la creazione di una parola di esempio conteggio topologia.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: apache storm, esempio di apache storm, storm java, esempio di topologia storm
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a>Creare una topologia Apache Storm in Java

Informazioni su come toocreate una topologia basata su Java per Apache Storm. Creare una topologia Storm che implementa un'applicazione di conteggio delle parole. Utilizzare Maven toobuild pacchetto hello nel progetto. Quindi, imparare come toodefine hello topologia utilizzando hello framework luminoso.

> [!NOTE]
> il framework di flusso Hello è disponibile in Storm 0.10.0 o versione successiva. Storm 0.10.0 è disponibile con HDInsight 3.3 e 3.4.

Dopo aver completato i passaggi di hello in questo documento, è possibile distribuire hello topologia tooApache Storm in HDInsight.

> [!NOTE]
> Una versione completa degli esempi di topologia Storm hello creato in questo documento è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).

## <a name="prerequisites"></a>Prerequisiti

* [Java Developer Kit (JDK) versione 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* [Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven è un sistema per la compilazione di progetti per Java.

* Un editor di testo o ambiente IDE.

## <a name="configure-environment-variables"></a>Configurare le variabili di ambiente

Hello seguenti variabili di ambiente possono essere impostate quando si installa Java e hello JDK. Tuttavia, è necessario verificare che esistano e che contengono i valori corretti di hello per il sistema.

* **JAVA_HOME** -deve puntare toohello directory in cui è installato Java runtime environment (JRE) di hello. Ad esempio, in una distribuzione di Unix o Linux, deve essere un valore simile troppo`/usr/lib/jvm/java-7-oracle`. In Windows, avrebbe un valore simile troppo`c:\Program Files (x86)\Java\jre1.7`

* **PERCORSO** -deve contenere hello seguenti percorsi:

  * **JAVA_HOME** (o percorso equivalente hello)

  * **JAVA_HOME\bin** (o percorso equivalente hello)

  * directory di Hello in cui è installato Maven

## <a name="create-a-maven-project"></a>Creare un progetto Maven

Dalla riga di comando hello, utilizzare hello comando che segue toocreate un progetto di Maven denominato **WordCount**:

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> Se si utilizza PowerShell, è necessario racchiudere i parametri `-D` tra virgolette.
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

Questo comando crea una directory denominata `WordCount` nella posizione corrente di hello, che contiene un progetto di Maven base. Hello `WordCount` directory contiene hello seguenti elementi:

* `pom.xml`: Contiene le impostazioni per il progetto di Maven hello.
* `src\main\java\com\microsoft\example`: contiene il codice dell'applicazione.
* `src\test\java\com\microsoft\example`: contiene i test per l'applicazione. 

### <a name="remove-hello-generated-example-code"></a>Rimuovere il codice di esempio hello generato

Eliminare i test generato hello e i file dell'applicazione hello:

* **src\test\java\com\microsoft\example\AppTest.java**
* **src\main\java\com\microsoft\example\App.java**

## <a name="add-maven-repositories"></a>Aggiungere archivi Maven

HDInsight è basato sulla hello Hortonworks Data Platform (HDP), pertanto si consiglia di utilizzare le dipendenze di toodownload hello Hortonworks repository per i progetti Apache Storm. In hello __pom.xml__ file, aggiungere hello seguente XML dopo hello `<url>http://maven.apache.org</url>` riga:

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a>Aggiungere le proprietà

Maven consente valori a livello di progetto toodefine denominati di proprietà. In hello __pom.xml__, aggiungere hello seguente testo dopo hello `</repositories>` riga:

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

È ora possibile utilizzare questo valore nelle altre sezioni di hello `pom.xml`. Ad esempio, quando si specifica versione di hello di Storm componenti, è possibile utilizzare `${storm.version}` anziché a livello di codice un valore.

## <a name="add-dependencies"></a>Aggiungere le dipendenze

Aggiungere una dipendenza per i componenti Storm. Aprire hello `pom.xml` file e aggiungere hello seguente di codice hello `<dependencies>` sezione:

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

In fase di compilazione Maven Usa questo toolook informazioni `storm-core` nel repository di Maven hello. Effettua prima una ricerca nel repository di hello nel computer locale. Se non vi sono file di hello, Maven li scarica da archivio Maven pubblico hello e li archivia nel repository locale hello.

> [!NOTE]
> Hello preavviso `<scope>provided</scope>` riga in questa sezione. Questa impostazione indica Maven tooexclude **elevato numero di core** dai file JAR di vengono creati, perché viene fornita dal sistema hello.

## <a name="build-configuration"></a>Configurare la compilazione

Plug-in di Maven consentono di fasi di compilazione toocustomize hello del progetto hello. Ad esempio, come viene compilato il progetto hello o come toopackage in un file JAR. Aprire hello `pom.xml` file e aggiungere hello seguente codice direttamente sopra hello `</project>` riga.

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

In questa sezione viene utilizzato tooadd plug-in, risorse e altre opzioni di configurazione di compilazione. Per un riferimento completo di hello **pom.xml** file, vedere [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).

### <a name="add-plug-ins"></a>Aggiungere plug-in

Per le topologie di Apache Storm implementate in Java, hello [plug-in Maven Exec](http://www.mojohaus.org/exec-maven-plugin/) è utile perché consente tooeasily eseguire topologia hello in locale nell'ambiente di sviluppo. Aggiungere hello seguente toohello `<plugins>` sezione di hello `pom.xml` file plug-in di tooinclude hello Maven Exec:

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

Un'altra utile plug-in è hello [plug-in compilatore di Apache Maven](http://maven.apache.org/plugins/maven-compiler-plugin/), che viene utilizzato toochange opzioni di compilazione. modifiche di Hello hello versione Java che utilizza Maven per hello origine e di destinazione per l'applicazione.

* Per HDInsight __3.4 o versioni precedenti__, impostare l'origine hello e too__1.7__ versione Java di destinazione.

* Per HDInsight __3.5__, impostare l'origine hello e too__1.8__ versione Java di destinazione.

Aggiungere hello seguente testo hello `<plugins>` sezione di hello `pom.xml` file plug-in Apache Maven compilatore hello di tooinclude. In questo esempio specifica 1.8, pertanto la versione di HDInsight destinazione di hello è 3.5.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a>Configure resources

la sezione relativa alle risorse Hello consente le risorse non di codice tooinclude, ad esempio i file di configurazione necessari per i componenti nella topologia hello. Per questo esempio, aggiungere hello seguente testo hello `<resources>` sezione di hello ' pom.xml file.

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

Questo esempio aggiunge una directory delle risorse hello nella directory radice del progetto hello hello (`${basedir}`) come un percorso che contiene le risorse e include file hello denominato `log4j2.xml`. Questo file è utilizzato tooconfigure quali informazioni vengono registrate dalla topologia hello.

## <a name="create-hello-topology"></a>Creare la topologia hello

Una topologia Apache Storm basata su Java è costituita da tre componenti che è necessario creare o a cui è necessario fare riferimento come dipendenza.

* **Spouts**: legge origini dati dall'esterno e genera i flussi di dati nella topologia hello.

* **Bolt**: esegue l'elaborazione sui flussi generati dagli spout o da altri bolt e genera uno o più flussi.

* **Topologia**: definisce la modalità spouts hello e dadi sono disposti e fornisce il punto di ingresso di hello per topologia hello.

### <a name="create-hello-spout"></a>Creare beccuccio hello

tooreduce requisiti per la configurazione di origini dati esterne, hello seguente beccuccio genera semplicemente frasi casuale. È una versione modificata del beccuccio che viene fornito con hello [esempi Storm Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).

> [!NOTE]
> Per un esempio di beccuccio che legge da un'origine dati esterna, vedere uno dei seguenti esempi hello:
>
> * [TwitterSampleSpout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): spout di esempio che legge da Twitter
> * [Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): spout che legge da Kafka

Per beccuccio hello, creare un file denominato `RandomSentenceSpout.java` in hello `src\main\java\com\microsoft\example` hello directory e l'utilizzo seguente di codice Java come contenuto hello:

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> Anche se questa topologia viene utilizzato un solo beccuccio, altri utenti possono invece avere diversi che feed di dati da origini diverse in una topologia di hello.

### <a name="create-hello-bolts"></a>Creare bulloni hello

Bulloni gestiscono l'elaborazione dati hello. Questa topologia usa due bolt:

* **SplitSentence**: suddivide frasi hello generate da **RandomSentenceSpout** in singole parole.

* **WordCount**: conta le occorrenze di ciascuna parola.

> [!NOTE]
> Bulloni eseguire qualsiasi operazione, ad esempio, calcolo, la persistenza o tooexternal componenti per comunicare con.

Creare due nuovi file, `SplitSentence.java` e `WordCount.java` in hello `src\main\java\com\microsoft\example` directory. Utilizzare hello segue testo come contenuto di hello per i file hello:

#### <a name="splitsentence"></a>SplitSentence

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a>WordCount

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a>Definire la topologia hello

topologia Hello collega spouts hello e bulloni insieme in un grafico, che definisce il flusso dei dati tra i componenti di hello. Fornisce inoltre gli hint parallelismo Storm utilizza per la creazione di istanze dei componenti di hello all'interno del cluster di hello.

Hello immagine seguente è un diagramma di base del grafico hello dei componenti per questa topologia.

![hello visualizzazione Diagramma spouts e bulloni disposizione](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

tooimplement hello topologia, creare un file denominato `WordCountTopology.java` in hello `src\main\java\com\microsoft\example` directory. Utilizzare hello seguente di codice Java come contenuto di hello del file hello:

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a>Configurare la registrazione

Storm Usa Log4j Apache toolog informazioni. Se non si configura la registrazione, la topologia hello genera informazioni di diagnostica. toocontrol informazioni di connessione, creare un file denominato `log4j2.xml` in hello `resources` directory. Utilizzare hello seguente XML come contenuto di hello del file hello.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

Questo codice XML consente di configurare un nuovo logger per hello `com.microsoft.example` (classe), che include i componenti di hello in questa topologia di esempio. livello di Hello è impostato tootrace per questo logger, che acquisisce le informazioni di registrazione generate dai componenti in questa topologia.

Hello `<Root level="error">` sezione Configura a livello di radice hello di registrazione (tutti gli elementi non in `com.microsoft.example`) tooonly informazioni sugli errori di log.

Per altre informazioni sulla configurazione della registrazione per Log4j, vedere [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).

> [!NOTE]
> Storm versione 0.10.0 e successive usano Log4j 2.x. Le versioni precedenti usano Log4j 1.x, che impiega un formato diverso per la configurazione del log. Per informazioni sulla configurazione precedente hello, vedere [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).

## <a name="test-hello-topology-locally"></a>Topologia di hello test localmente

Dopo aver salvato il file hello, utilizzare hello seguente topologia hello tootest di comando localmente.

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

Durante l'esecuzione, la topologia hello Visualizza le informazioni di avvio. Hello testo riportato di seguito è riportato un esempio dell'output di hello word conteggio:

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

Questo log di esempio indica tale parola hello ' e ' è stato emesso 113 volte. Hello conteggio risale toogo purché topologia hello eseguito poiché beccuccio hello genera continuamente hello stesse frasi.

C'è un intervallo di 5 secondi tra l'emissione di parole e i conteggi. Hello **WordCount** configurato tooonly generi informazioni quando arriva una tupla di segni di graduazione. Richiede che le tuple tick vengano recapitate solo ogni cinque secondi.

## <a name="convert-hello-topology-tooflux"></a>Convertire hello topologia tooFlux

Flusso è un nuovo framework disponibili con Storm 0.10.0 e versioni successive, che consente la configurazione tooseparate dall'implementazione. I componenti sono ancora definiti in Java, ma la topologia hello è definita mediante un file YAML. È possibile creare un pacchetto una definizione di topologia predefinito con il progetto o utilizzare un file autonomo per l'invio di topologia hello. Quando si inviano hello topologia tooStorm, è possibile utilizzare variabili di ambiente o i valori di configurazione file toopopulate nella definizione della topologia YAML hello.

file YAML Hello definisce hello componenti toouse per topologia hello e flusso di dati hello tra di essi. È possibile includere un file YAML come parte del file jar hello o è possibile utilizzare un file YAML esterno.

Per altre informazioni su Flux, vedere [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

> [!WARNING]
> Scadenza tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) con Storm 1.0.1, potrebbe essere necessario tooinstall un [ambiente di sviluppo Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun localmente topologie di flusso.

1. Spostare hello `WordCountTopology.java` file di progetto hello. In precedenza, questo file definito topologia hello, ma non è necessaria con flusso.

2. In hello `resources` directory, creare un file denominato `topology.yaml`. Utilizzare hello segue testo come contenuto di hello di questo file.

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. Rendere hello dopo le modifiche toohello `pom.xml` file.
   
   * Aggiungere hello seguente nuove dipendenze nella hello `<dependencies>` sezione:
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * Aggiungere i seguenti plug-in toohello hello `<plugins>` sezione. Questo plug-in gestisce la creazione di hello di un pacchetto (file jar) per il progetto hello e applica alcuni tooFlux specifico di trasformazioni durante la creazione di pacchetti hello.
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
                </transformers>
                <!-- Keep us from getting a bad signature error -->
                <filters>
                    <filter>
                        <artifact>*:*</artifact>
                        <excludes>
                            <exclude>META-INF/*.SF</exclude>
                            <exclude>META-INF/*.DSA</exclude>
                            <exclude>META-INF/*.RSA</exclude>
                        </excludes>
                    </filter>
                </filters>
            </configuration>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        ```

   * In hello **plug-in exec maven** `<configuration>` sezione, modificare il valore di hello per `<mainClass>` troppo`org.apache.storm.flux.Flux`. Questa impostazione consente toohandle luminoso eseguito localmente topologia hello in fase di sviluppo.

   * In hello `<resources>` sezione, aggiungere hello seguente toohello `<includes>`. Questo codice XML include file YAML hello che definisce la topologia hello come parte del progetto hello.

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a>Topologia luminoso hello di test in locale

1. Utilizzare hello seguente toocompile ed eseguire topologia luminoso hello Maven utilizzando:

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    Se si usa PowerShell, usare hello comando seguente:

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > Questo comando non va a buon fine se la topologia usa bit di Storm 1.0.1. I motivi della mancata riuscita sono indicati in [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055). In alternativa, [installare Storm nell'ambiente di sviluppo](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) e hello di utilizzare le seguenti informazioni.

    Se dispone di [installato Storm nell'ambiente di sviluppo](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), è possibile utilizzare i seguenti comandi invece hello:

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    Hello `--local` parametro viene eseguito topologia hello in modalità locale in ambiente di sviluppo. Hello `-R /topology.yaml` parametro utilizza hello `topology.yaml` risorsa file dalla topologia di hello jar file toodefine hello.

    Durante l'esecuzione, la topologia hello Visualizza le informazioni di avvio. Dopo il testo Hello è riportato un esempio di output di hello:

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    C'è un ritardo di 10 secondi tra i batch delle informazioni registrate.

2. Creare una copia di hello `topology.yaml` file dal progetto hello. Nuovo file di nome hello `newtopology.yaml`. In hello `newtopology.yaml` file, trovare il seguente hello sezione e modificare il valore di hello di `10` troppo`5`. Questo intervallo di hello modifica modifiche tra la creazione di batch di word conta da too5 10 secondi.

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    In alternativa, se si dispone di Storm nell'ambiente di sviluppo:

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    Hello modifica `/path/to/newtopology.yaml` toohello percorso toohello newtopology.yaml file creato nel passaggio precedente hello. Questo comando Usa hello newtopology.yaml come definizione della topologia hello. Poiché non è stato incluso hello `compile` Maven parametro, utilizza la versione di hello del progetto hello creato nei passaggi precedenti.

    Una volta hello topologia venga avviato, si noterà che ora hello tra i batch generato è stato modificato il valore hello tooreflect in newtopology.yaml. Pertanto, è possibile vedere che è possibile modificare la configurazione tramite un file YAML senza la necessità della topologia hello toorecompile.

Per ulteriori informazioni su queste e altre funzionalità di hello luminoso framework, vedere [luminoso (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

## <a name="trident"></a>Trident

Trident è un'astrazione di alto livello fornita da Storm che supporta l'elaborazione con informazioni sullo stato. Hello il vantaggio principale di Trident consiste nel fatto che sia possibile garantire che ogni messaggio che viene inserito topologia hello viene elaborata una sola volta. Senza l'uso di Trident, la topologia può garantire solo che i messaggi vengono elaborati almeno una volta. Esistono altre differenze, ad esempio la disponibilità di componenti predefiniti che possono essere usati senza che sia necessario creare bolt. I bolt sono infatti sostituiti da componenti meno generici, ad esempio filtri, proiezioni e funzioni.

È possibile creare applicazioni Trident mediante progetti Maven Utilizzare hello basic stesso i passaggi come riportata in precedenza in questo articolo, ovvero solo codice hello è diverso. Trident anche non (attualmente) utilizzabile con framework di hello luminoso.

Per ulteriori informazioni su Trident, vedere hello [panoramica dell'API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).

Per un'applicazione Trident di esempio, vedere [Temi di tendenza Twitter con Apache Storm in HDInsight](hdinsight-storm-twitter-trending.md).

## <a name="next-steps"></a>Passaggi successivi

Si è appreso come toocreate una topologia di Storm con Java. è possibile passare agli argomenti seguenti:

* [Distribuzione e gestione di topologie Apache Storm in HDInsight](hdinsight-storm-deploy-monitor-topology.md)

* [Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Per altri esempi di topologie Storm, vedere [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md).

