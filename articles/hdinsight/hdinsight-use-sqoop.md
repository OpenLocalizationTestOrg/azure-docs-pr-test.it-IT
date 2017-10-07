---
title: aaaRun Sqoop Apache processi con Azure HDInsight (Hadoop) | Documenti Microsoft
description: Informazioni su come toouse Azure PowerShell da un toorun workstation Sqoop importare ed esportare tra un cluster Hadoop e un database SQL di Azure.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a>Usare Sqoop con Hadoop in HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Informazioni su come toouse Sqoop in HDInsight tooimport ed Esporta tra cluster HDInsight e database SQL di Azure o database di SQL Server.

Anche se Hadoop è una scelta naturale per l'elaborazione dei dati non strutturati e semistrutturati, ad esempio i registri e file, è inoltre possibile un necessità tooprocess strutturato i dati archiviati nei database relazionali.

[Sqoop] [ sqoop-user-guide-1.4.4] è un tootransfer strumento progettato dati tra i cluster Hadoop e database relazionali. È possibile utilizzarlo tooimport dati da un sistema di gestione di database relazionali (RDBMS) ad esempio SQL Server, MySQL o Oracle in hello distributed file system Hadoop (HDFS), la trasformazione dei dati di hello in Hadoop MapReduce o Hive e quindi esportare i dati hello in un RDBMS. In questa esercitazione si userà un database SQL Server per il database relazionale.

Per le versioni Sqoop che sono supportate nei cluster HDInsight, vedere [novità introdotta nelle versioni di cluster hello fornite da HDInsight?][hdinsight-versions]

## <a name="understand-hello-scenario"></a>Comprendere scenario hello

Il cluster HDInsight include alcuni dati di esempio. Utilizzare hello due esempi seguenti:

* Un file di log log4j presente in */example/data/sample.log*. Hello seguenti registri viene estratti dal file hello:
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* Una tabella Hive denominata *hivesampletable*, che i riferimenti hello file di dati si trova in */hive/warehouse/hivesampletable*. tabella Hello contiene alcuni dati del dispositivo mobile. 
  
  | Campo | Tipo di dati |
  | --- | --- |
  | clientid |string |
  | querytime |string |
  | market |string |
  | deviceplatform |string |
  | devicemake |string |
  | devicemodel |string |
  | state |string |
  | country |string |
  | querydwelltime |double |
  | sessionid |bigint |
  | sessionpagevieworder |bigint |

Esportare innanzitutto *sample.log* e *hivesampletable* toohello Azure SQL database o tooSQL Server e quindi Importa hello tabella che contiene i dati dei dispositivi mobili hello eseguire il backup tooHDInsight utilizzando hello percorso seguente:

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a>Creare un cluster e un database SQL
In questa sezione viene illustrato come toocreate un cluster, un Database SQL e schemi di database SQL di hello per l'utilizzo in esecuzione di esercitazione hello hello portale di Azure e un modello di gestione risorse di Azure. Hello è reperibile [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/). il modello di gestione risorse di Hello chiama un database di tooSQL di bacpac pacchetto toodeploy hello tabella schemi.  pacchetto bacpac Hello si trova in un contenitore di blob pubblici, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac. Se si desidera toouse un contenitore privato per i file bacpac hello, utilizzare hello valori hello modello seguente:
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

Se si preferisce toouse Azure PowerShell toocreate hello cluster e hello Database SQL, vedere [appendice](#appendix-a---a-powershell-sample).

1. Fare clic su hello seguente immagine tooopen un modello di gestione risorse di hello portale di Azure.         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. Immettere hello le proprietà seguenti:

    - **Sottoscrizione**: immettere una sottoscrizione di Azure.
    - **Gruppo di risorse**: creare un nuovo gruppo di risorse di Azure o selezionarne uno esistente.  Un gruppo di risorse viene usato per finalità di gestione  come contenitore per gli oggetti.
    - **Località**: selezionare un'area.
    - **ClusterName**: immettere un nome per un cluster Hadoop hello.
    - **Nome account di accesso e la password del cluster**: nome di account di accesso predefinito di hello è amministratore.
    - **Nome utente e password SSH**.
    - **SQL database server login name and password**(Nome utente e password di accesso al server di database SQL).
    - **percorso _artifacts**: utilizzare il valore di predefinito hello, a meno che non si desidera toouse file backpac in un percorso diverso.
    - **_artifacts Location Sas Token** (_Token di firma di accesso condiviso posizione elementi): lasciare vuoto.
    - **Nome del File Bacpac**: utilizzare il valore di predefinito hello, a meno che non si desidera toouse backpac un file personalizzato.
     
     Hello i valori seguenti è hardcoded nella sezione variabili hello:
     
     | Nome dell'account di archiviazione predefinito | <CluterName>archivio |
     | --- | --- |
     | Nome server del database SQL di Azure |<ClusterName>dbserver |
     | Nome del database SQL di Azure |<ClusterName>db |
     
     Annotare questi valori.  È necessario più avanti nell'esercitazione di hello.

3. fare clic su **OK** parametri hello toosave.

4 da hello **distribuzione personalizzata** pannello, fare clic su **gruppo di risorse** elenco a discesa e quindi scegliere **New** toocreate un nuovo gruppo di risorse. gruppo di risorse Hello è un contenitore che raggruppa i cluster di hello, account di archiviazione dipendenti hello e altre risorse collegate.

5. Fare clic su **Note legali** e quindi su **Crea**.

6. Fare clic su **Crea**. Viene visualizzato un nuovo riquadro denominato Invio della distribuzione per Distribuzione modello. Richiede circa cluster hello toocreate di circa 20 minuti e il database SQL.

Se si sceglie di database SQL di Azure esistente toouse o Microsoft SQL Server

* **Database SQL di Azure**: È necessario configurare una regola del firewall per l'accesso di SQL Azure database server tooallow hello dalla propria workstation. Per istruzioni sulla creazione di un database SQL di Azure e configurazione di firewall hello, vedere [iniziare a usare database SQL di Azure][sqldatabase-get-started]. 
  
  > [!NOTE]
  > Per impostazione predefinita, un database SQL di Azure consente connessioni da servizi di Azure, ad esempio Azure HDinsight. Se questa impostazione del firewall è disabilitata, è necessario tooenable dal portale di Azure hello. Per istruzioni sulla creazione di un database SQL di Azure e sulla configurazione di regole del firewall, vedere l'articolo su come [creare e configurare un database SQL][sqldatabase-create-configue].
  > 
  > 
* **SQL Server**: se il cluster HDInsight su hello stessa rete virtuale in Azure come SQL Server, è possibile utilizzare i passaggi di hello in questo articolo tooimport ed esportazione dati tooa database di SQL Server.
  
  > [!NOTE]
  > HDInsight supporta solo reti virtuali basate sulla posizione e attualmente non funziona con le reti virtuali basate su gruppi di affinità.
  > 
  > 
  
  * toocreate e configurare una rete virtuale, vedere [creare una rete virtuale usando il portale di Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    
    * Quando si utilizza SQL Server nel Data Center, è necessario configurare la rete virtuale di hello come *site-to-site* o *point-to-site*.
      
      > [!NOTE]
      > Per **point-to-site** reti virtuali, SQL Server devono essere in esecuzione il client VPN di hello applicazione di configurazione, è disponibile da hello **Dashboard** della configurazione di rete virtuale di Azure.
      > 
      > 
    * Quando si utilizza SQL Server in una macchina virtuale di Azure, è possibile utilizzare qualsiasi configurazione di rete virtuale se macchina virtuale hello che ospita SQL Server è un membro di hello stessa rete virtuale di HDInsight.
  * toocreate un cluster HDInsight in una rete virtuale, vedere [cluster creare Hadoop in HDInsight mediante le opzioni personalizzate](hdinsight-hadoop-provision-linux-clusters.md)
    
    > [!NOTE]
    > SQL Server deve sempre consentire l'autenticazione. È necessario utilizzare un Server SQL hello toocomplete account di accesso i passaggi in questo articolo.
    > 
    > 

## <a name="run-sqoop-jobs"></a>Eseguire processi Sqoop
HDInsight è in grado di eseguire processi Sqoop in vari modi. Utilizzare hello seguente toodecide tabella quale metodo si adatta alle proprie esigenze, quindi seguire il collegamento hello per una procedura dettagliata.

| **Usare questo** se si desidera... | ...una shell **interattiva** | ...elaborazione**batch** | ...con questo **sistema operativo cluster** | ...da questo **sistema operativo client** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-use-sqoop-mac-linux.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X o Windows |
| [.NET SDK per Hadoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |✔ |Linux o Windows |Windows (per ora) |
| [Azure PowerShell](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |✔ |Linux o Windows |Windows |

## <a name="limitations"></a>Limitazioni
* Eseguire l'esportazione bulk - HDInsight basati su Linux con, hello Sqoop connettore utilizzato tooexport dati tooMicrosoft SQL Server o Database SQL di Azure attualmente non supporta inserimenti bulk.
* Divisione in batch - con HDInsight basati su Linux, quando si utilizza hello `-batch` passare quando l'esecuzione di inserimenti, Sqoop esegue più inserimenti anziché l'invio in batch le operazioni di inserimento hello.

## <a name="next-steps"></a>Passaggi successivi
Ora si è appreso come toouse Sqoop. toolearn informazioni, vedere:

* [Usare Hive con HDInsight](hdinsight-use-hive.md)
* [Usare Pig con HDInsight](hdinsight-use-pig.md)
* [Usare Oozie con HDInsight][hdinsight-use-oozie]: usare un'azione di Sqoop nel flusso di lavoro di Oozie.
* [Analizzare i dati di ritardo volo tramite HDInsight][hdinsight-analyze-flight-data]: utilizzare Hive volo tooanalyze ritardare dati e quindi utilizzare il database SQL di Azure tooan di Sqoop tooexport dati.
* [Caricare dati tooHDInsight][hdinsight-upload-data]: trovare altri metodi per il caricamento di archiviazione Blob di dati tooHDInsight/Azure.

## <a name="appendix-a---a-powershell-sample"></a>Appendice A - Esempio di PowerShell
esempio di PowerShell Hello esegue hello alla procedura seguente:

1. Connettersi tooAzure.
2. Creare un gruppo di risorse di Azure. Per altre informazioni, vedere [Uso di Azure PowerShell con Gestione risorse di Azure](../powershell-azure-resource-manager.md)
3. Creare un server di Database SQL di Azure, un database SQL Azure e due tabelle. 
   
    Se invece si usa SQL Server, utilizzare hello le tabelle di hello toocreate le istruzioni seguenti:
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    tabelle e database hello più semplice modo tooexamine hello è toouse Visual Studio. server di database di Hello e hello database possono essere esaminati tramite hello portale di Azure.
4. Creare un cluster HDInsight
   
    cluster hello tooexamine, è possibile utilizzare hello portale di Azure o Azure PowerShell.
5. File di dati di origine hello pre-elaborazione.
   
    In questa esercitazione, si esporta un file di log log4j (un file delimitato da virgole) e un database di SQL Azure tooan tabella Hive. Hello file delimitato viene chiamato */example/data/sample.log*. In precedenza nell'esercitazione di hello, si è visto alcuni esempi dei registri log4j. Nel file di log hello, esistono alcune righe vuote e alcuni toothese simile righe:
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    L'operazione è corretta per altri esempi che utilizzano questo tipo di dati, ma è necessario rimuovere queste eccezioni prima sarà possibile importare in database SQL di Azure hello o SQL Server. Sqoop esportazione ha esito negativo se è presente una stringa vuota o una riga con meno elementi numero hello di campi definiti nella tabella di database SQL di Azure hello. tabella log4jlogs Hello è 7 campi di tipo stringa.
   
    Questa procedura crea un nuovo file nel cluster hello: tutorials/usesqoop/data/sample.log. file di dati modificati hello tooexamine, è possibile utilizzare hello portale di Azure, uno strumento di esplorazione di archiviazione di Azure o Azure PowerShell. [Guida introduttiva di HDInsight] [ hdinsight-get-started] dispone di un codice di esempio per l'utilizzo di Azure PowerShell toodownload un file e visualizzare il contenuto di file hello.
6. Esportare un database di SQL Azure toohello file di dati.
   
    file di origine Hello è tutorials/usesqoop/data/sample.log. Hello tabella in cui hello dati esportati toois chiamato log4jlogs.
   
   > [!NOTE]
   > Diverso da informazioni sulla stringa di connessione, i passaggi hello in questa sezione dovrebbero funzionare per un database SQL di Azure o per SQL Server. Questi passaggi sono stati testati tramite hello seguente configurazione:
   > 
   > * **Configurazione di rete virtuale di Azure point-to-site**: una rete virtuale connessa hello HDInsight cluster tooa SQL Server in un centro dati privato. Vedere [configurare una VPN Point-to-Site nel portale di gestione di hello](../vpn-gateway/vpn-gateway-point-to-site-create.md) per ulteriori informazioni.
   > * **Azure HDInsight 3.1**: per informazioni sulla creazione di un cluster in una rete virtuale, vedere l'articolo relativo alla [creazione di cluster Hadoop in HDInsight con opzioni personalizzate](hdinsight-hadoop-provision-linux-clusters.md) .
   > * **SQL Server 2014**: configurato in modo sicuro l'autenticazione tooallow e in esecuzione hello VPN client configurazione pacchetto tooconnect toohello di rete virtuale.
   > 
   > 
7. Esportare un database di SQL Azure toohello tabella Hive.
8. Importare il cluster HDInsight toohello di hello mobiledata tabella.
   
    file di dati modificati hello tooexamine, è possibile utilizzare hello portale di Azure, uno strumento di esplorazione di archiviazione di Azure o Azure PowerShell.  [Guida introduttiva di HDInsight] [ hdinsight-get-started] dispone di un codice di esempio sull'uso di Azure PowerShell toodownload un file e visualizzare il contenuto di file hello.

### <a name="hello-powershell-sample"></a>esempio di PowerShell Hello
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

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
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
