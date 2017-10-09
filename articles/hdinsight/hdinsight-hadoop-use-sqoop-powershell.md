---
title: i processi di Sqoop aaaRun tramite PowerShell e Azure HDInsight | Documenti Microsoft
description: Informazioni su come toouse Azure PowerShell da un toorun workstation Sqoop importare ed esportare tra un cluster Hadoop e un database SQL di Azure.
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
ms.openlocfilehash: 8313bbd109e968aeab540bbcefefe84ebd64c87e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-azure-powershell-for-hadoop-in-hdinsight"></a><span data-ttu-id="a3094-103">Eseguire processi Sqoop con Azure PowerShell per Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a3094-103">Run Sqoop jobs using Azure PowerShell for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="a3094-104">Informazioni su come i processi di toouse Azure PowerShell toorun Sqoop in HDInsight tooimport ed esportare tra cluster HDInsight e database SQL di Azure o database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a3094-104">Learn how toouse Azure PowerShell toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="a3094-105">passaggi di Hello in questo articolo possono essere utilizzati con entrambi un cluster HDInsight basati su Linux o Windows. Tuttavia, questa procedura funziona solo da un client di Windows.</span><span class="sxs-lookup"><span data-stu-id="a3094-105">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps will only work from a Windows client.</span></span> <span data-ttu-id="a3094-106">Per altri metodi di invio del processo, fare clic sul selettore di hello scheda nella parte superiore di hello dell'articolo hello.</span><span class="sxs-lookup"><span data-stu-id="a3094-106">For other job submission methods, click hello tab selector on hello top of hello article.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="a3094-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a3094-107">Prerequisites</span></span>
<span data-ttu-id="a3094-108">Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="a3094-108">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="a3094-109">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a3094-109">**A workstation with Azure PowerShell**.</span></span>
  
    [!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
* <span data-ttu-id="a3094-110">**Un cluster Hadoop in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a3094-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="a3094-111">Vedere le informazioni su come [creare un cluster e un database SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="a3094-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="run-sqoop-using-powershell"></a><span data-ttu-id="a3094-112">Eseguire Sqoop tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3094-112">Run Sqoop using PowerShell</span></span>
<span data-ttu-id="a3094-113">lo script di PowerShell seguente Hello pre-elabora file di origine hello e li Esporta in un database SQL di Azure tooan:</span><span class="sxs-lookup"><span data-stu-id="a3094-113">hello following PowerShell script pre-processes hello source file, and exports it tooan Azure SQL database:</span></span>

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

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - pre-process hello source file

    Write-Host "`nPreprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = Get-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $defaultStorageAccountName
    $storageContainer = ($storageAccount |Get-AzureStorageContainer -Name $defaultBlobContainerName).CloudBlobContainer
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

    #region - export hello log file from hello cluster toohello SQL database

    Write-Host "Exporting hello log file ..." -ForegroundColor Green

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

## <a name="limitations"></a><span data-ttu-id="a3094-114">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="a3094-114">Limitations</span></span>
* <span data-ttu-id="a3094-115">Eseguire l'esportazione bulk - HDInsight basati su Linux con, hello Sqoop connettore utilizzato tooexport dati tooMicrosoft SQL Server o Database SQL di Azure attualmente non supporta inserimenti bulk.</span><span class="sxs-lookup"><span data-stu-id="a3094-115">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="a3094-116">Divisione in batch - con HDInsight basati su Linux, quando si utilizza hello `-batch` passare quando l'esecuzione di inserimenti, Sqoop eseguirà più inserimenti anziché l'invio in batch le operazioni di inserimento hello.</span><span class="sxs-lookup"><span data-stu-id="a3094-116">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3094-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3094-117">Next steps</span></span>
<span data-ttu-id="a3094-118">Ora si è appreso come toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="a3094-118">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="a3094-119">toolearn informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="a3094-119">toolearn more, see:</span></span>

* <span data-ttu-id="a3094-120">[Usare Oozie con HDInsight](hdinsight-use-oozie.md): usare un'azione di Sqoop nel flusso di lavoro di Oozie.</span><span class="sxs-lookup"><span data-stu-id="a3094-120">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="a3094-121">[Analizzare i dati di ritardo volo tramite HDInsight](hdinsight-analyze-flight-delay-data.md): utilizzare Hive volo tooanalyze ritardare dati e quindi utilizzare il database SQL di Azure tooan di Sqoop tooexport dati.</span><span class="sxs-lookup"><span data-stu-id="a3094-121">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="a3094-122">[Caricare dati tooHDInsight](hdinsight-upload-data.md): trovare altri metodi per il caricamento di archiviazione Blob di dati tooHDInsight/Azure.</span><span class="sxs-lookup"><span data-stu-id="a3094-122">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
