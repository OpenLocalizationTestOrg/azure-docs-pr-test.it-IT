---
title: aaaCreate MapReduce Java per Hadoop - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse applicazione MapReduce toocreate basato su Java di Apache Maven, quindi eseguirlo con Hadoop in HDInsight di Azure.
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
ms.assetid: 9ee6384c-cb61-4087-8273-fb53fa27c1c3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 903a57a482395f7da79002188399a4d6288ff0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="fe5b1-103">Sviluppare programmi Java MapReduce per Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe5b1-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="fe5b1-104">Informazioni su come toouse applicazione MapReduce toocreate basato su Java di Apache Maven, quindi eseguirlo con Hadoop in HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-104">Learn how toouse Apache Maven toocreate a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="fe5b1-105">Questo esempio è stato testato molto recentemente in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="fe5b1-106"><a name="prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fe5b1-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="fe5b1-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 o versione successiva oppure prodotto equivalente, ad esempio OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="fe5b1-108">HDInsight versione 3.4 e precedenti usano Java 7.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="fe5b1-109">HDInsight 3.5 e versioni successive usano Java 8.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="fe5b1-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="fe5b1-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="fe5b1-111">Configurare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="fe5b1-111">Configure development environment</span></span>

<span data-ttu-id="fe5b1-112">Hello seguenti variabili di ambiente possono essere impostate quando si installa Java e hello JDK.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-112">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="fe5b1-113">Tuttavia, è necessario verificare che esistano e che contengono i valori corretti di hello per il sistema.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-113">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="fe5b1-114">`JAVA_HOME`-deve puntare toohello directory in cui è installato Java runtime environment (JRE) di hello.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-114">`JAVA_HOME` - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="fe5b1-115">Ad esempio, in un sistema OS X, Unix o Linux, deve essere un valore simile troppo`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-115">For example, on an OS X, Unix or Linux system, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="fe5b1-116">In Windows, avrebbe un valore simile troppo`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="fe5b1-116">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="fe5b1-117">`PATH`-deve contenere hello seguenti percorsi:</span><span class="sxs-lookup"><span data-stu-id="fe5b1-117">`PATH` - should contain hello following paths:</span></span>
  
  * <span data-ttu-id="fe5b1-118">`JAVA_HOME`(o percorso equivalente hello)</span><span class="sxs-lookup"><span data-stu-id="fe5b1-118">`JAVA_HOME` (or hello equivalent path)</span></span>

  * <span data-ttu-id="fe5b1-119">`JAVA_HOME\bin`(o percorso equivalente hello)</span><span class="sxs-lookup"><span data-stu-id="fe5b1-119">`JAVA_HOME\bin` (or hello equivalent path)</span></span>

  * <span data-ttu-id="fe5b1-120">directory di Hello in cui è installato Maven</span><span class="sxs-lookup"><span data-stu-id="fe5b1-120">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="fe5b1-121">Creare un progetto Maven</span><span class="sxs-lookup"><span data-stu-id="fe5b1-121">Create a Maven project</span></span>

1. <span data-ttu-id="fe5b1-122">Da una sessione terminal o la riga di comando nell'ambiente di sviluppo, modificare le directory toohello desiderata toostore questo progetto.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-122">From a terminal session, or command line in your development environment, change directories toohello location you want toostore this project.</span></span>

2. <span data-ttu-id="fe5b1-123">Hello utilizzare `mvn` comando, che viene installato con Maven, hello toogenerate lo scaffolding per progetto hello.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-123">Use hello `mvn` command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="fe5b1-124">Se si usa PowerShell, è necessario racchiudere hello `-D` parametri racchiuso tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-124">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="fe5b1-125">Questo comando crea una directory con nome hello specificato da hello `artifactID` parametro (**wordcountjava** in questo esempio.) Questa directory contiene hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="fe5b1-125">This command creates a directory with hello name specified by hello `artifactID` parameter (**wordcountjava** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="fe5b1-126">`pom.xml`-hello [modello oggetto di progetto (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) che contiene informazioni e i dettagli di configurazione utilizzato progetto hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-126">`pom.xml` - hello [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used toobuild hello project.</span></span>

   * <span data-ttu-id="fe5b1-127">`src`-directory hello che contiene l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-127">`src` - hello directory that contains hello application.</span></span>

3. <span data-ttu-id="fe5b1-128">Eliminare hello `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-128">Delete hello `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="fe5b1-129">Non viene usato in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="fe5b1-130">Aggiungere le dipendenze</span><span class="sxs-lookup"><span data-stu-id="fe5b1-130">Add dependencies</span></span>

1. <span data-ttu-id="fe5b1-131">Modifica hello `pom.xml` file e aggiungere hello segue testo all'interno di hello `<dependencies>` sezione:</span><span class="sxs-lookup"><span data-stu-id="fe5b1-131">Edit hello `pom.xml` file and add hello following text inside hello `<dependencies>` section:</span></span>
   
   ```xml
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-examples</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-client-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
   ```

    <span data-ttu-id="fe5b1-132">Questa operazione definisce le librerie richieste (elencate in &lt;artifactId\>) con una versione specifica (elencata in &lt;version\>).</span><span class="sxs-lookup"><span data-stu-id="fe5b1-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="fe5b1-133">In fase di compilazione, queste dipendenze vengono scaricate dal repository di Maven hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-133">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="fe5b1-134">È possibile utilizzare hello [ricerca repository Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview altre.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-134">You can use hello [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview more.</span></span>
   
    <span data-ttu-id="fe5b1-135">Hello `<scope>provided</scope>` indica Maven che queste dipendenze non devono essere fornite con un'applicazione hello, così come sono forniti dal cluster HDInsight hello in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-135">hello `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with hello application, as they are provided by hello HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fe5b1-136">versione di Hello utilizzato deve corrispondere versione di hello presente nel cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-136">hello version used should match hello version of Hadoop present on your cluster.</span></span> <span data-ttu-id="fe5b1-137">Per ulteriori informazioni sulle versioni, vedere hello [il controllo delle versioni di HDInsight componente](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-137">For more information on versions, see hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="fe5b1-138">Aggiungere hello seguente toohello `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-138">Add hello following toohello `pom.xml` file.</span></span> <span data-ttu-id="fe5b1-139">Questo testo deve trovarsi all'interno di hello `<project>...</project>` tag nel file hello, ad esempio tra `</dependencies>` e `</project>`.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-139">This text must be inside hello `<project>...</project>` tags in hello file; for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
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
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.1</version>
            <configuration>
            <source>1.8</source>
            <target>1.8</target>
            </configuration>
        </plugin>
        </plugins>
    </build>
   ```

    <span data-ttu-id="fe5b1-140">plug-in prima Hello Configura hello [plug-in Maven sfumatura](http://maven.apache.org/plugins/maven-shade-plugin/), che viene utilizzato toobuild un uberjar (talvolta denominato un fatjar), che contiene dipendenze richieste da un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-140">hello first plugin configures hello [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used toobuild an uberjar (sometimes called a fatjar), which contains dependencies required by hello application.</span></span> <span data-ttu-id="fe5b1-141">Inoltre, impedisce la duplicazione di licenze di pacchetto di file jar hello, che può causare problemi in alcuni sistemi.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-141">It also prevents duplication of licenses within hello jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="fe5b1-142">plug-in seconda Hello Configura versione Java di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-142">hello second plugin configures hello target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fe5b1-143">HDInsight 3.4 e versioni precedenti usano Java 7.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="fe5b1-144">HDInsight 3.5 e versioni successive usano Java 8.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="fe5b1-145">Salvare hello `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-145">Save hello `pom.xml` file.</span></span>

## <a name="create-hello-mapreduce-application"></a><span data-ttu-id="fe5b1-146">Creare un'applicazione hello MapReduce</span><span class="sxs-lookup"><span data-stu-id="fe5b1-146">Create hello MapReduce application</span></span>

1. <span data-ttu-id="fe5b1-147">Passare toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` hello directory e rinominare `App.java` file troppo`WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-147">Go toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename hello `App.java` file too`WordCount.java`.</span></span>

2. <span data-ttu-id="fe5b1-148">Aprire hello `WordCount.java` file in un editor di testo e sostituire il contenuto di hello con hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="fe5b1-148">Open hello `WordCount.java` file in a text editor and replace hello contents with hello following text:</span></span>
   
    ```java
    package org.apache.hadoop.examples;

    import java.io.IOException;
    import java.util.StringTokenizer;
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.fs.Path;
    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Job;
    import org.apache.hadoop.mapreduce.Mapper;
    import org.apache.hadoop.mapreduce.Reducer;
    import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
    import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class WordCount {

        public static class TokenizerMapper
            extends Mapper<Object, Text, Text, IntWritable>{

        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context
                        ) throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
            word.set(itr.nextToken());
            context.write(word, one);
            }
        }
    }

    public static class IntSumReducer
            extends Reducer<Text,IntWritable,Text,IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values,
                            Context context
                            ) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
            sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
        if (otherArgs.length != 2) {
            System.err.println("Usage: wordcount <in> <out>");
            System.exit(2);
        }
        Job job = new Job(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
        FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
        }
    }
    ```
   
    <span data-ttu-id="fe5b1-149">Nome del pacchetto hello informativa è `org.apache.hadoop.examples` e nome della classe hello `WordCount`.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-149">Notice hello package name is `org.apache.hadoop.examples` and hello class name is `WordCount`.</span></span> <span data-ttu-id="fe5b1-150">Utilizzare questi nomi quando si invia il processo MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-150">You use these names when you submit hello MapReduce job.</span></span>

3. <span data-ttu-id="fe5b1-151">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-151">Save hello file.</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="fe5b1-152">Compilare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="fe5b1-152">Build hello application</span></span>

1. <span data-ttu-id="fe5b1-153">Modificare toohello `wordcountjava` directory, se non si è già presente.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-153">Change toohello `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="fe5b1-154">Utilizzare hello toobuild un file JAR contenente un'applicazione hello del file di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fe5b1-154">Use hello following command toobuild a JAR file containing hello application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="fe5b1-155">Questo comando Elimina gli artefatti di compilazione precedente, Scarica qualsiasi dipendenze che non sono già state installate, e quindi la compilazione e l'applicazione hello del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package hello application.</span></span>

3. <span data-ttu-id="fe5b1-156">Una volta terminato il comando hello, hello `wordcountjava/target` directory contiene un file denominato `wordcountjava-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-156">Once hello command finishes, hello `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fe5b1-157">Hello `wordcountjava-1.0-SNAPSHOT.jar` file è un uberjar, che contiene non solo il processo di WordCount hello, ma richiede anche le dipendenze che hello processo in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-157">hello `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only hello WordCount job, but also dependencies that hello job requires at runtime.</span></span>

## <span data-ttu-id="fe5b1-158"><a id="upload"></a>Caricare file jar hello</span><span class="sxs-lookup"><span data-stu-id="fe5b1-158"><a id="upload"></a>Upload hello jar</span></span>

<span data-ttu-id="fe5b1-159">Utilizzare hello successivo comando tooupload hello jar file toohello HDInsight nodo head:</span><span class="sxs-lookup"><span data-stu-id="fe5b1-159">Use hello following command tooupload hello jar file toohello HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

<span data-ttu-id="fe5b1-160">Questo comando Copia file hello dal nodo head toohello di hello sistema locale.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-160">This command copies hello files from hello local system toohello head node.</span></span> <span data-ttu-id="fe5b1-161">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="fe5b1-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="fe5b1-162"><a name="run"></a>Eseguire il processo MapReduce hello in Hadoop</span><span class="sxs-lookup"><span data-stu-id="fe5b1-162"><a name="run"></a>Run hello MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="fe5b1-163">Connettersi tramite SSH tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-163">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="fe5b1-164">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="fe5b1-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="fe5b1-165">Dalla sessione SSH hello, utilizzare hello applicazione MapReduce hello toorun di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fe5b1-165">From hello SSH session, use hello following command toorun hello MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="fe5b1-166">Questo comando Avvia hello applicazione WordCount MapReduce.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-166">This command starts hello WordCount MapReduce application.</span></span> <span data-ttu-id="fe5b1-167">file di input Hello `/example/data/gutenberg/davinci.txt`, e directory di output di hello è `/example/data/wordcountout`.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-167">hello input file is `/example/data/gutenberg/davinci.txt`, and hello output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="fe5b1-168">File di input hello sia di output sono toohello stored spazio di archiviazione predefinito per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-168">Both hello input file and output are stored toohello default storage for hello cluster.</span></span>

3. <span data-ttu-id="fe5b1-169">Al termine del processo di hello, utilizzare hello risultati hello tooview del comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fe5b1-169">Once hello job completes, use hello following command tooview hello results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="fe5b1-170">Verrà visualizzato un elenco di parole e i conteggi, con toohello simile di valori seguente testo:</span><span class="sxs-lookup"><span data-stu-id="fe5b1-170">You should receive a list of words and counts, with values similar toohello following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="fe5b1-171"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe5b1-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="fe5b1-172">In questo documento, si è appreso come toodevelop un processo MapReduce Java.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-172">In this document, you have learned how toodevelop a Java MapReduce job.</span></span> <span data-ttu-id="fe5b1-173">Vedere i seguenti documenti per altri modi di toowork con HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-173">See hello following documents for other ways toowork with HDInsight.</span></span>

* <span data-ttu-id="fe5b1-174">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="fe5b1-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="fe5b1-175">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="fe5b1-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="fe5b1-176">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe5b1-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="fe5b1-177">Per ulteriori informazioni, vedere anche hello [Centro per sviluppatori Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="fe5b1-177">For more information, see also hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[powershell-PSCredential]: http://social.technet.microsoft.com/wiki/contents/articles/4546.working-with-passwords-secure-strings-and-credentials-in-windows-powershell.aspx

