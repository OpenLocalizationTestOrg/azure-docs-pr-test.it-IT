---
title: Elaborare eventi di Hub eventi con Storm in HDInsight usando Java| Documentazione Microsoft
description: Informazioni su come elaborare i dati dell'hub eventi con una topologia Storm Java creata con Maven.
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
ms.openlocfilehash: 2e8ebbdab2be7bed224a67facec798820615bb22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="55283-103">Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="55283-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="55283-104">Informazioni su come usare l'hub eventi di Azure con Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="55283-104">Learn how to use Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="55283-105">Questo esempio usa componenti basati su Java per leggere e scrivere dati nell'hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="55283-105">This example uses Java-based components to read and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="55283-106">L'hub eventi di Azure consente di elaborare grandi quantità di dati da siti Web, app e dispositivi.</span><span class="sxs-lookup"><span data-stu-id="55283-106">Azure Event Hubs allows you to process massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="55283-107">Lo spout dell'hub eventi semplifica l'uso di Apache Storm in HDInsight per analizzare questi dati in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="55283-107">The Event Hub spout makes it easy to use Apache Storm on HDInsight to analyze this data in real time.</span></span> <span data-ttu-id="55283-108">È anche possibile scrivere dati nell'hub eventi da Storm usando il relativo bolt.</span><span class="sxs-lookup"><span data-stu-id="55283-108">You can also write data to Event Hubs from Storm by using the Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55283-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="55283-109">Prerequisites</span></span>

* <span data-ttu-id="55283-110">Un cluster Apache Storm in HDInsight versione 3.6.</span><span class="sxs-lookup"><span data-stu-id="55283-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="55283-111">Per altre informazioni, vedere [Introduzione a Storm in un cluster HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="55283-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="55283-112">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="55283-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="55283-113">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="55283-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="55283-114">Un [Hub eventi di Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="55283-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="55283-115">[Oracle Java Developer Kit (JDK) versione 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o equivalente, ad esempio [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="55283-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="55283-116">[Maven](https://maven.apache.org/download.cgi): Maven è un sistema di compilazione per progetti Java.</span><span class="sxs-lookup"><span data-stu-id="55283-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="55283-117">Un editor di testo o un IDE (Integrated Development Environment).</span><span class="sxs-lookup"><span data-stu-id="55283-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="55283-118">È possibile che l'editor di testo o l'ambiente IDE offra funzionalità specifiche per l'uso di Maven non descritte in questo documento.</span><span class="sxs-lookup"><span data-stu-id="55283-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="55283-119">Per informazioni sulle funzionalità dell'ambiente di modifica, vedere la documentazione del prodotto usato.</span><span class="sxs-lookup"><span data-stu-id="55283-119">For information about the capabilities of your editing environment, see the documentation for the product you are using.</span></span>

    * <span data-ttu-id="55283-120">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="55283-120">An SSH client.</span></span> <span data-ttu-id="55283-121">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="55283-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="55283-122">Comandi `ssh` e `scp`.</span><span class="sxs-lookup"><span data-stu-id="55283-122">The `ssh` and `scp` commands.</span></span> <span data-ttu-id="55283-123">Questi vengono usati per copiare i file nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="55283-123">These are used to copy files to the HDInsight cluster.</span></span> <span data-ttu-id="55283-124">In Windows, è possibile ottenerli con Bash in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="55283-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-the-example"></a><span data-ttu-id="55283-125">Informazioni sull'esempio</span><span class="sxs-lookup"><span data-stu-id="55283-125">Understanding the example</span></span>

<span data-ttu-id="55283-126">L'esempio [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) include due topologie:</span><span class="sxs-lookup"><span data-stu-id="55283-126">The [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="55283-127">La topologia `resources/writer.yaml` scrive dati casuali in un hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="55283-127">The `resources/writer.yaml` topology writes random data to an Azure Event Hub.</span></span> <span data-ttu-id="55283-128">I dati vengono generati dal componente `DeviceSpout` e sono costituiti da un ID dispositivo casuale e da un valore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="55283-128">The data is generated by the `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="55283-129">Simula quindi un dispositivo hardware che genera un ID stringa e un valore numerico.</span><span class="sxs-lookup"><span data-stu-id="55283-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="55283-130">La topologia `resources/reader.yaml` legge i dati provenienti dall'Hub di eventi, ovvero i dati scritti da EventHubWriter, analizza i dati JSON e quindi registra i dati `deviceId` e `deviceValue`.</span><span class="sxs-lookup"><span data-stu-id="55283-130">Thee `resources/reader.yaml` topology reads data from Event Hub (the data written by EventHubWriter,) parses the JSON data, and then logs the `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="55283-131">I dati vengono formattati come documento JSON prima di essere scritti nell'hub eventi e quando vengono letti dal lettore, vengono analizzati da JSON e inseriti in tuple.</span><span class="sxs-lookup"><span data-stu-id="55283-131">The data is formatted as a JSON document before it is written to Event Hub, and when read by the reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="55283-132">Il formato JSON è il seguente:</span><span class="sxs-lookup"><span data-stu-id="55283-132">The JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="55283-133">Configurazione del progetto</span><span class="sxs-lookup"><span data-stu-id="55283-133">Project configuration</span></span>

<span data-ttu-id="55283-134">Il file `POM.xml` contiene informazioni di configurazione per questo progetto Maven.</span><span class="sxs-lookup"><span data-stu-id="55283-134">The `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="55283-135">Ecco gli aspetti interessanti:</span><span class="sxs-lookup"><span data-stu-id="55283-135">The interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="55283-136">Componenti di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="55283-136">Event Hub components</span></span>

<span data-ttu-id="55283-137">Il componente che legge e scrive in Hub di eventi di Azure si trova nel [repository HDInsight](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="55283-137">The component that reads and writes to Azure Event Hubs is located in the [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="55283-138">Le sezioni seguenti nel file `POM.xml` caricano i componenti da questo repository</span><span class="sxs-lookup"><span data-stu-id="55283-138">The following sections in the `POM.xml` file load the components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="the-eventhubs-storm-spout-dependency"></a><span data-ttu-id="55283-139">Dipendenza di spout Storm in EventHubs</span><span class="sxs-lookup"><span data-stu-id="55283-139">The EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="55283-140">Questo XML definisce una dipendenza per il pacchetto eventhubs che contiene sia uno spout per la lettura dall'hub eventi sia un bolt per la scrittura nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="55283-140">This xml defines a dependency for the eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing to it.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="55283-141">Questo file XML consente di configurare il progetto per generare l'output per Java 8, che viene usato da HDInsight 3.5 o una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="55283-141">This xml configures the project to generate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="the-maven-shade-plugin"></a><span data-ttu-id="55283-142">Maven-shade-plugin</span><span class="sxs-lookup"><span data-stu-id="55283-142">The maven-shade-plugin</span></span>

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

<span data-ttu-id="55283-143">Questo file XML consente di configurare la soluzione per impacchettare l'output in un file uber jar.</span><span class="sxs-lookup"><span data-stu-id="55283-143">This xml configures the solution to package the output into an uber jar.</span></span> <span data-ttu-id="55283-144">Il file jar contiene sia il codice del progetto sia le dipendenze necessarie.</span><span class="sxs-lookup"><span data-stu-id="55283-144">The jar contains both the project code and required dependencies.</span></span> <span data-ttu-id="55283-145">Viene usato anche per:</span><span class="sxs-lookup"><span data-stu-id="55283-145">It is also used to:</span></span>

* <span data-ttu-id="55283-146">Rinominare i file di licenza per le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="55283-146">Rename license files for the dependencies.</span></span>
* <span data-ttu-id="55283-147">Escludere sicurezza/firme.</span><span class="sxs-lookup"><span data-stu-id="55283-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="55283-148">Verificare che più implementazioni della stessa interfaccia vengano unite in un'unica voce.</span><span class="sxs-lookup"><span data-stu-id="55283-148">Ensure that multiple implementations of the same interface are merged into one entry.</span></span>

<span data-ttu-id="55283-149">Queste impostazioni di configurazione impediscono il verificarsi di errori in fase di runtime.</span><span class="sxs-lookup"><span data-stu-id="55283-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="55283-150">Definizioni di topologia</span><span class="sxs-lookup"><span data-stu-id="55283-150">Topology definitions</span></span>

<span data-ttu-id="55283-151">Questo esempio usa il framework [Flux](https://storm.apache.org/releases/1.1.0/flux.html),</span><span class="sxs-lookup"><span data-stu-id="55283-151">This example uses the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="55283-152">il quale usa YAML per definire le topologie.</span><span class="sxs-lookup"><span data-stu-id="55283-152">This framework uses YAML to define the topologies.</span></span> <span data-ttu-id="55283-153">Il vantaggio principale è che non è necessaria una codifica complessa per la topologia nel codice Java.</span><span class="sxs-lookup"><span data-stu-id="55283-153">The primary benefit is that you aren't hard coding the topology in Java code.</span></span> <span data-ttu-id="55283-154">Poiché la definizione è YAML, è possibile modificarla prima di inviare la topologia, senza dover ricompilare tutti gli elementi.</span><span class="sxs-lookup"><span data-stu-id="55283-154">Since the definition is YAML, you can change it before submitting the topology, without having to recompile everything.</span></span>

<span data-ttu-id="55283-155">__writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="55283-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure the Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
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
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through the components
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

<span data-ttu-id="55283-156">__reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="55283-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure the Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
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
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
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

# How data flows through the components
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

#### <a name="tell-the-topology-about-event-hub"></a><span data-ttu-id="55283-157">Informare la topologia sull'hub eventi</span><span class="sxs-lookup"><span data-stu-id="55283-157">Tell the topology about Event Hub</span></span>

<span data-ttu-id="55283-158">In fase di esecuzione il file `dev.properties` viene usato per passare la configurazione di Hub di eventi nella topologia.</span><span class="sxs-lookup"><span data-stu-id="55283-158">At run time, the `dev.properties` file is used to pass the Event Hub configuration to the topology.</span></span> <span data-ttu-id="55283-159">I contenuti predefiniti del file sono analoghi a quelli dell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="55283-159">The following example is the default contents of the file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="55283-160">Configurare le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="55283-160">Configure environment variables</span></span>

<span data-ttu-id="55283-161">Le variabili di ambiente seguenti possono essere impostate quando si installa Java e l'JDK nella workstation di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="55283-161">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="55283-162">È tuttavia necessario verificare che esistano e che contengano i valori corretti per il sistema in uso.</span><span class="sxs-lookup"><span data-stu-id="55283-162">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="55283-163">**JAVA_HOME**: deve puntare alla directory in cui è installato Java Runtime Environment (JRE).</span><span class="sxs-lookup"><span data-stu-id="55283-163">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="55283-164">In una distribuzione Unix o Linux, ad esempio, deve avere un valore simile a `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="55283-164">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="55283-165">In Windows, avrebbe un valore simile a `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="55283-165">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="55283-166">**PATH** : deve contenere i percorsi seguenti:</span><span class="sxs-lookup"><span data-stu-id="55283-166">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="55283-167">**JAVA_HOME** o il percorso equivalente</span><span class="sxs-lookup"><span data-stu-id="55283-167">**JAVA_HOME** (or the equivalent path)</span></span>
  * <span data-ttu-id="55283-168">**JAVA_HOME\bin** o il percorso equivalente</span><span class="sxs-lookup"><span data-stu-id="55283-168">**JAVA_HOME\bin** (or the equivalent path)</span></span>
  * <span data-ttu-id="55283-169">Directory in cui è installato Maven</span><span class="sxs-lookup"><span data-stu-id="55283-169">The directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="55283-170">Configurare l'hub eventi</span><span class="sxs-lookup"><span data-stu-id="55283-170">Configure Event Hub</span></span>

<span data-ttu-id="55283-171">L'hub eventi è l'origine dati per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="55283-171">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="55283-172">Per creare un hub eventi, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="55283-172">Use the following steps to create a Event Hub.</span></span>

1. <span data-ttu-id="55283-173">Nel [Portale di Azure classico](https://manage.windowsazure.com) selezionare **NUOVO** > **Bus di servizio** > **Hub eventi** > **Creazione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="55283-173">From the [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="55283-174">Nella schermata **Crea un nuovo hub eventi** immettere un **Nome hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="55283-174">On the **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="55283-175">Selezionare l'**Area** in cui creare l'hub e quindi creare uno spazio dei nomi o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="55283-175">Select the **Region** to create the hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="55283-176">Infine fare clic sulla **freccia** per continuare.</span><span class="sxs-lookup"><span data-stu-id="55283-176">Finally, click the **Arrow** to continue.</span></span>

    ![procedura guidata - pagina 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="55283-178">Selezionare lo stesso **Percorso** di Storm nel server HDInsight per ridurre la latenza e i costi.</span><span class="sxs-lookup"><span data-stu-id="55283-178">Select the same **Location** as your Storm on HDInsight server to reduce latency and costs.</span></span>

3. <span data-ttu-id="55283-179">Nella schermata **Configura hub eventi** immettere i valori per **Conteggio partizioni** e **Conservazione messaggi**.</span><span class="sxs-lookup"><span data-stu-id="55283-179">On the **Configure Event Hub** screen, enter the **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="55283-180">Per questo esempio usare un numero di partizioni pari a 10 e un valore di conservazione dei messaggi pari a 1.</span><span class="sxs-lookup"><span data-stu-id="55283-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="55283-181">Prendere nota del numero di partizioni, perché questo valore sarà necessario in seguito.</span><span class="sxs-lookup"><span data-stu-id="55283-181">Note the partition count because you need this value later.</span></span>

    ![procedura guidata - pagina 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="55283-183">Dopo aver creato l'hub eventi, selezionare lo spazio dei nomi, selezionare **Hub eventi**, quindi selezionare l'hub eventi creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="55283-183">After the event hub has been created, select the namespace, select **Event Hubs**, and then select the event hub that you created earlier.</span></span>
5. <span data-ttu-id="55283-184">Selezionare **Configura** e quindi creare due nuovi criteri di accesso usando le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="55283-184">Select **Configure**, then create two new access policies by using the following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="55283-185">Nome</span><span class="sxs-lookup"><span data-stu-id="55283-185">Name</span></span></th><th><span data-ttu-id="55283-186">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="55283-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="55283-187">Writer</span><span class="sxs-lookup"><span data-stu-id="55283-187">Writer</span></span></td><td><span data-ttu-id="55283-188">Invio</span><span class="sxs-lookup"><span data-stu-id="55283-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="55283-189">Reader</span><span class="sxs-lookup"><span data-stu-id="55283-189">Reader</span></span></td><td><span data-ttu-id="55283-190">Attesa</span><span class="sxs-lookup"><span data-stu-id="55283-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="55283-191">Dopo avere creato le autorizzazioni, selezionare l'icona **Salva** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="55283-191">After You create the permissions, select the **Save** icon at the bottom of the page.</span></span> <span data-ttu-id="55283-192">Questi criteri di accesso condiviso vengono usati per leggere e scrivere nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="55283-192">These shared access policies are used to read and write to Event Hub.</span></span>

    ![criteri](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="55283-194">Dopo avere salvato i criteri, usare **Generatore di chiavi di accesso condivise** nella parte inferiore della pagina per recuperare la chiave per i criteri **writer** e **reader**.</span><span class="sxs-lookup"><span data-stu-id="55283-194">After you save the policies, use the **Shared access key generator** at the bottom of the page to retrieve the key for the **writer** and **reader** policies.</span></span> <span data-ttu-id="55283-195">Salvare queste chiavi.</span><span class="sxs-lookup"><span data-stu-id="55283-195">Save these keys.</span></span>

## <a name="download-and-build-the-project"></a><span data-ttu-id="55283-196">Scaricare e compilare il progetto</span><span class="sxs-lookup"><span data-stu-id="55283-196">Download and build the project</span></span>

1. <span data-ttu-id="55283-197">Scaricare il progetto da GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="55283-197">Download the project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="55283-198">È possibile scaricare il pacchetto come archivio ZIP o usare [git](https://git-scm.com/) per clonare il progetto in locale.</span><span class="sxs-lookup"><span data-stu-id="55283-198">You can either download the package as a zip archive, or use [git](https://git-scm.com/) to clone the project locally.</span></span>

2. <span data-ttu-id="55283-199">Modificare il file `dev.properties` con la configurazione per l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="55283-199">Modify the `dev.properties` file with the configuration for your Event Hub.</span></span>

3. <span data-ttu-id="55283-200">Usare il comando seguente per compilare il progetto e creare il pacchetto:</span><span class="sxs-lookup"><span data-stu-id="55283-200">Use the following to build and package the project:</span></span>

        mvn package

    <span data-ttu-id="55283-201">Questo comando scarica le dipendenze necessarie, compila il progetto e quindi crea il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55283-201">This command downloads required dependencies, builds, and then packages the project.</span></span> <span data-ttu-id="55283-202">L'output viene archiviato nella directory **/target** come **EventHubExample-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="55283-202">The output is stored in the **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="55283-203">Test in locale</span><span class="sxs-lookup"><span data-stu-id="55283-203">Test locally</span></span>

<span data-ttu-id="55283-204">Poiché queste topologie possono solo leggere e scrivere gli hub eventi, è possibile eseguirne il test in locale se si dispone di un [ambiente di sviluppo Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="55283-204">Since these topologies just read and write to Event Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="55283-205">Seguire la procedura seguente per eseguire in locale nell'ambiente di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="55283-205">Use the following steps to run locally in the dev environment:</span></span>

1. <span data-ttu-id="55283-206">Eseguire il writer:</span><span class="sxs-lookup"><span data-stu-id="55283-206">Run the writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="55283-207">Eseguire il reader:</span><span class="sxs-lookup"><span data-stu-id="55283-207">Run the reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="55283-208">`--local`: consente di eseguire la topologia in modalità locale, non distribuita.</span><span class="sxs-lookup"><span data-stu-id="55283-208">`--local`: Run the topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="55283-209">`-R /writer.yaml`: consente di caricare la definizione di topologia da `resources` sotto forma di file con estensione JAR.</span><span class="sxs-lookup"><span data-stu-id="55283-209">`-R /writer.yaml`: Load the topology definition from the `resources` packaged in the jar.</span></span> <span data-ttu-id="55283-210">Se la topologia è un file nel file system locale, specificare il percorso come ultimo parametro.</span><span class="sxs-lookup"><span data-stu-id="55283-210">If the topology is a file on the local file system, specify the path to it as the last parameter instead.</span></span>
> * <span data-ttu-id="55283-211">`--filter dev.properties`: consente di usare il contenuto di `dev.properties` per inserire i valori nelle definizioni di topologia.</span><span class="sxs-lookup"><span data-stu-id="55283-211">`--filter dev.properties`: Use the contents of `dev.properties` to fill in the values in the topology definitions.</span></span> <span data-ttu-id="55283-212">Ad esempio: `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="55283-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="55283-213">L'output viene registrato nella console durante l'esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="55283-213">Output is logged to the console when running locally.</span></span> <span data-ttu-id="55283-214">Per arrestare la topologia, usare __CTRL+C__.</span><span class="sxs-lookup"><span data-stu-id="55283-214">Use __Ctrl+C__ to stop the topology.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="55283-215">Distribuire le topologie</span><span class="sxs-lookup"><span data-stu-id="55283-215">Deploy the topologies</span></span>

1. <span data-ttu-id="55283-216">Usare SCP per copiare il pacchetto JAR nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="55283-216">Use SCP to copy the jar package to your HDInsight cluster.</span></span> <span data-ttu-id="55283-217">Sostituire USERNAME con l'utente SSH del cluster.</span><span class="sxs-lookup"><span data-stu-id="55283-217">Replace USERNAME with the SSH user for your cluster.</span></span> <span data-ttu-id="55283-218">Sostituire CLUSTERNAME con il nome del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="55283-218">Replace CLUSTERNAME with the name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="55283-219">Se è stata usata una password per l'account SSH, viene richiesto di immetterla.</span><span class="sxs-lookup"><span data-stu-id="55283-219">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="55283-220">Se è stata usata una chiave SSH con l'account, potrebbe essere necessario usare il parametro `-i` per specificare il percorso del file di chiave.</span><span class="sxs-lookup"><span data-stu-id="55283-220">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="55283-221">Ad esempio: `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="55283-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="55283-222">Questo comando copia il file nella home directory dell'utente SSH nel cluster.</span><span class="sxs-lookup"><span data-stu-id="55283-222">This command copies the file to the home directory of your SSH user on the cluster.</span></span>

2. <span data-ttu-id="55283-223">Una volta completato il caricamento del file, usare SSH per connettersi al cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="55283-223">Once the file has finished uploading, use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="55283-224">Sostituire **USERNAME** con il nome di accesso a SSH.</span><span class="sxs-lookup"><span data-stu-id="55283-224">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="55283-225">Sostituire **CLUSTERNAME** con il nome del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="55283-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="55283-226">Se è stata usata una password per l'account SSH, viene richiesto di immetterla.</span><span class="sxs-lookup"><span data-stu-id="55283-226">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="55283-227">Se è stata usata una chiave SSH con l'account, potrebbe essere necessario usare il parametro `-i` per specificare il percorso del file di chiave.</span><span class="sxs-lookup"><span data-stu-id="55283-227">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="55283-228">Nell'esempio seguente la chiave privata viene caricata da `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="55283-228">The following example loads the private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="55283-229">Per avviare le topologie, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="55283-229">Use the following command to start the topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="55283-230">`--remote`: consente di inviare la topologia al servizio Nimbus, che lo avvia sui nodi di lavoro nel cluster.</span><span class="sxs-lookup"><span data-stu-id="55283-230">`--remote`: Submits the topology to the Nimbus service, which starts it on the worker nodes in the cluster.</span></span>

4. <span data-ttu-id="55283-231">Per visualizzare i dati registrati, passare a https://CLUSTERNAME.azurehdinsight.net/stormui, dove __CLUSTERNAME__ è il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="55283-231">To view the logged data, go to https://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is the name of your HDInsight cluster.</span></span> <span data-ttu-id="55283-232">Selezionare le topologie ed eseguire il drill-down per i componenti.</span><span class="sxs-lookup"><span data-stu-id="55283-232">Select the topologies and drill down to the components.</span></span> <span data-ttu-id="55283-233">Selezionare la voce __port__ per un'istanza di un componente e visualizzare le informazioni registrate.</span><span class="sxs-lookup"><span data-stu-id="55283-233">Select the __port__ entry for an instance of a component to view logged information.</span></span>

5. <span data-ttu-id="55283-234">Per arrestare le topologie, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="55283-234">Use the following commands to stop the topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="55283-235">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="55283-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="55283-236">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="55283-236">Next steps</span></span>

* [<span data-ttu-id="55283-237">Topologie di esempio per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="55283-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
