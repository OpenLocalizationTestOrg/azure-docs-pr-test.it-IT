---
title: aaaBuild e ottimizzare le tabelle per l'importazione parallela veloce dei dati in un Server SQL in una macchina virtuale di Azure | Documenti Microsoft
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
ms.openlocfilehash: ab748c47348ec6ca3b98ba39e27181bba5d36fc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="c953d-103">Importazione di dati in blocco utilizzando le tabelle di partizione SQL</span><span class="sxs-lookup"><span data-stu-id="c953d-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="c953d-104">Questo documento viene descritto come modalità di partizionamento delle tabelle per l'importazione bulk parallela rapido del database di SQL Server data tooa toobuild.</span><span class="sxs-lookup"><span data-stu-id="c953d-104">This document describes how toobuild partitioned tables for fast parallel bulk importing of data tooa SQL Server database.</span></span> <span data-ttu-id="c953d-105">Per il database SQL di tooa caricamento/trasferimento di dati di grandi dimensioni, l'importazione di dati toohello database di SQL Server e le query successive possono essere migliorata tramite *viste e tabelle partizionate*.</span><span class="sxs-lookup"><span data-stu-id="c953d-105">For big data loading/transfer tooa SQL database, importing data toohello SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="c953d-106">Creazione di un nuovo database e di un set di filegroup</span><span class="sxs-lookup"><span data-stu-id="c953d-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="c953d-107">[Creare un nuovo database](https://technet.microsoft.com/library/ms176061.aspx) se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="c953d-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="c953d-108">Aggiungere filegroup toohello di database di cui verranno memorizzati i file fisici hello partizionata. Questa operazione può essere eseguita con [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) se la nuova o [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) se database hello esiste già.</span><span class="sxs-lookup"><span data-stu-id="c953d-108">Add database filegroups toohello database which will hold hello partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if hello database exists already.</span></span>
* <span data-ttu-id="c953d-109">Aggiungere uno o più filegroup di database di tooeach file (in base alle esigenze).</span><span class="sxs-lookup"><span data-stu-id="c953d-109">Add one or more files (as needed) tooeach database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="c953d-110">Specificare i filegroup di destinazione hello che contiene i dati per questa partizione e hello nomi dei file di database fisico in cui verranno archiviati i dati del filegroup hello.</span><span class="sxs-lookup"><span data-stu-id="c953d-110">Specify hello target filegroup which holds data for this partition and hello physical database file name(s) where hello filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="c953d-111">Hello seguente esempio viene creato un nuovo database con tre filegroup diversi hello primario e i gruppi di log, che contiene un file fisico in ogni.</span><span class="sxs-lookup"><span data-stu-id="c953d-111">hello following example creates a new database with three filegroups other than hello primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="c953d-112">file di database Hello vengono creati nella cartella di dati di SQL Server predefinita hello, come configurato nell'istanza di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="c953d-112">hello database files are created in hello default SQL Server Data folder, as configured in hello SQL Server instance.</span></span> <span data-ttu-id="c953d-113">Per ulteriori informazioni sui percorsi dei file hello predefinito, vedere [percorsi di File per predefinite e denominate di istanze di SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span><span class="sxs-lookup"><span data-stu-id="c953d-113">For more information about hello default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

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

## <a name="create-a-partitioned-table"></a><span data-ttu-id="c953d-114">Creazione di una tabella partizionata</span><span class="sxs-lookup"><span data-stu-id="c953d-114">Create a partitioned table</span></span>
<span data-ttu-id="c953d-115">Creare tabelle partizionate in base toohello schema di dati, filegroup del database mappato toohello creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="c953d-115">Create partitioned table(s) according toohello data schema, mapped toohello database filegroups created in hello previous step.</span></span> <span data-ttu-id="c953d-116">Quando i dati vengono importati globalmente toohello partizionata o più tabelle, i record vengono distribuiti tra filegroup hello in base a uno schema di partizione tooa come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="c953d-116">When data is bulk imported toohello partitioned table(s), records will be distributed among hello filegroups according tooa partition scheme, as described below.</span></span>

<span data-ttu-id="c953d-117">**toocreate una tabella di partizione, è necessario:**</span><span class="sxs-lookup"><span data-stu-id="c953d-117">**toocreate a partition table, you need to:**</span></span>

* <span data-ttu-id="c953d-118">[Creare una funzione di partizione](https://msdn.microsoft.com/library/ms187802.aspx) che definisce l'intervallo di hello di valori o i limiti toobe inclusi in ogni tabella delle partizioni singole, ad esempio, toolimit partizioni in base al mese (alcuni\_datetime\_campo) nell'anno hello 2013:</span><span class="sxs-lookup"><span data-stu-id="c953d-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines hello range of values/boundaries toobe included in each individual partition table, e.g., toolimit partitions by month(some\_datetime\_field) in hello year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="c953d-119">[Creare uno schema di partizione](https://msdn.microsoft.com/library/ms179854.aspx) che esegue il mapping di ogni intervallo di partizione hello partizione funzione tooa fisico filegroup, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c953d-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in hello partition function tooa physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="c953d-120">gli intervalli hello tooverify attiva in ogni secondo toohello funzione o schema di partizione, eseguire hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="c953d-120">tooverify hello ranges in effect in each partition according toohello function/scheme, run hello following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="c953d-121">[Creare una tabella partizionata](https://msdn.microsoft.com/library/ms174979.aspx)(s) in base tooyour schema di dati e specificare campo vincolo e lo schema di partizione hello utilizzato tabella hello toopartition, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c953d-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according tooyour data schema, and specify hello partition scheme and constraint field used toopartition hello table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="c953d-122">Per altre informazioni, vedere [Creazione di tabelle e indici partizionati](https://msdn.microsoft.com/library/ms188730.aspx).</span><span class="sxs-lookup"><span data-stu-id="c953d-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a><span data-ttu-id="c953d-123">Importazione BULK hello dei dati per ogni tabella singola partizione</span><span class="sxs-lookup"><span data-stu-id="c953d-123">Bulk import hello data for each individual partition table</span></span>
* <span data-ttu-id="c953d-124">È possibile utilizzare BCP, l'INSERIMENTO DI MASSA o altri metodi quali la [migrazione guidata di SQL Server](http://sqlazuremw.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="c953d-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="c953d-125">esempio Hello fornito Usa il metodo BCP hello.</span><span class="sxs-lookup"><span data-stu-id="c953d-125">hello example provided uses hello BCP method.</span></span>
* <span data-ttu-id="c953d-126">[ALTER database hello](https://msdn.microsoft.com/library/bb522682.aspx) transazione toochange schema tooBULK_LOGGED toominimize overhead di registrazione, ad esempio, di registrazione:</span><span class="sxs-lookup"><span data-stu-id="c953d-126">[Alter hello database](https://msdn.microsoft.com/library/bb522682.aspx) toochange transaction logging scheme tooBULK_LOGGED toominimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="c953d-127">dati tooexpedite durante il caricamento, avviare le operazioni di importazione bulk hello in parallelo.</span><span class="sxs-lookup"><span data-stu-id="c953d-127">tooexpedite data loading, launch hello bulk import operations in parallel.</span></span> <span data-ttu-id="c953d-128">Per suggerimenti su come accelerare l'importazione in blocco di dati di grandi dimensioni nei database di SQL Server, vedere [Caricamento di 1 TB in meno di 1 ora](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span><span class="sxs-lookup"><span data-stu-id="c953d-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="c953d-129">Hello script PowerShell riportato di seguito è riportato un esempio paralleli di caricamento di dati tramite BCP.</span><span class="sxs-lookup"><span data-stu-id="c953d-129">hello following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # hello example assumes hello partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes hello input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set hello server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match hello number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name toobe loaded, basename of input data files, input format file, and number of partitions
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


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a><span data-ttu-id="c953d-130">Creare indici toooptimize join e le prestazioni delle query</span><span class="sxs-lookup"><span data-stu-id="c953d-130">Create indexes toooptimize joins and query performance</span></span>
* <span data-ttu-id="c953d-131">Se i dati per la modellazione verranno estratte da più tabelle, creare indici su chiavi di join hello prestazioni dei join tooimprove hello.</span><span class="sxs-lookup"><span data-stu-id="c953d-131">If you will extract data for modeling from multiple tables, create indexes on hello join keys tooimprove hello join performance.</span></span>
* <span data-ttu-id="c953d-132">[Creare indici](https://technet.microsoft.com/library/ms188783.aspx) (cluster o non cluster) come destinazione hello stesso filegroup per ogni partizione, per esempio:</span><span class="sxs-lookup"><span data-stu-id="c953d-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting hello same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="c953d-133">o</span><span class="sxs-lookup"><span data-stu-id="c953d-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="c953d-134">È possibile scegliere toocreate indici hello prima dell'importazione bulk di dati hello.</span><span class="sxs-lookup"><span data-stu-id="c953d-134">You may choose toocreate hello indexes before bulk importing hello data.</span></span> <span data-ttu-id="c953d-135">Creazione dell'indice prima dell'importazione bulk rallenterà il caricamento dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="c953d-135">Index creation before bulk importing will slow down hello data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="c953d-136">Esempio di Advanced Analytics Process and Technology in azione</span><span class="sxs-lookup"><span data-stu-id="c953d-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="c953d-137">Per un esempio di questa procedura dettagliata end-to-end utilizzando hello Cortana Analitica processo con un set di dati pubblici, vedere [processo Analitica Cortana in azione: utilizzo di SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="c953d-137">For an end-to-end walkthrough example using hello Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

