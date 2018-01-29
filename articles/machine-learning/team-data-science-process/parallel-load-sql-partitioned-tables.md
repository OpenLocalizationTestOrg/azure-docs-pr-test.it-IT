---
title: Creare e ottimizzare le tabelle per l'importazione parallela rapida dei dati in SQL Server in una macchina virtuale di Azure | Documentazione Microsoft
description: Importazione di dati in blocco utilizzando le tabelle di partizione SQL
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/09/2017
ms.author: bradsev
ms.openlocfilehash: 77638ff52edbc2b782b21a4ca1c727a2b46f22f3
ms.sourcegitcommit: bc8d39fa83b3c4a66457fba007d215bccd8be985
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/10/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a>Importazione di dati in blocco utilizzando le tabelle di partizione SQL
Questo documento descrive come creare tabelle partizionate per l'importazione in blocco in parallelo di dati in un database di SQL Server. Per il caricamento/trasferimento di Big Data, l'importazione di dati nel database SQL e le query successive possono essere migliorate usando *tabelle e visualizzazioni di partizione*. 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a>Creazione di un nuovo database e di un set di filegroup
* [Creare un nuovo database](https://technet.microsoft.com/library/ms176061.aspx) se non esiste già.
* Aggiungere filegroup del database al database che contiene i file fisici partizionati. 
* Questa operazione può essere eseguita con [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) se il database è nuovo o con [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) se il database esiste già.
* Aggiungere uno o più file (se necessario) per ogni filegroup del database.
  
  > [!NOTE]
  > Specificare il filegroup di destinazione contenente i dati della partizione e i nomi dei file del database fisico in cui sono archiviati i dati del filegroup.
  > 
  > 

Nell'esempio seguente vengono creati un nuovo database con tre filegroup diverso da quello primario e gruppi di log, ognuno contenente un file fisico. I file di database vengono creati nella cartella dei dati di SQL Server predefinita, come configurato nell'istanza di SQL Server. Per ulteriori informazioni sui percorsi dei file predefiniti, vedere [Percorsi dei file per istanze predefinite e denominate di SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).

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

## <a name="create-a-partitioned-table"></a>Creazione di una tabella partizionata
Per creare tabelle partizionate in base allo schema dei dati, mappate ai filegroup del database creato nel passaggio precedente, è prima necessario creare una funzione e uno schema di partizione. Quando i dati vengono importati in blocco nelle tabelle partizionate, i record vengono distribuiti tra i filegroup secondo uno schema di partizione, come descritto di seguito.

### <a name="1-create-a-partition-function"></a>1. Creare una funzione di partizione
[Creare una funzione di partizione](https://msdn.microsoft.com/library/ms187802.aspx) Questa funzione definisce l'intervallo di valori/limiti da includere in ogni tabella delle partizioni, ad esempio per limitare le partizioni per mese (some\_datetime\_field) nell'anno 2013:
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )

### <a name="2-create-a-partition-scheme"></a>2. Creare uno schema di partizione
[Creare uno schema di partizione](https://msdn.microsoft.com/library/ms179854.aspx). Questo schema esegue il mapping di ogni intervallo di partizione della funzione di partizione a un filegroup fisico, ad esempio:
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> TO (
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  per verificare gli intervalli in vigore in ogni partizione secondo funzione/schema, eseguire la query seguente:
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>

### <a name="3-create-a-partition-table"></a>3. Creare una tabella delle partizioni
[Creare tabelle partizionate](https://msdn.microsoft.com/library/ms174979.aspx) in base allo schema dei dati e specificare lo schema di partizione e il campo di vincolo usati per partizionare la tabella, ad esempio:
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

Per altre informazioni, vedere [Creazione di tabelle e indici partizionati](https://msdn.microsoft.com/library/ms188730.aspx).

## <a name="bulk-import-the-data-for-each-individual-partition-table"></a>Importazione in blocco dei dati per ogni singola tabella di partizione

* È possibile utilizzare BCP, l'INSERIMENTO DI MASSA o altri metodi quali la [migrazione guidata di SQL Server](http://sqlazuremw.codeplex.com/). L'esempio fornito utilizza il metodo BCP.
* [Modificare il database](https://msdn.microsoft.com/library/bb522682.aspx) per modificare lo schema di registrazione delle transazioni in BULK_LOGGED e ridurre il sovraccarico della registrazione, ad esempio:
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* Per accelerare il caricamento dei dati, avviare le operazioni di importazione in blocco in parallelo. Per suggerimenti su come accelerare l'importazione in blocco di dati di grandi dimensioni nei database di SQL Server, vedere [Caricamento di 1 TB in meno di 1 ora](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).

Il seguente script di PowerShell è un esempio di caricamento dei dati parallelo tramite BCP.

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


## <a name="create-indexes-to-optimize-joins-and-query-performance"></a>Creazione di indici per ottimizzare i join e le prestazioni delle query
* Per estrarre i dati di modellazione da più tabelle, creare indici sulle chiavi di join per migliorare le prestazioni dei join.
* [Creare indici](https://technet.microsoft.com/library/ms188783.aspx) (in cluster o non in cluster) destinati allo stesso filegroup per ogni partizione, ad esempio:
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  o
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > È possibile scegliere di creare gli indici prima di importare in blocco i dati. La creazione degli indici prima dell'importazione dei dati in blocco rallenta il caricamento dei dati.
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a>Esempio di Advanced Analytics Process and Technology in azione
Per un esempio di procedura dettagliata end-to-end tramite il processo di data science per i team con un set di dati pubblico, vedere [Processo di data science per i team in azione: uso di SQL Server](sql-walkthrough.md).

