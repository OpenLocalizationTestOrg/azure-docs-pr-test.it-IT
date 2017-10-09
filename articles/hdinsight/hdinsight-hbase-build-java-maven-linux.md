---
title: client di HBase aaaJava - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse applicazione di HBase Apache Apache Maven toobuild basato su Java, quindi distribuirlo tooHBase in Azure HDInsight.
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
ms.openlocfilehash: 41ef92b2900280dd59089c4fa40686c44133b337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="01940-103">Compilare applicazioni Java per Apache HBase</span><span class="sxs-lookup"><span data-stu-id="01940-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="01940-104">Informazioni su come toocreate un [HBase Apache](http://hbase.apache.org/) applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="01940-104">Learn how toocreate an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="01940-105">Utilizzare quindi l'applicazione hello con HBase in HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="01940-105">Then use hello application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="01940-106">i passaggi di questo documento viene utilizzato da Hello [Maven](http://maven.apache.org/) toocreate e compilazione progetto hello.</span><span class="sxs-lookup"><span data-stu-id="01940-106">hello steps in this document use [Maven](http://maven.apache.org/) toocreate and build hello project.</span></span> <span data-ttu-id="01940-107">Maven è uno strumento di comprensione che consente di toobuild software, documentazione e report per i progetti di Java e la gestione dei progetti software.</span><span class="sxs-lookup"><span data-stu-id="01940-107">Maven is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="01940-108">Hello passaggi descritti in questo documento più recente testati con 3.6 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="01940-108">hello steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01940-109">passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux.</span><span class="sxs-lookup"><span data-stu-id="01940-109">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="01940-110">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="01940-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="01940-111">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="01940-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="01940-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="01940-112">Requirements</span></span>

* <span data-ttu-id="01940-113">[Piattaforma Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="01940-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="01940-114">HDInsight 3.5 e versioni successive richiedono Java 8.</span><span class="sxs-lookup"><span data-stu-id="01940-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="01940-115">Le versioni precedenti di HDInsight richiedono Java 7.</span><span class="sxs-lookup"><span data-stu-id="01940-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="01940-116">Maven</span><span class="sxs-lookup"><span data-stu-id="01940-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="01940-117">Un cluster Azure HDInsight basato su Linux con HBase</span><span class="sxs-lookup"><span data-stu-id="01940-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="01940-118">passaggi di Hello in questo documento sono stati testati con le versioni cluster HDInsight 3.4 e 3.5.</span><span class="sxs-lookup"><span data-stu-id="01940-118">hello steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="01940-119">i valori predefiniti di Hello forniti negli esempi sono per un cluster HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="01940-119">hello default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="01940-120">Creare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="01940-120">Create hello project</span></span>

1. <span data-ttu-id="01940-121">Dalla riga di comando hello nell'ambiente di sviluppo, modificare il percorso di toohello directory in cui si desidera progetto hello toocreate, ad esempio, `cd code\hbase`.</span><span class="sxs-lookup"><span data-stu-id="01940-121">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="01940-122">Hello utilizzare **mvn** comando, che viene installato con Maven, hello toogenerate lo scaffolding per progetto hello.</span><span class="sxs-lookup"><span data-stu-id="01940-122">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="01940-123">Se si usa PowerShell, è necessario racchiudere hello `-D` parametri racchiuso tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="01940-123">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="01940-124">Questo comando crea una directory con stesso nome come hello hello **ID** parametro (**hbaseapp** in questo esempio.) Questa directory contiene hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="01940-124">This command creates a directory with hello same name as hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="01940-125">**POM.XML**: hello modello oggetto di progetto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contiene informazioni e la configurazione progetto hello toobuild di dettagli utilizzati.</span><span class="sxs-lookup"><span data-stu-id="01940-125">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="01940-126">**src**: directory hello contenente hello **main/java/com/microsoft/esempi** directory, in cui si crea un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="01940-126">**src**: hello directory that contains hello **main/java/com/microsoft/examples** directory, where you author hello application.</span></span>

3. <span data-ttu-id="01940-127">Eliminare hello `src/test/java/com/microsoft/examples/apptest.java` file.</span><span class="sxs-lookup"><span data-stu-id="01940-127">Delete hello `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="01940-128">Non viene usato in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="01940-128">It is not be used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="01940-129">Aggiornare hello progetto modello a oggetti</span><span class="sxs-lookup"><span data-stu-id="01940-129">Update hello Project Object Model</span></span>

1. <span data-ttu-id="01940-130">Modifica hello `pom.xml` file e aggiungere hello seguente codice all'interno di hello `<dependencies>` sezione:</span><span class="sxs-lookup"><span data-stu-id="01940-130">Edit hello `pom.xml` file and add hello following code inside hello `<dependencies>` section:</span></span>

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

    <span data-ttu-id="01940-131">In questa sezione indica che il progetto hello deve **hbase client** e **phoenix core** componenti.</span><span class="sxs-lookup"><span data-stu-id="01940-131">This section indicates that hello project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="01940-132">In fase di compilazione, queste dipendenze vengono scaricate dal repository di Maven hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="01940-132">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="01940-133">È possibile utilizzare hello [ricerca Repository centrale Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn informazioni su questa dipendenza.</span><span class="sxs-lookup"><span data-stu-id="01940-133">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="01940-134">numero di versione di Hello del client di hbase hello deve corrispondere una versione di hello di HBase che viene fornito con il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="01940-134">hello version number of hello hbase-client must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="01940-135">Utilizzare hello seguente numero di versione corretto hello toofind tabella.</span><span class="sxs-lookup"><span data-stu-id="01940-135">Use hello following table toofind hello correct version number.</span></span>

   | <span data-ttu-id="01940-136">Versione del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="01940-136">HDInsight cluster version</span></span> | <span data-ttu-id="01940-137">Toouse versione HBase</span><span class="sxs-lookup"><span data-stu-id="01940-137">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="01940-138">3.2</span><span class="sxs-lookup"><span data-stu-id="01940-138">3.2</span></span> |<span data-ttu-id="01940-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="01940-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="01940-140">3.3, 3.4, 3.5 e 3.6</span><span class="sxs-lookup"><span data-stu-id="01940-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="01940-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="01940-141">1.1.2</span></span> |

    <span data-ttu-id="01940-142">Per ulteriori informazioni sulle versioni di HDInsight e i componenti, vedere [quali sono hello Hadoop componenti diversi disponibili con HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="01940-142">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="01940-143">Aggiungere i seguenti toohello codice hello **pom.xml** file.</span><span class="sxs-lookup"><span data-stu-id="01940-143">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="01940-144">Questo testo deve trovarsi all'interno di hello `<project>...</project>` tag hello file, ad esempio tra `</dependencies>` e `</project>`.</span><span class="sxs-lookup"><span data-stu-id="01940-144">This text must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="01940-145">Questa sezione configura una risorsa (`conf/hbase-site.xml`) che contiene informazioni di configurazione per HBase.</span><span class="sxs-lookup"><span data-stu-id="01940-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="01940-146">È anche possibile impostare i valori di configurazione tramite codice.</span><span class="sxs-lookup"><span data-stu-id="01940-146">You can also set configuration values via code.</span></span> <span data-ttu-id="01940-147">Vedere i commenti di hello in hello `CreateTable` esempio.</span><span class="sxs-lookup"><span data-stu-id="01940-147">See hello comments in hello `CreateTable` example.</span></span>

    <span data-ttu-id="01940-148">In questa sezione Configura inoltre hello [plug-in compilatore Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) e [plug-in Maven sfumatura](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="01940-148">This section also configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="01940-149">compilatore Hello plug-in è usato toocompile hello topologia.</span><span class="sxs-lookup"><span data-stu-id="01940-149">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="01940-150">sfumatura Hello plug-in è la duplicazione di licenza tooprevent utilizzati nel pacchetto JAR hello Maven compilata.</span><span class="sxs-lookup"><span data-stu-id="01940-150">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="01940-151">Questo plug-in è tooprevent usato un errore di "duplicato. i file di licenza" in fase di esecuzione nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="01940-151">This plugin is used tooprevent a "duplicate license files" error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="01940-152">Utilizzo di plug-in maven sfumatura con hello `ApacheLicenseResourceTransformer` errore hello impedisce l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="01940-152">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents hello error.</span></span>

    <span data-ttu-id="01940-153">Hello maven-sfumatura-plug-in anche produce un file jar uber che contiene tutte le dipendenze di hello richieste da un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="01940-153">hello maven-shade-plugin also produces an uber jar that contains all hello dependencies required by hello application.</span></span>

4. <span data-ttu-id="01940-154">Salvare hello `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="01940-154">Save hello `pom.xml` file.</span></span>

5. <span data-ttu-id="01940-155">Creare una directory denominata `conf` in hello `hbaseapp` directory.</span><span class="sxs-lookup"><span data-stu-id="01940-155">Create a directory named `conf` in hello `hbaseapp` directory.</span></span> <span data-ttu-id="01940-156">Questa directory contiene informazioni di configurazione toohold utilizzato per la connessione tooHBase.</span><span class="sxs-lookup"><span data-stu-id="01940-156">This directory is used toohold configuration information for connecting tooHBase.</span></span>

6. <span data-ttu-id="01940-157">Comando che segue hello di utilizzare la configurazione di HBase di hello toocopy da toohello cluster HBase di hello `conf` directory.</span><span class="sxs-lookup"><span data-stu-id="01940-157">Use hello following command toocopy hello HBase configuration from hello HBase cluster toohello `conf` directory.</span></span> <span data-ttu-id="01940-158">Sostituire `USERNAME` con nome hello dell'accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="01940-158">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="01940-159">Sostituire `CLUSTERNAME` con il nome del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="01940-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="01940-160">Per altre informazioni sull'uso di `ssh` e `scp`, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="01940-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="01940-161">Creare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="01940-161">Create hello application</span></span>

1. <span data-ttu-id="01940-162">Passare toohello `hbaseapp/src/main/java/com/microsoft/examples` directory e rinominare hello app.java file troppo`CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="01940-162">Go toohello `hbaseapp/src/main/java/com/microsoft/examples` directory and rename hello app.java file too`CreateTable.java`.</span></span>

2. <span data-ttu-id="01940-163">Aprire hello `CreateTable.java` file e sostituire contenuto esistente hello con hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="01940-163">Open hello `CreateTable.java` file and replace hello existing contents with hello following text:</span></span>

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

        //Linux-based HDInsight clusters use /hbase-unsecure as hello znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create hello table...
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

        // Add each person toohello table
        //   Use hello `name` column family for hello name
        //   Use hello `contactinfo` column family for hello email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close hello table
        table.flushCommits();
        table.close();
        }
    }
   ```

    <span data-ttu-id="01940-164">Questo codice è hello **CreateTable** (classe), che consente di creare una tabella denominata **persone** e viene popolato con alcuni utenti predefiniti.</span><span class="sxs-lookup"><span data-stu-id="01940-164">This code is hello **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="01940-165">Salvare hello `CreateTable.java` file.</span><span class="sxs-lookup"><span data-stu-id="01940-165">Save hello `CreateTable.java` file.</span></span>

4. <span data-ttu-id="01940-166">In hello `hbaseapp/src/main/java/com/microsoft/examples` directory, creare un file denominato `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="01940-166">In hello `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="01940-167">Utilizzare hello segue testo come contenuto di hello di questo file:</span><span class="sxs-lookup"><span data-stu-id="01940-167">Use hello following text as hello contents of this file:</span></span>

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

        // Use GenericOptionsParser tooget only hello parameters toohello class
        // and not all hello parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open hello table
        HTable table = new HTable(config, "people");

        // Define hello family and qualifiers toobe used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach hello regex filter tooa filter
        //   for hello email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set hello filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get hello results
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

    <span data-ttu-id="01940-168">Hello **SearchByEmail** classe può essere utilizzato tooquery per le righe dall'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="01940-168">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="01940-169">Poiché utilizza un filtro di espressione regolare, è possibile fornire una stringa o un'espressione regolare, quando si utilizza la classe hello.</span><span class="sxs-lookup"><span data-stu-id="01940-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>

5. <span data-ttu-id="01940-170">Salvare hello `SearchByEmail.java` file.</span><span class="sxs-lookup"><span data-stu-id="01940-170">Save hello `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="01940-171">In hello `hbaseapp/src/main/hava/com/microsoft/examples` directory, creare un file denominato `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="01940-171">In hello `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="01940-172">Utilizzare hello segue testo come contenuto di hello di questo file:</span><span class="sxs-lookup"><span data-stu-id="01940-172">Use hello following text as hello contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete hello table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    <span data-ttu-id="01940-173">Questa classe elimina le tabelle di HBase create in questo esempio disabilitando hello ed eliminazione tabella hello creati hello `CreateTable` classe.</span><span class="sxs-lookup"><span data-stu-id="01940-173">This class cleans up hello HBase tables created in this example by disabling and dropping hello table created by hello `CreateTable` class.</span></span>

7. <span data-ttu-id="01940-174">Salvare hello `DeleteTable.java` file.</span><span class="sxs-lookup"><span data-stu-id="01940-174">Save hello `DeleteTable.java` file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="01940-175">Compilazione e del pacchetto applicazione hello</span><span class="sxs-lookup"><span data-stu-id="01940-175">Build and package hello application</span></span>

1. <span data-ttu-id="01940-176">Da hello `hbaseapp` directory di comando che segue hello utilizzare toobuild un file JAR contenente un'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="01940-176">From hello `hbaseapp` directory, use hello following command toobuild a JAR file that contains hello application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="01940-177">Questo comando Compila e pacchetti hello applicazione in un file JAR.</span><span class="sxs-lookup"><span data-stu-id="01940-177">This command builds and packages hello application into a .jar file.</span></span>

2. <span data-ttu-id="01940-178">Quando il comando hello viene completata, hello `hbaseapp/target` directory contiene un file denominato `hbaseapp-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="01940-178">When hello command completes, hello `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="01940-179">Hello `hbaseapp-1.0-SNAPSHOT.jar` file è un file jar uber.</span><span class="sxs-lookup"><span data-stu-id="01940-179">hello `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="01940-180">Contiene tutte le dipendenze necessarie toorun hello un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="01940-180">It contains all hello dependencies required toorun hello application.</span></span>


## <a name="upload-hello-jar-and-run-jobs-ssh"></a><span data-ttu-id="01940-181">Caricare hello JAR ed eseguire i processi (SSH)</span><span class="sxs-lookup"><span data-stu-id="01940-181">Upload hello JAR and run jobs (SSH)</span></span>

<span data-ttu-id="01940-182">Hello seguenti utilizzano `scp` toocopy hello JAR toohello head nodo primario dell'HBase in cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="01940-182">hello following steps use `scp` toocopy hello JAR toohello primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="01940-183">Hello `ssh` comando viene quindi utilizzato tooconnect toohello cluster e di esecuzione l'esempio hello direttamente nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="01940-183">hello `ssh` command is then used tooconnect toohello cluster and run hello example directly on hello head node.</span></span>

1. <span data-ttu-id="01940-184">tooupload hello jar toohello cluster utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01940-184">tooupload hello jar toohello cluster, use hello following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="01940-185">Sostituire `USERNAME` con nome hello dell'accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="01940-185">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="01940-186">Sostituire `CLUSTERNAME` con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="01940-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="01940-187">tooconnect toohello cluster HBase, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01940-187">tooconnect toohello HBase cluster, use hello following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="01940-188">Sostituire `USERNAME` nome hello dell'accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="01940-188">Replace `USERNAME` hello name of your SSH login.</span></span> <span data-ttu-id="01940-189">Sostituire `CLUSTERNAME` con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="01940-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="01940-190">una tabella HBase tramite toocreate hello applicazione Java, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01940-190">toocreate an HBase table using hello Java application, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="01940-191">Il comando crea una nuova tabella HBase denominata **people** e la popola con i dati.</span><span class="sxs-lookup"><span data-stu-id="01940-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="01940-192">toosearch per gli indirizzi di posta elettronica memorizzati nella tabella di hello, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01940-192">toosearch for email addresses stored in hello table, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="01940-193">Viene visualizzato hello seguenti risultati:</span><span class="sxs-lookup"><span data-stu-id="01940-193">You receive hello following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="01940-194">tabella di hello toodelete, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01940-194">toodelete hello table, use hello following command:</span></span>

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a><span data-ttu-id="01940-195">Caricare hello JAR ed eseguire i processi (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="01940-195">Upload hello JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="01940-196">Hello alla procedura seguente utilizza l'archiviazione di Azure PowerShell tooupload hello JAR toohello predefinita per il cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="01940-196">hello following steps use Azure PowerShell tooupload hello JAR toohello default storage for your HBase cluster.</span></span> <span data-ttu-id="01940-197">Cmdlet di HDInsight vengono quindi utilizzati toorun hello esempi in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="01940-197">HDInsight cmdlets are then used toorun hello examples remotely.</span></span>

1. <span data-ttu-id="01940-198">Dopo aver installato e configurato Azure PowerShell, creare un file denominato `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="01940-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="01940-199">Utilizzare hello segue testo come contenuto di hello di questo file:</span><span class="sxs-lookup"><span data-stu-id="01940-199">Use hello following text as hello contents of this file:</span></span>

   ```powershell
    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
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
    #hello class toorun
    [Parameter(Mandatory = $true)]
    [String]$className,

    #hello name of hello HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want toosee stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is hello Azure module installed?
    FindAzure

    # Get hello login for hello HDInsight cluster
    $creds=Get-Credential -Message "Enter hello login for hello cluster" -UserName "admin"

    # hello JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # hello job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get hello job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
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
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
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
            #hello path toohello local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #hello destination path and file name, relative toohello root of hello container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #hello name of hello HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is hello Azure module installed?
        FindAzure

        # Get authentication for hello cluster
        $creds=Get-Credential

        # Does hello local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get hello primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file toostorage, overwriting existing files if -force was used.
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
            throw "No active Azure subscription found! If you have a subscription, use hello Login-AzureRmAccount cmdlet toologin tooyour subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does hello cluster exist?
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
        # Get hello resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get hello storage context, as we can't depend
        # on using hello default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get hello container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts toosupport finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export hello verb-phrase things
    export-modulemember *-*
   ```

    <span data-ttu-id="01940-200">Questo file contiene due moduli:</span><span class="sxs-lookup"><span data-stu-id="01940-200">This file contains two modules:</span></span>

   * <span data-ttu-id="01940-201">**HDInsightFile aggiungere** : utilizzato cluster toohello di tooupload file</span><span class="sxs-lookup"><span data-stu-id="01940-201">**Add-HDInsightFile** - used tooupload files toohello cluster</span></span>
   * <span data-ttu-id="01940-202">**Inizio HBaseExample** -toorun hello classi creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="01940-202">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>

2. <span data-ttu-id="01940-203">Salvare hello `hbase-runner.psm1` file.</span><span class="sxs-lookup"><span data-stu-id="01940-203">Save hello `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="01940-204">Aprire una nuova finestra di PowerShell di Azure, modificare le directory toohello `hbaseapp` directory, e quindi eseguire hello finestra di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01940-204">Open a new Azure PowerShell window, change directories toohello `hbaseapp` directory, and then run hello following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="01940-205">Modificare toohello percorso hello di hello `hbase-runner.psm1` file creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="01940-205">Change hello path toohello location of hello `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="01940-206">Questo comando registra modulo hello con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01940-206">This command registers hello module with Azure PowerShell.</span></span>

4. <span data-ttu-id="01940-207">Comando che segue di hello utilizzare hello tooupload `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="01940-207">Use hello following command tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="01940-208">Sostituire `hdinsightclustername` con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="01940-208">Replace `hdinsightclustername` with hello name of your cluster.</span></span> <span data-ttu-id="01940-209">comando Hello carica hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` percorso di archiviazione primaria di hello per il cluster.</span><span class="sxs-lookup"><span data-stu-id="01940-209">hello command uploads hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` location in hello primary storage for your cluster.</span></span>

5. <span data-ttu-id="01940-210">una tabella utilizzando toocreate hello `hbaseapp`, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01940-210">toocreate a table using hello `hbaseapp`, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="01940-211">Sostituire `hdinsightclustername` con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="01940-211">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="01940-212">Questo comando consente di creare una nuova tabella denominata **people** in HBase nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="01940-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="01940-213">Questo comando non visualizza alcun output nella finestra di console hello.</span><span class="sxs-lookup"><span data-stu-id="01940-213">This command does not show any output in hello console window.</span></span>

6. <span data-ttu-id="01940-214">toosearch per le voci nella tabella di hello, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01940-214">toosearch for entries in hello table, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="01940-215">Sostituire `hdinsightclustername` con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="01940-215">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="01940-216">Questo comando Usa hello `SearchByEmail` classe toosearch per tutte le righe in cui hello `contactinformation` famiglia di colonna e hello `email` colonna contiene la stringa hello `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="01940-216">This command uses hello `SearchByEmail` class toosearch for any rows where hello `contactinformation` column family and hello `email` column, contains hello string `contoso.com`.</span></span> <span data-ttu-id="01940-217">Si dovrebbe ricevere hello seguenti risultati:</span><span class="sxs-lookup"><span data-stu-id="01940-217">You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="01940-218">Utilizzando **fabrikam.com** per hello `-emailRegex` valore restituisce utenti hello che dispongono di **fabrikam.com** nel campo messaggio di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="01940-218">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="01940-219">È inoltre possibile utilizzare espressioni regolari come termine di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="01940-219">You can also use regular expressions as hello search term.</span></span> <span data-ttu-id="01940-220">Ad esempio, **^ r** restituisce di posta elettronica gli indirizzi che iniziano con la lettera hello 'r'.</span><span class="sxs-lookup"><span data-stu-id="01940-220">For example, **^r** returns email addresses that begin with hello letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="01940-221">Nessun risultato o risultati imprevisti quando si usa Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="01940-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="01940-222">Hello utilizzare `-showErr` parametro tooview hello standard errore (STDERR) che viene generato durante il processo di hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="01940-222">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="01940-223">Eliminare la tabella hello</span><span class="sxs-lookup"><span data-stu-id="01940-223">Delete hello table</span></span>

<span data-ttu-id="01940-224">Una volta con l'esempio hello, utilizzare hello seguente hello toodelete **persone** tabella utilizzata in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="01940-224">When you are done with hello example, use hello following toodelete hello **people** table used in this example:</span></span>

<span data-ttu-id="01940-225">__Da una sessione `ssh`__:</span><span class="sxs-lookup"><span data-stu-id="01940-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="01940-226">__Da Azure PowerShell__:</span><span class="sxs-lookup"><span data-stu-id="01940-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="01940-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01940-227">Next steps</span></span>

[<span data-ttu-id="01940-228">Informazioni su come toouse SQL esce con HBase</span><span class="sxs-lookup"><span data-stu-id="01940-228">Learn how toouse SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
