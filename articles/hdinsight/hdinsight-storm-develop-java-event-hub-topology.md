---
title: eventi aaaProcess dagli hub eventi con Storm in HDInsight mediante Java | Documenti Microsoft
description: Informazioni su come creare i dati di hub eventi con una topologia di Java Storm tooprocess con Maven.
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="4aae3-103">Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="4aae3-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="4aae3-104">Informazioni su come toouse hub di eventi di Azure con Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4aae3-104">Learn how toouse Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="4aae3-105">In questo esempio utilizza i componenti basati su Java tooread e scrittura dati in hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="4aae3-105">This example uses Java-based components tooread and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="4aae3-106">Hub eventi di Azure consente tooprocess enormi quantità di dati da siti Web, applicazioni e dispositivi.</span><span class="sxs-lookup"><span data-stu-id="4aae3-106">Azure Event Hubs allows you tooprocess massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="4aae3-107">Hello beccuccio Hub eventi rende facile toouse Apache Storm in HDInsight tooanalyze questi dati in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="4aae3-107">hello Event Hub spout makes it easy toouse Apache Storm on HDInsight tooanalyze this data in real time.</span></span> <span data-ttu-id="4aae3-108">È anche possibile scrivere dati tooEvent hub dal Storm utilizzando hello bullone hub eventi.</span><span class="sxs-lookup"><span data-stu-id="4aae3-108">You can also write data tooEvent Hubs from Storm by using hello Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4aae3-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4aae3-109">Prerequisites</span></span>

* <span data-ttu-id="4aae3-110">Un cluster Apache Storm in HDInsight versione 3.6.</span><span class="sxs-lookup"><span data-stu-id="4aae3-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="4aae3-111">Per altre informazioni, vedere [Introduzione a Storm in un cluster HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4aae3-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4aae3-112">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="4aae3-112">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4aae3-113">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4aae3-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="4aae3-114">Un [Hub eventi di Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="4aae3-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="4aae3-115">[Oracle Java Developer Kit (JDK) versione 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o equivalente, ad esempio [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="4aae3-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="4aae3-116">[Maven](https://maven.apache.org/download.cgi): Maven è un sistema di compilazione per progetti Java.</span><span class="sxs-lookup"><span data-stu-id="4aae3-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="4aae3-117">Un editor di testo o un IDE (Integrated Development Environment).</span><span class="sxs-lookup"><span data-stu-id="4aae3-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4aae3-118">È possibile che l'editor di testo o l'ambiente IDE offra funzionalità specifiche per l'uso di Maven non descritte in questo documento.</span><span class="sxs-lookup"><span data-stu-id="4aae3-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="4aae3-119">Per informazioni sulle funzionalità di hello dell'ambiente di modifica, vedere la documentazione di hello per prodotto hello in uso.</span><span class="sxs-lookup"><span data-stu-id="4aae3-119">For information about hello capabilities of your editing environment, see hello documentation for hello product you are using.</span></span>

    * <span data-ttu-id="4aae3-120">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="4aae3-120">An SSH client.</span></span> <span data-ttu-id="4aae3-121">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4aae3-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="4aae3-122">Hello `ssh` e `scp` comandi.</span><span class="sxs-lookup"><span data-stu-id="4aae3-122">hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="4aae3-123">Questi sono i cluster di HDInsight toohello file toocopy utilizzato.</span><span class="sxs-lookup"><span data-stu-id="4aae3-123">These are used toocopy files toohello HDInsight cluster.</span></span> <span data-ttu-id="4aae3-124">In Windows, è possibile ottenerli con Bash in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="4aae3-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-hello-example"></a><span data-ttu-id="4aae3-125">Esempio hello comprensione</span><span class="sxs-lookup"><span data-stu-id="4aae3-125">Understanding hello example</span></span>

<span data-ttu-id="4aae3-126">Hello [eventhub hdinsight-java-storm](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) esempio contiene due topologie:</span><span class="sxs-lookup"><span data-stu-id="4aae3-126">hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="4aae3-127">Hello `resources/writer.yaml` topologia scrive dati casuali tooan Hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="4aae3-127">hello `resources/writer.yaml` topology writes random data tooan Azure Event Hub.</span></span> <span data-ttu-id="4aae3-128">dati Hello sono generati da hello `DeviceSpout` componente, ed è un ID dispositivo casuale e il valore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4aae3-128">hello data is generated by hello `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="4aae3-129">Simula quindi un dispositivo hardware che genera un ID stringa e un valore numerico.</span><span class="sxs-lookup"><span data-stu-id="4aae3-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="4aae3-130">Tre `resources/reader.yaml` topologia legge i dati provenienti dall'Hub di eventi (dati hello scritti da EventHubWriter,) analizza i dati JSON hello e quindi Registra hello `deviceId` e `deviceValue` dati.</span><span class="sxs-lookup"><span data-stu-id="4aae3-130">Thee `resources/reader.yaml` topology reads data from Event Hub (hello data written by EventHubWriter,) parses hello JSON data, and then logs hello `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="4aae3-131">dati Hello sono formattati come un documento JSON prima che venga scritto tooEvent Hub e durante la lettura dal lettore hello viene analizzata da JSON e in tuple.</span><span class="sxs-lookup"><span data-stu-id="4aae3-131">hello data is formatted as a JSON document before it is written tooEvent Hub, and when read by hello reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="4aae3-132">il formato JSON Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="4aae3-132">hello JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="4aae3-133">Configurazione del progetto</span><span class="sxs-lookup"><span data-stu-id="4aae3-133">Project configuration</span></span>

<span data-ttu-id="4aae3-134">Hello `POM.xml` file contiene informazioni di configurazione per il progetto di Maven.</span><span class="sxs-lookup"><span data-stu-id="4aae3-134">hello `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="4aae3-135">GetStringLayout Hello sono:</span><span class="sxs-lookup"><span data-stu-id="4aae3-135">hello interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="4aae3-136">Componenti di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="4aae3-136">Event Hub components</span></span>

<span data-ttu-id="4aae3-137">componente Hello che legge e scrive gli hub di eventi tooAzure si trova nella hello [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="4aae3-137">hello component that reads and writes tooAzure Event Hubs is located in hello [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="4aae3-138">Hello seguenti sezioni in hello `POM.xml` carico hello componenti del file di questo repository</span><span class="sxs-lookup"><span data-stu-id="4aae3-138">hello following sections in hello `POM.xml` file load hello components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a><span data-ttu-id="4aae3-139">Hello EventHubs Storm Spout dipendenza</span><span class="sxs-lookup"><span data-stu-id="4aae3-139">hello EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="4aae3-140">Questo codice xml definisce una dipendenza per il pacchetto eventhubs hello, che contiene un beccuccio per la lettura dagli hub eventi e un fulmine per la scrittura di tooit.</span><span class="sxs-lookup"><span data-stu-id="4aae3-140">This xml defines a dependency for hello eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing tooit.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="4aae3-141">Questo codice xml consente di configurare output di hello progetto toogenerate per Java 8, viene utilizzato da HDInsight 3.5 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="4aae3-141">This xml configures hello project toogenerate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="hello-maven-shade-plugin"></a><span data-ttu-id="4aae3-142">Hello maven-sfumatura-plug-in</span><span class="sxs-lookup"><span data-stu-id="4aae3-142">hello maven-shade-plugin</span></span>

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
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

<span data-ttu-id="4aae3-143">Questo codice xml consente di configurare output di hello toopackage soluzione hello in un file jar uber.</span><span class="sxs-lookup"><span data-stu-id="4aae3-143">This xml configures hello solution toopackage hello output into an uber jar.</span></span> <span data-ttu-id="4aae3-144">file jar Hello contiene sia il codice di progetto hello dipendenze richieste.</span><span class="sxs-lookup"><span data-stu-id="4aae3-144">hello jar contains both hello project code and required dependencies.</span></span> <span data-ttu-id="4aae3-145">Viene usato anche per:</span><span class="sxs-lookup"><span data-stu-id="4aae3-145">It is also used to:</span></span>

* <span data-ttu-id="4aae3-146">Rinominare i file di licenza per le dipendenze di hello.</span><span class="sxs-lookup"><span data-stu-id="4aae3-146">Rename license files for hello dependencies.</span></span>
* <span data-ttu-id="4aae3-147">Escludere sicurezza/firme.</span><span class="sxs-lookup"><span data-stu-id="4aae3-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="4aae3-148">Verificare che più implementazioni di hello stessa interfaccia vengono uniti in una sola voce.</span><span class="sxs-lookup"><span data-stu-id="4aae3-148">Ensure that multiple implementations of hello same interface are merged into one entry.</span></span>

<span data-ttu-id="4aae3-149">Queste impostazioni di configurazione impediscono il verificarsi di errori in fase di runtime.</span><span class="sxs-lookup"><span data-stu-id="4aae3-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="4aae3-150">Definizioni di topologia</span><span class="sxs-lookup"><span data-stu-id="4aae3-150">Topology definitions</span></span>

<span data-ttu-id="4aae3-151">Questo esempio viene utilizzato hello [flusso](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span><span class="sxs-lookup"><span data-stu-id="4aae3-151">This example uses hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="4aae3-152">Il framework utilizza le topologie di hello toodefine YAML.</span><span class="sxs-lookup"><span data-stu-id="4aae3-152">This framework uses YAML toodefine hello topologies.</span></span> <span data-ttu-id="4aae3-153">Il vantaggio principale di Hello è che non si è rigido topologia hello nel codice di linguaggio di codifica.</span><span class="sxs-lookup"><span data-stu-id="4aae3-153">hello primary benefit is that you aren't hard coding hello topology in Java code.</span></span> <span data-ttu-id="4aae3-154">Poiché è una definizione di hello YAML, è possibile modificarlo prima di inviare una topologia hello, senza la necessità di toorecompile tutti gli elementi.</span><span class="sxs-lookup"><span data-stu-id="4aae3-154">Since hello definition is YAML, you can change it before submitting hello topology, without having toorecompile everything.</span></span>

<span data-ttu-id="4aae3-155">__writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="4aae3-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

<span data-ttu-id="4aae3-156">__reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="4aae3-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a><span data-ttu-id="4aae3-157">Informare topologia hello Hub eventi</span><span class="sxs-lookup"><span data-stu-id="4aae3-157">Tell hello topology about Event Hub</span></span>

<span data-ttu-id="4aae3-158">In fase di esecuzione hello `dev.properties` file è utilizzato toopass hello Hub eventi configurazione toohello topologia.</span><span class="sxs-lookup"><span data-stu-id="4aae3-158">At run time, hello `dev.properties` file is used toopass hello Event Hub configuration toohello topology.</span></span> <span data-ttu-id="4aae3-159">Hello esempio seguente è contenuto predefinito hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="4aae3-159">hello following example is hello default contents of hello file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="4aae3-160">Configurare le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="4aae3-160">Configure environment variables</span></span>

<span data-ttu-id="4aae3-161">Hello seguenti variabili di ambiente possono essere impostate durante l'installazione di Java e hello JDK nella workstation di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="4aae3-161">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="4aae3-162">Tuttavia, è necessario verificare che esistano e che contengono i valori corretti di hello per il sistema.</span><span class="sxs-lookup"><span data-stu-id="4aae3-162">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="4aae3-163">**JAVA_HOME** -deve puntare toohello directory in cui è installato Java runtime environment (JRE) di hello.</span><span class="sxs-lookup"><span data-stu-id="4aae3-163">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="4aae3-164">Ad esempio, in una distribuzione di Unix o Linux, deve essere un valore simile troppo`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="4aae3-164">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="4aae3-165">In Windows, avrebbe un valore simile troppo`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="4aae3-165">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="4aae3-166">**PERCORSO** -deve contenere hello seguenti percorsi:</span><span class="sxs-lookup"><span data-stu-id="4aae3-166">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="4aae3-167">**JAVA_HOME** (o percorso equivalente hello)</span><span class="sxs-lookup"><span data-stu-id="4aae3-167">**JAVA_HOME** (or hello equivalent path)</span></span>
  * <span data-ttu-id="4aae3-168">**JAVA_HOME\bin** (o percorso equivalente hello)</span><span class="sxs-lookup"><span data-stu-id="4aae3-168">**JAVA_HOME\bin** (or hello equivalent path)</span></span>
  * <span data-ttu-id="4aae3-169">directory di Hello in cui è installato Maven</span><span class="sxs-lookup"><span data-stu-id="4aae3-169">hello directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="4aae3-170">Configurare l'hub eventi</span><span class="sxs-lookup"><span data-stu-id="4aae3-170">Configure Event Hub</span></span>

<span data-ttu-id="4aae3-171">Hub eventi è l'origine dati hello per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="4aae3-171">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="4aae3-172">Utilizzare hello seguendo i passaggi toocreate un Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="4aae3-172">Use hello following steps toocreate a Event Hub.</span></span>

1. <span data-ttu-id="4aae3-173">Da hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **NEW** > **Bus di servizio** > **Hub eventi**  >  **Creazione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="4aae3-173">From hello [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="4aae3-174">In hello **aggiungere un nuovo Hub eventi** schermata, immettere un **nome Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="4aae3-174">On hello **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="4aae3-175">Seleziona hello **area** toocreate hello hub, quindi creare uno spazio dei nomi o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="4aae3-175">Select hello **Region** toocreate hello hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="4aae3-176">Infine, fare clic su hello **freccia** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="4aae3-176">Finally, click hello **Arrow** toocontinue.</span></span>

    ![procedura guidata - pagina 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="4aae3-178">Selezionare hello stesso **percorso** come l'elevato numero di latenza tooreduce di HDInsight server e i costi.</span><span class="sxs-lookup"><span data-stu-id="4aae3-178">Select hello same **Location** as your Storm on HDInsight server tooreduce latency and costs.</span></span>

3. <span data-ttu-id="4aae3-179">In hello **configurare Hub eventi** immettere hello **numero di partizione** e **memorizzazione dei messaggi** valori.</span><span class="sxs-lookup"><span data-stu-id="4aae3-179">On hello **Configure Event Hub** screen, enter hello **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="4aae3-180">Per questo esempio usare un numero di partizioni pari a 10 e un valore di conservazione dei messaggi pari a 1.</span><span class="sxs-lookup"><span data-stu-id="4aae3-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="4aae3-181">Si noti il numero di partizioni hello perché questo valore è necessario in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="4aae3-181">Note hello partition count because you need this value later.</span></span>

    ![procedura guidata - pagina 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="4aae3-183">Una volta hub eventi hello hello creati, selezionare lo spazio dei nomi, selezionare **hub eventi**, quindi selezionare l'hub di eventi hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4aae3-183">After hello event hub has been created, select hello namespace, select **Event Hubs**, and then select hello event hub that you created earlier.</span></span>
5. <span data-ttu-id="4aae3-184">Selezionare **configura**, quindi creare due nuovi criteri di accesso utilizzando hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="4aae3-184">Select **Configure**, then create two new access policies by using hello following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="4aae3-185">Nome</span><span class="sxs-lookup"><span data-stu-id="4aae3-185">Name</span></span></th><th><span data-ttu-id="4aae3-186">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="4aae3-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="4aae3-187">Writer</span><span class="sxs-lookup"><span data-stu-id="4aae3-187">Writer</span></span></td><td><span data-ttu-id="4aae3-188">Invio</span><span class="sxs-lookup"><span data-stu-id="4aae3-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="4aae3-189">Reader</span><span class="sxs-lookup"><span data-stu-id="4aae3-189">Reader</span></span></td><td><span data-ttu-id="4aae3-190">Attesa</span><span class="sxs-lookup"><span data-stu-id="4aae3-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="4aae3-191">Dopo aver creato le autorizzazioni di hello, selezionare hello **salvare** icona hello parte inferiore della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="4aae3-191">After You create hello permissions, select hello **Save** icon at hello bottom of hello page.</span></span> <span data-ttu-id="4aae3-192">Questi criteri di accesso condiviso sono utilizzati tooread e scrivere tooEvent Hub.</span><span class="sxs-lookup"><span data-stu-id="4aae3-192">These shared access policies are used tooread and write tooEvent Hub.</span></span>

    ![criteri](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="4aae3-194">Dopo aver salvato i criteri di hello, usare hello **generatore di chiavi di accesso condiviso** nella parte inferiore di hello della chiave di hello pagina tooretrieve hello per hello **writer** e **lettore** criteri.</span><span class="sxs-lookup"><span data-stu-id="4aae3-194">After you save hello policies, use hello **Shared access key generator** at hello bottom of hello page tooretrieve hello key for hello **writer** and **reader** policies.</span></span> <span data-ttu-id="4aae3-195">Salvare queste chiavi.</span><span class="sxs-lookup"><span data-stu-id="4aae3-195">Save these keys.</span></span>

## <a name="download-and-build-hello-project"></a><span data-ttu-id="4aae3-196">Scaricare e compilare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="4aae3-196">Download and build hello project</span></span>

1. <span data-ttu-id="4aae3-197">Scaricare il progetto di hello da GitHub: [eventhub hdinsight-java-storm](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="4aae3-197">Download hello project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="4aae3-198">È possibile scaricare il pacchetto di hello come archivio zip o utilizzare [git](https://git-scm.com/) tooclone il progetto hello in locale.</span><span class="sxs-lookup"><span data-stu-id="4aae3-198">You can either download hello package as a zip archive, or use [git](https://git-scm.com/) tooclone hello project locally.</span></span>

2. <span data-ttu-id="4aae3-199">Modificare hello `dev.properties` file con la configurazione di hello per l'Hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="4aae3-199">Modify hello `dev.properties` file with hello configuration for your Event Hub.</span></span>

3. <span data-ttu-id="4aae3-200">Utilizzare hello seguente progetto hello toobuild e del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="4aae3-200">Use hello following toobuild and package hello project:</span></span>

        mvn package

    <span data-ttu-id="4aae3-201">Questo comando Scarica le dipendenze richieste, le compilazioni, e quindi i pacchetti hello progetto.</span><span class="sxs-lookup"><span data-stu-id="4aae3-201">This command downloads required dependencies, builds, and then packages hello project.</span></span> <span data-ttu-id="4aae3-202">output di Hello viene archiviato in hello **/destinazione** directory come **EventHubExample-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="4aae3-202">hello output is stored in hello **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="4aae3-203">Test in locale</span><span class="sxs-lookup"><span data-stu-id="4aae3-203">Test locally</span></span>

<span data-ttu-id="4aae3-204">Poiché queste topologie solo leggere e scrivere tooEvent hub, è possibile eseguirne il test in locale se dispone di un [ambiente di sviluppo Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="4aae3-204">Since these topologies just read and write tooEvent Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="4aae3-205">Utilizzare hello seguendo i passaggi toorun localmente nell'ambiente di sviluppo hello:</span><span class="sxs-lookup"><span data-stu-id="4aae3-205">Use hello following steps toorun locally in hello dev environment:</span></span>

1. <span data-ttu-id="4aae3-206">Eseguire writer hello:</span><span class="sxs-lookup"><span data-stu-id="4aae3-206">Run hello writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="4aae3-207">Eseguire la lettura hello:</span><span class="sxs-lookup"><span data-stu-id="4aae3-207">Run hello reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="4aae3-208">`--local`: Topologia di hello esecuzione in modalità locale (non distribuite).</span><span class="sxs-lookup"><span data-stu-id="4aae3-208">`--local`: Run hello topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="4aae3-209">`-R /writer.yaml`: Caricare la definizione di topologia hello da hello `resources` sotto forma di file jar hello.</span><span class="sxs-lookup"><span data-stu-id="4aae3-209">`-R /writer.yaml`: Load hello topology definition from hello `resources` packaged in hello jar.</span></span> <span data-ttu-id="4aae3-210">Se la topologia hello è un file hello file System locale, specificare hello percorso tooit come ultimo parametro hello.</span><span class="sxs-lookup"><span data-stu-id="4aae3-210">If hello topology is a file on hello local file system, specify hello path tooit as hello last parameter instead.</span></span>
> * <span data-ttu-id="4aae3-211">`--filter dev.properties`: Utilizzare il contenuto di hello del `dev.properties` toofill valori hello in definizioni di topologia hello.</span><span class="sxs-lookup"><span data-stu-id="4aae3-211">`--filter dev.properties`: Use hello contents of `dev.properties` toofill in hello values in hello topology definitions.</span></span> <span data-ttu-id="4aae3-212">ad esempio `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="4aae3-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="4aae3-213">Output è connesso toohello console durante l'esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="4aae3-213">Output is logged toohello console when running locally.</span></span> <span data-ttu-id="4aae3-214">Utilizzare __Ctrl + C__ topologia hello toostop.</span><span class="sxs-lookup"><span data-stu-id="4aae3-214">Use __Ctrl+C__ toostop hello topology.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="4aae3-215">Distribuire le topologie di hello</span><span class="sxs-lookup"><span data-stu-id="4aae3-215">Deploy hello topologies</span></span>

1. <span data-ttu-id="4aae3-216">Utilizzare SCP toocopy hello jar pacchetto tooyour cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4aae3-216">Use SCP toocopy hello jar package tooyour HDInsight cluster.</span></span> <span data-ttu-id="4aae3-217">Sostituire il nome utente con utente SSH hello per il cluster.</span><span class="sxs-lookup"><span data-stu-id="4aae3-217">Replace USERNAME with hello SSH user for your cluster.</span></span> <span data-ttu-id="4aae3-218">Sostituire CLUSTERNAME con nome hello del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4aae3-218">Replace CLUSTERNAME with hello name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="4aae3-219">Se si utilizza una password per l'account SSH, si è password hello tooenter richiesta.</span><span class="sxs-lookup"><span data-stu-id="4aae3-219">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="4aae3-220">Se si utilizza una chiave SSH con l'account di hello, potrebbe essere necessario hello toouse `-i` parametro toospecify hello percorso toohello file di chiave.</span><span class="sxs-lookup"><span data-stu-id="4aae3-220">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="4aae3-221">Ad esempio, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="4aae3-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="4aae3-222">Questo comando copia hello toohello home directory del file dell'utente di SSH nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4aae3-222">This command copies hello file toohello home directory of your SSH user on hello cluster.</span></span>

2. <span data-ttu-id="4aae3-223">Al termine il caricamento di file hello, utilizzare cluster di HDInsight toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="4aae3-223">Once hello file has finished uploading, use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="4aae3-224">Sostituire **USERNAME** nome hello dell'accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="4aae3-224">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="4aae3-225">Sostituire **CLUSTERNAME** con il nome del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4aae3-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="4aae3-226">Se si utilizza una password per l'account SSH, si è password hello tooenter richiesta.</span><span class="sxs-lookup"><span data-stu-id="4aae3-226">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="4aae3-227">Se si utilizza una chiave SSH con l'account di hello, potrebbe essere necessario hello toouse `-i` parametro toospecify hello percorso toohello file di chiave.</span><span class="sxs-lookup"><span data-stu-id="4aae3-227">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="4aae3-228">esempio Hello carica hello della chiave privata `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="4aae3-228">hello following example loads hello private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="4aae3-229">Utilizzare hello topologie hello toostart di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4aae3-229">Use hello following command toostart hello topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="4aae3-230">`--remote`: Invia hello topologia toohello servizio Nimbus, che avvia su nodi di lavoro hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4aae3-230">`--remote`: Submits hello topology toohello Nimbus service, which starts it on hello worker nodes in hello cluster.</span></span>

4. <span data-ttu-id="4aae3-231">dati registrato hello tooview, visitare toohttps://CLUSTERNAME.azurehdinsight.net/stormui, in cui __CLUSTERNAME__ hello nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4aae3-231">tooview hello logged data, go toohttps://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="4aae3-232">Selezionare le topologie di hello e drill-down toohello componenti.</span><span class="sxs-lookup"><span data-stu-id="4aae3-232">Select hello topologies and drill down toohello components.</span></span> <span data-ttu-id="4aae3-233">Seleziona hello __porta__ voce per un'istanza di un componente di tooview le informazioni registrate.</span><span class="sxs-lookup"><span data-stu-id="4aae3-233">Select hello __port__ entry for an instance of a component tooview logged information.</span></span>

5. <span data-ttu-id="4aae3-234">Utilizzare hello topologie di hello toostop i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4aae3-234">Use hello following commands toostop hello topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="4aae3-235">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="4aae3-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="4aae3-236">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4aae3-236">Next steps</span></span>

* [<span data-ttu-id="4aae3-237">Topologie di esempio per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4aae3-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
