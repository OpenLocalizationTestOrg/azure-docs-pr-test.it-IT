---
title: Creare e ottimizzare le tabelle per l'importazione parallela rapida dei dati in SQL Server in una macchina virtuale di Azure | Documentazione Microsoft
description: Importazione di dati in blocco utilizzando le tabelle di partizione SQL
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: aae4e4f59e76bf48b00a2ee92aedd7d5643ba91a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="cff71-103">Importazione di dati in blocco utilizzando le tabelle di partizione SQL</span><span class="sxs-lookup"><span data-stu-id="cff71-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="cff71-104">Questo documento descrive come creare tabelle partizionate per l'importazione in blocco in parallelo di dati in un database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cff71-104">This document describes how to build partitioned tables for fast parallel bulk importing of data to a SQL Server database.</span></span> <span data-ttu-id="cff71-105">Per il caricamento/trasferimento di Big Data, l'importazione di dati nel database SQL e le query successive possono essere migliorate usando *tabelle e visualizzazioni di partizione*.</span><span class="sxs-lookup"><span data-stu-id="cff71-105">For big data loading/transfer to a SQL database, importing data to the SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="cff71-106">Creazione di un nuovo database e di un set di filegroup</span><span class="sxs-lookup"><span data-stu-id="cff71-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="cff71-107">[Creare un nuovo database](https://technet.microsoft.com/library/ms176061.aspx) se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="cff71-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="cff71-108">Aggiungere filegroup di database al database che conterranno i file fisici partizionati. Questa operazione può essere eseguita con [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) per un nuovo database o [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) se il database esiste già.</span><span class="sxs-lookup"><span data-stu-id="cff71-108">Add database filegroups to the database which will hold the partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if the database exists already.</span></span>
* <span data-ttu-id="cff71-109">Aggiungere uno o più file (se necessario) per ogni filegroup del database.</span><span class="sxs-lookup"><span data-stu-id="cff71-109">Add one or more files (as needed) to each database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="cff71-110">Specificare il filegroup di destinazione contenente i dati della partizione e i nomi dei file del database fisico in cui verranno archiviati i dati del filegroup.</span><span class="sxs-lookup"><span data-stu-id="cff71-110">Specify the target filegroup which holds data for this partition and the physical database file name(s) where the filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="cff71-111">Nell'esempio seguente vengono creati un nuovo database con tre filegroup diverso da quello primario e gruppi di log, ognuno contenente un file fisico.</span><span class="sxs-lookup"><span data-stu-id="cff71-111">The following example creates a new database with three filegroups other than the primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="cff71-112">I file di database vengono creati nella cartella dei dati di SQL Server predefinita, come configurato nell'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cff71-112">The database files are created in the default SQL Server Data folder, as configured in the SQL Server instance.</span></span> <span data-ttu-id="cff71-113">Per ulteriori informazioni sui percorsi dei file predefiniti, vedere [Percorsi dei file per istanze predefinite e denominate di SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span><span class="sxs-lookup"><span data-stu-id="cff71-113">For more information about the default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);

    EXECUTE ('
        CREATE DATABASE <database_name>
         ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
         LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')

## <a name="create-a-partitioned-table"></a><span data-ttu-id="cff71-114">Creazione di una tabella partizionata</span><span class="sxs-lookup"><span data-stu-id="cff71-114">Create a partitioned table</span></span>
<span data-ttu-id="cff71-115">Creare tabelle partizionate in base allo schema dei dati, mappate ai filegroup del database creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="cff71-115">Create partitioned table(s) according to the data schema, mapped to the database filegroups created in the previous step.</span></span> <span data-ttu-id="cff71-116">Quando i dati vengono importati in blocco nelle tabelle partizionate, i record verranno distribuiti tra i filegroup secondo uno schema di partizione, come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="cff71-116">When data is bulk imported to the partitioned table(s), records will be distributed among the filegroups according to a partition scheme, as described below.</span></span>

<span data-ttu-id="cff71-117">**Per creare una tabella di partizione, è necessario:**</span><span class="sxs-lookup"><span data-stu-id="cff71-117">**To create a partition table, you need to:**</span></span>

* <span data-ttu-id="cff71-118">[Creare una funzione di partizione](https://msdn.microsoft.com/library/ms187802.aspx) che definisce l'intervallo di valori/limiti da includere in ogni tabella di partizione, ad esempio, per limitare le partizioni per mese (some\_datetime\_field) nell'anno 2013:</span><span class="sxs-lookup"><span data-stu-id="cff71-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines the range of values/boundaries to be included in each individual partition table, e.g., to limit partitions by month(some\_datetime\_field) in the year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="cff71-119">[Creare uno schema di partizione](https://msdn.microsoft.com/library/ms179854.aspx) che esegue il mapping di ogni intervallo di partizione della funzione di partizione a un filegroup fisico, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cff71-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in the partition function to a physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> TO (
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="cff71-120">per verificare gli intervalli in vigore in ogni partizione secondo funzione/schema, eseguire la query seguente:</span><span class="sxs-lookup"><span data-stu-id="cff71-120">To verify the ranges in effect in each partition according to the function/scheme, run the following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="cff71-121">[Creare le tabelle partizionate](https://msdn.microsoft.com/library/ms174979.aspx)in base allo schema dei dati e specificare lo schema di partizione e il campo dei vincoli utilizzati per partizionare la tabella, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cff71-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according to your data schema, and specify the partition scheme and constraint field used to partition the table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="cff71-122">Per altre informazioni, vedere [Creazione di tabelle e indici partizionati](https://msdn.microsoft.com/library/ms188730.aspx).</span><span class="sxs-lookup"><span data-stu-id="cff71-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-the-data-for-each-individual-partition-table"></a><span data-ttu-id="cff71-123">Importazione in blocco dei dati per ogni singola tabella di partizione</span><span class="sxs-lookup"><span data-stu-id="cff71-123">Bulk import the data for each individual partition table</span></span>
* <span data-ttu-id="cff71-124">È possibile utilizzare BCP, l'INSERIMENTO DI MASSA o altri metodi quali la [migrazione guidata di SQL Server](http://sqlazuremw.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="cff71-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="cff71-125">L'esempio fornito utilizza il metodo BCP.</span><span class="sxs-lookup"><span data-stu-id="cff71-125">The example provided uses the BCP method.</span></span>
* <span data-ttu-id="cff71-126">[Modificare il database](https://msdn.microsoft.com/library/bb522682.aspx) per modificare lo schema di registrazione delle transazioni in BULK_LOGGED per ridurre il sovraccarico della registrazione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cff71-126">[Alter the database](https://msdn.microsoft.com/library/bb522682.aspx) to change transaction logging scheme to BULK_LOGGED to minimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="cff71-127">Per accelerare il caricamento dei dati, avviare le operazioni di importazione in blocco in parallelo.</span><span class="sxs-lookup"><span data-stu-id="cff71-127">To expedite data loading, launch the bulk import operations in parallel.</span></span> <span data-ttu-id="cff71-128">Per suggerimenti su come accelerare l'importazione in blocco di dati di grandi dimensioni nei database di SQL Server, vedere [Caricamento di 1 TB in meno di 1 ora](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span><span class="sxs-lookup"><span data-stu-id="cff71-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="cff71-129">Il seguente script di PowerShell è un esempio di caricamento dei dati parallelo tramite BCP.</span><span class="sxs-lookup"><span data-stu-id="cff71-129">The following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # The example assumes the partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes the input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set the server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match the number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name to be loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"

    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir

    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }

    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }

    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }

    Get-Job

    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-to-optimize-joins-and-query-performance"></a><span data-ttu-id="cff71-130">Creazione di indici per ottimizzare i join e le prestazioni delle query</span><span class="sxs-lookup"><span data-stu-id="cff71-130">Create indexes to optimize joins and query performance</span></span>
* <span data-ttu-id="cff71-131">Per estrarre i dati di modellazione da più tabelle, creare indici sulle chiavi join per migliorare le prestazioni dei join.</span><span class="sxs-lookup"><span data-stu-id="cff71-131">If you will extract data for modeling from multiple tables, create indexes on the join keys to improve the join performance.</span></span>
* <span data-ttu-id="cff71-132">[Creare indici](https://technet.microsoft.com/library/ms188783.aspx) (in cluster o non in cluster) indirizzati allo stesso filegroup per ogni partizione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cff71-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting the same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="cff71-133">o</span><span class="sxs-lookup"><span data-stu-id="cff71-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="cff71-134">È possibile scegliere di creare gli indici prima di importare in blocco i dati.</span><span class="sxs-lookup"><span data-stu-id="cff71-134">You may choose to create the indexes before bulk importing the data.</span></span> <span data-ttu-id="cff71-135">La creazione degli indici prima dell'importazione dei dati in blocco rallenterà il caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="cff71-135">Index creation before bulk importing will slow down the data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="cff71-136">Esempio di Advanced Analytics Process and Technology in azione</span><span class="sxs-lookup"><span data-stu-id="cff71-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="cff71-137">Per un esempio della procedura dettagliata end-to-end mediante Cortana Analytics Process con un set di dati pubblico, vedere [Cortana Analytics Process in azione: utilizzo di SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="cff71-137">For an end-to-end walkthrough example using the Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

