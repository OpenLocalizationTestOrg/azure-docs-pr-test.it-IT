---
title: Funzione definita dall'utente (UDF) Java con Hive in HDInsight - Azure | Documentazione Microsoft
description: Informazioni su come creare una funzione definita dall'utente (UDF) basata su Java che funzioni con Hive. In questo esempio, UDF converte una tabella di stringhe di testo in caratteri minuscoli.
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
ms.openlocfilehash: 481d234eaf88bdb210821084ee4154159470eda0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="917a0-104">Utilizzare una UDF Java con Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="917a0-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="917a0-105">Informazioni su come creare una funzione definita dall'utente (UDF) basata su Java che funzioni con Hive.</span><span class="sxs-lookup"><span data-stu-id="917a0-105">Learn how to create a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="917a0-106">La UDF Java di questo esempio converte una tabella di stringhe di testo in caratteri minuscoli.</span><span class="sxs-lookup"><span data-stu-id="917a0-106">The Java UDF in this example converts a table of text strings to all-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="917a0-107">Requisiti</span><span class="sxs-lookup"><span data-stu-id="917a0-107">Requirements</span></span>

* <span data-ttu-id="917a0-108">Un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="917a0-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="917a0-109">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="917a0-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="917a0-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="917a0-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="917a0-111">La maggior parte dei passaggi di questo documento vale per entrambi i cluster basati su Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="917a0-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="917a0-112">I passaggi necessari per caricare la funzione definita dall'utente compilata nel cluster ed eseguirla sono tuttavia specifici per i cluster basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="917a0-112">However, the steps used to upload the compiled UDF to the cluster and run it are specific to Linux-based clusters.</span></span> <span data-ttu-id="917a0-113">Vengono forniti i collegamenti alle informazioni utili per i cluster basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="917a0-113">Links are provided to information that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="917a0-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 o versione successiva (o equivalente, ad esempio OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="917a0-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="917a0-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="917a0-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="917a0-116">Un editor di testo o ambiente IDE Java</span><span class="sxs-lookup"><span data-stu-id="917a0-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="917a0-117">Se si creano i file Python in un client Windows, è necessario usare un editor che usa LF come terminazione di riga.</span><span class="sxs-lookup"><span data-stu-id="917a0-117">If you create the Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="917a0-118">Se non si è certi se l'editor usa LF o CRLF, vedere la sezione [Risoluzione dei problemi](#troubleshooting) , che include passaggi per la rimozione del carattere CR.</span><span class="sxs-lookup"><span data-stu-id="917a0-118">If you are not sure whether your editor uses LF or CRLF, see the [Troubleshooting](#troubleshooting) section for steps on removing the CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="917a0-119">Creare una UDF Java di esempio</span><span class="sxs-lookup"><span data-stu-id="917a0-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="917a0-120">Da una riga di comando seguire questa procedura per creare un nuovo progetto Maven.</span><span class="sxs-lookup"><span data-stu-id="917a0-120">From a command line, use the following to create a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="917a0-121">Se si utilizza PowerShell, è necessario racchiudere i parametri tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="917a0-121">If you are using PowerShell, you must put quotes around the parameters.</span></span> <span data-ttu-id="917a0-122">Ad esempio: `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="917a0-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="917a0-123">Questo comando crea una directory denominata **exampleudf**, che contiene un progetto Maven.</span><span class="sxs-lookup"><span data-stu-id="917a0-123">This command creates a directory named **exampleudf**, which contains the Maven project.</span></span>

2. <span data-ttu-id="917a0-124">Dopo aver creato il progetto, eliminare la directory **exampleudf/src/test** creata nell'ambito del progetto.</span><span class="sxs-lookup"><span data-stu-id="917a0-124">Once the project has been created, delete the **exampleudf/src/test** directory that was created as part of the project.</span></span>

3. <span data-ttu-id="917a0-125">Aprire **exampleudf/pom.xml** e sostituire la voce `<dependencies>` esistente con il seguente XML:</span><span class="sxs-lookup"><span data-stu-id="917a0-125">Open the **exampleudf/pom.xml**, and replace the existing `<dependencies>` entry with the following XML:</span></span>

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

    <span data-ttu-id="917a0-126">Queste voci specificano le versioni di Hadoop e Hive incluse con HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="917a0-126">These entries specify the version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="917a0-127">È possibile trovare informazioni sulle versioni di Hadoop e Hive fornite con HDInsight dal documento relativo al [controllo delle versioni dei componenti di HDInsight](hdinsight-component-versioning.md) .</span><span class="sxs-lookup"><span data-stu-id="917a0-127">You can find information on the versions of Hadoop and Hive provided with HDInsight from the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="917a0-128">Aggiungere una sezione `<build>` prima della riga `</project>` alla fine del file.</span><span class="sxs-lookup"><span data-stu-id="917a0-128">Add a `<build>` section before the `</project>` line at the end of the file.</span></span> <span data-ttu-id="917a0-129">Questa sezione deve contenere il seguente XML:</span><span class="sxs-lookup"><span data-stu-id="917a0-129">This section should contain the following XML:</span></span>

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

    <span data-ttu-id="917a0-130">Queste voci definiscono la modalità di realizzazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="917a0-130">These entries define how to build the project.</span></span> <span data-ttu-id="917a0-131">In particolare, la versione di Java usata dal progetto e il modo in cui creare un file uberjar per la distribuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="917a0-131">Specifically, the version of Java that the project uses and how to build an uberjar for deployment to the cluster.</span></span>

    <span data-ttu-id="917a0-132">Salvare il file dopo avere apportato le modifiche.</span><span class="sxs-lookup"><span data-stu-id="917a0-132">Save the file once the changes have been made.</span></span>

4. <span data-ttu-id="917a0-133">Rinominare **exampleudf/src/main/java/com/microsoft/examples/App.java** in **ExampleUDF.java** e aprire il file nell'editor.</span><span class="sxs-lookup"><span data-stu-id="917a0-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** to **ExampleUDF.java**, and then open the file in your editor.</span></span>

5. <span data-ttu-id="917a0-134">Sostituire i contenuti del file **ExampleUDF.java** con quanto segue, quindi salvare il file.</span><span class="sxs-lookup"><span data-stu-id="917a0-134">Replace the contents of the **ExampleUDF.java** file with the following, then save the file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of the UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of the input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If the value is null, return a null
            if(input == null)
                return null;
            // Lowercase the input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="917a0-135">Questo codice implementa una funzione definita dall'utente che accetta un valore stringa e restituisce una versione in lettere minuscole della stringa.</span><span class="sxs-lookup"><span data-stu-id="917a0-135">This code implements a UDF that accepts a string value, and returns a lowercase version of the string.</span></span>

## <a name="build-and-install-the-udf"></a><span data-ttu-id="917a0-136">Compilare e installare la UDF</span><span class="sxs-lookup"><span data-stu-id="917a0-136">Build and install the UDF</span></span>

1. <span data-ttu-id="917a0-137">Eseguire il comando seguente per compilare la UDF e inserirla nel pacchetto:</span><span class="sxs-lookup"><span data-stu-id="917a0-137">Use the following command to compile and package the UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="917a0-138">Questo comando compila e impacchetta la UDF nel file `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="917a0-138">This command builds and packages the UDF into the `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="917a0-139">Usare il comando `scp` per copiare il file nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="917a0-139">Use the `scp` command to copy the file to the HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="917a0-140">Sostituire `myuser` con l'account utente SSH del cluster.</span><span class="sxs-lookup"><span data-stu-id="917a0-140">Replace `myuser` with the SSH user account for your cluster.</span></span> <span data-ttu-id="917a0-141">Sostituire `mycluster` con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="917a0-141">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="917a0-142">Se l'account SSH è protetto da una password, viene richiesto di immetterla.</span><span class="sxs-lookup"><span data-stu-id="917a0-142">If you used a password to secure the SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="917a0-143">Se è stata usato un certificato, può essere necessario usare il parametro `-i` per specificare il file della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="917a0-143">If you used a certificate, you may need to use the `-i` parameter to specify the private key file.</span></span>

3. <span data-ttu-id="917a0-144">Connettersi al cluster tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="917a0-144">Connect to the cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="917a0-145">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="917a0-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="917a0-146">Dalla sessione SSH, copiare il file jar nell’archiviazione HDInsight.</span><span class="sxs-lookup"><span data-stu-id="917a0-146">From the SSH session, copy the jar file to HDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-the-udf-from-hive"></a><span data-ttu-id="917a0-147">Utilizzare la UDF da Hive</span><span class="sxs-lookup"><span data-stu-id="917a0-147">Use the UDF from Hive</span></span>

1. <span data-ttu-id="917a0-148">Per avviare il client Beeline, dalla sessione SSH usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="917a0-148">Use the following to start the Beeline client from the SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="917a0-149">Questo comando presuppone che sia stato utilizzato il valore predefinito di **admin** per l'account di accesso del cluster.</span><span class="sxs-lookup"><span data-stu-id="917a0-149">This command assumes that you used the default of **admin** for the login account for your cluster.</span></span>

2. <span data-ttu-id="917a0-150">Una volta arrivati al prompt `jdbc:hive2://localhost:10001/>` , immettere il comando seguente per aggiungere la UDF a Hive ed esporla come una funzione.</span><span class="sxs-lookup"><span data-stu-id="917a0-150">Once you arrive at the `jdbc:hive2://localhost:10001/>` prompt, enter the following to add the UDF to Hive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="917a0-151">Questo esempio assume che Archiviazione di Azure sia la risorsa di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="917a0-151">This example assumes that Azure Storage is default storage for the cluster.</span></span> <span data-ttu-id="917a0-152">Se il cluster usa invece Data Lake Store, modificare il valore `wasb:///` in `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="917a0-152">If your cluster uses Data Lake Store instead, change the `wasb:///` value to `adl:///`.</span></span>

3. <span data-ttu-id="917a0-153">Utilizzare la UDF per convertire i valori recuperati da una tabella in stringhe con lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="917a0-153">Use the UDF to convert values retrieved from a table to lower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="917a0-154">Questa query seleziona la piattaforma del dispositivo (Android, Windows, iOS e così via) dalla tabella, converte la stringa in lettere minuscole e la visualizza.</span><span class="sxs-lookup"><span data-stu-id="917a0-154">This query selects the device platform (Android, Windows, iOS, etc.) from the table, convert the string to lower case, and then display them.</span></span> <span data-ttu-id="917a0-155">L'output appare simile al seguente testo:</span><span class="sxs-lookup"><span data-stu-id="917a0-155">The output appears similar to the following text:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="917a0-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="917a0-156">Next steps</span></span>

<span data-ttu-id="917a0-157">Per apprendere altri modi di utilizzare Hive, vedere [Utilizzare Hive con HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="917a0-157">For other ways to work with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="917a0-158">Per ulteriori informazioni sulle UDF di Hive, vedere la sezione [Operatori e funzioni definite dall’utente di Hive](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) del wiki di Hive all’indirizzo apache.org.</span><span class="sxs-lookup"><span data-stu-id="917a0-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of the Hive wiki at apache.org.</span></span>
