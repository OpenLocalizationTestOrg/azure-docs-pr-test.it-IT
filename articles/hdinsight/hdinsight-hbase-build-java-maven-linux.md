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
# <a name="build-java-applications-for-apache-hbase"></a>Compilare applicazioni Java per Apache HBase

Informazioni su come toocreate un [HBase Apache](http://hbase.apache.org/) applicazione Java. Utilizzare quindi l'applicazione hello con HBase in HDInsight di Azure.

i passaggi di questo documento viene utilizzato da Hello [Maven](http://maven.apache.org/) toocreate e compilazione progetto hello. Maven è uno strumento di comprensione che consente di toobuild software, documentazione e report per i progetti di Java e la gestione dei progetti software.

> [!NOTE]
> Hello passaggi descritti in questo documento più recente testati con 3.6 di HDInsight.

> [!IMPORTANT]
> passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="requirements"></a>Requisiti

* [Piattaforma Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 o versioni successive.

    > [!NOTE]
    > HDInsight 3.5 e versioni successive richiedono Java 8. Le versioni precedenti di HDInsight richiedono Java 7.

* [Maven](http://maven.apache.org/)

* [Un cluster Azure HDInsight basato su Linux con HBase](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > passaggi di Hello in questo documento sono stati testati con le versioni cluster HDInsight 3.4 e 3.5. i valori predefiniti di Hello forniti negli esempi sono per un cluster HDInsight 3.5.

## <a name="create-hello-project"></a>Creare il progetto hello

1. Dalla riga di comando hello nell'ambiente di sviluppo, modificare il percorso di toohello directory in cui si desidera progetto hello toocreate, ad esempio, `cd code\hbase`.

2. Hello utilizzare **mvn** comando, che viene installato con Maven, hello toogenerate lo scaffolding per progetto hello.

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > Se si usa PowerShell, è necessario racchiudere hello `-D` parametri racchiuso tra virgolette doppie.
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Questo comando crea una directory con stesso nome come hello hello **ID** parametro (**hbaseapp** in questo esempio.) Questa directory contiene hello seguenti elementi:

   * **POM.XML**: hello modello oggetto di progetto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contiene informazioni e la configurazione progetto hello toobuild di dettagli utilizzati.
   * **src**: directory hello contenente hello **main/java/com/microsoft/esempi** directory, in cui si crea un'applicazione hello.

3. Eliminare hello `src/test/java/com/microsoft/examples/apptest.java` file. Non viene usato in questo esempio.

## <a name="update-hello-project-object-model"></a>Aggiornare hello progetto modello a oggetti

1. Modifica hello `pom.xml` file e aggiungere hello seguente codice all'interno di hello `<dependencies>` sezione:

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

    In questa sezione indica che il progetto hello deve **hbase client** e **phoenix core** componenti. In fase di compilazione, queste dipendenze vengono scaricate dal repository di Maven hello predefinito. È possibile utilizzare hello [ricerca Repository centrale Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn informazioni su questa dipendenza.

   > [!IMPORTANT]
   > numero di versione di Hello del client di hbase hello deve corrispondere una versione di hello di HBase che viene fornito con il cluster HDInsight. Utilizzare hello seguente numero di versione corretto hello toofind tabella.

   | Versione del cluster HDInsight | Toouse versione HBase |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3, 3.4, 3.5 e 3.6 |1.1.2 |

    Per ulteriori informazioni sulle versioni di HDInsight e i componenti, vedere [quali sono hello Hadoop componenti diversi disponibili con HDInsight](hdinsight-component-versioning.md).

3. Aggiungere i seguenti toohello codice hello **pom.xml** file. Questo testo deve trovarsi all'interno di hello `<project>...</project>` tag hello file, ad esempio tra `</dependencies>` e `</project>`.

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

    Questa sezione configura una risorsa (`conf/hbase-site.xml`) che contiene informazioni di configurazione per HBase.

   > [!NOTE]
   > È anche possibile impostare i valori di configurazione tramite codice. Vedere i commenti di hello in hello `CreateTable` esempio.

    In questa sezione Configura inoltre hello [plug-in compilatore Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) e [plug-in Maven sfumatura](http://maven.apache.org/plugins/maven-shade-plugin/). compilatore Hello plug-in è usato toocompile hello topologia. sfumatura Hello plug-in è la duplicazione di licenza tooprevent utilizzati nel pacchetto JAR hello Maven compilata. Questo plug-in è tooprevent usato un errore di "duplicato. i file di licenza" in fase di esecuzione nel cluster HDInsight hello. Utilizzo di plug-in maven sfumatura con hello `ApacheLicenseResourceTransformer` errore hello impedisce l'implementazione.

    Hello maven-sfumatura-plug-in anche produce un file jar uber che contiene tutte le dipendenze di hello richieste da un'applicazione hello.

4. Salvare hello `pom.xml` file.

5. Creare una directory denominata `conf` in hello `hbaseapp` directory. Questa directory contiene informazioni di configurazione toohold utilizzato per la connessione tooHBase.

6. Comando che segue hello di utilizzare la configurazione di HBase di hello toocopy da toohello cluster HBase di hello `conf` directory. Sostituire `USERNAME` con nome hello dell'accesso SSH. Sostituire `CLUSTERNAME` con il nome del cluster HDInsight:

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   Per altre informazioni sull'uso di `ssh` e `scp`, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-hello-application"></a>Creare un'applicazione hello

1. Passare toohello `hbaseapp/src/main/java/com/microsoft/examples` directory e rinominare hello app.java file troppo`CreateTable.java`.

2. Aprire hello `CreateTable.java` file e sostituire contenuto esistente hello con hello seguente testo:

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

    Questo codice è hello **CreateTable** (classe), che consente di creare una tabella denominata **persone** e viene popolato con alcuni utenti predefiniti.

3. Salvare hello `CreateTable.java` file.

4. In hello `hbaseapp/src/main/java/com/microsoft/examples` directory, creare un file denominato `SearchByEmail.java`. Utilizzare hello segue testo come contenuto di hello di questo file:

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

    Hello **SearchByEmail** classe può essere utilizzato tooquery per le righe dall'indirizzo di posta elettronica. Poiché utilizza un filtro di espressione regolare, è possibile fornire una stringa o un'espressione regolare, quando si utilizza la classe hello.

5. Salvare hello `SearchByEmail.java` file.

6. In hello `hbaseapp/src/main/hava/com/microsoft/examples` directory, creare un file denominato `DeleteTable.java`. Utilizzare hello segue testo come contenuto di hello di questo file:

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

    Questa classe elimina le tabelle di HBase create in questo esempio disabilitando hello ed eliminazione tabella hello creati hello `CreateTable` classe.

7. Salvare hello `DeleteTable.java` file.

## <a name="build-and-package-hello-application"></a>Compilazione e del pacchetto applicazione hello

1. Da hello `hbaseapp` directory di comando che segue hello utilizzare toobuild un file JAR contenente un'applicazione hello:

    ```bash
    mvn clean package
    ```

    Questo comando Compila e pacchetti hello applicazione in un file JAR.

2. Quando il comando hello viene completata, hello `hbaseapp/target` directory contiene un file denominato `hbaseapp-1.0-SNAPSHOT.jar`.

   > [!NOTE]
   > Hello `hbaseapp-1.0-SNAPSHOT.jar` file è un file jar uber. Contiene tutte le dipendenze necessarie toorun hello un'applicazione hello.


## <a name="upload-hello-jar-and-run-jobs-ssh"></a>Caricare hello JAR ed eseguire i processi (SSH)

Hello seguenti utilizzano `scp` toocopy hello JAR toohello head nodo primario dell'HBase in cluster HDInsight. Hello `ssh` comando viene quindi utilizzato tooconnect toohello cluster e di esecuzione l'esempio hello direttamente nel nodo head hello.

1. tooupload hello jar toohello cluster utilizzare hello comando seguente:

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    Sostituire `USERNAME` con nome hello dell'accesso SSH. Sostituire `CLUSTERNAME` con il nome del cluster HDInsight.

2. tooconnect toohello cluster HBase, utilizzare hello comando seguente:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Sostituire `USERNAME` nome hello dell'accesso SSH. Sostituire `CLUSTERNAME` con il nome del cluster HDInsight.

3. una tabella HBase tramite toocreate hello applicazione Java, utilizzare hello comando seguente:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    Il comando crea una nuova tabella HBase denominata **people** e la popola con i dati.

4. toosearch per gli indirizzi di posta elettronica memorizzati nella tabella di hello, utilizzare hello comando seguente:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    Viene visualizzato hello seguenti risultati:

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. tabella di hello toodelete, utilizzare hello comando seguente:

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a>Caricare hello JAR ed eseguire i processi (PowerShell)

Hello alla procedura seguente utilizza l'archiviazione di Azure PowerShell tooupload hello JAR toohello predefinita per il cluster HBase. Cmdlet di HDInsight vengono quindi utilizzati toorun hello esempi in modalità remota.

1. Dopo aver installato e configurato Azure PowerShell, creare un file denominato `hbase-runner.psm1`. Utilizzare hello segue testo come contenuto di hello di questo file:

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

    Questo file contiene due moduli:

   * **HDInsightFile aggiungere** : utilizzato cluster toohello di tooupload file
   * **Inizio HBaseExample** -toorun hello classi creato in precedenza

2. Salvare hello `hbase-runner.psm1` file.

3. Aprire una nuova finestra di PowerShell di Azure, modificare le directory toohello `hbaseapp` directory, e quindi eseguire hello finestra di comando seguente:

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    Modificare toohello percorso hello di hello `hbase-runner.psm1` file creato in precedenza. Questo comando registra modulo hello con Azure PowerShell.

4. Comando che segue di hello utilizzare hello tooupload `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    Sostituire `hdinsightclustername` con nome hello del cluster. comando Hello carica hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` percorso di archiviazione primaria di hello per il cluster.

5. una tabella utilizzando toocreate hello `hbaseapp`, utilizzare hello comando seguente:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    Sostituire `hdinsightclustername` con nome hello del cluster.

    Questo comando consente di creare una nuova tabella denominata **people** in HBase nel cluster HDInsight. Questo comando non visualizza alcun output nella finestra di console hello.

6. toosearch per le voci nella tabella di hello, utilizzare hello comando seguente:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    Sostituire `hdinsightclustername` con nome hello del cluster.

    Questo comando Usa hello `SearchByEmail` classe toosearch per tutte le righe in cui hello `contactinformation` famiglia di colonna e hello `email` colonna contiene la stringa hello `contoso.com`. Si dovrebbe ricevere hello seguenti risultati:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Utilizzando **fabrikam.com** per hello `-emailRegex` valore restituisce utenti hello che dispongono di **fabrikam.com** nel campo messaggio di posta elettronica hello. È inoltre possibile utilizzare espressioni regolari come termine di ricerca hello. Ad esempio, **^ r** restituisce di posta elettronica gli indirizzi che iniziano con la lettera hello 'r'.

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Nessun risultato o risultati imprevisti quando si usa Start-HBaseExample

Hello utilizzare `-showErr` parametro tooview hello standard errore (STDERR) che viene generato durante il processo di hello in esecuzione.

## <a name="delete-hello-table"></a>Eliminare la tabella hello

Una volta con l'esempio hello, utilizzare hello seguente hello toodelete **persone** tabella utilizzata in questo esempio:

__Da una sessione `ssh`__:

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

__Da Azure PowerShell__:

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a>Passaggi successivi

[Informazioni su come toouse SQL esce con HBase](hdinsight-hbase-phoenix-squirrel-linux.md)
