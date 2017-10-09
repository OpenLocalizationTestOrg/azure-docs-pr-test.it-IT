---
title: un'applicazione Java HBase per basati su Windows Azure HDInsight aaaBuild | Documenti Microsoft
description: Informazioni su come toouse applicazione di HBase Apache Apache Maven toobuild basato su Java, quindi distribuirlo tooa basati su Windows Azure HDInsight cluster.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f4a4e02-45ab-40dd-842b-3ec034f256c9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 33c2f3d12cb6a17b5406817e8bcd3accff239517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="ad88b-103">Utilizzare le applicazioni Java di Maven toobuild che utilizzano HBase di HDInsight basati su Windows (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="ad88b-103">Use Maven toobuild Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="ad88b-104">Informazioni su come toocreate e compilare un [HBase Apache](http://hbase.apache.org/) applicazione Java mediante Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="ad88b-104">Learn how toocreate and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="ad88b-105">Utilizzare quindi l'applicazione hello con Azure HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="ad88b-105">Then use hello application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="ad88b-106">[Maven](http://maven.apache.org/) è un software progetto comprensione e gestione strumento che consente toobuild software, documentazione e report per i progetti di Java.</span><span class="sxs-lookup"><span data-stu-id="ad88b-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="ad88b-107">In questo articolo viene illustrato come toouse, toocreate un'applicazione Java che che crea, Elimina un HBase ed esegue query di tabella in un cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad88b-107">In this article, you learn how toouse it toocreate a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad88b-108">passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Windows.</span><span class="sxs-lookup"><span data-stu-id="ad88b-108">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="ad88b-109">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="ad88b-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ad88b-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ad88b-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="ad88b-111">Requisiti</span><span class="sxs-lookup"><span data-stu-id="ad88b-111">Requirements</span></span>
* <span data-ttu-id="ad88b-112">[Piattaforma Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="ad88b-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="ad88b-113">Maven</span><span class="sxs-lookup"><span data-stu-id="ad88b-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="ad88b-114">Un cluster HDInsight basato su Windows con HBase</span><span class="sxs-lookup"><span data-stu-id="ad88b-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="ad88b-115">passaggi di Hello in questo documento sono stati testati con le versioni cluster HDInsight 3.2 e 3.3.</span><span class="sxs-lookup"><span data-stu-id="ad88b-115">hello steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="ad88b-116">i valori predefiniti di Hello forniti negli esempi sono per un cluster HDInsight 3.3.</span><span class="sxs-lookup"><span data-stu-id="ad88b-116">hello default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="ad88b-117">Creare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="ad88b-117">Create hello project</span></span>
1. <span data-ttu-id="ad88b-118">Dalla riga di comando hello nell'ambiente di sviluppo, modificare il percorso di toohello directory in cui si desidera progetto hello toocreate, ad esempio, `cd code\hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="ad88b-118">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="ad88b-119">Hello utilizzare **mvn** comando, che viene installato con Maven, hello toogenerate lo scaffolding per progetto hello.</span><span class="sxs-lookup"><span data-stu-id="ad88b-119">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="ad88b-120">Questo comando crea una directory nel percorso corrente hello, con il nome di hello specificato da hello **ID** parametro (**hbaseapp** in questo esempio.) Questa directory contiene hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ad88b-120">This command creates a directory in hello current location, with hello name specified by hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="ad88b-121">**POM.XML**: hello modello oggetto di progetto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contiene informazioni e la configurazione progetto hello toobuild di dettagli utilizzati.</span><span class="sxs-lookup"><span data-stu-id="ad88b-121">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="ad88b-122">**src**: directory hello contenente hello **main\java\com\microsoft\examples** directory, verrà creata un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ad88b-122">**src**: hello directory that contains hello **main\java\com\microsoft\examples** directory, where you will author hello application.</span></span>
3. <span data-ttu-id="ad88b-123">Eliminare hello **src\test\java\com\microsoft\examples\apptest.java** file perché non è stato utilizzato in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="ad88b-123">Delete hello **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="ad88b-124">Aggiornare hello progetto modello a oggetti</span><span class="sxs-lookup"><span data-stu-id="ad88b-124">Update hello Project Object Model</span></span>
1. <span data-ttu-id="ad88b-125">Modifica hello **pom.xml** file e aggiungere hello seguente codice all'interno di hello `<dependencies>` sezione:</span><span class="sxs-lookup"><span data-stu-id="ad88b-125">Edit hello **pom.xml** file and add hello following code inside hello `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="ad88b-126">Questa sezione viene spiegato Maven che hello progetto richiede **hbase client** versione **1.1.2**.</span><span class="sxs-lookup"><span data-stu-id="ad88b-126">This section tells Maven that hello project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="ad88b-127">In fase di compilazione, la dipendenza viene scaricata dal repository di Maven hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="ad88b-127">At compile time, this dependency is downloaded from hello default Maven repository.</span></span> <span data-ttu-id="ad88b-128">È possibile utilizzare hello [ricerca Repository centrale Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn informazioni su questa dipendenza.</span><span class="sxs-lookup"><span data-stu-id="ad88b-128">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ad88b-129">numero di versione di Hello deve corrispondere una versione di hello di HBase che viene fornito con il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad88b-129">hello version number must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="ad88b-130">Utilizzare hello seguente numero di versione corretto hello toofind tabella.</span><span class="sxs-lookup"><span data-stu-id="ad88b-130">Use hello following table toofind hello correct version number.</span></span>
   >
   >

   | <span data-ttu-id="ad88b-131">Versione del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="ad88b-131">HDInsight cluster version</span></span> | <span data-ttu-id="ad88b-132">Toouse versione HBase</span><span class="sxs-lookup"><span data-stu-id="ad88b-132">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="ad88b-133">3.2</span><span class="sxs-lookup"><span data-stu-id="ad88b-133">3.2</span></span> |<span data-ttu-id="ad88b-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="ad88b-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="ad88b-135">3.3</span><span class="sxs-lookup"><span data-stu-id="ad88b-135">3.3</span></span> |<span data-ttu-id="ad88b-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="ad88b-136">1.1.2</span></span> |

    <span data-ttu-id="ad88b-137">Per ulteriori informazioni sulle versioni di HDInsight e i componenti, vedere [quali sono hello Hadoop componenti diversi disponibili con HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ad88b-137">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="ad88b-138">Se si utilizza un cluster HDInsight 3.3, è necessario aggiungere anche hello seguente toohello `<dependencies>` sezione:</span><span class="sxs-lookup"><span data-stu-id="ad88b-138">If you are using an HDInsight 3.3 cluster, you must also add hello following toohello `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="ad88b-139">Questa dipendenza verrà caricati i componenti di core phoenix hello, utilizzato dalla versione di Hbase 1.1.x.</span><span class="sxs-lookup"><span data-stu-id="ad88b-139">This dependency will load hello phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="ad88b-140">Aggiungere i seguenti toohello codice hello **pom.xml** file.</span><span class="sxs-lookup"><span data-stu-id="ad88b-140">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="ad88b-141">In questa sezione deve trovarsi all'interno di hello `<project>...</project>` tag hello file, ad esempio tra `</dependencies>` e `</project>`.</span><span class="sxs-lookup"><span data-stu-id="ad88b-141">This section must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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
                    <source>1.7</source>
                    <target>1.7</target>
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

    <span data-ttu-id="ad88b-142">Hello `<resources>` sezione Configura una risorsa (**conf\hbase site.xml**) che contiene informazioni sulla configurazione di HBase.</span><span class="sxs-lookup"><span data-stu-id="ad88b-142">hello `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ad88b-143">È anche possibile impostare i valori di configurazione tramite codice.</span><span class="sxs-lookup"><span data-stu-id="ad88b-143">You can also set configuration values via code.</span></span> <span data-ttu-id="ad88b-144">Vedere i commenti di hello in hello **CreateTable** esempio riportato di seguito per informazioni su come toodo questo.</span><span class="sxs-lookup"><span data-stu-id="ad88b-144">See hello comments in hello **CreateTable** example that follows for how toodo this.</span></span>
   >
   >

    <span data-ttu-id="ad88b-145">Questo `<plugins>` sezione Configura hello [plug-in compilatore Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) e [plug-in Maven sfumatura](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="ad88b-145">This `<plugins>` section configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="ad88b-146">compilatore Hello plug-in è usato toocompile hello topologia.</span><span class="sxs-lookup"><span data-stu-id="ad88b-146">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="ad88b-147">sfumatura Hello plug-in è la duplicazione di licenza tooprevent utilizzati nel pacchetto JAR hello Maven compilata.</span><span class="sxs-lookup"><span data-stu-id="ad88b-147">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="ad88b-148">motivo di Hello che viene utilizzato è che i file di licenza duplicati hello generano un errore in fase di esecuzione nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ad88b-148">hello reason this is used is that hello duplicate license files cause an error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="ad88b-149">Utilizzo di plug-in maven sfumatura con hello `ApacheLicenseResourceTransformer` implementazione impedisce a questo errore.</span><span class="sxs-lookup"><span data-stu-id="ad88b-149">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="ad88b-150">Hello plug-in maven sfumatura genera inoltre un file jar uber (o jar fat) che contiene tutte le dipendenze di hello richieste da un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ad88b-150">hello maven-shade-plugin also produces an uber jar (or fat jar) that contains all hello dependencies required by hello application.</span></span>
4. <span data-ttu-id="ad88b-151">Salvare hello **pom.xml** file.</span><span class="sxs-lookup"><span data-stu-id="ad88b-151">Save hello **pom.xml** file.</span></span>
5. <span data-ttu-id="ad88b-152">Creare una nuova directory denominata **conf** in hello **hbaseapp** directory.</span><span class="sxs-lookup"><span data-stu-id="ad88b-152">Create a new directory named **conf** in hello **hbaseapp** directory.</span></span> <span data-ttu-id="ad88b-153">In hello **conf** directory, creare un file denominato **hbase-Site.XML**.</span><span class="sxs-lookup"><span data-stu-id="ad88b-153">In hello **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="ad88b-154">Utilizzare l'esempio hello come contenuto di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="ad88b-154">Use hello following as hello contents of hello file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 hello Apache Software Foundation
          *
          * Licensed toohello Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See hello NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  hello ASF licenses this file
          * tooyou under hello Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with hello License.  You may obtain a copy of hello License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed tooin writing, software
          * distributed under hello License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See hello License for hello specific language governing permissions and
          * limitations under hello License.
          */
        -->
        <configuration>
          <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
          </property>
          <property>
            <name>hbase.zookeeper.quorum</name>
            <value>zookeeper0,zookeeper1,zookeeper2</value>
          </property>
          <property>
            <name>hbase.zookeeper.property.clientPort</name>
            <value>2181</value>
          </property>
        </configuration>

    <span data-ttu-id="ad88b-155">Questo file sarà configurazione di HBase hello tooload utilizzati per un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad88b-155">This file will be used tooload hello HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ad88b-156">Si tratta di un file hbase-Site.XML minimo, e contiene le impostazioni minime bare hello per cluster di HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ad88b-156">This is a minimal hbase-site.xml file, and it contains hello bare minimum settings for hello HDInsight cluster.</span></span>

6. <span data-ttu-id="ad88b-157">Salvare hello **hbase-Site.XML** file.</span><span class="sxs-lookup"><span data-stu-id="ad88b-157">Save hello **hbase-site.xml** file.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="ad88b-158">Creare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="ad88b-158">Create hello application</span></span>
1. <span data-ttu-id="ad88b-159">Passare toohello **hbaseapp\src\main\java\com\microsoft\examples** directory e rinominare hello app.java file troppo**CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="ad88b-159">Go toohello **hbaseapp\src\main\java\com\microsoft\examples** directory and rename hello app.java file too**CreateTable.java**.</span></span>
2. <span data-ttu-id="ad88b-160">Aprire hello **CreateTable.java** file e sostituire i contenuti esistenti hello con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="ad88b-160">Open hello **CreateTable.java** file and replace hello existing contents with hello following code:</span></span>

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
            // hello following sets hello znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

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

    <span data-ttu-id="ad88b-161">Si tratta di hello **CreateTable** (classe), che verrà creata una tabella denominata **persone** e viene popolato con alcuni utenti predefiniti.</span><span class="sxs-lookup"><span data-stu-id="ad88b-161">This is hello **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="ad88b-162">Salvare hello **CreateTable.java** file.</span><span class="sxs-lookup"><span data-stu-id="ad88b-162">Save hello **CreateTable.java** file.</span></span>
4. <span data-ttu-id="ad88b-163">In hello **hbaseapp\src\main\java\com\microsoft\examples** directory, creare un nuovo file denominato **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="ad88b-163">In hello **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="ad88b-164">Utilizzare hello seguente di codice come contenuto di hello di questo file:</span><span class="sxs-lookup"><span data-stu-id="ad88b-164">Use hello following code as hello contents of this file:</span></span>

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

            // Create a new regex filter
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

    <span data-ttu-id="ad88b-165">Hello **SearchByEmail** classe può essere utilizzato tooquery per le righe dall'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="ad88b-165">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="ad88b-166">Poiché utilizza un filtro di espressione regolare, è possibile fornire una stringa o un'espressione regolare, quando si utilizza la classe hello.</span><span class="sxs-lookup"><span data-stu-id="ad88b-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>
5. <span data-ttu-id="ad88b-167">Salvare hello **SearchByEmail.java** file.</span><span class="sxs-lookup"><span data-stu-id="ad88b-167">Save hello **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="ad88b-168">In hello **hbaseapp\src\main\hava\com\microsoft\examples** directory, creare un nuovo file denominato **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="ad88b-168">In hello **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="ad88b-169">Utilizzare hello seguente di codice come contenuto di hello di questo file:</span><span class="sxs-lookup"><span data-stu-id="ad88b-169">Use hello following code as hello contents of this file:</span></span>

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

    <span data-ttu-id="ad88b-170">Questa classe per la pulizia di questo esempio disabilitando ed eliminazione tabella hello creati hello **CreateTable** classe.</span><span class="sxs-lookup"><span data-stu-id="ad88b-170">This class is for cleaning up this example by disabling and dropping hello table created by hello **CreateTable** class.</span></span>
7. <span data-ttu-id="ad88b-171">Salvare hello **DeleteTable.java** file.</span><span class="sxs-lookup"><span data-stu-id="ad88b-171">Save hello **DeleteTable.java** file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="ad88b-172">Compilazione e del pacchetto applicazione hello</span><span class="sxs-lookup"><span data-stu-id="ad88b-172">Build and package hello application</span></span>
1. <span data-ttu-id="ad88b-173">Aprire un prompt dei comandi e modificare le directory toohello **hbaseapp** directory.</span><span class="sxs-lookup"><span data-stu-id="ad88b-173">Open a command prompt and change directories toohello **hbaseapp** directory.</span></span>
2. <span data-ttu-id="ad88b-174">Utilizzare hello comando toobuild un file JAR contenente un'applicazione hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad88b-174">Use hello following command toobuild a JAR file that contains hello application:</span></span>

        mvn clean package

    <span data-ttu-id="ad88b-175">Ciò elimina gli artefatti di compilazione precedente, Scarica tutte le dipendenze che non sono già state installate, quindi compila e pacchetti applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ad88b-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages hello application.</span></span>
3. <span data-ttu-id="ad88b-176">Quando il comando hello viene completata, hello **hbaseapp\target** directory contiene un file denominato **hbaseapp-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="ad88b-176">When hello command completes, hello **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ad88b-177">Hello **hbaseapp-1.0-SNAPSHOT.jar** file è un uber jar (detto anche un file jar fat,) che contiene tutte le dipendenze di hello è necessaria un'applicazione hello toorun.</span><span class="sxs-lookup"><span data-stu-id="ad88b-177">hello **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all hello dependencies required toorun hello application.</span></span>

## <a name="upload-hello-jar-file-and-start-a-job"></a><span data-ttu-id="ad88b-178">Caricare il file JAR hello e avviare un processo</span><span class="sxs-lookup"><span data-stu-id="ad88b-178">Upload hello JAR file and start a job</span></span>
<span data-ttu-id="ad88b-179">Esistono molti tooupload modi un cluster di HDInsight tooyour file, come descritto in [caricare dati per i processi di Hadoop in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="ad88b-179">There are many ways tooupload a file tooyour HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="ad88b-180">Hello segue usano Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad88b-180">hello following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="ad88b-181">Dopo aver installato e configurato Azure PowerShell, creare un nuovo file denominato **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="ad88b-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="ad88b-182">Utilizzare i seguenti hello come contenuto hello di questo file:</span><span class="sxs-lookup"><span data-stu-id="ad88b-182">Use hello following as hello contents of this file:</span></span>

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

    <span data-ttu-id="ad88b-183">Questo file contiene due moduli:</span><span class="sxs-lookup"><span data-stu-id="ad88b-183">This file contains two modules:</span></span>

   * <span data-ttu-id="ad88b-184">**HDInsightFile aggiungere** -utilizzato tooupload file tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="ad88b-184">**Add-HDInsightFile** - used tooupload files tooHDInsight</span></span>
   * <span data-ttu-id="ad88b-185">**Inizio HBaseExample** -toorun hello classi creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="ad88b-185">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>
2. <span data-ttu-id="ad88b-186">Salvare hello **hbase runner.psm1** file.</span><span class="sxs-lookup"><span data-stu-id="ad88b-186">Save hello **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="ad88b-187">Aprire una nuova finestra di PowerShell di Azure, modificare le directory toohello **hbaseapp** directory, e quindi di comando seguente hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ad88b-187">Open a new Azure PowerShell window, change directories toohello **hbaseapp** directory, and then run hello following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="ad88b-188">Modificare toohello percorso hello di hello **hbase runner.psm1** file creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ad88b-188">Change hello path toohello location of hello **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="ad88b-189">In questo modo viene registrata modulo hello per questa sessione di PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad88b-189">This registers hello module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="ad88b-190">Comando che segue di hello utilizzare hello tooupload **hbaseapp-1.0-SNAPSHOT.jar** tooyour cluster di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad88b-190">Use hello following command tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="ad88b-191">Sostituire **hdinsightclustername** con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad88b-191">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="ad88b-192">comando Hello carica hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **esempio/JAR** percorso di archiviazione primaria di hello per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad88b-192">hello command uploads hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **example/jars** location in hello primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="ad88b-193">Una volta caricati i file hello, utilizzare hello di codice seguente toocreate una tabella utilizzando hello **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="ad88b-193">After hello files are uploaded, use hello following code toocreate a table using hello **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="ad88b-194">Sostituire **hdinsightclustername** con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad88b-194">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="ad88b-195">Questo comando consente di creare una nuova tabella denominata **people** nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad88b-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="ad88b-196">Questo comando non visualizza alcun output nella finestra di console hello.</span><span class="sxs-lookup"><span data-stu-id="ad88b-196">This command does not show any output in hello console window.</span></span>
6. <span data-ttu-id="ad88b-197">toosearch per le voci nella tabella di hello, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ad88b-197">toosearch for entries in hello table, use hello following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="ad88b-198">Sostituire **hdinsightclustername** con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad88b-198">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="ad88b-199">Questo comando Usa hello **SearchByEmail** classe toosearch per tutte le righe in cui hello **informazionidicontatto** famiglia di colonna e hello **posta elettronica** colonna contiene la stringa hello **contoso.com**. Si dovrebbe ricevere hello seguenti risultati:</span><span class="sxs-lookup"><span data-stu-id="ad88b-199">This command uses hello **SearchByEmail** class toosearch for any rows where hello **contactinformation** column family and hello **email** column, contains hello string **contoso.com**. You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="ad88b-200">Utilizzando **fabrikam.com** per hello `-emailRegex` valore restituisce utenti hello che dispongono di **fabrikam.com** nel campo messaggio di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="ad88b-200">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="ad88b-201">Poiché questa ricerca viene implementata utilizzando un filtro basato su espressioni regolari, è inoltre possibile immettere espressioni regolari, ad esempio **^ r**, le voci che restituisce in cui posta elettronica hello inizia con la lettera di hello 'r'.</span><span class="sxs-lookup"><span data-stu-id="ad88b-201">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where hello email begins with hello letter 'r'.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="ad88b-202">Eliminare la tabella hello</span><span class="sxs-lookup"><span data-stu-id="ad88b-202">Delete hello table</span></span>
<span data-ttu-id="ad88b-203">Una volta con l'esempio hello, comando che segue di hello utilizzare da hello di hello Azure PowerShell sessione toodelete **persone** tabella utilizzata in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="ad88b-203">When you are done with hello example, use hello following command from hello Azure PowerShell session toodelete hello **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="ad88b-204">Sostituire **hdinsightclustername** con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad88b-204">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ad88b-205">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ad88b-205">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="ad88b-206">Nessun risultato o risultati imprevisti quando si usa Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="ad88b-206">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="ad88b-207">Hello utilizzare `-showErr` parametro tooview hello standard errore (STDERR) che viene generato durante il processo di hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ad88b-207">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>
