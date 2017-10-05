---
title: Eseguire processi Sqoop usando PowerShell e Azure HDInsight | Documentazione Microsoft
description: Informazioni su come usare Azure PowerShell da una workstation per eseguire importazioni ed esportazioni con Sqoop tra un cluster Hadoop e un database SQL di Azure.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: bbb6f53a-e019-4d01-92bd-92c208c760b6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 956f4ac7c39e2936a2a6b5e5108dbe302446270c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="run-sqoop-jobs-using-azure-powershell-for-hadoop-in-hdinsight"></a><span data-ttu-id="60b8e-103">Eseguire processi Sqoop con Azure PowerShell per Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="60b8e-103">Run Sqoop jobs using Azure PowerShell for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="60b8e-104">Informazioni su come usare Azure PowerShell per eseguire processi Sqoop in HDInsight per importazioni ed esportazioni tra un cluster HDInsight e un database SQL di Azure o un database SQL Server.</span><span class="sxs-lookup"><span data-stu-id="60b8e-104">Learn how to use Azure PowerShell to run Sqoop jobs in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="60b8e-105">La procedura illustrata in questo articolo può essere usata con un cluster HDInsight basato su Windows o su Linux, ma funziona solo se eseguita da un client Windows.</span><span class="sxs-lookup"><span data-stu-id="60b8e-105">The steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps will only work from a Windows client.</span></span> <span data-ttu-id="60b8e-106">Per altri metodi di invio di un processo, fare clic sul selettore di schede all'inizio dell'articolo.</span><span class="sxs-lookup"><span data-stu-id="60b8e-106">For other job submission methods, click the tab selector on the top of the article.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="60b8e-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="60b8e-107">Prerequisites</span></span>
<span data-ttu-id="60b8e-108">Prima di iniziare questa esercitazione, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="60b8e-108">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="60b8e-109">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="60b8e-109">**A workstation with Azure PowerShell**.</span></span>
  
    [!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
* <span data-ttu-id="60b8e-110">**Un cluster Hadoop in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="60b8e-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="60b8e-111">Vedere le informazioni su come [creare un cluster e un database SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="60b8e-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="run-sqoop-using-powershell"></a><span data-ttu-id="60b8e-112">Eseguire Sqoop tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="60b8e-112">Run Sqoop using PowerShell</span></span>
<span data-ttu-id="60b8e-113">Lo script di PowerShell seguente pre-elabora il file di origine e lo esporta in un database SQL di Azure:</span><span class="sxs-lookup"><span data-stu-id="60b8e-113">The following PowerShell script pre-processes the source file, and exports it to an Azure SQL database:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $hdinsightClusterName = "<HDInsightClusterName>"

    $httpUserName = "admin"
    $httpPassword = "<Password>"

    $defaultStorageAccountName = $hdinsightClusterName + "store"
    $defaultBlobContainerName = $hdinsightClusterName


    $sqlDatabaseServerName = $hdinsightClusterName + "dbserver"
    $sqlDatabaseName = $hdinsightClusterName + "db"
    $sqlDatabaseLogin = "sqluser"
    $sqlDatabasePassword = "<Password>"

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - pre-process the source file

    Write-Host "`nPreprocessing the source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define the connection string
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing the source and destination blob.
    $storageAccount = Get-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $defaultStorageAccountName
    $storageContainer = ($storageAccount |Get-AzureStorageContainer -Name $defaultBlobContainerName).CloudBlobContainer
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from the source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into the destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process the source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove the "java.lang.Exception" from the first element of the array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList to remove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove the lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write to the destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export the log file from the cluster to the SQL database

    Write-Host "Exporting the log file ..." -ForegroundColor Green

    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $tableName_log4j = "log4jlogs"
    $exportDir_log4j = "/tutorials/usesqoop/data"
    $sqljdbcdriver = "/user/oozie/share/lib/sqoop/sqljdbc41.jar"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1" `
        -Files $sqljdbcdriver

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

## <a name="limitations"></a><span data-ttu-id="60b8e-114">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="60b8e-114">Limitations</span></span>
* <span data-ttu-id="60b8e-115">Esportazione di massa: con HDInsight basato su Linux, attualmente il connettore Sqoop, usato per esportare dati in Microsoft SQL Server o nel database SQL di Azure, non supporta inserimenti di massa.</span><span class="sxs-lookup"><span data-stu-id="60b8e-115">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="60b8e-116">Invio in batch: con HDInsight basato su Linux, quando si usa il comando `-batch` durante gli inserimenti, Sqoop esegue più inserimenti invece di suddividere in batch le operazioni di inserimento.</span><span class="sxs-lookup"><span data-stu-id="60b8e-116">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60b8e-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="60b8e-117">Next steps</span></span>
<span data-ttu-id="60b8e-118">In questa esercitazione si è appreso come usare Sqoop.</span><span class="sxs-lookup"><span data-stu-id="60b8e-118">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="60b8e-119">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="60b8e-119">To learn more, see:</span></span>

* <span data-ttu-id="60b8e-120">[Usare Oozie con HDInsight](hdinsight-use-oozie.md): usare un'azione di Sqoop nel flusso di lavoro di Oozie.</span><span class="sxs-lookup"><span data-stu-id="60b8e-120">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="60b8e-121">[Analizzare i dati sui ritardi dei voli usando HDInsight](hdinsight-analyze-flight-delay-data.md): usare Hive nell'analisi dei dati sui ritardi dei voli e quindi usare Sqoop per esportare dati nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="60b8e-121">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="60b8e-122">[Caricare i dati in HDInsight](hdinsight-upload-data.md): per altri metodi per il caricamento di file in HDInsight o nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="60b8e-122">[Upload data to HDInsight](hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
