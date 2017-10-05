---
title: Esempio Java di topologia Apache Storm - Azure HDInsight | Microsoft Docs
description: Informazioni su come creare topologie apache Storm in Java mediante la creazione di una topologia di conteggio parole di esempio.
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
ms.openlocfilehash: 36285fbaf1da3c566d338bd5612eebad327eaf50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="0dc88-104">Creare una topologia Apache Storm in Java</span><span class="sxs-lookup"><span data-stu-id="0dc88-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="0dc88-105">Informazioni su come creare una topologia basata su Java per Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="0dc88-105">Learn how to create a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="0dc88-106">Creare una topologia Storm che implementa un'applicazione di conteggio delle parole.</span><span class="sxs-lookup"><span data-stu-id="0dc88-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="0dc88-107">Per compilare il progetto e creare il pacchetto si usa Maven.</span><span class="sxs-lookup"><span data-stu-id="0dc88-107">You use Maven to build and package the project.</span></span> <span data-ttu-id="0dc88-108">Quindi, si apprenderà come definire la topologia usando il framework Flux.</span><span class="sxs-lookup"><span data-stu-id="0dc88-108">Then, you learn how to define the topology using the Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="0dc88-109">Il framework Flux è disponibile in Storm 0.10.0 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="0dc88-109">The Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="0dc88-110">Storm 0.10.0 è disponibile con HDInsight 3.3 e 3.4.</span><span class="sxs-lookup"><span data-stu-id="0dc88-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="0dc88-111">Dopo aver completato i passaggi descritti in questo documento, è possibile distribuire la topologia ad Apache Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0dc88-111">After completing the steps in this document, you can deploy the topology to Apache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="0dc88-112">Una versione completa degli esempi di topologia Storm creati in questo documento è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="0dc88-112">A completed version of the Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dc88-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0dc88-113">Prerequisites</span></span>

* [<span data-ttu-id="0dc88-114">Java Developer Kit (JDK) versione 7</span><span class="sxs-lookup"><span data-stu-id="0dc88-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="0dc88-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven è un sistema per la compilazione di progetti per Java.</span><span class="sxs-lookup"><span data-stu-id="0dc88-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="0dc88-116">Un editor di testo o ambiente IDE.</span><span class="sxs-lookup"><span data-stu-id="0dc88-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="0dc88-117">Configurare le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="0dc88-117">Configure environment variables</span></span>

<span data-ttu-id="0dc88-118">Quando si installa Java e JDK, è possibile impostare le variabili di ambiente indicate di seguito.</span><span class="sxs-lookup"><span data-stu-id="0dc88-118">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="0dc88-119">È tuttavia necessario verificare che esistano e che contengano i valori corretti per il sistema in uso.</span><span class="sxs-lookup"><span data-stu-id="0dc88-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="0dc88-120">**JAVA_HOME**: deve puntare alla directory in cui è installato Java Runtime Environment (JRE).</span><span class="sxs-lookup"><span data-stu-id="0dc88-120">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="0dc88-121">In una distribuzione Unix o Linux, ad esempio, deve avere un valore simile a `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-121">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="0dc88-122">In Windows, avrebbe un valore simile a `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="0dc88-122">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="0dc88-123">**PATH** : deve contenere i percorsi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0dc88-123">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="0dc88-124">**JAVA_HOME** o il percorso equivalente</span><span class="sxs-lookup"><span data-stu-id="0dc88-124">**JAVA_HOME** (or the equivalent path)</span></span>

  * <span data-ttu-id="0dc88-125">**JAVA_HOME\bin** o il percorso equivalente</span><span class="sxs-lookup"><span data-stu-id="0dc88-125">**JAVA_HOME\bin** (or the equivalent path)</span></span>

  * <span data-ttu-id="0dc88-126">Directory in cui è installato Maven</span><span class="sxs-lookup"><span data-stu-id="0dc88-126">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="0dc88-127">Creare un progetto Maven</span><span class="sxs-lookup"><span data-stu-id="0dc88-127">Create a Maven project</span></span>

<span data-ttu-id="0dc88-128">Dalla riga di comando usare il comando seguente per creare un progetto Maven denominato **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="0dc88-128">From the command line, use the following command to create a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="0dc88-129">Se si utilizza PowerShell, è necessario racchiudere i parametri `-D` tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="0dc88-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="0dc88-130">Questo comando crea una nuova directory denominata `WordCount` nella posizione corrente, contenente un progetto Maven di base.</span><span class="sxs-lookup"><span data-stu-id="0dc88-130">This command creates a directory named `WordCount` at the current location, which contains a basic Maven project.</span></span> <span data-ttu-id="0dc88-131">La directory `WordCount` contiene gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0dc88-131">The `WordCount` directory contains the following items:</span></span>

* <span data-ttu-id="0dc88-132">`pom.xml`: contiene le impostazioni per il progetto Maven.</span><span class="sxs-lookup"><span data-stu-id="0dc88-132">`pom.xml`: Contains settings for the Maven project.</span></span>
* <span data-ttu-id="0dc88-133">`src\main\java\com\microsoft\example`: contiene il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0dc88-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="0dc88-134">`src\test\java\com\microsoft\example`: contiene i test per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0dc88-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-the-generated-example-code"></a><span data-ttu-id="0dc88-135">Rimuovere il codice di esempio generato</span><span class="sxs-lookup"><span data-stu-id="0dc88-135">Remove the generated example code</span></span>

<span data-ttu-id="0dc88-136">Eliminare i file dell'applicazione e il test generato:</span><span class="sxs-lookup"><span data-stu-id="0dc88-136">Delete the generated test and the application files:</span></span>

* <span data-ttu-id="0dc88-137">**src\test\java\com\microsoft\example\AppTest.java**</span><span class="sxs-lookup"><span data-stu-id="0dc88-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="0dc88-138">**src\main\java\com\microsoft\example\App.java**</span><span class="sxs-lookup"><span data-stu-id="0dc88-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="0dc88-139">Aggiungere archivi Maven</span><span class="sxs-lookup"><span data-stu-id="0dc88-139">Add Maven repositories</span></span>

<span data-ttu-id="0dc88-140">HDInsight si basa su Hortonworks Data Platform (HDP), perciò è consigliabile usare l'archivio Hortonworks per scaricare le dipendenze per i progetti Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="0dc88-140">HDInsight is based on the Hortonworks Data Platform (HDP), so we recommend using the Hortonworks repository to download dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="0dc88-141">Aggiungere il seguente XML al file __pom.xml__, dopo la riga `<url>http://maven.apache.org</url>`:</span><span class="sxs-lookup"><span data-stu-id="0dc88-141">In the __pom.xml__ file, add the following XML after the `<url>http://maven.apache.org</url>` line:</span></span>

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

## <a name="add-properties"></a><span data-ttu-id="0dc88-142">Aggiungere le proprietà</span><span class="sxs-lookup"><span data-stu-id="0dc88-142">Add properties</span></span>

<span data-ttu-id="0dc88-143">Maven consente di definire i valori a livello di progetto denominati proprietà.</span><span class="sxs-lookup"><span data-stu-id="0dc88-143">Maven allows you to define project-level values called properties.</span></span> <span data-ttu-id="0dc88-144">Aggiungere il testo seguente al file __pom.xml__, dopo la riga `</repositories>`:</span><span class="sxs-lookup"><span data-stu-id="0dc88-144">In the __pom.xml__, add the following text after the `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from the Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="0dc88-145">È ora possibile usare questo valore in altre sezioni del file `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-145">You can now use this value in other sections of the `pom.xml`.</span></span> <span data-ttu-id="0dc88-146">Ad esempio, quando si specifica la versione dei componenti Storm, è possibile usare `${storm.version}` anziché codificare un valore.</span><span class="sxs-lookup"><span data-stu-id="0dc88-146">For example, when specifying the version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="0dc88-147">Aggiungere le dipendenze</span><span class="sxs-lookup"><span data-stu-id="0dc88-147">Add dependencies</span></span>

<span data-ttu-id="0dc88-148">Aggiungere una dipendenza per i componenti Storm.</span><span class="sxs-lookup"><span data-stu-id="0dc88-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="0dc88-149">Aprire il file `pom.xml` e aggiungere il codice seguente nella sezione `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="0dc88-149">Open the `pom.xml` file and add the following code in the `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of the jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="0dc88-150">In fase di compilazione, Maven usa queste informazioni per cercare `storm-core` nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="0dc88-150">At compile time, Maven uses this information to look up `storm-core` in the Maven repository.</span></span> <span data-ttu-id="0dc88-151">Viene innanzitutto esaminato il repository del computer locale.</span><span class="sxs-lookup"><span data-stu-id="0dc88-151">It first looks in the repository on your local computer.</span></span> <span data-ttu-id="0dc88-152">Se i file non sono presenti, verranno scaricati tramite Maven dall'archivio pubblico Maven e inseriti nell'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="0dc88-152">If the files aren't there, Maven downloads them from the public Maven repository and stores them in the local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="0dc88-153">Si noti la riga `<scope>provided</scope>` in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="0dc88-153">Notice the `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="0dc88-154">Questa impostazione indica a Maven di escludere **storm-core** da qualsiasi file con estensione JAR creato, poiché viene fornito dal sistema.</span><span class="sxs-lookup"><span data-stu-id="0dc88-154">This setting tells Maven to exclude **storm-core** from any JAR files that are created, because it is provided by the system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="0dc88-155">Configurare la compilazione</span><span class="sxs-lookup"><span data-stu-id="0dc88-155">Build configuration</span></span>

<span data-ttu-id="0dc88-156">I plug-in di Maven consentono di personalizzare le fasi di compilazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="0dc88-156">Maven plug-ins allow you to customize the build stages of the project.</span></span> <span data-ttu-id="0dc88-157">Ad esempio, il modo in cui viene compilato il progetto o viene creato il pacchetto come file JAR.</span><span class="sxs-lookup"><span data-stu-id="0dc88-157">For example, how the project is compiled or how to package it into a JAR file.</span></span> <span data-ttu-id="0dc88-158">Aprire il file `pom.xml` e aggiungere il codice seguente direttamente sopra la riga `</project>`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-158">Open the `pom.xml` file and add the following code directly above the `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="0dc88-159">Questa sezione viene usata per aggiungere plug-in, risorse e altre opzioni di configurazione della compilazione.</span><span class="sxs-lookup"><span data-stu-id="0dc88-159">This section is used to add plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="0dc88-160">Per un riferimento completo del file **pom.xml**, vedere [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="0dc88-160">For a full reference of the **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="0dc88-161">Aggiungere plug-in</span><span class="sxs-lookup"><span data-stu-id="0dc88-161">Add plug-ins</span></span>

<span data-ttu-id="0dc88-162">Per le topologie Apache Storm implementate in Java, il [plug-in Exec Maven](http://www.mojohaus.org/exec-maven-plugin/) risulta particolarmente utile in quanto consente di eseguire facilmente la topologia nell'ambiente di sviluppo in uso.</span><span class="sxs-lookup"><span data-stu-id="0dc88-162">For Apache Storm topologies implemented in Java, the [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you to easily run the topology locally in your development environment.</span></span> <span data-ttu-id="0dc88-163">Aggiungere quanto segue alla sezione `<plugins>` del file `pom.xml` per includere il plug-in Exec Maven:</span><span class="sxs-lookup"><span data-stu-id="0dc88-163">Add the following to the `<plugins>` section of the `pom.xml` file to include the Exec Maven plugin:</span></span>

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

<span data-ttu-id="0dc88-164">Anche il [plug-in Apache Maven Compiler](http://maven.apache.org/plugins/maven-compiler-plugin/), usato per modificare le opzioni di compilazione, è molto utile.</span><span class="sxs-lookup"><span data-stu-id="0dc88-164">Another useful plug-in is the [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used to change compilation options.</span></span> <span data-ttu-id="0dc88-165">Questo consente di modificare la versione di Java usata da Maven come versione di origine e destinazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0dc88-165">The changes the Java version that Maven uses for the source and target for your application.</span></span>

* <span data-ttu-id="0dc88-166">Per HDInsight __3.4 o versioni precedenti__, impostare la versione di origine e di destinazione di Java su __1.7__.</span><span class="sxs-lookup"><span data-stu-id="0dc88-166">For HDInsight __3.4 or earlier__, set the source and target Java version to __1.7__.</span></span>

* <span data-ttu-id="0dc88-167">Per HDInsight __3.5__, impostare la versione di origine e di destinazione di Java su __1.8__.</span><span class="sxs-lookup"><span data-stu-id="0dc88-167">For HDInsight __3.5__, set the source and target Java version to __1.8__.</span></span>

<span data-ttu-id="0dc88-168">Aggiungere il testo seguente nella sezione `<plugins>` del file `pom.xml` per includere il plug-in Apache Maven Compiler.</span><span class="sxs-lookup"><span data-stu-id="0dc88-168">Add the following text in the `<plugins>` section of the `pom.xml` file to include the Apache Maven Compiler plugin.</span></span> <span data-ttu-id="0dc88-169">Questo esempio specifica la versione 1.8, quindi la versione di HDInsight di destinazione è 3.5.</span><span class="sxs-lookup"><span data-stu-id="0dc88-169">This example specifies 1.8, so the target HDInsight version is 3.5.</span></span>

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

### <a name="configure-resources"></a><span data-ttu-id="0dc88-170">Configure resources</span><span class="sxs-lookup"><span data-stu-id="0dc88-170">Configure resources</span></span>

<span data-ttu-id="0dc88-171">La sezione delle risorse consente di includere le risorse non di codice, ad esempio i file di configurazione richiesti dai componenti della topologia.</span><span class="sxs-lookup"><span data-stu-id="0dc88-171">The resources section allows you to include non-code resources such as configuration files needed by components in the topology.</span></span> <span data-ttu-id="0dc88-172">In questo esempio aggiungere il testo seguente nella sezione `<resources>` del file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="0dc88-172">For this example, add the following text in the `<resources>` section of the \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="0dc88-173">In questo esempio viene aggiunta la directory delle risorse nella radice del progetto (`${basedir}`) come posizione contenente le risorse e include il file denominato `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-173">This example adds the resources directory in the root of the project (`${basedir}`) as a location that contains resources, and includes the file named `log4j2.xml`.</span></span> <span data-ttu-id="0dc88-174">Questo file viene usato per configurare le informazioni registrate dalla topologia.</span><span class="sxs-lookup"><span data-stu-id="0dc88-174">This file is used to configure what information is logged by the topology.</span></span>

## <a name="create-the-topology"></a><span data-ttu-id="0dc88-175">Creare la topologia</span><span class="sxs-lookup"><span data-stu-id="0dc88-175">Create the topology</span></span>

<span data-ttu-id="0dc88-176">Una topologia Apache Storm basata su Java è costituita da tre componenti che è necessario creare o a cui è necessario fare riferimento come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="0dc88-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="0dc88-177">**Spout**: legge i dati da origini esterne e genera flussi di dati nella topologia.</span><span class="sxs-lookup"><span data-stu-id="0dc88-177">**Spouts**: Reads data from external sources and emits streams of data into the topology.</span></span>

* <span data-ttu-id="0dc88-178">**Bolt**: esegue l'elaborazione sui flussi generati dagli spout o da altri bolt e genera uno o più flussi.</span><span class="sxs-lookup"><span data-stu-id="0dc88-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="0dc88-179">**Topologia**: definisce il modo in cui vengono disposti gli spout e i bolt e fornisce il punto di ingresso per la topologia.</span><span class="sxs-lookup"><span data-stu-id="0dc88-179">**Topology**: Defines how the spouts and bolts are arranged, and provides the entry point for the topology.</span></span>

### <a name="create-the-spout"></a><span data-ttu-id="0dc88-180">Creare lo spout</span><span class="sxs-lookup"><span data-stu-id="0dc88-180">Create the spout</span></span>

<span data-ttu-id="0dc88-181">Per ridurre i requisiti relativi all'impostazione di origini dati esterne, lo spout seguente genera semplicemente frasi casuali.</span><span class="sxs-lookup"><span data-stu-id="0dc88-181">To reduce requirements for setting up external data sources, the following spout simply emits random sentences.</span></span> <span data-ttu-id="0dc88-182">Si tratta di una versione modificata di uno spout fornito con gli esempi di [Storm-Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="0dc88-182">It is a modified version of a spout that is provided with the [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="0dc88-183">Per uno spout in grado di leggere da un'origine dati esterna, vedere uno degli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0dc88-183">For an example of a spout that reads from an external data source, see one of the following examples:</span></span>
>
> * <span data-ttu-id="0dc88-184">[TwitterSampleSpout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): spout di esempio che legge da Twitter</span><span class="sxs-lookup"><span data-stu-id="0dc88-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="0dc88-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): spout che legge da Kafka</span><span class="sxs-lookup"><span data-stu-id="0dc88-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="0dc88-186">Per lo spout, creare un file denominato `RandomSentenceSpout.java` nella directory `src\main\java\com\microsoft\example` e usare il codice Java seguente come contenuto:</span><span class="sxs-lookup"><span data-stu-id="0dc88-186">For the spout, create a file named `RandomSentenceSpout.java` in the `src\main\java\com\microsoft\example` directory and use the following Java code as the contents:</span></span>

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
  //Collector used to emit output
  SpoutOutputCollector _collector;
  //Used to generate a random number
  Random _rand;

  //Open is called when an instance of the class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set the instance collector to the one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data to the stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //The sentences that are randomly emitted
    String[] sentences = new String[]{ "the cow jumped over the moon", "an apple a day keeps the doctor away",
        "four score and seven years ago", "snow white and the seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit the sentence
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

  //Declare the output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="0dc88-187">Anche se questa topologia usa soltanto uno spout, altre topologie possono avere diversi spout che inseriscono dati da diverse origini.</span><span class="sxs-lookup"><span data-stu-id="0dc88-187">Although this topology uses only one spout, others may have several that feed data from different sources into the topology.</span></span>

### <a name="create-the-bolts"></a><span data-ttu-id="0dc88-188">Creare i bolt</span><span class="sxs-lookup"><span data-stu-id="0dc88-188">Create the bolts</span></span>

<span data-ttu-id="0dc88-189">I bolt gestiscono l'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="0dc88-189">Bolts handle the data processing.</span></span> <span data-ttu-id="0dc88-190">Questa topologia usa due bolt:</span><span class="sxs-lookup"><span data-stu-id="0dc88-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="0dc88-191">**SplitSentence**: divide le frasi generate da **RandomSentenceSpout** in singole parole.</span><span class="sxs-lookup"><span data-stu-id="0dc88-191">**SplitSentence**: Splits the sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="0dc88-192">**WordCount**: conta le occorrenze di ciascuna parola.</span><span class="sxs-lookup"><span data-stu-id="0dc88-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="0dc88-193">I bolt eseguono qualsiasi tipo di attività, ad esempio calcolo, persistenza o comunicazione con componenti esterni.</span><span class="sxs-lookup"><span data-stu-id="0dc88-193">Bolts can do anything, for example, computation, persistence, or talking to external components.</span></span>

<span data-ttu-id="0dc88-194">Nella directory `src\main\java\com\microsoft\example` creare due nuovi file, `SplitSentence.java` e `WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-194">Create two new files, `SplitSentence.java` and `WordCount.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="0dc88-195">Usare come contenuto dei file il testo riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0dc88-195">Use the following text as the contents for the files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="0dc88-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="0dc88-196">SplitSentence</span></span>

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

  //Execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get the sentence content from the tuple
    String sentence = tuple.getString(0);
    //An iterator to get each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give the iterator the sentence
    boundary.setText(sentence);
    //Find the beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it to the output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get the word
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

#### <a name="wordcount"></a><span data-ttu-id="0dc88-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="0dc88-197">WordCount</span></span>

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
  //How often to emit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default to 60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used to trigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called to process tuples
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
      //Get the word contents from the tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment the count and store it
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

### <a name="define-the-topology"></a><span data-ttu-id="0dc88-198">Definire la topologia</span><span class="sxs-lookup"><span data-stu-id="0dc88-198">Define the topology</span></span>

<span data-ttu-id="0dc88-199">La topologia collega gli spout e i bolt in un grafico, che definisce il flusso di dati tra i componenti.</span><span class="sxs-lookup"><span data-stu-id="0dc88-199">The topology ties the spouts and bolts together into a graph, which defines how data flows between the components.</span></span> <span data-ttu-id="0dc88-200">Fornisce inoltre suggerimenti di parallelismo usati da Storm durante la creazione di istanze di componenti all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="0dc88-200">It also provides parallelism hints that Storm uses when creating instances of the components within the cluster.</span></span>

<span data-ttu-id="0dc88-201">La seguente immagine è un diagramma di base del grafico dei componenti della topologia.</span><span class="sxs-lookup"><span data-stu-id="0dc88-201">The following image is a basic diagram of the graph of components for this topology.</span></span>

![diagramma che mostra la disposizione degli spout e dei bolt](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="0dc88-203">Per implementare la topologia, creare un file denominato `WordCountTopology.java` nella directory `src\main\java\com\microsoft\example`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-203">To implement the topology, create a file named `WordCountTopology.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="0dc88-204">Usare il codice Java seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="0dc88-204">Use the following Java code as the contents of the file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for the topology
  public static void main(String[] args) throws Exception {
  //Used to build the topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add the spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add the SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes to the spout, and equally distributes
    //tuples (sentences) across instances of the SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add the counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes to the split bolt, and
    //ensures that the same word is sent to the same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set to false to disable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint to set the number of workers
      conf.setNumWorkers(3);
      //submit the topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap the maximum number of executors that can be spawned
      //for a component to 3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used to run locally
      LocalCluster cluster = new LocalCluster();
      //submit the topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down the cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="0dc88-205">Configurare la registrazione</span><span class="sxs-lookup"><span data-stu-id="0dc88-205">Configure logging</span></span>

<span data-ttu-id="0dc88-206">Storm usa Apache Log4j per registrare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="0dc88-206">Storm uses Apache Log4j to log information.</span></span> <span data-ttu-id="0dc88-207">Se non si configura la registrazione, la topologia genera informazioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="0dc88-207">If you do not configure logging, the topology emits diagnostic information.</span></span> <span data-ttu-id="0dc88-208">Per controllare ciò che viene registrato, creare un file denominato `log4j2.xml` nella directory `resources`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-208">To control what is logged, create a file named `log4j2.xml` in the `resources` directory.</span></span> <span data-ttu-id="0dc88-209">Usare l'XML seguente come contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="0dc88-209">Use the following XML as the contents of the file.</span></span>

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

<span data-ttu-id="0dc88-210">Questo XML consente di configurare un nuovo logger per la classe `com.microsoft.example`, che include i componenti in questa topologia di esempio.</span><span class="sxs-lookup"><span data-stu-id="0dc88-210">This XML configures a new logger for the `com.microsoft.example` class, which includes the components in this example topology.</span></span> <span data-ttu-id="0dc88-211">Il livello è impostato sul monitoraggio per questo logger tramite il quale acquisisce le informazioni di registrazione generate dai componenti in questa topologia.</span><span class="sxs-lookup"><span data-stu-id="0dc88-211">The level is set to trace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="0dc88-212">La sezione `<Root level="error">` configura il livello radice di registrazione, ovvero tutti gli elementi non presenti in `com.microsoft.example`, per poter registrare solo le informazioni relative agli errori.</span><span class="sxs-lookup"><span data-stu-id="0dc88-212">The `<Root level="error">` section configures the root level of logging (everything not in `com.microsoft.example`) to only log error information.</span></span>

<span data-ttu-id="0dc88-213">Per altre informazioni sulla configurazione della registrazione per Log4j, vedere [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="0dc88-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="0dc88-214">Storm versione 0.10.0 e successive usano Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="0dc88-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="0dc88-215">Le versioni precedenti usano Log4j 1.x, che impiega un formato diverso per la configurazione del log.</span><span class="sxs-lookup"><span data-stu-id="0dc88-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="0dc88-216">Per informazioni sulla configurazione precedente, vedere [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="0dc88-216">For information on the older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-the-topology-locally"></a><span data-ttu-id="0dc88-217">Testare la topologia in locale</span><span class="sxs-lookup"><span data-stu-id="0dc88-217">Test the topology locally</span></span>

<span data-ttu-id="0dc88-218">Dopo aver salvato i file, usare il comando seguente per testare la topologia in locale.</span><span class="sxs-lookup"><span data-stu-id="0dc88-218">After you save the files, use the following command to test the topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="0dc88-219">Durante l'esecuzione, la topologia mostra le informazioni di avvio.</span><span class="sxs-lookup"><span data-stu-id="0dc88-219">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="0dc88-220">Il testo seguente è un esempio di output del conteggio parole:</span><span class="sxs-lookup"><span data-stu-id="0dc88-220">The following text is an example of the word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="0dc88-221">Questo log di esempio indica che la parola "and" è stata generata 113 volte.</span><span class="sxs-lookup"><span data-stu-id="0dc88-221">This example log indicates that the word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="0dc88-222">Il conteggio continua ad aumentare fintanto che la topologia è in esecuzione perché lo spout emette continuamente le stesse frasi.</span><span class="sxs-lookup"><span data-stu-id="0dc88-222">The count continues to go up as long as the topology runs because the spout continuously emits the same sentences.</span></span>

<span data-ttu-id="0dc88-223">C'è un intervallo di 5 secondi tra l'emissione di parole e i conteggi.</span><span class="sxs-lookup"><span data-stu-id="0dc88-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="0dc88-224">Il componente **WordCount** è configurato per generare informazioni solo quando arriva una tupla tick.</span><span class="sxs-lookup"><span data-stu-id="0dc88-224">The **WordCount** component is configured to only emit information when a tick tuple arrives.</span></span> <span data-ttu-id="0dc88-225">Richiede che le tuple tick vengano recapitate solo ogni cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="0dc88-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-the-topology-to-flux"></a><span data-ttu-id="0dc88-226">Convertire la topologia in Flux</span><span class="sxs-lookup"><span data-stu-id="0dc88-226">Convert the topology to Flux</span></span>

<span data-ttu-id="0dc88-227">Flux è un nuovo framework disponibile con Storm 0.10.0 e versioni successive, che consente di separare la configurazione dall'implementazione.</span><span class="sxs-lookup"><span data-stu-id="0dc88-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you to separate configuration from implementation.</span></span> <span data-ttu-id="0dc88-228">I componenti sono ancora definiti in Java, ma la topologia viene definita mediante un file YAML.</span><span class="sxs-lookup"><span data-stu-id="0dc88-228">Your components are still defined in Java, but the topology is defined using a YAML file.</span></span> <span data-ttu-id="0dc88-229">È possibile impacchettare una definizione di topologia predefinita con il progetto o usare un file autonomo per l'invio della topologia.</span><span class="sxs-lookup"><span data-stu-id="0dc88-229">You can package a default topology definition with your project, or use a standalone file when submitting the topology.</span></span> <span data-ttu-id="0dc88-230">Quando si invia la topologia a Storm, è possibile usare variabili di ambiente o file di configurazione per popolare i valori nella definizione della topologia YAML.</span><span class="sxs-lookup"><span data-stu-id="0dc88-230">When submitting the topology to Storm, you can use environment variables or configuration files to populate values in the YAML topology definition.</span></span>

<span data-ttu-id="0dc88-231">Il file YAML definisce i componenti da usare per la topologia e i dati di flusso tra essi.</span><span class="sxs-lookup"><span data-stu-id="0dc88-231">The YAML file defines the components to use for the topology and the data flow between them.</span></span> <span data-ttu-id="0dc88-232">È possibile includere un file YAML come parte del file con estensione JAR oppure usare un file esterno YAML.</span><span class="sxs-lookup"><span data-stu-id="0dc88-232">You can include a YAML file as part of the jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="0dc88-233">Per altre informazioni su Flux, vedere [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="0dc88-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="0dc88-234">A causa di un [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) per Storm 1.0.1, può essere necessario installare un [ambiente di sviluppo Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) eseguire localmente le topologie Flux.</span><span class="sxs-lookup"><span data-stu-id="0dc88-234">Due to a [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need to install a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) to run Flux topologies locally.</span></span>

1. <span data-ttu-id="0dc88-235">Spostare il file `WordCountTopology.java` fuori dal progetto.</span><span class="sxs-lookup"><span data-stu-id="0dc88-235">Move the `WordCountTopology.java` file out of the project.</span></span> <span data-ttu-id="0dc88-236">In precedenza questo file ha definito la topologia, ma non è necessario con Flux.</span><span class="sxs-lookup"><span data-stu-id="0dc88-236">Previously, this file defined the topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="0dc88-237">Creare un nuovo file denominato `topology.yaml` nella directory `resources`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-237">In the `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="0dc88-238">Usare il testo seguente come contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="0dc88-238">Use the following text as the contents of this file.</span></span>

        name: "wordcount"       # friendly name for the topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for the number of workers to create
        
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
            from: "sentence-spout"       # The stream emitter
            to: "splitter-bolt"          # The stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) to group on

3. <span data-ttu-id="0dc88-239">Apportare le modifiche seguenti al file `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-239">Make the following changes to the `pom.xml` file.</span></span>
   
   * <span data-ttu-id="0dc88-240">Aggiungere la nuova dipendenza seguente nella sezione `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="0dc88-240">Add the following new dependency in the `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on the Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="0dc88-241">Aggiungere il plug-in seguente per la sezione `<plugins>` .</span><span class="sxs-lookup"><span data-stu-id="0dc88-241">Add the following plugin to the `<plugins>` section.</span></span> <span data-ttu-id="0dc88-242">Questo plug-in gestisce la creazione di un pacchetto (file jar) per il progetto e applica alcune trasformazioni specifiche a Flux durante la creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0dc88-242">This plugin handles the creation of a package (jar file) for the project, and applies some transformations specific to Flux when creating the package.</span></span>
     
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
                    <!-- We're using Flux, so refer to it as main -->
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

   * <span data-ttu-id="0dc88-243">Nella sezione `<configuration>` di **exec-maven-plugin** sostituire il valore di `<mainClass>` con `org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-243">In the **exec-maven-plugin** `<configuration>` section, change the value for `<mainClass>` to `org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="0dc88-244">Questa impostazione consente a Flux di gestire l'esecuzione in locale della topologia nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="0dc88-244">This setting allows Flux to handle running the topology locally in development.</span></span>

   * <span data-ttu-id="0dc88-245">Nella sezione `<resources>`, aggiungere quanto segue a `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-245">In the `<resources>` section, add the following to the `<includes>`.</span></span> <span data-ttu-id="0dc88-246">Questo XML include il file YAML che definisce la topologia come parte del progetto.</span><span class="sxs-lookup"><span data-stu-id="0dc88-246">This XML includes the YAML file that defines the topology as part of the project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-the-flux-topology-locally"></a><span data-ttu-id="0dc88-247">Testare la topologia Flux in locale</span><span class="sxs-lookup"><span data-stu-id="0dc88-247">Test the flux topology locally</span></span>

1. <span data-ttu-id="0dc88-248">Usare la seguente procedura per compilare ed eseguire la topologia Flux usando Maven:</span><span class="sxs-lookup"><span data-stu-id="0dc88-248">Use the following to compile and execute the Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="0dc88-249">Se si utilizza PowerShell, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0dc88-249">If you are using PowerShell, use the following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="0dc88-250">Questo comando non va a buon fine se la topologia usa bit di Storm 1.0.1.</span><span class="sxs-lookup"><span data-stu-id="0dc88-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="0dc88-251">I motivi della mancata riuscita sono indicati in [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="0dc88-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="0dc88-252">[Installare Storm nell'ambiente di sviluppo](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) e usare le informazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="0dc88-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use the following information.</span></span>

    <span data-ttu-id="0dc88-253">Se [Storm è installato nell'ambiente di sviluppo](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), è possibile usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0dc88-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use the following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="0dc88-254">Il parametro `--local` esegue la topologia in modalità locale nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="0dc88-254">The `--local` parameter runs the topology in local mode on your development environment.</span></span> <span data-ttu-id="0dc88-255">Il parametro `-R /topology.yaml` usa la risorsa file `topology.yaml` dal file jar per definire la topologia.</span><span class="sxs-lookup"><span data-stu-id="0dc88-255">The `-R /topology.yaml` parameter uses the `topology.yaml` file resource from the jar file to define the topology.</span></span>

    <span data-ttu-id="0dc88-256">Durante l'esecuzione, la topologia mostra le informazioni di avvio.</span><span class="sxs-lookup"><span data-stu-id="0dc88-256">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="0dc88-257">Il testo seguente è un esempio di output:</span><span class="sxs-lookup"><span data-stu-id="0dc88-257">The following text is an example of the output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="0dc88-258">C'è un ritardo di 10 secondi tra i batch delle informazioni registrate.</span><span class="sxs-lookup"><span data-stu-id="0dc88-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="0dc88-259">Creare una copia del file `topology.yaml` dal progetto.</span><span class="sxs-lookup"><span data-stu-id="0dc88-259">Make a copy of the `topology.yaml` file from the project.</span></span> <span data-ttu-id="0dc88-260">Assegnare al nuovo file il nome `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-260">Name the new file `newtopology.yaml`.</span></span> <span data-ttu-id="0dc88-261">Nel file `newtopology.yaml` individuare la sezione seguente e modificare il valore di `10` su `5`.</span><span class="sxs-lookup"><span data-stu-id="0dc88-261">In the `newtopology.yaml` file, find the following section and change the value of `10` to `5`.</span></span> <span data-ttu-id="0dc88-262">Questa modifica consente di cambiare l'intervallo tra i batch di emissione del conteggio di parole da 10 secondi a 5.</span><span class="sxs-lookup"><span data-stu-id="0dc88-262">This modification changes the interval between emitting batches of word counts from 10 seconds to 5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. To run the topology, use the following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="0dc88-263">In alternativa, se si dispone di Storm nell'ambiente di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="0dc88-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="0dc88-264">Modificare `/path/to/newtopology.yaml` sul percorso al file newtopology.yaml creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="0dc88-264">Change the `/path/to/newtopology.yaml` to the path to the newtopology.yaml file you created in the previous step.</span></span> <span data-ttu-id="0dc88-265">Questo comando usa il file newtopology.yaml come definizione della topologia.</span><span class="sxs-lookup"><span data-stu-id="0dc88-265">This command uses the newtopology.yaml as the topology definition.</span></span> <span data-ttu-id="0dc88-266">Siccome il parametro `compile` non è stato incluso, Maven usa la versione del progetto creato nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="0dc88-266">Since we didn't include the `compile` parameter, Maven uses the version of the project built in previous steps.</span></span>

    <span data-ttu-id="0dc88-267">Una volta avviata la topologia, si dovrebbe notare che il tempo tra i batch emessi è cambiato per riflettere il valore in newtopology.yaml.</span><span class="sxs-lookup"><span data-stu-id="0dc88-267">Once the topology starts, you should notice that the time between emitted batches has changed to reflect the value in newtopology.yaml.</span></span> <span data-ttu-id="0dc88-268">Pertanto, è possibile modificare la configurazione tramite un file YAML senza dover ricompilare la topologia.</span><span class="sxs-lookup"><span data-stu-id="0dc88-268">So you can see that you can change your configuration through a YAML file without having to recompile the topology.</span></span>

<span data-ttu-id="0dc88-269">Per ulteriori informazioni su queste e altre funzionalità del framework Flux, vedere [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="0dc88-269">For more information on these and other features of the Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="0dc88-270">Trident</span><span class="sxs-lookup"><span data-stu-id="0dc88-270">Trident</span></span>

<span data-ttu-id="0dc88-271">Trident è un'astrazione di alto livello fornita da Storm</span><span class="sxs-lookup"><span data-stu-id="0dc88-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="0dc88-272">che supporta l'elaborazione con informazioni sullo stato.</span><span class="sxs-lookup"><span data-stu-id="0dc88-272">It supports stateful processing.</span></span> <span data-ttu-id="0dc88-273">Il principale vantaggio offerto da Trident è la garanzia che ogni messaggio introdotto nella topologia viene elaborato una sola volta.</span><span class="sxs-lookup"><span data-stu-id="0dc88-273">The primary advantage of Trident is that it can guarantee that every message that enters the topology is processed only once.</span></span> <span data-ttu-id="0dc88-274">Senza l'uso di Trident, la topologia può garantire solo che i messaggi vengono elaborati almeno una volta.</span><span class="sxs-lookup"><span data-stu-id="0dc88-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="0dc88-275">Esistono altre differenze, ad esempio la disponibilità di componenti predefiniti che possono essere usati senza che sia necessario creare bolt.</span><span class="sxs-lookup"><span data-stu-id="0dc88-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="0dc88-276">I bolt sono infatti sostituiti da componenti meno generici, ad esempio filtri, proiezioni e funzioni.</span><span class="sxs-lookup"><span data-stu-id="0dc88-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="0dc88-277">È possibile creare applicazioni Trident mediante progetti Maven</span><span class="sxs-lookup"><span data-stu-id="0dc88-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="0dc88-278">L'unica differenza consiste nel codice.</span><span class="sxs-lookup"><span data-stu-id="0dc88-278">You use the same basic steps as presented earlier in this article—only the code is different.</span></span> <span data-ttu-id="0dc88-279">Trident, inoltre, non è (attualmente) utilizzabile con il framework Flux.</span><span class="sxs-lookup"><span data-stu-id="0dc88-279">Trident also cannot (currently) be used with the Flux framework.</span></span>

<span data-ttu-id="0dc88-280">Per altre informazioni su Trident, vedere la [panoramica dell'API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="0dc88-280">For more information about Trident, see the [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="0dc88-281">Per un'applicazione Trident di esempio, vedere [Temi di tendenza Twitter con Apache Storm in HDInsight](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="0dc88-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dc88-282">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0dc88-282">Next Steps</span></span>

<span data-ttu-id="0dc88-283">A questo punto, dopo aver appreso come creare una topologia Storm con Java,</span><span class="sxs-lookup"><span data-stu-id="0dc88-283">You have learned how to create a Storm topology by using Java.</span></span> <span data-ttu-id="0dc88-284">è possibile passare agli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0dc88-284">Now learn how to:</span></span>

* [<span data-ttu-id="0dc88-285">Distribuzione e gestione di topologie Apache Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0dc88-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="0dc88-286">Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0dc88-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="0dc88-287">Per altri esempi di topologie Storm, vedere [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="0dc88-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

