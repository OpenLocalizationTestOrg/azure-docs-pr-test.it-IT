---
title: aaaUse basati sul tempo coordinator Hadoop Oozie in HDInsight | Documenti Microsoft
description: Usare il coordinatore Oozie di Hadoop basato sul tempo in HDInsight, un servizio per Big Data. Informazioni su come toodefine Oozie coordinatori e flussi di lavoro e inviare i processi.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a>Utilizzare basati sul tempo coordinator Oozie con Hadoop in HDInsight toodefine flussi di lavoro e coordinare i processi
In questo articolo si apprenderà come flussi di lavoro toodefine e coordinatori e come tootrigger hello processi coordinatore, basati sul tempo. È utile toogo tramite [utilizzare Oozie con HDInsight] [ hdinsight-use-oozie] prima di leggere questo articolo. Inoltre tooOozie, è inoltre possibile pianificare i processi tramite Azure Data Factory. toolearn Data Factory di Azure, vedere [usare Pig e Hive con Data Factory](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> Questo articolo richiede un cluster HDInsight basato su Windows. Per informazioni sull'utilizzo di Oozie, inclusi i processi basati sul tempo, in un cluster basato su Linux, vedere [utilizzare Oozie con Hadoop toodefine ed eseguire un flusso di lavoro in HDInsight basati su Linux](hdinsight-use-oozie-linux-mac.md)

## <a name="what-is-oozie"></a>Informazioni su Oozie
Apache Oozie è un sistema di flusso di lavoro/coordinamento che consente di gestire i processi Hadoop. È integrato con lo stack di Hadoop hello e supporta i processi Hadoop MapReduce Apache, Pig Apache, Apache Hive e Sqoop Apache. Può essere anche i processi utilizzati tooschedule sistema tooa specifico, ad esempio programmi Java o gli script della shell.

Hello immagine seguente mostra del flusso di lavoro hello che verrà implementata:

![Diagramma del flusso di lavoro][img-workflow-diagram]

flusso di lavoro di Hello contiene due azioni:

1. Un'azione di Hive viene eseguito un hello toocount di script HiveQL le occorrenze di ogni tipo di livello di registrazione in un file di registro log4j. Ogni log log4j è costituita da una riga di campi che contiene un [LOG livello] campo tooshow hello hello e tipo di gravità, ad esempio:

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    output dello script Hive Hello è simile a:

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    Per altre informazioni su Hive, vedere [Usare Hive con HDInsight][hdinsight-use-hive].
2. Un'azione Sqoop Esporta tabella tooa output hello HiveQL azioni in un database SQL di Azure. Per altre informazioni su Sqoop, vedere [Usare Sqoop con HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Per le versioni Oozie supportate nei cluster HDInsight, vedere [novità introdotta nelle versioni di cluster hello fornite da HDInsight?] [hdinsight-versions].
>
>

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:

* **Workstation con Azure PowerShell**.

    > [!IMPORTANT]
    > Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** e verrà rimosso dal 1° gennaio 2017. Hello passaggi in questo documento usa hello nuovi cmdlet di HDInsight che funzionano con Gestione risorse di Azure.
    >
    > Eseguire le operazioni di hello in [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello più recente di Azure PowerShell. Se si dispone di script che toobe necessità modificato toouse hello nuovi cmdlet che funzionano con Gestione risorse di Azure, vedere [di strumenti di migrazione tooAzure sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) per ulteriori informazioni.

* **Un cluster HDInsight**. Per informazioni sulla creazione di un cluster HDInsight, vedere [Creare cluster HDInsight][hdinsight-provision] o [Introduzione a HDInsight][hdinsight-get-started]. È necessario hello toogo dati esercitazione hello seguenti:

    <table border = "1">
    <tr><th>Proprietà del cluster</th><th>Nome variabile di Windows PowerShell</th><th>Valore</th><th>Descrizione</th></tr>
    <tr><td>Nome del cluster HDInsight</td><td>$clusterName</td><td></td><td>cluster HDInsight Hello in cui verrà eseguito in questa esercitazione.</td></tr>
    <tr><td>Nome utente del cluster HDInsight</td><td>$clusterUsername</td><td></td><td>nome utente del cluster HDInsight Hello. </td></tr>
    <tr><td>Password utente del cluster HDInsight </td><td>$clusterPassword</td><td></td><td>password dell'utente del cluster HDInsight Hello.</td></tr>
    <tr><td>Nome dell'account di archiviazione di Azure</td><td>$storageAccountName</td><td></td><td>Un cluster di HDInsight toohello disponibili account di archiviazione di Azure. Per questa esercitazione, utilizzare l'account di archiviazione hello predefinito specificato durante il processo di provisioning di cluster hello.</td></tr>
    <tr><td>Nome del contenitore BLOB di Azure</td><td>$containerName</td><td></td><td>Per questo esempio, utilizzare il contenitore di archiviazione Blob di Azure hello utilizzata per file system cluster HDInsight di hello predefinito. Per impostazione predefinita, ha hello stesso nome del cluster HDInsight hello.</td></tr>
    </table>
* **Un database SQL di Azure**. È necessario configurare una regola del firewall per l'accesso al Database di SQL server tooallow hello dalla propria workstation. Per istruzioni sulla creazione di un database SQL di Azure e configurazione di firewall hello, vedere [iniziare a usare database SQL di Azure] [sqldatabase-get-avviato]. In questo articolo fornisce uno script di Windows PowerShell per la creazione di tabella di database SQL di Azure hello che è necessario per questa esercitazione.

    <table border = "1">
    <tr><th>Proprietà del database SQL</th><th>Nome variabile di Windows PowerShell</th><th>Valore</th><th>Descrizione</th></tr>
    <tr><td>Nome del server di database SQL</td><td>$sqlDatabaseServer</td><td></td><td>Hello SQL database server toowhich Sqoop esporterà i dati. </td></tr>
    <tr><td>Nome di accesso al database SQL</td><td>$sqlDatabaseLogin</td><td></td><td>Il nome di accesso al database SQL.</td></tr>
    <tr><td>Password di accesso al database SQL</td><td>$sqlDatabaseLoginPassword</td><td></td><td>La password di accesso al database SQL.</td></tr>
    <tr><td>Nome del database SQL</td><td>$sqlDatabaseName</td><td></td><td>Hello Azure SQL database toowhich Sqoop esporterà i dati. </td></tr>
    </table>

  > [!NOTE]
  > Per impostazione predefinita, un database SQL di Azure consente connessioni da servizi di Azure, ad esempio Azure HDinsight. Se questa impostazione del firewall è disabilitata, è necessario abilitarlo dal portale di Azure hello. Per istruzioni sulla creazione di un database SQL e sulla configurazione di regole del firewall, vedere [Creare e configurare un database SQL][sqldatabase-get-started].

> [!NOTE]
> Valori hello di riempimento nelle tabelle di hello. potrà essere utile per completare questa esercitazione.

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a>Definire Oozie del flusso di lavoro e hello script HiveQL correlato
Le definizioni dei flussi di lavoro di Oozie sono scritte in linguaggio hPDL (XML Process Definition Language). nome del file di flusso di lavoro predefinito Hello *workflow*.  Si verrà salvare file in locale di hello del flusso di lavoro e quindi distribuirlo cluster HDInsight toohello tramite Azure PowerShell più avanti in questa esercitazione.

Hello Hive azione nel flusso di lavoro hello chiama un file di script HiveQL. che contiene tre istruzioni HiveQL:

1. **istruzione DROP TABLE Hello** eliminazioni hello tabella Hive log4j se esiste.
2. **istruzione CREATE TABLE Hello** crea una tabella esterna di Hive log4j, che fa riferimento toohello percorso del file di log log4j hello.
3. **percorso del file di registro log4j hello Hello**. delimitatore di campo Hello è ",". delimitatore di riga Hello predefinito è "\n". Una tabella esterna Hive è tooavoid utilizzato i file di dati di hello viene rimosso dalla posizione originale hello, nel caso in cui si desidera del flusso di lavoro di toorun hello Oozie più volte.
4. **istruzione INSERT SOVRASCRIVERE Hello** conta le occorrenze di hello di ogni tipo di log a livello di tabella Hive log4j hello e Salva percorso di archiviazione Blob di Azure tooan output hello.

> [!NOTE]
> Il percorso di Hive è caratterizzato da un problema noto che si verifica durante l'invio di un processo Oozie. Hello istruzioni per risoluzione hello problema sono disponibili su TechNet Wiki hello: [Hive di HDInsight errore: Impossibile toorename][technetwiki-hive-error].

**chiamato dal flusso di lavoro hello toodefine hello HiveQL script file toobe**

1. Creare un file di testo con hello seguente contenuto:

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    Esistono tre variabili utilizzate nello script hello:

   * ${hiveTableName}
   * ${hiveDataFolder}
   * ${hiveOutputFolder}

     file di definizione del flusso di lavoro Hello (workflow in questa esercitazione) passerà questi toothis valori script HiveQL in fase di esecuzione.
2. Salvare il file hello come **C:\Tutorials\UseOozie\useooziewf.hql** utilizzando la codifica ANSI (ASCII). Usare il blocco note se l'editor di testo non offre questa opzione. Questo file di script sarà cluster HDInsight toohello distribuito in un secondo momento nell'esercitazione di hello.

**toodefine un flusso di lavoro**

1. Creare un file di testo con hello seguente contenuto:

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    Esistono due azioni definite nel flusso di lavoro hello. start-tooaction Hello è *RunHiveScript*. Se viene eseguito l'azione di hello *OK*, azione successiva hello è *RunSqoopExport*.

    Hello RunHiveScript ha diverse variabili. I valori hello verrà passato quando si invia il processo di Oozie hello dalla propria workstation con Azure PowerShell.

    Variabili del flusso di lavoro

    <table border = "1">
    <tr><th>Variabili del flusso di lavoro</th><th>Descrizione</th></tr>
    <tr><td>${jobTracker}</td><td>Specificare l'URL di hello di gestione di processi Hadoop hello. Usare <strong>jobtrackerhost:9010</strong> nel cluster HDInsight versione 3.0 e 2.0.</td></tr>
    <tr><td>${nameNode}</td><td>Specificare l'URL di hello del nodo del nome hello Hadoop. Utilizzare hello predefinito file system wasb: / / l'indirizzo, ad esempio, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. n e t</i>.</td></tr>
    <tr><td>${queueName}</td><td>Specifica del nome della coda hello hello processo verrà inviato a. Usare l'<strong>impostazione predefinita</strong>.</td></tr>
    </table>

    Variabili dell'azione Hive

    <table border = "1">
    <tr><th>Variabile azione Hive</th><th>Descrizione</th></tr>
    <tr><td>${hiveDataFolder}</td><td>directory di origine Hello per hello comando Hive Create Table.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>cartella di output di Hello per hello istruzione INSERT SOVRASCRIVERE.</td></tr>
    <tr><td>${hiveTableName}</td><td>nome Hello della tabella Hive hello che fa riferimento a file di dati log4j hello.</td></tr>
    </table>

    Variabili dell'azione Sqoop

    <table border = "1">
    <tr><th>Variabile azione Sqoop</th><th>Descrizione</th></tr>
    <tr><td>${sqlDatabaseConnectionString}</td><td>Stringa di connessione del database SQL.</td></tr>
    <tr><td>${sqlDatabaseTableName}</td><td>verrà esportato Hello dati hello toowhere tabella del database SQL di Azure.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>cartella di output di Hello per hello istruzione INSERT SOVRASCRIVERE l'Hive. Si tratta di hello stessa cartella per l'esportazione Sqoop hello (esportazione-dir).</td></tr>
    </table>

    Per ulteriori informazioni sulla Oozie del flusso di lavoro e l'utilizzo di azioni del flusso di lavoro hello, vedere [documentazione di Apache Oozie 4.0] [ apache-oozie-400] (per la versione del cluster HDInsight 3.0) o [Oozie Apache 3.3.2 documentazione] [ apache-oozie-332] (per la versione del cluster HDInsight 2.1).

1. Salvare il file hello come **C:\Tutorials\UseOozie\workflow.xml** utilizzando la codifica ANSI (ASCII). Usare il blocco note se l'editor di testo non offre questa opzione.

**coordinatore toodefine**

1. Creare un file di testo con hello seguente contenuto:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    Esistono cinque variabili utilizzate nel file di definizione hello:

   | Variabile | Descrizione |
   | --- | --- |
   | ${coordFrequency} |Tempo di sospensione del processo. La frequenza è sempre espressa in minuti. |
   | ${coordStart} |Ora di inizio del processo. |
   | ${coordEnd} |Ora di fine del processo. |
   | ${coordTimezone} |Oozie elabora i processi del coordinatore in un fuso orario predefinito che non tiene conto dell'ora legale (in genere rappresentato dall'acronimo UTC). Il fuso orario viene definito come hello "Oozie elaborazione fuso orario." |
   | ${wfPath} |percorso Hello hello workflow.  Se non nome del file del flusso di lavoro hello è nome del file hello predefinito (workflow), è necessario specificarlo. |
2. Salvare il file hello come **C:\Tutorials\UseOozie\coordinator.xml** usando la codifica ANSI (ASCII) hello. Usare il blocco note se l'editor di testo non offre questa opzione.

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a>Distribuire il progetto di Oozie hello e preparare l'esercitazione hello
Eseguire un esempio di hello tooperform script Azure PowerShell:

* Hello copia nell'archiviazione Blob tooAzure script (useoozie.hql) HiveQL, wasb:///tutorials/useoozie/useoozie.hql.
* Copiare toowasb:///tutorials/useoozie/workflow.xml workflow.
* Copiare coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.
* File di dati di Windows hello (o example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.
* Creare una tabella di database SQL di Azure per l'archiviazione dei dati di esportazione di Sqoop. nome della tabella Hello *log4jLogCount*.

**Informazioni sull'archiviazione in HDInsight**

HDInsight usa l'archiviazione BLOB di Azure per l'archiviazione dei dati. wasb: / / è l'implementazione Microsoft di hello file system distribuito Hadoop (HDFS) nell'archiviazione Blob di Azure. Per altre informazioni, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage].

Quando si esegue il provisioning di un cluster HDInsight, un account di archiviazione Blob di Azure e un contenitore specifico da tale account viene designato come hello predefiniti del file system, ad esempio in HDFS. In account di archiviazione toothis, è inoltre possibile aggiungere ulteriore spazio di archiviazione di account da hello stessa sottoscrizione di Azure o da diverse sottoscrizioni di Azure durante il processo di provisioning hello. Per istruzioni sull'aggiunta di altri account di archiviazione, vedere [Effettuare il provisioning di cluster HDInsight][hdinsight-provision]. script di PowerShell Azure hello toosimplify utilizzati in questa esercitazione, tutti i file vengono archiviati nel contenitore di sistema di hello predefinito file hello posizione *esercitazioni/useoozie*. Per impostazione predefinita, questo contenitore comprende hello stesso nome come nome del cluster HDInsight hello.
sintassi di Hello è:

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> Solo hello *wasb: / /* sintassi è supportata nella versione 3.0 del cluster HDInsight. Hello precedente *asv: / /* sintassi è supportata in HDInsight 2.1 e 1.6 cluster, ma non è supportata nei cluster di HDInsight 3.0.
>
> Hello wasb: / / percorso è un percorso virtuale. Per altre informazioni, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage].

Un file che viene archiviato nel contenitore di sistema di hello predefinito file è possibile accedere da HDInsight utilizzando uno dei seguenti URI (ad esempio utilizzando workflow) hello:

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

Se si desidera file hello tooaccess direttamente dall'account di archiviazione hello, nome blob hello file hello è:

    tutorials/useoozie/workflow.xml

**Informazioni sulle tabelle interne ed esterne di Hive**

Esistono alcuni aspetti, è necessario tooknow sulle tabelle interne ed esterne di Hive:

* Hello comando CREATE TABLE crea una tabella interna, noto anche come una tabella gestita. file di dati Hello deve trovarsi nel contenitore predefinito hello.
* comando CREATE TABLE Hello sposta dati hello filetoohello/hive/warehouse/<TableName> cartella nel contenitore predefinito hello.
* Hello comando CREATE EXTERNAL TABLE crea una tabella esterna. file di dati Hello può trovarsi all'esterno di contenitore predefinito hello.
* Hello comando CREATE EXTERNAL TABLE non sposta i file di dati hello.
* Hello comando CREATE EXTERNAL TABLE non consente sottocartelle nella cartella hello specificato nella clausola percorso hello. Questo è il motivo di hello perché esercitazione hello crea una copia del file sample.log hello.

Per altre informazioni, vedere [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables] (HDInsight: introduzione alle tabelle Hive interne ed esterne).

**esercitazione hello tooprepare**

1. Hello aprire Windows PowerShell ISE (nella schermata iniziale di Windows 8 hello digitare **PowerShell_ISE**, quindi fare clic su **Windows PowerShell ISE**. Per altre informazioni, vedere [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Avviare Windows PowerShell in Windows 8 e Windows).
2. Nel riquadro inferiore hello eseguire hello successivo comando tooconnect tooyour sottoscrizione di Azure:

    ```powershell
    Add-AzureAccount
    ```

    Si sarà tooenter richieste le credenziali dell'account Azure. Questo metodo di aggiunta di una connessione di sottoscrizione scade e dopo 12 ore, si disporrà di cmdlet hello toorun nuovamente.

   > [!NOTE]
   > Se si dispone di più sottoscrizioni di Azure e sottoscrizione predefinita hello non è hello quello desiderato toouse, utilizzare hello <strong>Select-AzureSubscription</strong> tooselect cmdlet una sottoscrizione.

3. Copiare lo script seguente nel riquadro di script hello hello e quindi impostare le variabili primi sei hello:

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    Per ulteriori descrizioni delle variabili di hello, vedere hello [prerequisiti](#prerequisites) sezione in questa esercitazione.

4. Aggiungere hello toohello lo script nel riquadro di script hello seguente:

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. Fare clic su **Esegui Script** o premere **F5** script hello toorun. output di Hello sarà simile a:

    ![Output delle operazioni preliminari all'esercitazione][img-preparation-output]

## <a name="run-hello-oozie-project"></a>Eseguire il progetto di Oozie hello
Attualmente Azure PowerShell non fornisce alcun cmdlet per la definizione dei processi Oozie. È possibile utilizzare hello **Invoke-RestMethod** cmdlet tooinvoke Oozie i servizi web. API dei servizi web di Hello Oozie è un'API di HTTP REST JSON. Per ulteriori informazioni sui servizi web di hello Oozie API, vedere [documentazione di Apache Oozie 4.0] [ apache-oozie-400] (per la versione del cluster HDInsight 3.0) o [documentazione di Apache Oozie 3.3.2] [ apache-oozie-332] (per la versione del cluster HDInsight 2.1).

**un processo di Oozie toosubmit**

1. Hello aprire Windows PowerShell ISE (nella schermata iniziale di Windows 8 digitare **PowerShell_ISE**, quindi fare clic su **Windows PowerShell ISE**. Per altre informazioni, vedere [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Avviare Windows PowerShell in Windows 8 e Windows).
2. Lo script seguente di hello di copia nel riquadro di script hello e quindi set hello innanzitutto quattordici variabili (tuttavia, ignorare **$storageUri**).

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    Per ulteriori descrizioni delle variabili di hello, vedere hello [prerequisiti](#prerequisites) sezione in questa esercitazione.

    $coordstart e $coordend sono l'avvio del flusso di lavoro di hello e l'ora di fine. toofind ora UTC o GMT hello, cercare "utc ora" bing.com. Hello $coordFrequency è la frequenza in minuti che toorun hello flusso di lavoro.
3. Aggiungere lo script toohello seguente hello. Questa parte definisce payload Oozie hello:

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > file di payload invio del flusso di lavoro toohello differenza principale rispetto Hello è variabile hello **oozie.coord.application.path**. Quando si invia un processo del flusso di lavoro si usa invece la variabile **oozie.wf.application.path** .

4. Aggiungere lo script toohello seguente hello. Questa parte Controlla stato del servizio web Oozie hello:

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. Aggiungere lo script toohello seguente hello. Questa parte consente di creare un processo Oozie:

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > Quando si invia un processo del flusso di lavoro, è necessario effettuare un altro processo di hello toostart web servizio chiamata dopo hello processo viene creato. In questo caso, il processo di coordinatore hello viene attivato da ora. processo Hello verrà avviato automaticamente.

6. Aggiungere lo script toohello seguente hello. Questa parte controlla lo stato del processo Oozie hello:

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. (Facoltativo) Aggiungere lo script toohello seguente hello.

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. Aggiungere hello toohello script seguente:

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    Rimuovere i segni # hello se si desidera toorun hello altre funzioni.
9. Se si usa la versione 2.1 del cluster HDinsight, sostituire "https://$clusterName.azurehdinsight.net:443/oozie/v2/" con "https://$clusterName.azurehdinsight.net:443/oozie/v1/". Versione del cluster HDInsight 2.1 non non supporta la versione 2 di servizi web hello.
10. Fare clic su **Esegui Script** o premere **F5** script hello toorun. output di Hello sarà simile a:

     ![Output dell'esecuzione del flusso di lavoro nell'esercitazione][img-runworkflow-output]
11. Connettersi tooyour dati del Database SQL toosee hello esportata.

**log degli errori di processo hello toocheck**

tootroubleshoot un flusso di lavoro, file di log Oozie hello è reperibile in C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log dal nodo head del cluster di hello. Per informazioni su RDP, vedere [cluster HDInsight amministrazione mediante hello Azure portal][hdinsight-admin-portal].

**esercitazione hello toorerun**

flusso di lavoro hello toorerun, è necessario eseguire hello seguenti attività:

* Eliminare i file di output di hello Hive script.
* Eliminare i dati di hello nella tabella log4jLogsCount hello.

Di seguito è riportato un esempio di script di Windows PowerShell che è possibile usare:

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, si è appreso come toodefine un flusso di lavoro Oozie e un coordinatore Oozie e come toorun un coordinatore Oozie processo usando Azure PowerShell. toolearn informazioni, vedere hello seguenti articoli:

* [Introduzione a HDInsight][hdinsight-get-started]
* [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage]
* [Amministrare HDInsight con Azure PowerShell][hdinsight-admin-powershell]
* [Caricare dati tooHDInsight][hdinsight-upload-data]
* [Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]
* [Usare Hive con HDInsight][hdinsight-use-hive]
* [Usare Pig con HDInsight][hdinsight-use-pig]
* [Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-java-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
