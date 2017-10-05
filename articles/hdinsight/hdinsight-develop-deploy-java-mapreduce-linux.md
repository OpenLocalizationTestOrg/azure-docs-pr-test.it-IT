---
title: Creare Java MapReduce per Hadoop - Azure HDInsight | Microsoft Docs
description: Informazioni sull'uso di Apache Maven per creare un'applicazione MapReduce basata su Java, quindi per eseguirla con Hadoop su Azure HDInsight.
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
ms.openlocfilehash: 11d63f22204eb2acb530378f53ac72f16a35a4f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="aa791-103">Sviluppare programmi Java MapReduce per Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa791-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="aa791-104">Informazioni sull'uso di Apache Maven per creare un'applicazione MapReduce basata su Java, quindi per eseguirla con Hadoop su Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aa791-104">Learn how to use Apache Maven to create a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="aa791-105">Questo esempio è stato testato molto recentemente in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="aa791-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="aa791-106"><a name="prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="aa791-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="aa791-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 o versione successiva oppure prodotto equivalente, ad esempio OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="aa791-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="aa791-108">HDInsight versione 3.4 e precedenti usano Java 7.</span><span class="sxs-lookup"><span data-stu-id="aa791-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="aa791-109">HDInsight 3.5 e versioni successive usano Java 8.</span><span class="sxs-lookup"><span data-stu-id="aa791-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="aa791-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="aa791-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="aa791-111">Configurare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="aa791-111">Configure development environment</span></span>

<span data-ttu-id="aa791-112">Quando si installa Java e JDK, è possibile impostare le variabili di ambiente indicate di seguito.</span><span class="sxs-lookup"><span data-stu-id="aa791-112">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="aa791-113">È tuttavia necessario verificare che esistano e che contengano i valori corretti per il sistema in uso.</span><span class="sxs-lookup"><span data-stu-id="aa791-113">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="aa791-114">`JAVA_HOME`: deve puntare alla directory in cui è installato Java Runtime Environment (JRE).</span><span class="sxs-lookup"><span data-stu-id="aa791-114">`JAVA_HOME` - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="aa791-115">Ad esempio, in un sistema OS X, Unix o Linux, deve avere un valore simile a `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="aa791-115">For example, on an OS X, Unix or Linux system, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="aa791-116">In Windows, avrebbe un valore simile a `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="aa791-116">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="aa791-117">`PATH`: deve contenere i percorsi seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa791-117">`PATH` - should contain the following paths:</span></span>
  
  * <span data-ttu-id="aa791-118">`JAVA_HOME` (o il percorso equivalente)</span><span class="sxs-lookup"><span data-stu-id="aa791-118">`JAVA_HOME` (or the equivalent path)</span></span>

  * <span data-ttu-id="aa791-119">`JAVA_HOME\bin` (o il percorso equivalente)</span><span class="sxs-lookup"><span data-stu-id="aa791-119">`JAVA_HOME\bin` (or the equivalent path)</span></span>

  * <span data-ttu-id="aa791-120">Directory in cui è installato Maven</span><span class="sxs-lookup"><span data-stu-id="aa791-120">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="aa791-121">Creare un progetto Maven</span><span class="sxs-lookup"><span data-stu-id="aa791-121">Create a Maven project</span></span>

1. <span data-ttu-id="aa791-122">Da una sessione terminal o dalla riga di comando nell'ambiente di sviluppo, passare alla directory in cui si vuole creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="aa791-122">From a terminal session, or command line in your development environment, change directories to the location you want to store this project.</span></span>

2. <span data-ttu-id="aa791-123">Usare il comando `mvn`, che viene installato con Maven, per generare lo scaffolding per il progetto.</span><span class="sxs-lookup"><span data-stu-id="aa791-123">Use the `mvn` command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="aa791-124">Se si usa PowerShell, è necessario racchiudere i parametri `-D` tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="aa791-124">If you are using PowerShell, you must enclose the `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="aa791-125">Questo comando crea una directory con il nome specificato dal parametro `artifactID` (in questo esempio **wordcountjava**). La directory contiene gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa791-125">This command creates a directory with the name specified by the `artifactID` parameter (**wordcountjava** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="aa791-126">`pom.xml`: il modello a oggetti dei progetti ([POM o Project Object Model](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) che contiene le informazioni e i dettagli di configurazione usati per compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="aa791-126">`pom.xml` - The [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used to build the project.</span></span>

   * <span data-ttu-id="aa791-127">`src`: la directory che contiene l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aa791-127">`src` - The directory that contains the application.</span></span>

3. <span data-ttu-id="aa791-128">Eliminare il file `src/test/java/org/apache/hadoop/examples/apptest.java`.</span><span class="sxs-lookup"><span data-stu-id="aa791-128">Delete the `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="aa791-129">Non viene usato in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="aa791-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="aa791-130">Aggiungere le dipendenze</span><span class="sxs-lookup"><span data-stu-id="aa791-130">Add dependencies</span></span>

1. <span data-ttu-id="aa791-131">Modificare il file `pom.xml` e aggiungere il testo seguente nella sezione `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="aa791-131">Edit the `pom.xml` file and add the following text inside the `<dependencies>` section:</span></span>
   
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

    <span data-ttu-id="aa791-132">Questa operazione definisce le librerie richieste (elencate in &lt;artifactId\>) con una versione specifica (elencata in &lt;version\>).</span><span class="sxs-lookup"><span data-stu-id="aa791-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="aa791-133">In fase di compilazione, queste dipendenze vengono scaricata dal repository Maven predefinito.</span><span class="sxs-lookup"><span data-stu-id="aa791-133">At compile time, these dependencies are downloaded from the default Maven repository.</span></span> <span data-ttu-id="aa791-134">È possibile usare la [ricerca nel repository Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) per visualizzare più informazioni.</span><span class="sxs-lookup"><span data-stu-id="aa791-134">You can use the [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) to view more.</span></span>
   
    <span data-ttu-id="aa791-135">`<scope>provided</scope>` indica a Maven che queste dipendenze non devono essere fornite con l'applicazione, perché vengono fornite dal cluster HDInsight in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="aa791-135">The `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with the application, as they are provided by the HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="aa791-136">La versione usata deve corrispondere alla versione di Hadoop presente nel cluster.</span><span class="sxs-lookup"><span data-stu-id="aa791-136">The version used should match the version of Hadoop present on your cluster.</span></span> <span data-ttu-id="aa791-137">Per altre informazioni sulle versioni, vedere il documento sulle [versioni dei componenti HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="aa791-137">For more information on versions, see the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="aa791-138">Aggiungere il testo seguente al file `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="aa791-138">Add the following to the `pom.xml` file.</span></span> <span data-ttu-id="aa791-139">Nel file, il testo deve essere incluso tra i tag `<project>...</project>`, ad esempio tra `</dependencies>` e `</project>`.</span><span class="sxs-lookup"><span data-stu-id="aa791-139">This text must be inside the `<project>...</project>` tags in the file; for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="aa791-140">Il primo plug-in configura il [plug-in Maven Shade](http://maven.apache.org/plugins/maven-shade-plugin/)che viene usato per compilare un file uberjar (detto a volte fatjar), che contiene le dipendenze richieste dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aa791-140">The first plugin configures the [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used to build an uberjar (sometimes called a fatjar), which contains dependencies required by the application.</span></span> <span data-ttu-id="aa791-141">Impedisce anche la duplicazione di licenze all'interno del pacchetto jar, cosa che potrebbe causare problemi in alcuni sistemi.</span><span class="sxs-lookup"><span data-stu-id="aa791-141">It also prevents duplication of licenses within the jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="aa791-142">Il secondo plug-in consente di configurare la versione Java di destinazione.</span><span class="sxs-lookup"><span data-stu-id="aa791-142">The second plugin configures the target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="aa791-143">HDInsight 3.4 e versioni precedenti usano Java 7.</span><span class="sxs-lookup"><span data-stu-id="aa791-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="aa791-144">HDInsight 3.5 e versioni successive usano Java 8.</span><span class="sxs-lookup"><span data-stu-id="aa791-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="aa791-145">Salvare il file.`pom.xml`</span><span class="sxs-lookup"><span data-stu-id="aa791-145">Save the `pom.xml` file.</span></span>

## <a name="create-the-mapreduce-application"></a><span data-ttu-id="aa791-146">Creare l'applicazione MapReduce</span><span class="sxs-lookup"><span data-stu-id="aa791-146">Create the MapReduce application</span></span>

1. <span data-ttu-id="aa791-147">Andare alla directory `wordcountjava/src/main/java/org/apache/hadoop/examples` e rinominare il file `App.java` in `WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="aa791-147">Go to the `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename the `App.java` file to `WordCount.java`.</span></span>

2. <span data-ttu-id="aa791-148">Aprire il file `WordCount.java` in un editor di testo e sostituire il contenuto con il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="aa791-148">Open the `WordCount.java` file in a text editor and replace the contents with the following text:</span></span>
   
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
   
    <span data-ttu-id="aa791-149">Si noti che il nome del pacchetto è `org.apache.hadoop.examples` e il nome della classe è `WordCount`.</span><span class="sxs-lookup"><span data-stu-id="aa791-149">Notice the package name is `org.apache.hadoop.examples` and the class name is `WordCount`.</span></span> <span data-ttu-id="aa791-150">Questi nomi vengono usati per l'invio del processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="aa791-150">You use these names when you submit the MapReduce job.</span></span>

3. <span data-ttu-id="aa791-151">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="aa791-151">Save the file.</span></span>

## <a name="build-the-application"></a><span data-ttu-id="aa791-152">Compilare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aa791-152">Build the application</span></span>

1. <span data-ttu-id="aa791-153">Passare alla directory `wordcountjava` se non è già visualizzata.</span><span class="sxs-lookup"><span data-stu-id="aa791-153">Change to the `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="aa791-154">Usare il comando seguente per compilare un file JAR contenente l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="aa791-154">Use the following command to build a JAR file containing the application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="aa791-155">In tal modo, vengono eliminati eventuali elementi di compilazione precedenti, scaricate le dipendenze non ancora installate e quindi compilato e creato il pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aa791-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package the application.</span></span>

3. <span data-ttu-id="aa791-156">Al completamento del comando, la directory `wordcountjava/target` contiene un file denominato `wordcountjava-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="aa791-156">Once the command finishes, the `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="aa791-157">Il file `wordcountjava-1.0-SNAPSHOT.jar` è un file di tipo uberjar che contiene non solo il processo WordCount, ma anche le dipendenze richieste dal processo durante il runtime.</span><span class="sxs-lookup"><span data-stu-id="aa791-157">The `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only the WordCount job, but also dependencies that the job requires at runtime.</span></span>

## <span data-ttu-id="aa791-158"><a id="upload"></a>Caricare il file JAR</span><span class="sxs-lookup"><span data-stu-id="aa791-158"><a id="upload"></a>Upload the jar</span></span>

<span data-ttu-id="aa791-159">Usare il comando seguente per caricare il file jar nel nodo head di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aa791-159">Use the following command to upload the jar file to the HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for the cluster. Replace __CLUSTERNAME__ with the HDInsight cluster name.

<span data-ttu-id="aa791-160">Questo comando copia i file dal sistema locale nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="aa791-160">This command copies the files from the local system to the head node.</span></span> <span data-ttu-id="aa791-161">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aa791-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="aa791-162"><a name="run"></a>Eseguire il processo MapReduce in Hadoop</span><span class="sxs-lookup"><span data-stu-id="aa791-162"><a name="run"></a>Run the MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="aa791-163">Connettersi a HDInsight tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="aa791-163">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="aa791-164">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aa791-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="aa791-165">Nella sessione SSH usare il comando seguente per eseguire l'applicazione MapReduce:</span><span class="sxs-lookup"><span data-stu-id="aa791-165">From the SSH session, use the following command to run the MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="aa791-166">Questo comando avvia l'applicazione MapReduce WordCount.</span><span class="sxs-lookup"><span data-stu-id="aa791-166">This command starts the WordCount MapReduce application.</span></span> <span data-ttu-id="aa791-167">Il file di input è `/example/data/gutenberg/davinci.txt` e la directory di output è `/example/data/wordcountout`.</span><span class="sxs-lookup"><span data-stu-id="aa791-167">The input file is `/example/data/gutenberg/davinci.txt`, and the output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="aa791-168">I file di input e di output saranno archiviati nell'archiviazione predefinita del cluster.</span><span class="sxs-lookup"><span data-stu-id="aa791-168">Both the input file and output are stored to the default storage for the cluster.</span></span>

3. <span data-ttu-id="aa791-169">Dopo il completamento del processo, usare il comando seguente per visualizzare i risultati:</span><span class="sxs-lookup"><span data-stu-id="aa791-169">Once the job completes, use the following command to view the results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="aa791-170">Dovrebbe essere visualizzato un elenco di parole e conteggi, con valori simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="aa791-170">You should receive a list of words and counts, with values similar to the following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="aa791-171"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aa791-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="aa791-172">In questo documento si è appreso come sviluppare un processo Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="aa791-172">In this document, you have learned how to develop a Java MapReduce job.</span></span> <span data-ttu-id="aa791-173">Vedere i documenti seguenti per altre modalità di utilizzo di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aa791-173">See the following documents for other ways to work with HDInsight.</span></span>

* <span data-ttu-id="aa791-174">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="aa791-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="aa791-175">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="aa791-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="aa791-176">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa791-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="aa791-177">Per altre informazioni, vedere anche il [Centro per sviluppatori Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="aa791-177">For more information, see also the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

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

