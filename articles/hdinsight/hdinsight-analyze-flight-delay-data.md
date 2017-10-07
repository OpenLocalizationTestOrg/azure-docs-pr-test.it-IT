---
title: dati del ritardo di volo aaaAnalyze con Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse uno Windows PowerShell script toocreate un cluster HDInsight, eseguire un processo Hive, eseguire un processo Sqoop ed eliminare cluster hello.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a>Analizzare i dati sui ritardi dei voli con Hive in HDInsight
Hive fornisce un metodo per l'esecuzione di processi MapReduce mediante un linguaggio di scripting simile a SQL, denominato *[HiveQL][hadoop-hiveql]*, che può essere applicato per attività di riepilogo, query e analisi di volumi di dati molto elevati.

> [!IMPORTANT]
> Hello passaggi in questo documento richiedono un cluster HDInsight basati su Windows. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Per i passaggi relativi a un cluster basato su Linux, vedere [Analizzare i dati sui ritardi dei voli con Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).

Uno dei vantaggi principali di hello di Azure HDInsight è la separazione di hello del calcolo e archiviazione dei dati. HDInsight usa l'archiviazione BLOB di Azure per l'archiviazione dei dati. Un tipico processo è costituito da tre parti:

1. **Archiviare dati nell'archivio BLOB di Azure:**  Ad esempio, i dati meteo, i dati dei sensori, i blog e, in questo caso, i dati sui ritardi dei voli vengono salvati nell'archivio BLOB.
2. **Eseguire i processi.** Quando si tratta di dati di ora tooprocess hello, si esegue uno script di Windows PowerShell (o un'applicazione client) toocreate un cluster HDInsight, eseguire i processi ed eliminare il cluster hello. processi di Hello Salva dati di output tooAzure nell'archiviazione Blob. dati di output di Hello viene mantenuti anche dopo l'eliminazione di cluster hello. In questo modo, l'utente paga solo in base al consumo effettivo.
3. **Recuperare l'output di hello dall'archiviazione Blob di Azure**, o l'esportazione di database SQL di Azure di hello dati tooan in questa esercitazione.

Hello seguente diagramma illustra uno scenario di hello e la struttura di hello di questa esercitazione:

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

Si noti che hello numeri nel diagramma hello corrispondono toohello i titoli di sezione. **M** è l'acronimo di processo principale hello. **Oggetto** è l'acronimo di contenuto hello nell'appendice hello.

parte principale di Hello dell'esercitazione hello viene illustrato come toouse uno Windows PowerShell script tooperform hello seguenti attività:

* Creare un cluster HDInsight
* Eseguire un processo Hive in Media ritardi di hello cluster toocalculate aeroporti. Hello flight delay vengono memorizzati in un account di archiviazione Blob di Azure.
* Eseguire un Sqoop processo tooexport hello Hive processo output tooan database SQL di Azure.
* Eliminare il cluster di HDInsight hello.

Nelle appendici hello, è possibile trovare istruzioni hello per il caricamento di dati di ritardo di volo, la creazione o il caricamento di una stringa di query Hive e preparazione dei database SQL di Azure hello per processo Sqoop hello.

> [!NOTE]
> passaggi di Hello in questo documento sono cluster HDInsight basati su tooWindows specifici. Per i passaggi relativi a un cluster basato su Linux, vedere [Analizzare i dati sui ritardi dei voli con Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)

### <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti elementi:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Workstation con Azure PowerShell**.

    > [!IMPORTANT]
    > Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** ed è stato rimosso dal 1° gennaio 2017. Hello passaggi in questo documento usa hello nuovi cmdlet di HDInsight che funzionano con Gestione risorse di Azure.
    >
    > Eseguire le operazioni di hello in [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello più recente di Azure PowerShell. Se si dispone di script che toobe necessità modificato toouse hello nuovi cmdlet che funzionano con Gestione risorse di Azure, vedere [di strumenti di migrazione tooAzure sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) per ulteriori informazioni.

**File usati in questa esercitazione**

Questa esercitazione viene utilizzato hello in prestazioni dei dati di volo airline da [Research e amministrazione tecnologia innovativa, Bureau delle statistiche di trasporto o RITA][rita-website].
Una copia di hello dati sono stati caricati tooan contenitore di archiviazione Blob di Azure con l'autorizzazione di accesso hello Blob pubblici.
Una parte dello script PowerShell copia i dati di hello dal contenitore di blob predefinito per la toohello contenitore hello blob pubblico del cluster. Hello HiveQL lo script è inoltre copiati toohello nello stesso contenitore di Blob.
Se si desidera toolearn come tooget/carica hello dati tooyour proprietari di account di archiviazione e come toocreate/carica hello HiveQL lo script di file, vedere [appendice](#appendix-a) e [appendice B](#appendix-b).

Hello nella tabella seguente sono elencati i file hello utilizzati in questa esercitazione:

<table border="1">
<tr><th>File</th><th>Descrizione</th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td>file di script HiveQL Hello utilizzato hello processo Hive. Questo script è stato caricato tooan account di archiviazione Blob di Azure con accesso pubblico hello. <a href="#appendix-b">Appendice B</a> include istruzioni sulla preparazione e sul caricamento di questo file tooyour un Blob di Azure account di archiviazione.</td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td>Dati di input per il processo Hive hello. dati Hello sono stato caricato tooan account di archiviazione Blob di Azure con accesso pubblico hello. <a href="#appendix-a">Appendice A</a> contiene istruzioni recupero di dati hello e il caricamento di hello dati tooyour un Blob di Azure account di archiviazione.</td></tr>
<tr><td>\tutorials\flightdelays\output</td><td>percorso di output di Hello per processo Hive hello. contenitore predefinito Hello viene utilizzato per archiviare i dati di output di hello.</td></tr>
<tr><td>\tutorials\flightdelays\jobstatus</td><td>Hello Hive processo stato cartella contenitore predefinito hello.</td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a>Creare cluster ed eseguire processi Hive/Sqoop
Per Hadoop MapReduce è prevista l'elaborazione batch. Hello toorun modo economico per la maggior parte un processo Hive è toocreate un cluster per il processo di hello ed eliminare il processo di hello dopo aver completato il processo di hello. Hello script riportato di seguito vengono illustrate intero processo hello.
Per altre informazioni sulla creazione di un cluster HDInsight e sull'esecuzione di processi Hive, vedere [Creare cluster Hadoop in HDInsight][hdinsight-provision] e [Usare Hive con HDInsight][hdinsight-use-hive].

**query Hive di hello toorun da Azure PowerShell**

1. Creare una tabella di database e hello SQL di Azure per l'output del processo Sqoop hello usando istruzioni hello in [appendice C](#appendix-c).
2. Aprire Windows PowerShell ISE ed eseguire lo script seguente hello:

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. La connessione a database SQL tooyour e vedere i ritardi dei voli Media in base alla città nella tabella AvgDelays hello:

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <a id="appendix-a"></a>Appendice A - caricamento volo ritardo dati tooAzure nell'archiviazione Blob
Caricamento dei file di dati hello e i file di script HiveQL hello (vedere [appendice B](#appendix-b)) richiede una pianificazione. idea Hello è il file di dati di toostore hello e file HiveQL hello prima di creare un cluster HDInsight e in esecuzione il processo di Hive hello. Sono disponibili due opzioni:

* **Utilizzare hello stesso account di archiviazione di Azure che verrà utilizzato dal cluster HDInsight hello come file system predefinito hello.** Poiché il cluster HDInsight hello avrà una chiave di accesso di account di archiviazione hello, non è necessario toomake modifiche aggiuntive.
* **Utilizzare un account di archiviazione di Azure diverso dal file system predefinito del cluster di HDInsight hello.** In caso di hello, è necessario modificare parte creazione hello di Windows PowerShell script trovato in hello [cluster HDInsight creare e esecuzione i processi Hive/Sqoop](#runjob) toolink hello account di archiviazione come un account di archiviazione aggiuntivo. Per istruzioni, vedere [Creare cluster Hadoop in HDInsight][hdinsight-provision]. cluster HDInsight Hello in grado di conoscere la chiave di accesso hello per hello account di archiviazione.

> [!NOTE]
> percorso di archiviazione Blob Hello per file di dati è hard-coded in file di script HiveQL hello hello. È necessario aggiornarlo di conseguenza.

**dati di volo hello toodownload**

1. Sfoglia troppo[Research e innovativa tecnologia amministrazione Bureau di statistiche trasporto][rita-website].
2. Nella pagina hello selezionare hello seguenti valori:

    <table border="1">
    <tr><th>Nome</th><th>Valore</th></tr>
    <tr><td>Filter Year</td><td>2013 </td></tr>
    <tr><td>Filter Period</td><td>January</td></tr>
    <tr><td>Fields</td><td>*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (deselezionare tutti gli altri campi)</td></tr>
    </table>
3. Fare clic su **Download**.
4. Decomprimere hello file toohello **C:\Tutorials\FlightDelay\2013Data** cartella. Ogni file è in formato CSV e ha dimensioni pari a circa 60 GB.
5. Rinominare hello file toohello del mese hello che contiene dati per. Ad esempio, verrebbe denominato file hello contenente i dati di gennaio hello *January.csv*.
6. Ripetere toodownload i passaggi 2 e 5 un file per ognuna delle hello in 2013 12 mesi. È necessario un minimo di un'esercitazione di hello toorun file.

**tooupload hello volo ritardo dati tooAzure nell'archiviazione Blob**

1. Preparare i parametri di hello:

    <table border="1">
    <tr><th>Nome variabile</th><th>Note</th></tr>
    <tr><td>$storageAccountName</td><td>account di archiviazione di Azure in cui si desidera tooupload hello dati Hello.</td></tr>
    <tr><td>$blobContainerName</td><td>contenitore Blob Hello in cui si desidera tooupload hello dati.</td></tr>
    </table>
2. Aprire Azure PowerShell ISE.
3. Incollare lo script seguente nel riquadro di script hello hello:

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. Premere **F5** script hello toorun.

Se si sceglie toouse un metodo diverso per il caricamento di file hello, verificare che il percorso di file hello è esercitazioni/flightdelay/data. sintassi di Hello per accedere ai file hello è:

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

percorso esercitazioni/flightdelay/dati Hello è hello virtuale creata durante il caricamento di file hello. Verificare che siano disponibili 12 file, uno per ogni mese.

> [!NOTE]
> È necessario aggiornare hello Hive query tooread dalla nuova posizione hello.
>
> È necessario configurare hello contenitore accesso autorizzazione toobe pubblico o associare toohello account di archiviazione hello cluster HDInsight. Stringa di query Hive hello in caso contrario, non sarà in grado di tooaccess i file di dati hello.

- - -

## <a id="appendix-b"></a>Appendice B: creare e caricare uno script HiveQL
Con Azure PowerShell, è possibile eseguire più istruzioni HiveQL uno alla volta oppure hello pacchetto HiveQL istruzione in un file di script. In questa sezione viene illustrato come uno script HiveQL toocreate hello caricamento script e tooAzure nell'archiviazione Blob tramite Azure PowerShell. Hive richiede hello HiveQL script toobe archiviati nell'archiviazione Blob di Azure.

Hello script HiveQL eseguirà seguente hello:

1. **Elimina tabella delays_raw hello**, nel caso in cui hello tabella esiste già.
2. **Creare una tabella hello delays_raw esterna Hive** che punta il percorso di archiviazione Blob toohello con i file di ritardo di hello volo. La query consente di specificare che i campi sono delimitati da "," e che le righe vengono interrotte da "\n". Poiché questo comportamento pone un problema quando i valori di campo contengono virgole perché Hive non è possibile distinguere tra una virgola, che è un delimitatore di campo e uno che fa parte di un valore del campo (caso hello nei valori dei campi per l'origine\_Città\_nome e destinazione\_ Città\_nome). tooaddress, hello query crea colonne TEMP toohold dati in modo non corretto sono suddiviso in colonne.
3. **Elimina tabella ritardi hello**, nel caso in cui hello tabella esiste già.
4. **Creare una tabella di ritardi hello**. È utile tooclean dei dati hello prima un'ulteriore elaborazione. Questa query crea una nuova tabella, *ritardi*, dalla tabella delays_raw hello. Si noti che le colonne TEMP hello (come indicato in precedenza) non vengono copiate e che hello **sottostringa** funzione è virgolette tooremove utilizzato dai dati hello.
5. **Calcolare hello weather medio ritardo e i gruppi hello risultati in base al nome di città.** Verranno inoltre visualizzate le archiviazione tooBlob di hello risultati. Si noti che eseguono query hello rimuoverà apostrofi dai dati hello ed escluderà le righe in cui il valore per hello **weather_delay** è null. Ciò è necessario perché Sqoop, usato più avanti nell'esercitazione, non è in grado di gestire correttamente tali valori per impostazione predefinita.

Per un elenco completo di comandi HiveQL hello, vedere [Hive Data Definition Language][hadoop-hiveql]. Ogni comando HiveQL deve terminare con un punto e virgola.

**un file di script HiveQL toocreate**

1. Preparare i parametri di hello:

    <table border="1">
    <tr><th>Nome variabile</th><th>Note</th></tr>
    <tr><td>$storageAccountName</td><td>account di archiviazione di Azure in cui si desidera tooupload hello HiveQL script Hello.</td></tr>
    <tr><td>$blobContainerName</td><td>contenitore Blob Hello in cui si desidera tooupload hello HiveQL script.</td></tr>
    </table>
2. Aprire Azure PowerShell ISE.
3. Copiare e incollare lo script seguente nel riquadro di script hello hello:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    Di seguito sono variabili hello utilizzate nello script hello:

   * **$hqlLocalFileName** -hello script Salva file di script HiveQL hello localmente prima di caricarlo tooBlob archiviazione. Questo è il nome di file hello. valore predefinito di Hello è <u>C:\tutorials\flightdelay\flightdelays.hql</u>.
   * **$hqlBlobName** -si tratta di hello HiveQL blob nome del file script utilizzato nell'archiviazione Blob di Azure hello. valore predefinito di Hello è tutorials/flightdelay/flightdelays.hql. Poiché verrà scritto il file hello direttamente tooAzure nell'archiviazione Blob, non c'è un "/" all'inizio di hello del nome blob hello. Se si desidera tooaccess hello file dall'archiviazione Blob, è necessario tooadd un "/" all'inizio di hello del nome file hello.
   * **$srcDataFolder** e **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"

- - -
## <a id="appendix-c"></a>Appendice C - preparare un database SQL di Azure per l'output del processo Sqoop hello
**database SQL di hello tooprepare (di tipo merge questo con hello Sqoop script)**

1. Preparare i parametri di hello:

    <table border="1">
    <tr><th>Nome variabile</th><th>Note</th></tr>
    <tr><td>$sqlDatabaseServerName</td><td>nome di Hello del server di database SQL di Azure hello. Immettere nulla toocreate un nuovo server.</td></tr>
    <tr><td>$sqlDatabaseUsername</td><td>nome dell'account Hello per server di database SQL di Azure hello. Se $sqlDatabaseServerName è un server esistente, hello account e la password di account di accesso sono utilizzati tooauthenticate con server hello. In caso contrario sono toocreate utilizzato un nuovo server.</td></tr>
    <tr><td>$sqlDatabasePassword</td><td>password di accesso Hello per server di database SQL di Azure hello.</td></tr>
    <tr><td>$sqlDatabaseLocation</td><td>Questo valore viene usato solo durante la creazione di un nuovo server di database di Azure.</td></tr>
    <tr><td>$sqlDatabaseName</td><td>database SQL Hello utilizzato nella tabella AvgDelays hello toocreate per processo Sqoop hello. Lasciando il valore vuoto, verrà creato un database denominato "HDISqoop". nome della tabella per l'output del processo Sqoop hello Hello è AvgDelays. </td></tr>
    </table>
2. Aprire Azure PowerShell ISE.
3. Copiare e incollare lo script seguente nel riquadro di script hello hello:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > Hello script Usa un servizio di stato representational transfer (REST), http://bot.whatismyipaddress.com, tooretrieve l'indirizzo IP esterno. indirizzo IP di Hello viene utilizzato per la creazione di una regola del firewall per il server di database SQL.

    Ecco alcune variabili utilizzate nello script hello:

   * **$ipAddressRestService** -hello predefinita è http://bot.whatismyipaddress.com. È un servizio REST per l'indirizzo IP pubblico che consente di ottenere l'indirizzo IP esterno. È anche possibile usare altri servizi. indirizzo IP esterno Hello recuperato tramite il servizio hello sarà toocreate utilizzata una regola del firewall per il server di database SQL di Azure, in modo che è possibile accedere ai database hello dalla propria workstation (usando uno script di Windows PowerShell).
   * **$fireWallRuleName** -nome hello hello regola del firewall per server di database SQL di Azure hello. nome predefinito Hello è <u>FlightDelay</u>. È anche possibile rinominarla.
   * **$sqlDatabaseMaxSizeGB** : questo valore viene usato solo durante la creazione di un nuovo server di database SQL di Azure. valore predefinito di Hello è 10GB. sufficiente per questa esercitazione.
   * **$sqlDatabaseName** : questo valore viene usato solo durante la creazione di un nuovo database SQL di Azure. valore predefinito di Hello è HDISqoop. Se si rinomina il, è necessario aggiornare di conseguenza script di Windows PowerShell di Sqoop hello.
4. Premere **F5** script hello toorun.
5. Convalidare l'output di hello dello script. Verificare che lo script hello è stato eseguito correttamente.

## <a id="nextsteps"></a> Passaggi successivi
Dopo aver compreso come tooupload tooAzure un file nell'archiviazione Blob, come un Hive toopopulate tabella utilizzando i dati di hello dall'archiviazione Blob di Azure, come toorun Hive query e come toouse Sqoop tooexport dati dal database di SQL Azure tooan HDFS. toolearn informazioni, vedere hello seguenti articoli:

* [Introduzione a HDInsight][hdinsight-get-started]
* [Usare Hive con HDInsight][hdinsight-use-hive]
* [Usare Oozie con HDInsight][hdinsight-use-oozie]
* [Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]
* [Usare Pig con HDInsight][hdinsight-use-pig]
* [Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-mapreduce]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
