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
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a>Sviluppare programmi Java MapReduce per Hadoop in HDInsight

Informazioni su come toouse applicazione MapReduce toocreate basato su Java di Apache Maven, quindi eseguirlo con Hadoop in HDInsight di Azure.

> [!NOTE]
> Questo esempio è stato testato molto recentemente in HDInsight 3.6.

## <a name="prerequisites"></a>Prerequisiti

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 o versione successiva oppure prodotto equivalente, ad esempio OpenJDK.
    
    > [!NOTE]
    > HDInsight versione 3.4 e precedenti usano Java 7. HDInsight 3.5 e versioni successive usano Java 8.

* [Apache Maven](http://maven.apache.org/)

## <a name="configure-development-environment"></a>Configurare l'ambiente di sviluppo

Hello seguenti variabili di ambiente possono essere impostate quando si installa Java e hello JDK. Tuttavia, è necessario verificare che esistano e che contengono i valori corretti di hello per il sistema.

* `JAVA_HOME`-deve puntare toohello directory in cui è installato Java runtime environment (JRE) di hello. Ad esempio, in un sistema OS X, Unix o Linux, deve essere un valore simile troppo`/usr/lib/jvm/java-7-oracle`. In Windows, avrebbe un valore simile troppo`c:\Program Files (x86)\Java\jre1.7`

* `PATH`-deve contenere hello seguenti percorsi:
  
  * `JAVA_HOME`(o percorso equivalente hello)

  * `JAVA_HOME\bin`(o percorso equivalente hello)

  * directory di Hello in cui è installato Maven

## <a name="create-a-maven-project"></a>Creare un progetto Maven

1. Da una sessione terminal o la riga di comando nell'ambiente di sviluppo, modificare le directory toohello desiderata toostore questo progetto.

2. Hello utilizzare `mvn` comando, che viene installato con Maven, hello toogenerate lo scaffolding per progetto hello.

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > Se si usa PowerShell, è necessario racchiudere hello `-D` parametri racchiuso tra virgolette doppie.
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Questo comando crea una directory con nome hello specificato da hello `artifactID` parametro (**wordcountjava** in questo esempio.) Questa directory contiene hello seguenti elementi:

   * `pom.xml`-hello [modello oggetto di progetto (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) che contiene informazioni e i dettagli di configurazione utilizzato progetto hello toobuild.

   * `src`-directory hello che contiene l'applicazione hello.

3. Eliminare hello `src/test/java/org/apache/hadoop/examples/apptest.java` file. Non viene usato in questo esempio.

## <a name="add-dependencies"></a>Aggiungere le dipendenze

1. Modifica hello `pom.xml` file e aggiungere hello segue testo all'interno di hello `<dependencies>` sezione:
   
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

    Questa operazione definisce le librerie richieste (elencate in &lt;artifactId\>) con una versione specifica (elencata in &lt;version\>). In fase di compilazione, queste dipendenze vengono scaricate dal repository di Maven hello predefinito. È possibile utilizzare hello [ricerca repository Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview altre.
   
    Hello `<scope>provided</scope>` indica Maven che queste dipendenze non devono essere fornite con un'applicazione hello, così come sono forniti dal cluster HDInsight hello in fase di esecuzione.

    > [!IMPORTANT]
    > versione di Hello utilizzato deve corrispondere versione di hello presente nel cluster Hadoop. Per ulteriori informazioni sulle versioni, vedere hello [il controllo delle versioni di HDInsight componente](hdinsight-component-versioning.md) documento.

2. Aggiungere hello seguente toohello `pom.xml` file. Questo testo deve trovarsi all'interno di hello `<project>...</project>` tag nel file hello, ad esempio tra `</dependencies>` e `</project>`.

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

    plug-in prima Hello Configura hello [plug-in Maven sfumatura](http://maven.apache.org/plugins/maven-shade-plugin/), che viene utilizzato toobuild un uberjar (talvolta denominato un fatjar), che contiene dipendenze richieste da un'applicazione hello. Inoltre, impedisce la duplicazione di licenze di pacchetto di file jar hello, che può causare problemi in alcuni sistemi.

    plug-in seconda Hello Configura versione Java di destinazione hello.

    > [!NOTE]
    > HDInsight 3.4 e versioni precedenti usano Java 7. HDInsight 3.5 e versioni successive usano Java 8.

3. Salvare hello `pom.xml` file.

## <a name="create-hello-mapreduce-application"></a>Creare un'applicazione hello MapReduce

1. Passare toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` hello directory e rinominare `App.java` file troppo`WordCount.java`.

2. Aprire hello `WordCount.java` file in un editor di testo e sostituire il contenuto di hello con hello seguente testo:
   
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
   
    Nome del pacchetto hello informativa è `org.apache.hadoop.examples` e nome della classe hello `WordCount`. Utilizzare questi nomi quando si invia il processo MapReduce hello.

3. Salvare il file hello.

## <a name="build-hello-application"></a>Compilare un'applicazione hello

1. Modificare toohello `wordcountjava` directory, se non si è già presente.

2. Utilizzare hello toobuild un file JAR contenente un'applicazione hello del file di comando seguente:

   ```
   mvn clean package
   ```

    Questo comando Elimina gli artefatti di compilazione precedente, Scarica qualsiasi dipendenze che non sono già state installate, e quindi la compilazione e l'applicazione hello del pacchetto.

3. Una volta terminato il comando hello, hello `wordcountjava/target` directory contiene un file denominato `wordcountjava-1.0-SNAPSHOT.jar`.
   
   > [!NOTE]
   > Hello `wordcountjava-1.0-SNAPSHOT.jar` file è un uberjar, che contiene non solo il processo di WordCount hello, ma richiede anche le dipendenze che hello processo in fase di esecuzione.

## <a id="upload"></a>Caricare file jar hello

Utilizzare hello successivo comando tooupload hello jar file toohello HDInsight nodo head:

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

Questo comando Copia file hello dal nodo head toohello di hello sistema locale. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="run"></a>Eseguire il processo MapReduce hello in Hadoop

1. Connettersi tramite SSH tooHDInsight. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Dalla sessione SSH hello, utilizzare hello applicazione MapReduce hello toorun di comando seguente:
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    Questo comando Avvia hello applicazione WordCount MapReduce. file di input Hello `/example/data/gutenberg/davinci.txt`, e directory di output di hello è `/example/data/wordcountout`. File di input hello sia di output sono toohello stored spazio di archiviazione predefinito per il cluster hello.

3. Al termine del processo di hello, utilizzare hello risultati hello tooview del comando seguente:
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    Verrà visualizzato un elenco di parole e i conteggi, con toohello simile di valori seguente testo:
   
        zeal    1
        zelus   1
        zenith  2

## <a id="nextsteps"></a>Passaggi successivi

In questo documento, si è appreso come toodevelop un processo MapReduce Java. Vedere i seguenti documenti per altri modi di toowork con HDInsight hello.

* [Usare Hive con HDInsight][hdinsight-use-hive]
* [Usare Pig con HDInsight][hdinsight-use-pig]
* [Usare MapReduce con HDInsight](hdinsight-use-mapreduce.md)

Per ulteriori informazioni, vedere anche hello [Centro per sviluppatori Java](https://azure.microsoft.com/develop/java/).

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

