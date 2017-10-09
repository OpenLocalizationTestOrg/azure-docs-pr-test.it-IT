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
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a>Utilizzare le applicazioni Java di Maven toobuild che utilizzano HBase di HDInsight basati su Windows (Hadoop)
Informazioni su come toocreate e compilare un [HBase Apache](http://hbase.apache.org/) applicazione Java mediante Apache Maven. Utilizzare quindi l'applicazione hello con Azure HDInsight (Hadoop).

[Maven](http://maven.apache.org/) è un software progetto comprensione e gestione strumento che consente toobuild software, documentazione e report per i progetti di Java. In questo articolo viene illustrato come toouse, toocreate un'applicazione Java che che crea, Elimina un HBase ed esegue query di tabella in un cluster HDInsight di Azure.

> [!IMPORTANT]
> passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Windows. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="requirements"></a>Requisiti
* [Piattaforma Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 o versioni successive
* [Maven](http://maven.apache.org/)
* Un cluster HDInsight basato su Windows con HBase

    > [!NOTE]
    > passaggi di Hello in questo documento sono stati testati con le versioni cluster HDInsight 3.2 e 3.3. i valori predefiniti di Hello forniti negli esempi sono per un cluster HDInsight 3.3.

## <a name="create-hello-project"></a>Creare il progetto hello
1. Dalla riga di comando hello nell'ambiente di sviluppo, modificare il percorso di toohello directory in cui si desidera progetto hello toocreate, ad esempio, `cd code\hdinsight`.
2. Hello utilizzare **mvn** comando, che viene installato con Maven, hello toogenerate lo scaffolding per progetto hello.

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    Questo comando crea una directory nel percorso corrente hello, con il nome di hello specificato da hello **ID** parametro (**hbaseapp** in questo esempio.) Questa directory contiene hello seguenti elementi:

   * **POM.XML**: hello modello oggetto di progetto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contiene informazioni e la configurazione progetto hello toobuild di dettagli utilizzati.
   * **src**: directory hello contenente hello **main\java\com\microsoft\examples** directory, verrà creata un'applicazione hello.
3. Eliminare hello **src\test\java\com\microsoft\examples\apptest.java** file perché non è stato utilizzato in questo esempio.

## <a name="update-hello-project-object-model"></a>Aggiornare hello progetto modello a oggetti
1. Modifica hello **pom.xml** file e aggiungere hello seguente codice all'interno di hello `<dependencies>` sezione:

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    Questa sezione viene spiegato Maven che hello progetto richiede **hbase client** versione **1.1.2**. In fase di compilazione, la dipendenza viene scaricata dal repository di Maven hello predefinito. È possibile utilizzare hello [ricerca Repository centrale Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn informazioni su questa dipendenza.

   > [!IMPORTANT]
   > numero di versione di Hello deve corrispondere una versione di hello di HBase che viene fornito con il cluster HDInsight. Utilizzare hello seguente numero di versione corretto hello toofind tabella.
   >
   >

   | Versione del cluster HDInsight | Toouse versione HBase |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3 |1.1.2 |

    Per ulteriori informazioni sulle versioni di HDInsight e i componenti, vedere [quali sono hello Hadoop componenti diversi disponibili con HDInsight](hdinsight-component-versioning.md).
2. Se si utilizza un cluster HDInsight 3.3, è necessario aggiungere anche hello seguente toohello `<dependencies>` sezione:

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    Questa dipendenza verrà caricati i componenti di core phoenix hello, utilizzato dalla versione di Hbase 1.1.x.
3. Aggiungere i seguenti toohello codice hello **pom.xml** file. In questa sezione deve trovarsi all'interno di hello `<project>...</project>` tag hello file, ad esempio tra `</dependencies>` e `</project>`.

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

    Hello `<resources>` sezione Configura una risorsa (**conf\hbase site.xml**) che contiene informazioni sulla configurazione di HBase.

   > [!NOTE]
   > È anche possibile impostare i valori di configurazione tramite codice. Vedere i commenti di hello in hello **CreateTable** esempio riportato di seguito per informazioni su come toodo questo.
   >
   >

    Questo `<plugins>` sezione Configura hello [plug-in compilatore Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) e [plug-in Maven sfumatura](http://maven.apache.org/plugins/maven-shade-plugin/). compilatore Hello plug-in è usato toocompile hello topologia. sfumatura Hello plug-in è la duplicazione di licenza tooprevent utilizzati nel pacchetto JAR hello Maven compilata. motivo di Hello che viene utilizzato è che i file di licenza duplicati hello generano un errore in fase di esecuzione nel cluster HDInsight hello. Utilizzo di plug-in maven sfumatura con hello `ApacheLicenseResourceTransformer` implementazione impedisce a questo errore.

    Hello plug-in maven sfumatura genera inoltre un file jar uber (o jar fat) che contiene tutte le dipendenze di hello richieste da un'applicazione hello.
4. Salvare hello **pom.xml** file.
5. Creare una nuova directory denominata **conf** in hello **hbaseapp** directory. In hello **conf** directory, creare un file denominato **hbase-Site.XML**. Utilizzare l'esempio hello come contenuto di hello del file hello:

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

    Questo file sarà configurazione di HBase hello tooload utilizzati per un cluster HDInsight.

   > [!NOTE]
   > Si tratta di un file hbase-Site.XML minimo, e contiene le impostazioni minime bare hello per cluster di HDInsight hello.

6. Salvare hello **hbase-Site.XML** file.

## <a name="create-hello-application"></a>Creare un'applicazione hello
1. Passare toohello **hbaseapp\src\main\java\com\microsoft\examples** directory e rinominare hello app.java file troppo**CreateTable.java**.
2. Aprire hello **CreateTable.java** file e sostituire i contenuti esistenti hello con hello seguente codice:

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

    Si tratta di hello **CreateTable** (classe), che verrà creata una tabella denominata **persone** e viene popolato con alcuni utenti predefiniti.
3. Salvare hello **CreateTable.java** file.
4. In hello **hbaseapp\src\main\java\com\microsoft\examples** directory, creare un nuovo file denominato **SearchByEmail.java**. Utilizzare hello seguente di codice come contenuto di hello di questo file:

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

    Hello **SearchByEmail** classe può essere utilizzato tooquery per le righe dall'indirizzo di posta elettronica. Poiché utilizza un filtro di espressione regolare, è possibile fornire una stringa o un'espressione regolare, quando si utilizza la classe hello.
5. Salvare hello **SearchByEmail.java** file.
6. In hello **hbaseapp\src\main\hava\com\microsoft\examples** directory, creare un nuovo file denominato **DeleteTable.java**. Utilizzare hello seguente di codice come contenuto di hello di questo file:

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

    Questa classe per la pulizia di questo esempio disabilitando ed eliminazione tabella hello creati hello **CreateTable** classe.
7. Salvare hello **DeleteTable.java** file.

## <a name="build-and-package-hello-application"></a>Compilazione e del pacchetto applicazione hello
1. Aprire un prompt dei comandi e modificare le directory toohello **hbaseapp** directory.
2. Utilizzare hello comando toobuild un file JAR contenente un'applicazione hello seguenti:

        mvn clean package

    Ciò elimina gli artefatti di compilazione precedente, Scarica tutte le dipendenze che non sono già state installate, quindi compila e pacchetti applicazione hello.
3. Quando il comando hello viene completata, hello **hbaseapp\target** directory contiene un file denominato **hbaseapp-1.0-SNAPSHOT.jar**.

   > [!NOTE]
   > Hello **hbaseapp-1.0-SNAPSHOT.jar** file è un uber jar (detto anche un file jar fat,) che contiene tutte le dipendenze di hello è necessaria un'applicazione hello toorun.

## <a name="upload-hello-jar-file-and-start-a-job"></a>Caricare il file JAR hello e avviare un processo
Esistono molti tooupload modi un cluster di HDInsight tooyour file, come descritto in [caricare dati per i processi di Hadoop in HDInsight](hdinsight-upload-data.md). Hello segue usano Azure PowerShell.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. Dopo aver installato e configurato Azure PowerShell, creare un nuovo file denominato **hbase-runner.psm1**. Utilizzare i seguenti hello come contenuto hello di questo file:

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

    Questo file contiene due moduli:

   * **HDInsightFile aggiungere** -utilizzato tooupload file tooHDInsight
   * **Inizio HBaseExample** -toorun hello classi creato in precedenza
2. Salvare hello **hbase runner.psm1** file.
3. Aprire una nuova finestra di PowerShell di Azure, modificare le directory toohello **hbaseapp** directory, e quindi di comando seguente hello esecuzione.

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    Modificare toohello percorso hello di hello **hbase runner.psm1** file creato in precedenza. In questo modo viene registrata modulo hello per questa sessione di PowerShell di Azure.
4. Comando che segue di hello utilizzare hello tooupload **hbaseapp-1.0-SNAPSHOT.jar** tooyour cluster di HDInsight.

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    Sostituire **hdinsightclustername** con nome hello del cluster HDInsight. comando Hello carica hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **esempio/JAR** percorso di archiviazione primaria di hello per il cluster HDInsight.
5. Una volta caricati i file hello, utilizzare hello di codice seguente toocreate una tabella utilizzando hello **hbaseapp**:

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    Sostituire **hdinsightclustername** con nome hello del cluster HDInsight.

    Questo comando consente di creare una nuova tabella denominata **people** nel cluster HDInsight. Questo comando non visualizza alcun output nella finestra di console hello.
6. toosearch per le voci nella tabella di hello, utilizzare hello comando seguente:

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    Sostituire **hdinsightclustername** con nome hello del cluster HDInsight.

    Questo comando Usa hello **SearchByEmail** classe toosearch per tutte le righe in cui hello **informazionidicontatto** famiglia di colonna e hello **posta elettronica** colonna contiene la stringa hello **contoso.com**. Si dovrebbe ricevere hello seguenti risultati:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Utilizzando **fabrikam.com** per hello `-emailRegex` valore restituisce utenti hello che dispongono di **fabrikam.com** nel campo messaggio di posta elettronica hello. Poiché questa ricerca viene implementata utilizzando un filtro basato su espressioni regolari, è inoltre possibile immettere espressioni regolari, ad esempio **^ r**, le voci che restituisce in cui posta elettronica hello inizia con la lettera di hello 'r'.

## <a name="delete-hello-table"></a>Eliminare la tabella hello
Una volta con l'esempio hello, comando che segue di hello utilizzare da hello di hello Azure PowerShell sessione toodelete **persone** tabella utilizzata in questo esempio:

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

Sostituire **hdinsightclustername** con nome hello del cluster HDInsight.

## <a name="troubleshooting"></a>Risoluzione dei problemi
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Nessun risultato o risultati imprevisti quando si usa Start-HBaseExample
Hello utilizzare `-showErr` parametro tooview hello standard errore (STDERR) che viene generato durante il processo di hello in esecuzione.
