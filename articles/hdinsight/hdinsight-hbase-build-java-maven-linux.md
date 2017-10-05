---
title: Client Java HBase - Azure HDInsight | Microsoft Docs
description: Informazioni su come usare Apache Maven per compilare un'applicazione Apache HBase basata su Java e poi distribuirla in HBase in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: 
ms.assetid: 1d1ed180-e0f4-4d1c-b5ea-72e0eda643bc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 03c88397e36c0fc7f19410e49f6b6f1a607659f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="97a39-103">Compilare applicazioni Java per Apache HBase</span><span class="sxs-lookup"><span data-stu-id="97a39-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="97a39-104">Informazioni su come creare e compilare un'applicazione [Apache HBase](http://hbase.apache.org/) in Java.</span><span class="sxs-lookup"><span data-stu-id="97a39-104">Learn how to create an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="97a39-105">Quindi usare l'applicazione con HBase in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97a39-105">Then use the application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="97a39-106">La procedura descritta in questo documento usa [Maven](http://maven.apache.org/) per creare e compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="97a39-106">The steps in this document use [Maven](http://maven.apache.org/) to create and build the project.</span></span> <span data-ttu-id="97a39-107">Maven è un progetto di gestione software e uno strumento di esplorazione che consente di compilare software, documentazione e report per i progetti Java.</span><span class="sxs-lookup"><span data-stu-id="97a39-107">Maven is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="97a39-108">La procedura descritta in questo documento è stata testata molto recentemente con HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="97a39-108">The steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97a39-109">I passaggi descritti in questo documento richiedono un cluster HDInsight che usa Linux.</span><span class="sxs-lookup"><span data-stu-id="97a39-109">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="97a39-110">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="97a39-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="97a39-111">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="97a39-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="97a39-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="97a39-112">Requirements</span></span>

* <span data-ttu-id="97a39-113">[Piattaforma Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="97a39-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97a39-114">HDInsight 3.5 e versioni successive richiedono Java 8.</span><span class="sxs-lookup"><span data-stu-id="97a39-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="97a39-115">Le versioni precedenti di HDInsight richiedono Java 7.</span><span class="sxs-lookup"><span data-stu-id="97a39-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="97a39-116">Maven</span><span class="sxs-lookup"><span data-stu-id="97a39-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="97a39-117">Un cluster Azure HDInsight basato su Linux con HBase</span><span class="sxs-lookup"><span data-stu-id="97a39-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="97a39-118">Le procedure descritte in questo documento sono state testate con le versioni del cluster HDInsight 3.4 e 3.5.</span><span class="sxs-lookup"><span data-stu-id="97a39-118">The steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="97a39-119">I valori predefiniti specificati negli esempi sono relativi a un cluster HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="97a39-119">The default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="97a39-120">Creare il progetto</span><span class="sxs-lookup"><span data-stu-id="97a39-120">Create the project</span></span>

1. <span data-ttu-id="97a39-121">Dalla riga di comando nell'ambiente di sviluppo, passare alla directory in cui si vuole creare il progetto, ad esempio `cd code\hbase`.</span><span class="sxs-lookup"><span data-stu-id="97a39-121">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="97a39-122">Usare il comando **mvn** , che viene installato con Maven, per generare lo scaffolding per il progetto.</span><span class="sxs-lookup"><span data-stu-id="97a39-122">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="97a39-123">Se si usa PowerShell, è necessario racchiudere i parametri `-D` tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="97a39-123">If you are using PowerShell, you must enclose the `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="97a39-124">Questo comando crea una directory con lo stesso nome del parametro **artifactID** (in questo esempio **hbaseapp**). La directory contiene gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="97a39-124">This command creates a directory with the same name as the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="97a39-125">**pom.xml**: il modello a oggetti dei progetti ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html), Project Object Model) contiene le informazioni e i dettagli di configurazione usati per compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="97a39-125">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span></span>
   * <span data-ttu-id="97a39-126">**src**: la directory che contiene la directory **main/java/com/microsoft/examples**, in cui viene creata l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="97a39-126">**src**: The directory that contains the **main/java/com/microsoft/examples** directory, where you author the application.</span></span>

3. <span data-ttu-id="97a39-127">Eliminare il file `src/test/java/com/microsoft/examples/apptest.java`.</span><span class="sxs-lookup"><span data-stu-id="97a39-127">Delete the `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="97a39-128">Non viene usato in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="97a39-128">It is not be used in this example.</span></span>

## <a name="update-the-project-object-model"></a><span data-ttu-id="97a39-129">Aggiornare il modello a oggetti dei progetti</span><span class="sxs-lookup"><span data-stu-id="97a39-129">Update the Project Object Model</span></span>

1. <span data-ttu-id="97a39-130">Modificare il file `pom.xml` e aggiungere il codice seguente nella sezione `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="97a39-130">Edit the `pom.xml` file and add the following code inside the `<dependencies>` section:</span></span>

   ```xml
    <dependency>
        <groupId>org.apache.hbase</groupId>
        <artifactId>hbase-client</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>org.apache.phoenix</groupId>
        <artifactId>phoenix-core</artifactId>
        <version>4.4.0-HBase-1.1</version>
    </dependency>
   ```

    <span data-ttu-id="97a39-131">Questa sezione indica che il progetto richiede i componenti **hbase-client** e **phoenix-core**.</span><span class="sxs-lookup"><span data-stu-id="97a39-131">This section indicates that the project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="97a39-132">In fase di compilazione, queste dipendenze vengono scaricata dal repository Maven predefinito.</span><span class="sxs-lookup"><span data-stu-id="97a39-132">At compile time, these dependencies are downloaded from the default Maven repository.</span></span> <span data-ttu-id="97a39-133">È possibile usare la [ricerca nel repository centrale Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) per ottenere altre informazioni su questa dipendenza.</span><span class="sxs-lookup"><span data-stu-id="97a39-133">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="97a39-134">Il numero di versione del client HBase deve corrispondere alla versione di HBase fornita con il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97a39-134">The version number of the hbase-client must match the version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="97a39-135">Usare la tabella seguente per trovare il numero di versione corretto.</span><span class="sxs-lookup"><span data-stu-id="97a39-135">Use the following table to find the correct version number.</span></span>

   | <span data-ttu-id="97a39-136">Versione del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="97a39-136">HDInsight cluster version</span></span> | <span data-ttu-id="97a39-137">Versione di HBase da usare</span><span class="sxs-lookup"><span data-stu-id="97a39-137">HBase version to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="97a39-138">3.2</span><span class="sxs-lookup"><span data-stu-id="97a39-138">3.2</span></span> |<span data-ttu-id="97a39-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="97a39-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="97a39-140">3.3, 3.4, 3.5 e 3.6</span><span class="sxs-lookup"><span data-stu-id="97a39-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="97a39-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="97a39-141">1.1.2</span></span> |

    <span data-ttu-id="97a39-142">Per altre informazioni sulle versioni e sui componenti di HDInsight, vedere [Quali sono i diversi componenti di Hadoop disponibili in HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="97a39-142">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="97a39-143">Aggiungere il codice seguente al file **pom.xml**.</span><span class="sxs-lookup"><span data-stu-id="97a39-143">Add the following code to the **pom.xml** file.</span></span> <span data-ttu-id="97a39-144">Nel file, il testo deve essere incluso tra i tag `<project>...</project>`, ad esempio tra `</dependencies>` e `</project>`.</span><span class="sxs-lookup"><span data-stu-id="97a39-144">This text must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <sourceDirectory>src</sourceDirectory>
        <resources>
        <resource>
            <directory>${basedir}/conf</directory>
            <filtering>false</filtering>
            <includes>
            <include>hbase-site.xml</include>
            </includes>
        </resource>
        </resources>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.3</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
            </plugin>
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
        </plugins>
    </build>
   ```

    <span data-ttu-id="97a39-145">Questa sezione configura una risorsa (`conf/hbase-site.xml`) che contiene informazioni di configurazione per HBase.</span><span class="sxs-lookup"><span data-stu-id="97a39-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="97a39-146">È anche possibile impostare i valori di configurazione tramite codice.</span><span class="sxs-lookup"><span data-stu-id="97a39-146">You can also set configuration values via code.</span></span> <span data-ttu-id="97a39-147">Vedere i commenti nell'esempio `CreateTable`.</span><span class="sxs-lookup"><span data-stu-id="97a39-147">See the comments in the `CreateTable` example.</span></span>

    <span data-ttu-id="97a39-148">Questa sezione configura anche i [plug-in compiler per Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) e i [plug-in shade per Maven](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="97a39-148">This section also configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="97a39-149">Il plug-in compiler viene usato per compilare la topologia,</span><span class="sxs-lookup"><span data-stu-id="97a39-149">The compiler plug-in is used to compile the topology.</span></span> <span data-ttu-id="97a39-150">mentre il plug-in shade viene usato per impedire la duplicazione della licenza nel pacchetto JAR compilato da Maven.</span><span class="sxs-lookup"><span data-stu-id="97a39-150">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span></span> <span data-ttu-id="97a39-151">Questo plug-in viene usato per evitare che i file di licenza duplicati causino un errore in fase di esecuzione sul cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97a39-151">This plugin is used to prevent a "duplicate license files" error at run time on the HDInsight cluster.</span></span> <span data-ttu-id="97a39-152">L'uso di maven-shade-plugin con l'implementazione di `ApacheLicenseResourceTransformer` previene il verificarsi di questo errore.</span><span class="sxs-lookup"><span data-stu-id="97a39-152">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents the error.</span></span>

    <span data-ttu-id="97a39-153">Il plug-in maven-shade-plugin produce anche un file uberjar, che contiene tutte le dipendenze richieste dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="97a39-153">The maven-shade-plugin also produces an uber jar that contains all the dependencies required by the application.</span></span>

4. <span data-ttu-id="97a39-154">Salvare il file.`pom.xml`</span><span class="sxs-lookup"><span data-stu-id="97a39-154">Save the `pom.xml` file.</span></span>

5. <span data-ttu-id="97a39-155">Creare una directory denominata `conf` nella directory `hbaseapp`.</span><span class="sxs-lookup"><span data-stu-id="97a39-155">Create a directory named `conf` in the `hbaseapp` directory.</span></span> <span data-ttu-id="97a39-156">La directory viene usata per contenere le informazioni di configurazione per la connessione a HBase.</span><span class="sxs-lookup"><span data-stu-id="97a39-156">This directory is used to hold configuration information for connecting to HBase.</span></span>

6. <span data-ttu-id="97a39-157">Usare il comando seguente per copiare la configurazione di HBase dal cluster HBase nella directory `conf`.</span><span class="sxs-lookup"><span data-stu-id="97a39-157">Use the following command to copy the HBase configuration from the HBase cluster to the `conf` directory.</span></span> <span data-ttu-id="97a39-158">Sostituire `USERNAME` con il nome di accesso a SSH.</span><span class="sxs-lookup"><span data-stu-id="97a39-158">Replace `USERNAME` with the name of your SSH login.</span></span> <span data-ttu-id="97a39-159">Sostituire `CLUSTERNAME` con il nome del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="97a39-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="97a39-160">Per altre informazioni sull'uso di `ssh` e `scp`, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="97a39-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-the-application"></a><span data-ttu-id="97a39-161">Creazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="97a39-161">Create the application</span></span>

1. <span data-ttu-id="97a39-162">Andare alla directory `hbaseapp/src/main/java/com/microsoft/examples` e rinominare il file app.java in `CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="97a39-162">Go to the `hbaseapp/src/main/java/com/microsoft/examples` directory and rename the app.java file to `CreateTable.java`.</span></span>

2. <span data-ttu-id="97a39-163">Aprire il file `CreateTable.java` e sostituire il contenuto esistente con il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="97a39-163">Open the `CreateTable.java` file and replace the existing contents with the following text:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.TableName;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.util.Bytes;

    public class CreateTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Example of setting zookeeper values for HDInsight
        // in code instead of an hbase-site.xml file
        //
        // config.set("hbase.zookeeper.quorum",
        //            "zookeepernode0,zookeepernode1,zookeepernode2");
        //config.set("hbase.zookeeper.property.clientPort", "2181");
        //config.set("hbase.cluster.distributed", "true");
        //
        //NOTE: Actual zookeeper host names can be found using Ambari:
        //curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts"

        //Linux-based HDInsight clusters use /hbase-unsecure as the znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using the config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create the table...
        HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
        // ... with two column families
        tableDescriptor.addFamily(new HColumnDescriptor("name"));
        tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
        admin.createTable(tableDescriptor);

        // define some people
        String[][] people = {
            { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
            { "2", "Franklin", "Holtz", "franklin@contoso.com" },
            { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
            { "4", "Rae", "Schroeder", "rae@contoso.com" },
            { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
            { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

        HTable table = new HTable(config, "people");

        // Add each person to the table
        //   Use the `name` column family for the name
        //   Use the `contactinfo` column family for the email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close the table
        table.flushCommits();
        table.close();
        }
    }
   ```

    <span data-ttu-id="97a39-164">Si tratta della classe **CreateTable**, che consente di creare una tabella denominata **people** e di popolarla con alcuni utenti predefiniti.</span><span class="sxs-lookup"><span data-stu-id="97a39-164">This code is the **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="97a39-165">Salvare il file.`CreateTable.java`</span><span class="sxs-lookup"><span data-stu-id="97a39-165">Save the `CreateTable.java` file.</span></span>

4. <span data-ttu-id="97a39-166">Creare un nuovo file denominato `SearchByEmail.java` nella directory `hbaseapp/src/main/java/com/microsoft/examples`.</span><span class="sxs-lookup"><span data-stu-id="97a39-166">In the `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="97a39-167">Usare il testo seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="97a39-167">Use the following text as the contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.filter.RegexStringComparator;
    import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
    import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
    import org.apache.hadoop.hbase.util.Bytes;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class SearchByEmail {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Use GenericOptionsParser to get only the parameters to the class
        // and not all the parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open the table
        HTable table = new HTable(config, "people");

        // Define the family and qualifiers to be used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach the regex filter to a filter
        //   for the email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set the filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get the results
        ResultScanner results = table.getScanner(scan);
        // Iterate over results and print  values
        for (Result result : results ) {
            String id = new String(result.getRow());
            byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
            String firstName = new String(firstNameObj);
            byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
            String lastName = new String(lastNameObj);
            System.out.println(firstName + " " + lastName + " - ID: " + id);
            byte[] emailObj = result.getValue(contactFamily, emailQualifier);
            String email = new String(emailObj);
            System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
        }
        results.close();
        table.close();
        }
    }
   ```

    <span data-ttu-id="97a39-168">È possibile usare la classe **SearchByEmail** per eseguire query sulle righe in base all'indirizzo e-mail.</span><span class="sxs-lookup"><span data-stu-id="97a39-168">The **SearchByEmail** class can be used to query for rows by email address.</span></span> <span data-ttu-id="97a39-169">Poiché usa un filtro di espressione regolare, è possibile fornire una stringa o un'espressione regolare quando si usa la classe.</span><span class="sxs-lookup"><span data-stu-id="97a39-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span></span>

5. <span data-ttu-id="97a39-170">Salvare il file.`SearchByEmail.java`</span><span class="sxs-lookup"><span data-stu-id="97a39-170">Save the `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="97a39-171">Creare un nuovo file denominato `DeleteTable.java` nella directory `hbaseapp/src/main/hava/com/microsoft/examples`.</span><span class="sxs-lookup"><span data-stu-id="97a39-171">In the `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="97a39-172">Usare il testo seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="97a39-172">Use the following text as the contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using the config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete the table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    <span data-ttu-id="97a39-173">Questa classe pulisce le tabelle HBase create in questo esempio disabilitando ed eliminando la tabella creata dalla classe `CreateTable`.</span><span class="sxs-lookup"><span data-stu-id="97a39-173">This class cleans up the HBase tables created in this example by disabling and dropping the table created by the `CreateTable` class.</span></span>

7. <span data-ttu-id="97a39-174">Salvare il file.`DeleteTable.java`</span><span class="sxs-lookup"><span data-stu-id="97a39-174">Save the `DeleteTable.java` file.</span></span>

## <a name="build-and-package-the-application"></a><span data-ttu-id="97a39-175">Compilare e creare il pacchetto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="97a39-175">Build and package the application</span></span>

1. <span data-ttu-id="97a39-176">Dalla directory `hbaseapp` usare il comando seguente per compilare un file JAR contenente l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="97a39-176">From the `hbaseapp` directory, use the following command to build a JAR file that contains the application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="97a39-177">Questo comando compila e crea il pacchetto dell'applicazione in un file con estensione .jar.</span><span class="sxs-lookup"><span data-stu-id="97a39-177">This command builds and packages the application into a .jar file.</span></span>

2. <span data-ttu-id="97a39-178">Al completamento del comando, la directory `hbaseapp/target` contiene un file denominato `hbaseapp-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="97a39-178">When the command completes, the `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="97a39-179">Il file `hbaseapp-1.0-SNAPSHOT.jar` è un file uber jar.</span><span class="sxs-lookup"><span data-stu-id="97a39-179">The `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="97a39-180">Questo file contiene tutte le dipendenze richieste per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="97a39-180">It contains all the dependencies required to run the application.</span></span>


## <a name="upload-the-jar-and-run-jobs-ssh"></a><span data-ttu-id="97a39-181">Caricare il file JAR ed eseguire i processi (SSH)</span><span class="sxs-lookup"><span data-stu-id="97a39-181">Upload the JAR and run jobs (SSH)</span></span>

<span data-ttu-id="97a39-182">La procedura seguente usa `scp` per copiare il file JAR nel nodo head primario di HBase nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97a39-182">The following steps use `scp` to copy the JAR to the primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="97a39-183">Il comando `ssh` viene quindi usato per connettersi al cluster ed eseguire l'esempio direttamente nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="97a39-183">The `ssh` command is then used to connect to the cluster and run the example directly on the head node.</span></span>

1. <span data-ttu-id="97a39-184">Per caricare il file jar nel cluster, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="97a39-184">To upload the jar to the cluster, use the following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="97a39-185">Sostituire `USERNAME` con il nome di accesso a SSH.</span><span class="sxs-lookup"><span data-stu-id="97a39-185">Replace `USERNAME` with the name of your SSH login.</span></span> <span data-ttu-id="97a39-186">Sostituire `CLUSTERNAME` con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97a39-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="97a39-187">Per collegarsi al cluster HBase, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="97a39-187">To connect to the HBase cluster, use the following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="97a39-188">Sostituire `USERNAME` con il nome di accesso a SSH.</span><span class="sxs-lookup"><span data-stu-id="97a39-188">Replace `USERNAME` the name of your SSH login.</span></span> <span data-ttu-id="97a39-189">Sostituire `CLUSTERNAME` con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97a39-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="97a39-190">Per creare una nuova tabella HBase tramite l'applicazione Java, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="97a39-190">To create an HBase table using the Java application, use the following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="97a39-191">Il comando crea una nuova tabella HBase denominata **people** e la popola con i dati.</span><span class="sxs-lookup"><span data-stu-id="97a39-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="97a39-192">Per la ricerca degli indirizzi di posta elettronica memorizzati nella tabella, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="97a39-192">To search for email addresses stored in the table, use the following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="97a39-193">Si ottengono i risultati seguenti:</span><span class="sxs-lookup"><span data-stu-id="97a39-193">You receive the following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="97a39-194">Per eliminare la tabella, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="97a39-194">To delete the table, use the following command:</span></span>

    

## <a name="upload-the-jar-and-run-jobs-powershell"></a><span data-ttu-id="97a39-195">Caricare il file JAR ed eseguire i processi (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="97a39-195">Upload the JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="97a39-196">La procedura seguente usa Azure PowerShell per caricare il file JAR nella risorsa di archiviazione predefinita per il cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="97a39-196">The following steps use Azure PowerShell to upload the JAR to the default storage for your HBase cluster.</span></span> <span data-ttu-id="97a39-197">I cmdlet di HDInsight vengono quindi usati per eseguire gli esempi in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="97a39-197">HDInsight cmdlets are then used to run the examples remotely.</span></span>

1. <span data-ttu-id="97a39-198">Dopo aver installato e configurato Azure PowerShell, creare un file denominato `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="97a39-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="97a39-199">Usare il testo seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="97a39-199">Use the following text as the contents of this file:</span></span>

   ```powershell
    <#
    .SYNOPSIS
    Copies a file to the primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory to the blob container for
    the HDInsight cluster.
    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.CreateTable"
    -clusterName "MyHDInsightCluster"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "contoso.com"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "^r" -showErr
    #>

    function Start-HBaseExample {
    [CmdletBinding(SupportsShouldProcess = $true)]
    param(
    #The class to run
    [Parameter(Mandatory = $true)]
    [String]$className,

    #The name of the HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want to see stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is the Azure module installed?
    FindAzure

    # Get the login for the HDInsight cluster
    $creds=Get-Credential -Message "Enter the login for the cluster" -UserName "admin"

    # The JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # The job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get the job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds
    if($showErr)
    {
    Write-Host "STDERR"
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds `
                -DisplayOutputType StandardError
    }
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file to the primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory to the blob container for
    the HDInsight cluster.
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    -Container "MyContainer"
    #>

    function Add-HDInsightFile {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
            #The path to the local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #The destination path and file name, relative to the root of the container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #The name of the HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is the Azure module installed?
        FindAzure

        # Get authentication for the cluster
        $creds=Get-Credential

        # Does the local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get the primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file to storage, overwriting existing files if -force was used.
        Set-AzureStorageBlobContent -File $localPath `
            -Blob $destinationPath `
            -force:$force `
            -Container $storage.container `
            -Context $storage.context
    }

    function FindAzure {
        # Is there an active Azure subscription?
        $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
        if(-not($sub))
        {
            throw "No active Azure subscription found! If you have a subscription, use the Login-AzureRmAccount cmdlet to login to your subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does the cluster exist?
        if (!$hdi)
        {
            throw "HDInsight cluster '$clusterName' does not exist."
        }
        # Create a return object for context & container
        $return = @{}
        $storageAccounts = @{}

        # Get storage information
        $resourceGroup = $hdi.ResourceGroup
        $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
        $container=$hdi.DefaultStorageContainer
        $storageAccountKey=(Get-AzureRmStorageAccountKey `
            -Name $storageAccountName `
        -ResourceGroupName $resourceGroup)[0].Value
        # Get the resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get the storage context, as we can't depend
        # on using the default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get the container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts to support finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export the verb-phrase things
    export-modulemember *-*
   ```

    <span data-ttu-id="97a39-200">Questo file contiene due moduli:</span><span class="sxs-lookup"><span data-stu-id="97a39-200">This file contains two modules:</span></span>

   * <span data-ttu-id="97a39-201">**Add-HDInsightFile**: viene usato per caricare file nel cluster</span><span class="sxs-lookup"><span data-stu-id="97a39-201">**Add-HDInsightFile** - used to upload files to the cluster</span></span>
   * <span data-ttu-id="97a39-202">**Start-HBaseExample**: usato per eseguire le classi create prima</span><span class="sxs-lookup"><span data-stu-id="97a39-202">**Start-HBaseExample** - used to run the classes created earlier</span></span>

2. <span data-ttu-id="97a39-203">Salvare il file.`hbase-runner.psm1`</span><span class="sxs-lookup"><span data-stu-id="97a39-203">Save the `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="97a39-204">Aprire una nuova finestra di Azure PowerShell, passare alla directory `hbaseapp` e quindi eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="97a39-204">Open a new Azure PowerShell window, change directories to the `hbaseapp` directory, and then run the following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="97a39-205">Cambiare il percorso con la posizione del file `hbase-runner.psm1` creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="97a39-205">Change the path to the location of the `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="97a39-206">Questo comando registra il modulo in Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97a39-206">This command registers the module with Azure PowerShell.</span></span>

4. <span data-ttu-id="97a39-207">Usare il comando seguente per caricare il `hbaseapp-1.0-SNAPSHOT.jar` nel cluster.</span><span class="sxs-lookup"><span data-stu-id="97a39-207">Use the following command to upload the `hbaseapp-1.0-SNAPSHOT.jar` to your cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="97a39-208">Sostituire `hdinsightclustername` con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="97a39-208">Replace `hdinsightclustername` with the name of your cluster.</span></span> <span data-ttu-id="97a39-209">Il comando Carica il `hbaseapp-1.0-SNAPSHOT.jar` nel percorso `example/jars` nell'archivio primario per il cluster.</span><span class="sxs-lookup"><span data-stu-id="97a39-209">The command uploads the `hbaseapp-1.0-SNAPSHOT.jar` to the `example/jars` location in the primary storage for your cluster.</span></span>

5. <span data-ttu-id="97a39-210">Per creare una tabella mediante `hbaseapp`, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="97a39-210">To create a table using the `hbaseapp`, use the following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="97a39-211">Sostituire `hdinsightclustername` con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="97a39-211">Replace `hdinsightclustername` with the name of your cluster.</span></span>

    <span data-ttu-id="97a39-212">Questo comando consente di creare una nuova tabella denominata **people** in HBase nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97a39-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="97a39-213">Non viene mostrato alcun output nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="97a39-213">This command does not show any output in the console window.</span></span>

6. <span data-ttu-id="97a39-214">Per cercare le voci nella tabella, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="97a39-214">To search for entries in the table, use the following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="97a39-215">Sostituire `hdinsightclustername` con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="97a39-215">Replace `hdinsightclustername` with the name of your cluster.</span></span>

    <span data-ttu-id="97a39-216">Questo comando usa la classe `SearchByEmail` per cercare le righe in cui la famiglia della colonna `contactinformation` e la colonna `email` contengono la stringa `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="97a39-216">This command uses the `SearchByEmail` class to search for any rows where the `contactinformation` column family and the `email` column, contains the string `contoso.com`.</span></span> <span data-ttu-id="97a39-217">Dovrebbero essere visualizzati i risultati seguenti:</span><span class="sxs-lookup"><span data-stu-id="97a39-217">You should receive the following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="97a39-218">L'uso di **fabrikam.com** per il valore `-emailRegex` restituirà gli utenti il cui campo email contiene **fabrikam.com**.</span><span class="sxs-lookup"><span data-stu-id="97a39-218">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span></span> <span data-ttu-id="97a39-219">È anche possibile usare espressioni regolari come termini di ricerca.</span><span class="sxs-lookup"><span data-stu-id="97a39-219">You can also use regular expressions as the search term.</span></span> <span data-ttu-id="97a39-220">Ad esempio, **^ r** restituisce gli indirizzi di posta elettronica che iniziano con la lettera "r".</span><span class="sxs-lookup"><span data-stu-id="97a39-220">For example, **^r** returns email addresses that begin with the letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="97a39-221">Nessun risultato o risultati imprevisti quando si usa Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="97a39-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="97a39-222">Usare il parametro `-showErr` per visualizzare l'errore standard (STDERR) prodotto durante l'esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="97a39-222">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span></span>

## <a name="delete-the-table"></a><span data-ttu-id="97a39-223">Eliminare la tabella</span><span class="sxs-lookup"><span data-stu-id="97a39-223">Delete the table</span></span>

<span data-ttu-id="97a39-224">Dopo aver completato l'esempio, usare il comando seguente per eliminare la tabella **people** usata nell'esempio:</span><span class="sxs-lookup"><span data-stu-id="97a39-224">When you are done with the example, use the following to delete the **people** table used in this example:</span></span>

<span data-ttu-id="97a39-225">__Da una sessione `ssh`__:</span><span class="sxs-lookup"><span data-stu-id="97a39-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="97a39-226">__Da Azure PowerShell__:</span><span class="sxs-lookup"><span data-stu-id="97a39-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="97a39-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="97a39-227">Next steps</span></span>

[<span data-ttu-id="97a39-228">Informazioni su come usare SQuirreL SQL con HBase</span><span class="sxs-lookup"><span data-stu-id="97a39-228">Learn how to use SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
