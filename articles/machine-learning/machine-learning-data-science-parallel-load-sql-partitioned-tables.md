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
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a>Importazione di dati in blocco utilizzando le tabelle di partizione SQL
Questo documento viene descritto come modalità di partizionamento delle tabelle per l'importazione bulk parallela rapido del database di SQL Server data tooa toobuild. Per il database SQL di tooa caricamento/trasferimento di dati di grandi dimensioni, l'importazione di dati toohello database di SQL Server e le query successive possono essere migliorata tramite *viste e tabelle partizionate*. 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a>Creazione di un nuovo database e di un set di filegroup
* [Creare un nuovo database](https://technet.microsoft.com/library/ms176061.aspx) se non esiste già.
* Aggiungere filegroup toohello di database di cui verranno memorizzati i file fisici hello partizionata. Questa operazione può essere eseguita con [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) se la nuova o [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) se database hello esiste già.
* Aggiungere uno o più filegroup di database di tooeach file (in base alle esigenze).
  
  > [!NOTE]
  > Specificare i filegroup di destinazione hello che contiene i dati per questa partizione e hello nomi dei file di database fisico in cui verranno archiviati i dati del filegroup hello.
  > 
  > 

Hello seguente esempio viene creato un nuovo database con tre filegroup diversi hello primario e i gruppi di log, che contiene un file fisico in ogni. file di database Hello vengono creati nella cartella di dati di SQL Server predefinita hello, come configurato nell'istanza di SQL Server hello. Per ulteriori informazioni sui percorsi dei file hello predefinito, vedere [percorsi di File per predefinite e denominate di istanze di SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).

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
Creare tabelle partizionate in base toohello schema di dati, filegroup del database mappato toohello creato nel passaggio precedente hello. Quando i dati vengono importati globalmente toohello partizionata o più tabelle, i record vengono distribuiti tra filegroup hello in base a uno schema di partizione tooa come descritto di seguito.

**toocreate una tabella di partizione, è necessario:**

* [Creare una funzione di partizione](https://msdn.microsoft.com/library/ms187802.aspx) che definisce l'intervallo di hello di valori o i limiti toobe inclusi in ogni tabella delle partizioni singole, ad esempio, toolimit partizioni in base al mese (alcuni\_datetime\_campo) nell'anno hello 2013:
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* [Creare uno schema di partizione](https://msdn.microsoft.com/library/ms179854.aspx) che esegue il mapping di ogni intervallo di partizione hello partizione funzione tooa fisico filegroup, ad esempio:
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  gli intervalli hello tooverify attiva in ogni secondo toohello funzione o schema di partizione, eseguire hello seguente query:
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* [Creare una tabella partizionata](https://msdn.microsoft.com/library/ms174979.aspx)(s) in base tooyour schema di dati e specificare campo vincolo e lo schema di partizione hello utilizzato tabella hello toopartition, ad esempio:
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

Per altre informazioni, vedere [Creazione di tabelle e indici partizionati](https://msdn.microsoft.com/library/ms188730.aspx).

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a>Importazione BULK hello dei dati per ogni tabella singola partizione
* È possibile utilizzare BCP, l'INSERIMENTO DI MASSA o altri metodi quali la [migrazione guidata di SQL Server](http://sqlazuremw.codeplex.com/). esempio Hello fornito Usa il metodo BCP hello.
* [ALTER database hello](https://msdn.microsoft.com/library/bb522682.aspx) transazione toochange schema tooBULK_LOGGED toominimize overhead di registrazione, ad esempio, di registrazione:
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* dati tooexpedite durante il caricamento, avviare le operazioni di importazione bulk hello in parallelo. Per suggerimenti su come accelerare l'importazione in blocco di dati di grandi dimensioni nei database di SQL Server, vedere [Caricamento di 1 TB in meno di 1 ora](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).

Hello script PowerShell riportato di seguito è riportato un esempio paralleli di caricamento di dati tramite BCP.

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


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a>Creare indici toooptimize join e le prestazioni delle query
* Se i dati per la modellazione verranno estratte da più tabelle, creare indici su chiavi di join hello prestazioni dei join tooimprove hello.
* [Creare indici](https://technet.microsoft.com/library/ms188783.aspx) (cluster o non cluster) come destinazione hello stesso filegroup per ogni partizione, per esempio:
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  o
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > È possibile scegliere toocreate indici hello prima dell'importazione bulk di dati hello. Creazione dell'indice prima dell'importazione bulk rallenterà il caricamento dei dati hello.
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a>Esempio di Advanced Analytics Process and Technology in azione
Per un esempio di questa procedura dettagliata end-to-end utilizzando hello Cortana Analitica processo con un set di dati pubblici, vedere [processo Analitica Cortana in azione: utilizzo di SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

