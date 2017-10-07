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
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="0732f-104">Creare una topologia Apache Storm in Java</span><span class="sxs-lookup"><span data-stu-id="0732f-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="0732f-105">Informazioni su come toocreate una topologia basata su Java per Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="0732f-105">Learn how toocreate a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="0732f-106">Creare una topologia Storm che implementa un'applicazione di conteggio delle parole.</span><span class="sxs-lookup"><span data-stu-id="0732f-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="0732f-107">Utilizzare Maven toobuild pacchetto hello nel progetto.</span><span class="sxs-lookup"><span data-stu-id="0732f-107">You use Maven toobuild and package hello project.</span></span> <span data-ttu-id="0732f-108">Quindi, imparare come toodefine hello topologia utilizzando hello framework luminoso.</span><span class="sxs-lookup"><span data-stu-id="0732f-108">Then, you learn how toodefine hello topology using hello Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="0732f-109">il framework di flusso Hello è disponibile in Storm 0.10.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="0732f-109">hello Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="0732f-110">Storm 0.10.0 è disponibile con HDInsight 3.3 e 3.4.</span><span class="sxs-lookup"><span data-stu-id="0732f-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="0732f-111">Dopo aver completato i passaggi di hello in questo documento, è possibile distribuire hello topologia tooApache Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0732f-111">After completing hello steps in this document, you can deploy hello topology tooApache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="0732f-112">Una versione completa degli esempi di topologia Storm hello creato in questo documento è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="0732f-112">A completed version of hello Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0732f-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0732f-113">Prerequisites</span></span>

* [<span data-ttu-id="0732f-114">Java Developer Kit (JDK) versione 7</span><span class="sxs-lookup"><span data-stu-id="0732f-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="0732f-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven è un sistema per la compilazione di progetti per Java.</span><span class="sxs-lookup"><span data-stu-id="0732f-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="0732f-116">Un editor di testo o ambiente IDE.</span><span class="sxs-lookup"><span data-stu-id="0732f-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="0732f-117">Configurare le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="0732f-117">Configure environment variables</span></span>

<span data-ttu-id="0732f-118">Hello seguenti variabili di ambiente possono essere impostate quando si installa Java e hello JDK.</span><span class="sxs-lookup"><span data-stu-id="0732f-118">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="0732f-119">Tuttavia, è necessario verificare che esistano e che contengono i valori corretti di hello per il sistema.</span><span class="sxs-lookup"><span data-stu-id="0732f-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="0732f-120">**JAVA_HOME** -deve puntare toohello directory in cui è installato Java runtime environment (JRE) di hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-120">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="0732f-121">Ad esempio, in una distribuzione di Unix o Linux, deve essere un valore simile troppo`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="0732f-121">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="0732f-122">In Windows, avrebbe un valore simile troppo`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="0732f-122">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="0732f-123">**PERCORSO** -deve contenere hello seguenti percorsi:</span><span class="sxs-lookup"><span data-stu-id="0732f-123">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="0732f-124">**JAVA_HOME** (o percorso equivalente hello)</span><span class="sxs-lookup"><span data-stu-id="0732f-124">**JAVA_HOME** (or hello equivalent path)</span></span>

  * <span data-ttu-id="0732f-125">**JAVA_HOME\bin** (o percorso equivalente hello)</span><span class="sxs-lookup"><span data-stu-id="0732f-125">**JAVA_HOME\bin** (or hello equivalent path)</span></span>

  * <span data-ttu-id="0732f-126">directory di Hello in cui è installato Maven</span><span class="sxs-lookup"><span data-stu-id="0732f-126">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="0732f-127">Creare un progetto Maven</span><span class="sxs-lookup"><span data-stu-id="0732f-127">Create a Maven project</span></span>

<span data-ttu-id="0732f-128">Dalla riga di comando hello, utilizzare hello comando che segue toocreate un progetto di Maven denominato **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="0732f-128">From hello command line, use hello following command toocreate a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="0732f-129">Se si utilizza PowerShell, è necessario racchiudere i parametri `-D` tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="0732f-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="0732f-130">Questo comando crea una directory denominata `WordCount` nella posizione corrente di hello, che contiene un progetto di Maven base.</span><span class="sxs-lookup"><span data-stu-id="0732f-130">This command creates a directory named `WordCount` at hello current location, which contains a basic Maven project.</span></span> <span data-ttu-id="0732f-131">Hello `WordCount` directory contiene hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0732f-131">hello `WordCount` directory contains hello following items:</span></span>

* <span data-ttu-id="0732f-132">`pom.xml`: Contiene le impostazioni per il progetto di Maven hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-132">`pom.xml`: Contains settings for hello Maven project.</span></span>
* <span data-ttu-id="0732f-133">`src\main\java\com\microsoft\example`: contiene il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0732f-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="0732f-134">`src\test\java\com\microsoft\example`: contiene i test per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0732f-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-hello-generated-example-code"></a><span data-ttu-id="0732f-135">Rimuovere il codice di esempio hello generato</span><span class="sxs-lookup"><span data-stu-id="0732f-135">Remove hello generated example code</span></span>

<span data-ttu-id="0732f-136">Eliminare i test generato hello e i file dell'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="0732f-136">Delete hello generated test and hello application files:</span></span>

* <span data-ttu-id="0732f-137">**src\test\java\com\microsoft\example\AppTest.java**</span><span class="sxs-lookup"><span data-stu-id="0732f-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="0732f-138">**src\main\java\com\microsoft\example\App.java**</span><span class="sxs-lookup"><span data-stu-id="0732f-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="0732f-139">Aggiungere archivi Maven</span><span class="sxs-lookup"><span data-stu-id="0732f-139">Add Maven repositories</span></span>

<span data-ttu-id="0732f-140">HDInsight è basato sulla hello Hortonworks Data Platform (HDP), pertanto si consiglia di utilizzare le dipendenze di toodownload hello Hortonworks repository per i progetti Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="0732f-140">HDInsight is based on hello Hortonworks Data Platform (HDP), so we recommend using hello Hortonworks repository toodownload dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="0732f-141">In hello __pom.xml__ file, aggiungere hello seguente XML dopo hello `<url>http://maven.apache.org</url>` riga:</span><span class="sxs-lookup"><span data-stu-id="0732f-141">In hello __pom.xml__ file, add hello following XML after hello `<url>http://maven.apache.org</url>` line:</span></span>

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

## <a name="add-properties"></a><span data-ttu-id="0732f-142">Aggiungere le proprietà</span><span class="sxs-lookup"><span data-stu-id="0732f-142">Add properties</span></span>

<span data-ttu-id="0732f-143">Maven consente valori a livello di progetto toodefine denominati di proprietà.</span><span class="sxs-lookup"><span data-stu-id="0732f-143">Maven allows you toodefine project-level values called properties.</span></span> <span data-ttu-id="0732f-144">In hello __pom.xml__, aggiungere hello seguente testo dopo hello `</repositories>` riga:</span><span class="sxs-lookup"><span data-stu-id="0732f-144">In hello __pom.xml__, add hello following text after hello `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="0732f-145">È ora possibile utilizzare questo valore nelle altre sezioni di hello `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="0732f-145">You can now use this value in other sections of hello `pom.xml`.</span></span> <span data-ttu-id="0732f-146">Ad esempio, quando si specifica versione di hello di Storm componenti, è possibile utilizzare `${storm.version}` anziché a livello di codice un valore.</span><span class="sxs-lookup"><span data-stu-id="0732f-146">For example, when specifying hello version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="0732f-147">Aggiungere le dipendenze</span><span class="sxs-lookup"><span data-stu-id="0732f-147">Add dependencies</span></span>

<span data-ttu-id="0732f-148">Aggiungere una dipendenza per i componenti Storm.</span><span class="sxs-lookup"><span data-stu-id="0732f-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="0732f-149">Aprire hello `pom.xml` file e aggiungere hello seguente di codice hello `<dependencies>` sezione:</span><span class="sxs-lookup"><span data-stu-id="0732f-149">Open hello `pom.xml` file and add hello following code in hello `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="0732f-150">In fase di compilazione Maven Usa questo toolook informazioni `storm-core` nel repository di Maven hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-150">At compile time, Maven uses this information toolook up `storm-core` in hello Maven repository.</span></span> <span data-ttu-id="0732f-151">Effettua prima una ricerca nel repository di hello nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="0732f-151">It first looks in hello repository on your local computer.</span></span> <span data-ttu-id="0732f-152">Se non vi sono file di hello, Maven li scarica da archivio Maven pubblico hello e li archivia nel repository locale hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-152">If hello files aren't there, Maven downloads them from hello public Maven repository and stores them in hello local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="0732f-153">Hello preavviso `<scope>provided</scope>` riga in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="0732f-153">Notice hello `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="0732f-154">Questa impostazione indica Maven tooexclude **elevato numero di core** dai file JAR di vengono creati, perché viene fornita dal sistema hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-154">This setting tells Maven tooexclude **storm-core** from any JAR files that are created, because it is provided by hello system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="0732f-155">Configurare la compilazione</span><span class="sxs-lookup"><span data-stu-id="0732f-155">Build configuration</span></span>

<span data-ttu-id="0732f-156">Plug-in di Maven consentono di fasi di compilazione toocustomize hello del progetto hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-156">Maven plug-ins allow you toocustomize hello build stages of hello project.</span></span> <span data-ttu-id="0732f-157">Ad esempio, come viene compilato il progetto hello o come toopackage in un file JAR.</span><span class="sxs-lookup"><span data-stu-id="0732f-157">For example, how hello project is compiled or how toopackage it into a JAR file.</span></span> <span data-ttu-id="0732f-158">Aprire hello `pom.xml` file e aggiungere hello seguente codice direttamente sopra hello `</project>` riga.</span><span class="sxs-lookup"><span data-stu-id="0732f-158">Open hello `pom.xml` file and add hello following code directly above hello `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="0732f-159">In questa sezione viene utilizzato tooadd plug-in, risorse e altre opzioni di configurazione di compilazione.</span><span class="sxs-lookup"><span data-stu-id="0732f-159">This section is used tooadd plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="0732f-160">Per un riferimento completo di hello **pom.xml** file, vedere [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="0732f-160">For a full reference of hello **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="0732f-161">Aggiungere plug-in</span><span class="sxs-lookup"><span data-stu-id="0732f-161">Add plug-ins</span></span>

<span data-ttu-id="0732f-162">Per le topologie di Apache Storm implementate in Java, hello [plug-in Maven Exec](http://www.mojohaus.org/exec-maven-plugin/) è utile perché consente tooeasily eseguire topologia hello in locale nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="0732f-162">For Apache Storm topologies implemented in Java, hello [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you tooeasily run hello topology locally in your development environment.</span></span> <span data-ttu-id="0732f-163">Aggiungere hello seguente toohello `<plugins>` sezione di hello `pom.xml` file plug-in di tooinclude hello Maven Exec:</span><span class="sxs-lookup"><span data-stu-id="0732f-163">Add hello following toohello `<plugins>` section of hello `pom.xml` file tooinclude hello Exec Maven plugin:</span></span>

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

<span data-ttu-id="0732f-164">Un'altra utile plug-in è hello [plug-in compilatore di Apache Maven](http://maven.apache.org/plugins/maven-compiler-plugin/), che viene utilizzato toochange opzioni di compilazione.</span><span class="sxs-lookup"><span data-stu-id="0732f-164">Another useful plug-in is hello [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used toochange compilation options.</span></span> <span data-ttu-id="0732f-165">modifiche di Hello hello versione Java che utilizza Maven per hello origine e di destinazione per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0732f-165">hello changes hello Java version that Maven uses for hello source and target for your application.</span></span>

* <span data-ttu-id="0732f-166">Per HDInsight __3.4 o versioni precedenti__, impostare l'origine hello e too__1.7__ versione Java di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0732f-166">For HDInsight __3.4 or earlier__, set hello source and target Java version too__1.7__.</span></span>

* <span data-ttu-id="0732f-167">Per HDInsight __3.5__, impostare l'origine hello e too__1.8__ versione Java di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0732f-167">For HDInsight __3.5__, set hello source and target Java version too__1.8__.</span></span>

<span data-ttu-id="0732f-168">Aggiungere hello seguente testo hello `<plugins>` sezione di hello `pom.xml` file plug-in Apache Maven compilatore hello di tooinclude.</span><span class="sxs-lookup"><span data-stu-id="0732f-168">Add hello following text in hello `<plugins>` section of hello `pom.xml` file tooinclude hello Apache Maven Compiler plugin.</span></span> <span data-ttu-id="0732f-169">In questo esempio specifica 1.8, pertanto la versione di HDInsight destinazione di hello è 3.5.</span><span class="sxs-lookup"><span data-stu-id="0732f-169">This example specifies 1.8, so hello target HDInsight version is 3.5.</span></span>

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

### <a name="configure-resources"></a><span data-ttu-id="0732f-170">Configure resources</span><span class="sxs-lookup"><span data-stu-id="0732f-170">Configure resources</span></span>

<span data-ttu-id="0732f-171">la sezione relativa alle risorse Hello consente le risorse non di codice tooinclude, ad esempio i file di configurazione necessari per i componenti nella topologia hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-171">hello resources section allows you tooinclude non-code resources such as configuration files needed by components in hello topology.</span></span> <span data-ttu-id="0732f-172">Per questo esempio, aggiungere hello seguente testo hello `<resources>` sezione di hello ' pom.xml file.</span><span class="sxs-lookup"><span data-stu-id="0732f-172">For this example, add hello following text in hello `<resources>` section of hello \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="0732f-173">Questo esempio aggiunge una directory delle risorse hello nella directory radice del progetto hello hello (`${basedir}`) come un percorso che contiene le risorse e include file hello denominato `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="0732f-173">This example adds hello resources directory in hello root of hello project (`${basedir}`) as a location that contains resources, and includes hello file named `log4j2.xml`.</span></span> <span data-ttu-id="0732f-174">Questo file è utilizzato tooconfigure quali informazioni vengono registrate dalla topologia hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-174">This file is used tooconfigure what information is logged by hello topology.</span></span>

## <a name="create-hello-topology"></a><span data-ttu-id="0732f-175">Creare la topologia hello</span><span class="sxs-lookup"><span data-stu-id="0732f-175">Create hello topology</span></span>

<span data-ttu-id="0732f-176">Una topologia Apache Storm basata su Java è costituita da tre componenti che è necessario creare o a cui è necessario fare riferimento come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="0732f-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="0732f-177">**Spouts**: legge origini dati dall'esterno e genera i flussi di dati nella topologia hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-177">**Spouts**: Reads data from external sources and emits streams of data into hello topology.</span></span>

* <span data-ttu-id="0732f-178">**Bolt**: esegue l'elaborazione sui flussi generati dagli spout o da altri bolt e genera uno o più flussi.</span><span class="sxs-lookup"><span data-stu-id="0732f-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="0732f-179">**Topologia**: definisce la modalità spouts hello e dadi sono disposti e fornisce il punto di ingresso di hello per topologia hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-179">**Topology**: Defines how hello spouts and bolts are arranged, and provides hello entry point for hello topology.</span></span>

### <a name="create-hello-spout"></a><span data-ttu-id="0732f-180">Creare beccuccio hello</span><span class="sxs-lookup"><span data-stu-id="0732f-180">Create hello spout</span></span>

<span data-ttu-id="0732f-181">tooreduce requisiti per la configurazione di origini dati esterne, hello seguente beccuccio genera semplicemente frasi casuale.</span><span class="sxs-lookup"><span data-stu-id="0732f-181">tooreduce requirements for setting up external data sources, hello following spout simply emits random sentences.</span></span> <span data-ttu-id="0732f-182">È una versione modificata del beccuccio che viene fornito con hello [esempi Storm Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="0732f-182">It is a modified version of a spout that is provided with hello [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="0732f-183">Per un esempio di beccuccio che legge da un'origine dati esterna, vedere uno dei seguenti esempi hello:</span><span class="sxs-lookup"><span data-stu-id="0732f-183">For an example of a spout that reads from an external data source, see one of hello following examples:</span></span>
>
> * <span data-ttu-id="0732f-184">[TwitterSampleSpout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): spout di esempio che legge da Twitter</span><span class="sxs-lookup"><span data-stu-id="0732f-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="0732f-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): spout che legge da Kafka</span><span class="sxs-lookup"><span data-stu-id="0732f-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="0732f-186">Per beccuccio hello, creare un file denominato `RandomSentenceSpout.java` in hello `src\main\java\com\microsoft\example` hello directory e l'utilizzo seguente di codice Java come contenuto hello:</span><span class="sxs-lookup"><span data-stu-id="0732f-186">For hello spout, create a file named `RandomSentenceSpout.java` in hello `src\main\java\com\microsoft\example` directory and use hello following Java code as hello contents:</span></span>

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
> <span data-ttu-id="0732f-187">Anche se questa topologia viene utilizzato un solo beccuccio, altri utenti possono invece avere diversi che feed di dati da origini diverse in una topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-187">Although this topology uses only one spout, others may have several that feed data from different sources into hello topology.</span></span>

### <a name="create-hello-bolts"></a><span data-ttu-id="0732f-188">Creare bulloni hello</span><span class="sxs-lookup"><span data-stu-id="0732f-188">Create hello bolts</span></span>

<span data-ttu-id="0732f-189">Bulloni gestiscono l'elaborazione dati hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-189">Bolts handle hello data processing.</span></span> <span data-ttu-id="0732f-190">Questa topologia usa due bolt:</span><span class="sxs-lookup"><span data-stu-id="0732f-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="0732f-191">**SplitSentence**: suddivide frasi hello generate da **RandomSentenceSpout** in singole parole.</span><span class="sxs-lookup"><span data-stu-id="0732f-191">**SplitSentence**: Splits hello sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="0732f-192">**WordCount**: conta le occorrenze di ciascuna parola.</span><span class="sxs-lookup"><span data-stu-id="0732f-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="0732f-193">Bulloni eseguire qualsiasi operazione, ad esempio, calcolo, la persistenza o tooexternal componenti per comunicare con.</span><span class="sxs-lookup"><span data-stu-id="0732f-193">Bolts can do anything, for example, computation, persistence, or talking tooexternal components.</span></span>

<span data-ttu-id="0732f-194">Creare due nuovi file, `SplitSentence.java` e `WordCount.java` in hello `src\main\java\com\microsoft\example` directory.</span><span class="sxs-lookup"><span data-stu-id="0732f-194">Create two new files, `SplitSentence.java` and `WordCount.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="0732f-195">Utilizzare hello segue testo come contenuto di hello per i file hello:</span><span class="sxs-lookup"><span data-stu-id="0732f-195">Use hello following text as hello contents for hello files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="0732f-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="0732f-196">SplitSentence</span></span>

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

#### <a name="wordcount"></a><span data-ttu-id="0732f-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="0732f-197">WordCount</span></span>

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

### <a name="define-hello-topology"></a><span data-ttu-id="0732f-198">Definire la topologia hello</span><span class="sxs-lookup"><span data-stu-id="0732f-198">Define hello topology</span></span>

<span data-ttu-id="0732f-199">topologia Hello collega spouts hello e bulloni insieme in un grafico, che definisce il flusso dei dati tra i componenti di hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-199">hello topology ties hello spouts and bolts together into a graph, which defines how data flows between hello components.</span></span> <span data-ttu-id="0732f-200">Fornisce inoltre gli hint parallelismo Storm utilizza per la creazione di istanze dei componenti di hello all'interno del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-200">It also provides parallelism hints that Storm uses when creating instances of hello components within hello cluster.</span></span>

<span data-ttu-id="0732f-201">Hello immagine seguente è un diagramma di base del grafico hello dei componenti per questa topologia.</span><span class="sxs-lookup"><span data-stu-id="0732f-201">hello following image is a basic diagram of hello graph of components for this topology.</span></span>

![hello visualizzazione Diagramma spouts e bulloni disposizione](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="0732f-203">tooimplement hello topologia, creare un file denominato `WordCountTopology.java` in hello `src\main\java\com\microsoft\example` directory.</span><span class="sxs-lookup"><span data-stu-id="0732f-203">tooimplement hello topology, create a file named `WordCountTopology.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="0732f-204">Utilizzare hello seguente di codice Java come contenuto di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="0732f-204">Use hello following Java code as hello contents of hello file:</span></span>

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

### <a name="configure-logging"></a><span data-ttu-id="0732f-205">Configurare la registrazione</span><span class="sxs-lookup"><span data-stu-id="0732f-205">Configure logging</span></span>

<span data-ttu-id="0732f-206">Storm Usa Log4j Apache toolog informazioni.</span><span class="sxs-lookup"><span data-stu-id="0732f-206">Storm uses Apache Log4j toolog information.</span></span> <span data-ttu-id="0732f-207">Se non si configura la registrazione, la topologia hello genera informazioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="0732f-207">If you do not configure logging, hello topology emits diagnostic information.</span></span> <span data-ttu-id="0732f-208">toocontrol informazioni di connessione, creare un file denominato `log4j2.xml` in hello `resources` directory.</span><span class="sxs-lookup"><span data-stu-id="0732f-208">toocontrol what is logged, create a file named `log4j2.xml` in hello `resources` directory.</span></span> <span data-ttu-id="0732f-209">Utilizzare hello seguente XML come contenuto di hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-209">Use hello following XML as hello contents of hello file.</span></span>

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

<span data-ttu-id="0732f-210">Questo codice XML consente di configurare un nuovo logger per hello `com.microsoft.example` (classe), che include i componenti di hello in questa topologia di esempio.</span><span class="sxs-lookup"><span data-stu-id="0732f-210">This XML configures a new logger for hello `com.microsoft.example` class, which includes hello components in this example topology.</span></span> <span data-ttu-id="0732f-211">livello di Hello è impostato tootrace per questo logger, che acquisisce le informazioni di registrazione generate dai componenti in questa topologia.</span><span class="sxs-lookup"><span data-stu-id="0732f-211">hello level is set tootrace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="0732f-212">Hello `<Root level="error">` sezione Configura a livello di radice hello di registrazione (tutti gli elementi non in `com.microsoft.example`) tooonly informazioni sugli errori di log.</span><span class="sxs-lookup"><span data-stu-id="0732f-212">hello `<Root level="error">` section configures hello root level of logging (everything not in `com.microsoft.example`) tooonly log error information.</span></span>

<span data-ttu-id="0732f-213">Per altre informazioni sulla configurazione della registrazione per Log4j, vedere [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="0732f-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="0732f-214">Storm versione 0.10.0 e successive usano Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="0732f-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="0732f-215">Le versioni precedenti usano Log4j 1.x, che impiega un formato diverso per la configurazione del log.</span><span class="sxs-lookup"><span data-stu-id="0732f-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="0732f-216">Per informazioni sulla configurazione precedente hello, vedere [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="0732f-216">For information on hello older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-hello-topology-locally"></a><span data-ttu-id="0732f-217">Topologia di hello test localmente</span><span class="sxs-lookup"><span data-stu-id="0732f-217">Test hello topology locally</span></span>

<span data-ttu-id="0732f-218">Dopo aver salvato il file hello, utilizzare hello seguente topologia hello tootest di comando localmente.</span><span class="sxs-lookup"><span data-stu-id="0732f-218">After you save hello files, use hello following command tootest hello topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="0732f-219">Durante l'esecuzione, la topologia hello Visualizza le informazioni di avvio.</span><span class="sxs-lookup"><span data-stu-id="0732f-219">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="0732f-220">Hello testo riportato di seguito è riportato un esempio dell'output di hello word conteggio:</span><span class="sxs-lookup"><span data-stu-id="0732f-220">hello following text is an example of hello word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="0732f-221">Questo log di esempio indica tale parola hello ' e ' è stato emesso 113 volte.</span><span class="sxs-lookup"><span data-stu-id="0732f-221">This example log indicates that hello word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="0732f-222">Hello conteggio risale toogo purché topologia hello eseguito poiché beccuccio hello genera continuamente hello stesse frasi.</span><span class="sxs-lookup"><span data-stu-id="0732f-222">hello count continues toogo up as long as hello topology runs because hello spout continuously emits hello same sentences.</span></span>

<span data-ttu-id="0732f-223">C'è un intervallo di 5 secondi tra l'emissione di parole e i conteggi.</span><span class="sxs-lookup"><span data-stu-id="0732f-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="0732f-224">Hello **WordCount** configurato tooonly generi informazioni quando arriva una tupla di segni di graduazione.</span><span class="sxs-lookup"><span data-stu-id="0732f-224">hello **WordCount** component is configured tooonly emit information when a tick tuple arrives.</span></span> <span data-ttu-id="0732f-225">Richiede che le tuple tick vengano recapitate solo ogni cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="0732f-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-hello-topology-tooflux"></a><span data-ttu-id="0732f-226">Convertire hello topologia tooFlux</span><span class="sxs-lookup"><span data-stu-id="0732f-226">Convert hello topology tooFlux</span></span>

<span data-ttu-id="0732f-227">Flusso è un nuovo framework disponibili con Storm 0.10.0 e versioni successive, che consente la configurazione tooseparate dall'implementazione.</span><span class="sxs-lookup"><span data-stu-id="0732f-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you tooseparate configuration from implementation.</span></span> <span data-ttu-id="0732f-228">I componenti sono ancora definiti in Java, ma la topologia hello è definita mediante un file YAML.</span><span class="sxs-lookup"><span data-stu-id="0732f-228">Your components are still defined in Java, but hello topology is defined using a YAML file.</span></span> <span data-ttu-id="0732f-229">È possibile creare un pacchetto una definizione di topologia predefinito con il progetto o utilizzare un file autonomo per l'invio di topologia hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-229">You can package a default topology definition with your project, or use a standalone file when submitting hello topology.</span></span> <span data-ttu-id="0732f-230">Quando si inviano hello topologia tooStorm, è possibile utilizzare variabili di ambiente o i valori di configurazione file toopopulate nella definizione della topologia YAML hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-230">When submitting hello topology tooStorm, you can use environment variables or configuration files toopopulate values in hello YAML topology definition.</span></span>

<span data-ttu-id="0732f-231">file YAML Hello definisce hello componenti toouse per topologia hello e flusso di dati hello tra di essi.</span><span class="sxs-lookup"><span data-stu-id="0732f-231">hello YAML file defines hello components toouse for hello topology and hello data flow between them.</span></span> <span data-ttu-id="0732f-232">È possibile includere un file YAML come parte del file jar hello o è possibile utilizzare un file YAML esterno.</span><span class="sxs-lookup"><span data-stu-id="0732f-232">You can include a YAML file as part of hello jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="0732f-233">Per altre informazioni su Flux, vedere [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="0732f-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="0732f-234">Scadenza tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) con Storm 1.0.1, potrebbe essere necessario tooinstall un [ambiente di sviluppo Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun localmente topologie di flusso.</span><span class="sxs-lookup"><span data-stu-id="0732f-234">Due tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need tooinstall a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun Flux topologies locally.</span></span>

1. <span data-ttu-id="0732f-235">Spostare hello `WordCountTopology.java` file di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-235">Move hello `WordCountTopology.java` file out of hello project.</span></span> <span data-ttu-id="0732f-236">In precedenza, questo file definito topologia hello, ma non è necessaria con flusso.</span><span class="sxs-lookup"><span data-stu-id="0732f-236">Previously, this file defined hello topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="0732f-237">In hello `resources` directory, creare un file denominato `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="0732f-237">In hello `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="0732f-238">Utilizzare hello segue testo come contenuto di hello di questo file.</span><span class="sxs-lookup"><span data-stu-id="0732f-238">Use hello following text as hello contents of this file.</span></span>

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

3. <span data-ttu-id="0732f-239">Rendere hello dopo le modifiche toohello `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="0732f-239">Make hello following changes toohello `pom.xml` file.</span></span>
   
   * <span data-ttu-id="0732f-240">Aggiungere hello seguente nuove dipendenze nella hello `<dependencies>` sezione:</span><span class="sxs-lookup"><span data-stu-id="0732f-240">Add hello following new dependency in hello `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="0732f-241">Aggiungere i seguenti plug-in toohello hello `<plugins>` sezione.</span><span class="sxs-lookup"><span data-stu-id="0732f-241">Add hello following plugin toohello `<plugins>` section.</span></span> <span data-ttu-id="0732f-242">Questo plug-in gestisce la creazione di hello di un pacchetto (file jar) per il progetto hello e applica alcuni tooFlux specifico di trasformazioni durante la creazione di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-242">This plugin handles hello creation of a package (jar file) for hello project, and applies some transformations specific tooFlux when creating hello package.</span></span>
     
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

   * <span data-ttu-id="0732f-243">In hello **plug-in exec maven** `<configuration>` sezione, modificare il valore di hello per `<mainClass>` troppo`org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="0732f-243">In hello **exec-maven-plugin** `<configuration>` section, change hello value for `<mainClass>` too`org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="0732f-244">Questa impostazione consente toohandle luminoso eseguito localmente topologia hello in fase di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="0732f-244">This setting allows Flux toohandle running hello topology locally in development.</span></span>

   * <span data-ttu-id="0732f-245">In hello `<resources>` sezione, aggiungere hello seguente toohello `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="0732f-245">In hello `<resources>` section, add hello following toohello `<includes>`.</span></span> <span data-ttu-id="0732f-246">Questo codice XML include file YAML hello che definisce la topologia hello come parte del progetto hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-246">This XML includes hello YAML file that defines hello topology as part of hello project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a><span data-ttu-id="0732f-247">Topologia luminoso hello di test in locale</span><span class="sxs-lookup"><span data-stu-id="0732f-247">Test hello flux topology locally</span></span>

1. <span data-ttu-id="0732f-248">Utilizzare hello seguente toocompile ed eseguire topologia luminoso hello Maven utilizzando:</span><span class="sxs-lookup"><span data-stu-id="0732f-248">Use hello following toocompile and execute hello Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="0732f-249">Se si usa PowerShell, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0732f-249">If you are using PowerShell, use hello following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="0732f-250">Questo comando non va a buon fine se la topologia usa bit di Storm 1.0.1.</span><span class="sxs-lookup"><span data-stu-id="0732f-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="0732f-251">I motivi della mancata riuscita sono indicati in [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="0732f-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="0732f-252">In alternativa, [installare Storm nell'ambiente di sviluppo](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) e hello di utilizzare le seguenti informazioni.</span><span class="sxs-lookup"><span data-stu-id="0732f-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use hello following information.</span></span>

    <span data-ttu-id="0732f-253">Se dispone di [installato Storm nell'ambiente di sviluppo](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), è possibile utilizzare i seguenti comandi invece hello:</span><span class="sxs-lookup"><span data-stu-id="0732f-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use hello following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="0732f-254">Hello `--local` parametro viene eseguito topologia hello in modalità locale in ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="0732f-254">hello `--local` parameter runs hello topology in local mode on your development environment.</span></span> <span data-ttu-id="0732f-255">Hello `-R /topology.yaml` parametro utilizza hello `topology.yaml` risorsa file dalla topologia di hello jar file toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-255">hello `-R /topology.yaml` parameter uses hello `topology.yaml` file resource from hello jar file toodefine hello topology.</span></span>

    <span data-ttu-id="0732f-256">Durante l'esecuzione, la topologia hello Visualizza le informazioni di avvio.</span><span class="sxs-lookup"><span data-stu-id="0732f-256">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="0732f-257">Dopo il testo Hello è riportato un esempio di output di hello:</span><span class="sxs-lookup"><span data-stu-id="0732f-257">hello following text is an example of hello output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="0732f-258">C'è un ritardo di 10 secondi tra i batch delle informazioni registrate.</span><span class="sxs-lookup"><span data-stu-id="0732f-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="0732f-259">Creare una copia di hello `topology.yaml` file dal progetto hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-259">Make a copy of hello `topology.yaml` file from hello project.</span></span> <span data-ttu-id="0732f-260">Nuovo file di nome hello `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="0732f-260">Name hello new file `newtopology.yaml`.</span></span> <span data-ttu-id="0732f-261">In hello `newtopology.yaml` file, trovare il seguente hello sezione e modificare il valore di hello di `10` troppo`5`.</span><span class="sxs-lookup"><span data-stu-id="0732f-261">In hello `newtopology.yaml` file, find hello following section and change hello value of `10` too`5`.</span></span> <span data-ttu-id="0732f-262">Questo intervallo di hello modifica modifiche tra la creazione di batch di word conta da too5 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="0732f-262">This modification changes hello interval between emitting batches of word counts from 10 seconds too5.</span></span>

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

    <span data-ttu-id="0732f-263">In alternativa, se si dispone di Storm nell'ambiente di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="0732f-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="0732f-264">Hello modifica `/path/to/newtopology.yaml` toohello percorso toohello newtopology.yaml file creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-264">Change hello `/path/to/newtopology.yaml` toohello path toohello newtopology.yaml file you created in hello previous step.</span></span> <span data-ttu-id="0732f-265">Questo comando Usa hello newtopology.yaml come definizione della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="0732f-265">This command uses hello newtopology.yaml as hello topology definition.</span></span> <span data-ttu-id="0732f-266">Poiché non è stato incluso hello `compile` Maven parametro, utilizza la versione di hello del progetto hello creato nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="0732f-266">Since we didn't include hello `compile` parameter, Maven uses hello version of hello project built in previous steps.</span></span>

    <span data-ttu-id="0732f-267">Una volta hello topologia venga avviato, si noterà che ora hello tra i batch generato è stato modificato il valore hello tooreflect in newtopology.yaml.</span><span class="sxs-lookup"><span data-stu-id="0732f-267">Once hello topology starts, you should notice that hello time between emitted batches has changed tooreflect hello value in newtopology.yaml.</span></span> <span data-ttu-id="0732f-268">Pertanto, è possibile vedere che è possibile modificare la configurazione tramite un file YAML senza la necessità della topologia hello toorecompile.</span><span class="sxs-lookup"><span data-stu-id="0732f-268">So you can see that you can change your configuration through a YAML file without having toorecompile hello topology.</span></span>

<span data-ttu-id="0732f-269">Per ulteriori informazioni su queste e altre funzionalità di hello luminoso framework, vedere [luminoso (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="0732f-269">For more information on these and other features of hello Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="0732f-270">Trident</span><span class="sxs-lookup"><span data-stu-id="0732f-270">Trident</span></span>

<span data-ttu-id="0732f-271">Trident è un'astrazione di alto livello fornita da Storm</span><span class="sxs-lookup"><span data-stu-id="0732f-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="0732f-272">che supporta l'elaborazione con informazioni sullo stato.</span><span class="sxs-lookup"><span data-stu-id="0732f-272">It supports stateful processing.</span></span> <span data-ttu-id="0732f-273">Hello il vantaggio principale di Trident consiste nel fatto che sia possibile garantire che ogni messaggio che viene inserito topologia hello viene elaborata una sola volta.</span><span class="sxs-lookup"><span data-stu-id="0732f-273">hello primary advantage of Trident is that it can guarantee that every message that enters hello topology is processed only once.</span></span> <span data-ttu-id="0732f-274">Senza l'uso di Trident, la topologia può garantire solo che i messaggi vengono elaborati almeno una volta.</span><span class="sxs-lookup"><span data-stu-id="0732f-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="0732f-275">Esistono altre differenze, ad esempio la disponibilità di componenti predefiniti che possono essere usati senza che sia necessario creare bolt.</span><span class="sxs-lookup"><span data-stu-id="0732f-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="0732f-276">I bolt sono infatti sostituiti da componenti meno generici, ad esempio filtri, proiezioni e funzioni.</span><span class="sxs-lookup"><span data-stu-id="0732f-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="0732f-277">È possibile creare applicazioni Trident mediante progetti Maven</span><span class="sxs-lookup"><span data-stu-id="0732f-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="0732f-278">Utilizzare hello basic stesso i passaggi come riportata in precedenza in questo articolo, ovvero solo codice hello è diverso.</span><span class="sxs-lookup"><span data-stu-id="0732f-278">You use hello same basic steps as presented earlier in this article—only hello code is different.</span></span> <span data-ttu-id="0732f-279">Trident anche non (attualmente) utilizzabile con framework di hello luminoso.</span><span class="sxs-lookup"><span data-stu-id="0732f-279">Trident also cannot (currently) be used with hello Flux framework.</span></span>

<span data-ttu-id="0732f-280">Per ulteriori informazioni su Trident, vedere hello [panoramica dell'API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="0732f-280">For more information about Trident, see hello [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="0732f-281">Per un'applicazione Trident di esempio, vedere [Temi di tendenza Twitter con Apache Storm in HDInsight](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="0732f-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0732f-282">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0732f-282">Next Steps</span></span>

<span data-ttu-id="0732f-283">Si è appreso come toocreate una topologia di Storm con Java.</span><span class="sxs-lookup"><span data-stu-id="0732f-283">You have learned how toocreate a Storm topology by using Java.</span></span> <span data-ttu-id="0732f-284">è possibile passare agli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0732f-284">Now learn how to:</span></span>

* [<span data-ttu-id="0732f-285">Distribuzione e gestione di topologie Apache Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0732f-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="0732f-286">Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0732f-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="0732f-287">Per altri esempi di topologie Storm, vedere [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="0732f-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

