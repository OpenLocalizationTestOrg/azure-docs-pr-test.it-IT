---
title: aaaJava-funzione definita dall'utente (UDF) con Hive in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toocreate basato su Java definito dall'utente (funzione) (funzione definita dall'utente) che funziona con Hive. Funzione definita dall'utente in questo esempio converte una tabella di toolowercase stringhe di testo.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="15ce6-104">Utilizzare una UDF Java con Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="15ce6-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="15ce6-105">Informazioni su come toocreate basato su Java definito dall'utente (funzione) (funzione definita dall'utente) che funziona con Hive.</span><span class="sxs-lookup"><span data-stu-id="15ce6-105">Learn how toocreate a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="15ce6-106">Hello Java funzione definita dall'utente in questo esempio converte una tabella di stringhe tooall minuscole dei caratteri del testo.</span><span class="sxs-lookup"><span data-stu-id="15ce6-106">hello Java UDF in this example converts a table of text strings tooall-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="15ce6-107">Requisiti</span><span class="sxs-lookup"><span data-stu-id="15ce6-107">Requirements</span></span>

* <span data-ttu-id="15ce6-108">Un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="15ce6-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="15ce6-109">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="15ce6-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="15ce6-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="15ce6-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="15ce6-111">La maggior parte dei passaggi di questo documento vale per entrambi i cluster basati su Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="15ce6-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="15ce6-112">Tuttavia, hello passaggi utilizzati tooupload hello compilata cluster toohello funzione definita dall'utente ed eseguire sono cluster basato su tooLinux specifici.</span><span class="sxs-lookup"><span data-stu-id="15ce6-112">However, hello steps used tooupload hello compiled UDF toohello cluster and run it are specific tooLinux-based clusters.</span></span> <span data-ttu-id="15ce6-113">Tooinformation che può essere utilizzato con i cluster basati su Windows vengono forniti collegamenti.</span><span class="sxs-lookup"><span data-stu-id="15ce6-113">Links are provided tooinformation that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="15ce6-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 o versione successiva (o equivalente, ad esempio OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="15ce6-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="15ce6-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="15ce6-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="15ce6-116">Un editor di testo o ambiente IDE Java</span><span class="sxs-lookup"><span data-stu-id="15ce6-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="15ce6-117">Se si crea hello file Python in un client Windows, è necessario utilizzare un editor che utilizza LF come una terminazione di riga.</span><span class="sxs-lookup"><span data-stu-id="15ce6-117">If you create hello Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="15ce6-118">Se non si è certi se l'editor utilizza LF o CRLF, vedere hello [Troubleshooting](#troubleshooting) sezione per i passaggi per la rimozione di hello carattere CR.</span><span class="sxs-lookup"><span data-stu-id="15ce6-118">If you are not sure whether your editor uses LF or CRLF, see hello [Troubleshooting](#troubleshooting) section for steps on removing hello CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="15ce6-119">Creare una UDF Java di esempio</span><span class="sxs-lookup"><span data-stu-id="15ce6-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="15ce6-120">Dalla riga di comando, utilizzare hello toocreate un nuovo progetto di Maven seguenti:</span><span class="sxs-lookup"><span data-stu-id="15ce6-120">From a command line, use hello following toocreate a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="15ce6-121">Se si usa PowerShell, è necessario racchiuderlo tra virgolette i parametri di hello.</span><span class="sxs-lookup"><span data-stu-id="15ce6-121">If you are using PowerShell, you must put quotes around hello parameters.</span></span> <span data-ttu-id="15ce6-122">ad esempio `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="15ce6-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="15ce6-123">Questo comando crea una directory denominata **exampleudf**, che contiene progetti Maven hello.</span><span class="sxs-lookup"><span data-stu-id="15ce6-123">This command creates a directory named **exampleudf**, which contains hello Maven project.</span></span>

2. <span data-ttu-id="15ce6-124">Dopo aver creato il progetto di hello, eliminare hello **exampleudf/src/test** directory in cui è stato creato come parte del progetto hello.</span><span class="sxs-lookup"><span data-stu-id="15ce6-124">Once hello project has been created, delete hello **exampleudf/src/test** directory that was created as part of hello project.</span></span>

3. <span data-ttu-id="15ce6-125">Aprire hello **exampleudf/pom.xml**e sostituire hello `<dependencies>` voce con hello XML seguente:</span><span class="sxs-lookup"><span data-stu-id="15ce6-125">Open hello **exampleudf/pom.xml**, and replace hello existing `<dependencies>` entry with hello following XML:</span></span>

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    <span data-ttu-id="15ce6-126">Queste voci specifichino la versione di hello di Hadoop e Hive incluso in HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="15ce6-126">These entries specify hello version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="15ce6-127">È possibile trovare informazioni sulle versioni di hello di Hadoop e Hive fornito con HDInsight da hello [il controllo delle versioni di HDInsight componente](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="15ce6-127">You can find information on hello versions of Hadoop and Hive provided with HDInsight from hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="15ce6-128">Aggiungere un `<build>` sezione prima hello `</project>` riga alla fine di hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="15ce6-128">Add a `<build>` section before hello `</project>` line at hello end of hello file.</span></span> <span data-ttu-id="15ce6-129">In questa sezione deve contenere hello XML seguente:</span><span class="sxs-lookup"><span data-stu-id="15ce6-129">This section should contain hello following XML:</span></span>

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
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
        </plugins>
    </build>
    ```

    <span data-ttu-id="15ce6-130">Queste voci definiscono come toobuild hello progetto.</span><span class="sxs-lookup"><span data-stu-id="15ce6-130">These entries define how toobuild hello project.</span></span> <span data-ttu-id="15ce6-131">In particolare, versione di hello Java che hello progetto usa e in che modo toobuild un uberjar per cluster toohello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="15ce6-131">Specifically, hello version of Java that hello project uses and how toobuild an uberjar for deployment toohello cluster.</span></span>

    <span data-ttu-id="15ce6-132">Dopo che sono state apportate modifiche hello, salvare file hello.</span><span class="sxs-lookup"><span data-stu-id="15ce6-132">Save hello file once hello changes have been made.</span></span>

4. <span data-ttu-id="15ce6-133">Rinominare **exampleudf/src/main/java/com/microsoft/examples/App.java** troppo**ExampleUDF.java**e quindi aprire il file hello nell'editor.</span><span class="sxs-lookup"><span data-stu-id="15ce6-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** too**ExampleUDF.java**, and then open hello file in your editor.</span></span>

5. <span data-ttu-id="15ce6-134">Sostituire il contenuto di hello di hello **ExampleUDF.java** file con il seguente hello, quindi salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="15ce6-134">Replace hello contents of hello **ExampleUDF.java** file with hello following, then save hello file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="15ce6-135">Questo codice implementa una funzione definita dall'utente che accetta un valore di stringa e restituisce una versione a caratteri minuscola della stringa hello.</span><span class="sxs-lookup"><span data-stu-id="15ce6-135">This code implements a UDF that accepts a string value, and returns a lowercase version of hello string.</span></span>

## <a name="build-and-install-hello-udf"></a><span data-ttu-id="15ce6-136">Compilare e installare hello funzione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="15ce6-136">Build and install hello UDF</span></span>

1. <span data-ttu-id="15ce6-137">Utilizzare hello successivo comando toocompile e pacchetto hello funzione definita dall'utente:</span><span class="sxs-lookup"><span data-stu-id="15ce6-137">Use hello following command toocompile and package hello UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="15ce6-138">Questo comando Compila e pacchetti hello funzione definita dall'utente in hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span><span class="sxs-lookup"><span data-stu-id="15ce6-138">This command builds and packages hello UDF into hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="15ce6-139">Hello utilizzare `scp` del cluster di HDInsight toohello comando toocopy hello file.</span><span class="sxs-lookup"><span data-stu-id="15ce6-139">Use hello `scp` command toocopy hello file toohello HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="15ce6-140">Sostituire `myuser` con hello account utente SSH per il cluster.</span><span class="sxs-lookup"><span data-stu-id="15ce6-140">Replace `myuser` with hello SSH user account for your cluster.</span></span> <span data-ttu-id="15ce6-141">Sostituire `mycluster` con il nome del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="15ce6-141">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="15ce6-142">Se si utilizza un hello toosecure password SSH account, si è password hello tooenter richiesta.</span><span class="sxs-lookup"><span data-stu-id="15ce6-142">If you used a password toosecure hello SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="15ce6-143">Se si utilizza un certificato, potrebbe essere necessario hello toouse `-i` parametro toospecify hello file di chiave privata.</span><span class="sxs-lookup"><span data-stu-id="15ce6-143">If you used a certificate, you may need toouse hello `-i` parameter toospecify hello private key file.</span></span>

3. <span data-ttu-id="15ce6-144">Connettere il cluster toohello tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="15ce6-144">Connect toohello cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="15ce6-145">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="15ce6-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="15ce6-146">Dalla sessione SSH hello, copiare archiviazione tooHDInsight file jar di hello.</span><span class="sxs-lookup"><span data-stu-id="15ce6-146">From hello SSH session, copy hello jar file tooHDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a><span data-ttu-id="15ce6-147">Utilizzare hello funzione definita dall'utente dall'Hive</span><span class="sxs-lookup"><span data-stu-id="15ce6-147">Use hello UDF from Hive</span></span>

1. <span data-ttu-id="15ce6-148">Utilizzare i seguenti client di Beeline toostart hello dalla sessione SSH hello hello.</span><span class="sxs-lookup"><span data-stu-id="15ce6-148">Use hello following toostart hello Beeline client from hello SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="15ce6-149">Questo comando si presuppone che sia stato utilizzato predefinito hello **admin** per account di accesso hello per il cluster.</span><span class="sxs-lookup"><span data-stu-id="15ce6-149">This command assumes that you used hello default of **admin** for hello login account for your cluster.</span></span>

2. <span data-ttu-id="15ce6-150">Dopo aver concluso hello `jdbc:hive2://localhost:10001/>` richiesto, immettere hello seguente tooadd hello funzione definita dall'utente tooHive e che venga esposto come una funzione.</span><span class="sxs-lookup"><span data-stu-id="15ce6-150">Once you arrive at hello `jdbc:hive2://localhost:10001/>` prompt, enter hello following tooadd hello UDF tooHive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="15ce6-151">Questo esempio si presuppone che l'archiviazione di Azure è archivio predefinito per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="15ce6-151">This example assumes that Azure Storage is default storage for hello cluster.</span></span> <span data-ttu-id="15ce6-152">Se il cluster utilizza invece l'archivio Data Lake, modificare hello `wasb:///` valore troppo`adl:///`.</span><span class="sxs-lookup"><span data-stu-id="15ce6-152">If your cluster uses Data Lake Store instead, change hello `wasb:///` value too`adl:///`.</span></span>

3. <span data-ttu-id="15ce6-153">Utilizzare hello UDF tooconvert valori recuperati da una stringa di case toolower tabella.</span><span class="sxs-lookup"><span data-stu-id="15ce6-153">Use hello UDF tooconvert values retrieved from a table toolower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="15ce6-154">La query Seleziona hello piattaforma del dispositivo (Android, Windows, iOS, e così via) dalla tabella hello, convertire hello stringa toolower maiuscole e quindi visualizzarli.</span><span class="sxs-lookup"><span data-stu-id="15ce6-154">This query selects hello device platform (Android, Windows, iOS, etc.) from hello table, convert hello string toolower case, and then display them.</span></span> <span data-ttu-id="15ce6-155">output di Hello viene visualizzato toohello simile, il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="15ce6-155">hello output appears similar toohello following text:</span></span>

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a><span data-ttu-id="15ce6-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15ce6-156">Next steps</span></span>

<span data-ttu-id="15ce6-157">Per altri modi toowork con Hive, vedere [utilizzare Hive con HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="15ce6-157">For other ways toowork with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="15ce6-158">Per ulteriori informazioni sulle funzioni Hive User-Defined, vedere [Hive operatori e funzioni definite dall'utente](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) sezione wiki di Hive hello in apache.org.</span><span class="sxs-lookup"><span data-stu-id="15ce6-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of hello Hive wiki at apache.org.</span></span>
