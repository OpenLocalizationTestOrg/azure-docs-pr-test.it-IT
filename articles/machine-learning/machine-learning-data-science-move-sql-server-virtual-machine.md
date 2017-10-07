---
title: aaaMove dati tooSQL Server in una macchina virtuale di Azure | Documenti Microsoft
description: Spostamento dei dati da file flat o da un tooSQL di SQL Server on-premise Server sulla macchina virtuale di Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a>Spostare dati tooSQL Server in una macchina virtuale di Azure
In questo argomento vengono descritte le opzioni di hello per lo spostamento dei dati da file flat (formati CSV o TSV) o da un tooSQL di Server SQL Server locale in una macchina virtuale di Azure. Queste attività per lo spostamento dati nel cloud toohello fanno parte del processo di analisi scientifica dei dati di Team hello.

Per un argomento che descrive le opzioni di hello per lo spostamento dati tooan Database SQL di Azure per Machine Learning, vedere [spostare dati tooan Database SQL di Azure per Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).

Hello **menu** seguito tootopics collegamenti che descrivono come dati tooingest in altri ambienti di destinazione in cui i dati hello possono essere archiviati ed elaborati durante hello Team Data Science processo (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Hello nella tabella seguente sono riepilogate le opzioni di hello per lo spostamento dati tooSQL Server in una macchina virtuale di Azure.

| <b>SOURCE</b> | <b>DESTINAZIONE: SQL Server in VM di Azure</b> |
| --- | --- |
| <b>File Flat</b> |1. <a href="#insert-tables-bcp">Utilità copia di massa della riga di comando (BCP) </a><br> 2. <a href="#insert-tables-bulkquery">Inserimento di massa query SQL </a><br> 3. <a href="#sql-builtin-utilities">Utilità grafiche integrate in SQL Server</a> |
| <b>Server SQL locale</b> |1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Distribuzione guidata di Microsoft Azure VM tooa un Database di SQL Server</a><br> 2. <a href="#export-flat-file">Esportare tooa File flat</a><br> 3. <a href="#sql-migration">Migrazione guidata database SQL </a> <br> 4. <a href="#sql-backup">Backup e ripristino database </a><br> |

Tenere presente che il presente documento presuppone che i comandi SQL vengano eseguiti da SQL Server Management Studio o Visual Studio Database Explorer.

> [!TIP]
> In alternativa, è possibile utilizzare [Data Factory di Azure](https://azure.microsoft.com/services/data-factory/) toocreate e pianificare una pipeline che sposta dati tooa macchina virtuale SQL Server in Azure. Per altre informazioni, vedere [Copia di dati con Data factory di Azure (Attività di copia)](../data-factory/data-factory-data-movement-activities.md).
>
>

## <a name="prereqs"></a>Prerequisiti
Il tutorial presuppone:

* Una **sottoscrizione di Azure**. Se non si ha una sottoscrizione, è possibile iscriversi per provare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Un **account di archiviazione Azure**. Utilizzare un account di archiviazione di Azure per archiviare i dati di hello in questa esercitazione. Se non si dispone di un account di archiviazione di Azure, vedere hello [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) articolo. Dopo aver creato l'account di archiviazione hello, occorrerà account hello tooobtain chiave utilizzata l'archiviazione di hello tooaccess. Vedere la sezione [Gestire le chiavi di accesso alle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Provisioning di **SQL Server in una VM di Azure**. Per le istruzioni, vedere [Configurare una macchina virtuale SQL Server di Azure come server IPython Notebook per l'analisi avanzata](machine-learning-data-science-setup-sql-server-virtual-machine.md).
* Installazione e configurazione di **Azure PowerShell** in locale. Per istruzioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

## <a name="filesource_to_sqlonazurevm"></a>Spostamento dei dati da un tooSQL origine file flat Server in una macchina virtuale di Azure
Se i dati sono in un file flat (disposto in un formato di riga/colonna), può essere spostato tooSQL Server VM in Azure tramite hello dei seguenti metodi:

1. [Utilità copia di massa della riga di comando (BCP)](#insert-tables-bcp)
2. [Inserimento di massa query SQL ](#insert-tables-bulkquery)
3. [Utilità grafiche integrate in SQL Server (importazione/esportazione, SSIS)](#sql-builtin-utilities)

### <a name="insert-tables-bcp"></a>Utilità copia di massa della riga di comando (BCP)
BCP è un'utilità della riga di comando installata con SQL Server ed è uno dei dati di toomove modi più rapido hello. Funziona in tutte e tre le varianti di SQL Server (SQL Server locale, SQL Azure e macchine virtuali SQL Server in Azure).

> [!NOTE]
> **Dove devono trovarsi i dati per eseguire la copia BCP?**  
> Sebbene non obbligatorio, il file contenente dati di origine nello stesso computer di destinazione hello SQL Server consente i trasferimenti più veloci (velocità vs locale disco di rete la velocità dei / o) hello. È possibile spostare una macchina di toohello contenente dati di file flat hello in cui è installato SQL Server utilizzando la copia dei file vari strumenti, ad esempio [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) oppure copiare e incollare windows tramite remoto Desktop Protocol (RDP).
>
>

1. Verificare che i database di hello e tabelle hello vengono create nel database di SQL Server di destinazione hello. Di seguito è riportato un esempio di come toodo che l'utilizzo di hello `Create Database` e `Create Table` comandi:

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. Generare hello file di formato che descrive lo schema di hello per tabella hello eseguendo hello comando seguente dalla riga di comando della macchina hello hello in cui è installato bcp.

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. Inserire dati hello database hello comando hello bcp come indicato di seguito. Supponendo che hello è installato SQL Server nello stesso computer, questo dovrebbe funzionare da hello della riga di comando:

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> **Ottimizzazione BCP inserisce** , vedere l'articolo seguente hello ['Linee guida per l'ottimizzazione dell'importazione Bulk'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) inserisce toooptimize questo tipo.
>
>

### <a name="insert-tables-bulkquery-parallel"></a>Parallelizzazione delle operazioni di inserimento per uno spostamento dei dati più veloce
Se si spostano dati di hello sono grandi, è possibile velocizzare il eseguendo contemporaneamente più comandi BCP in parallelo in uno Script di PowerShell.

> [!NOTE]
> **Inserimento di dati Big** toooptimize dati di caricamento per i set di dati di grandi, partizionare le tabelle di database logico e fisico con più tabelle di partizione e i filegroup. Per ulteriori informazioni sulla creazione e caricamento di dati toopartition tabelle, vedere [tabelle delle partizioni SQL caricamento parallelo](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
>
>

Hello script di PowerShell di esempio riportato di seguito illustrano parallelo degli inserimenti tramite bcp:

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <a name="insert-tables-bulkquery"></a>Inserimento di massa query SQL
[Bulk Insert Query SQL](https://msdn.microsoft.com/library/ms188365) possono essere utilizzati tooimport dati nel database di hello dai file basato su righe e colonne (tipi hello supportato sono trattate nel[prepara i dati per l'importazione (SQL Server) o l'esportazione Bulk](https://msdn.microsoft.com/library/ms188609)) argomento.

Ecco alcuni comandi di esempio per l'inserimento di massa:  

1. Analizzare i dati e impostare le opzioni personalizzate prima dell'importazione toomake che il database di SQL Server hello presuppone hello stesso formato per tutti i campi speciali, ad esempio le date. Di seguito è riportato un esempio di come tooset hello formato anno-mese-giorno (se i dati contengono date hello nel formato anno-mese-giorno):

        SET DATEFORMAT ymd;    
2. portare i dati utilizzando le istruzioni per eseguire importazioni di massa

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <a name="sql-builtin-utilities"></a>Utilità integrate in SQL Server
È possibile utilizzare i dati di SQL Server Integrations Services (SSIS) tooimport nella macchina virtuale di SQL Server in Azure da un file flat.
SSIS è disponibile in due ambienti studio. Per ulteriori informazioni, vedere [Integration Services (SSIS) e ambienti Studio](https://technet.microsoft.com/library/ms140028.aspx):

* Per informazioni dettagliate su SQL Server Data Tools, vedere [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)  
* Per informazioni dettagliate su hello importazione/esportazione guidata, vedere [SQL Server di importazione / esportazione guidata](https://msdn.microsoft.com/library/ms141209.aspx)

## <a name="sqlonprem_to_sqlonazurevm"></a>Spostamento dei dati da tooSQL di SQL Server on-premise Server in una macchina virtuale di Azure
È inoltre possibile utilizzare hello strategie di migrazione seguenti:

1. [Distribuzione guidata di Microsoft Azure VM tooa un Database di SQL Server](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [Esportazione tooFlat File](#export-flat-file)
3. [Migrazione guidata database SQL](#sql-migration)
4. [Backup e ripristino database](#sql-backup)

Tali procedure vengono descritte qui di seguito:

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a>Distribuzione guidata di Microsoft Azure VM tooa un Database di SQL Server
Hello **distribuzione guidata di Microsoft Azure VM tooa un Database di SQL Server** è di tipo semplice e consigliato toomove data da un tooSQL di istanza di SQL Server on-premise Server in una macchina virtuale di Azure. Per i passaggi dettagliati, nonché una descrizione delle altre alternative, vedere [eseguire la migrazione di un Server in una macchina virtuale Azure di tooSQL database](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).

### <a name="export-flat-file"></a>Esportazione tooFlat File
Vari metodi possono essere utilizzato toobulk esportazione dei dati da un Server SQL locale, come documentato in hello [Bulk importazione ed esportazione di dati (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) argomento. Ad esempio, questo documento verrà illustrate hello del programma di copia Bulk (BCP). Una volta che i dati vengono esportati in un file flat, può essere importato tooanother SQL server tramite l'importazione bulk.

1. Esportare i dati di hello da tooa di SQL Server on-premise File utilizzando utilità bcp hello nel modo seguente

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. Creare database hello e una tabella di hello nella macchina virtuale di SQL Server in Azure utilizzando hello `create database` e `create table` per schema della tabella hello esportato nel passaggio 1.
3. Creare un file di formato per la descrizione dello schema di tabella hello hello dati di esportazione/importazione. Sono descritti i dettagli del file di formato hello in [creare un File di formato (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).

    Generazione di file di formato quando esegue BCP da hello computer SQL Server

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    Creazione di file di formato quando si esegue BCP in remoto rispetto a SQL Server

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. Utilizzare uno dei metodi di hello descritti nella sezione [spostamento di dati da File di origine](#filesource_to_sqlonazurevm) dati hello toomove in file flat tooa SQL Server.

### <a name="sql-migration"></a>Migrazione guidata database SQL
[Migrazione guidata Database di SQL Server](http://sqlazuremw.codeplex.com/) fornisce toomove un modo semplice i dati tra due istanze di SQL server. Consente di hello utente toomap hello schema di dati tra origini e le tabelle di destinazione, scegliere i tipi di colonna e varie altre funzionalità. Usa la copia bulk (BCP) in copre hello. Una schermata di hello Benvenuti schermata per la migrazione del Database SQL di seguito è riportata guidata hello.  

![Migrazione guidata in SQL Server][2]

### <a name="sql-backup"></a>Backup e ripristino database
SQL Server supporta:

1. [Back backup e ripristino dei database funzionalità](https://msdn.microsoft.com/library/ms187048.aspx) (entrambi tooa locale bacpac o file di esportazione tooblob) e [applicazioni livello dati](https://msdn.microsoft.com/library/ee210546.aspx) (tramite bacpac).
2. Toodirectly possibilità di creare macchine virtuali di SQL Server in Azure con un database di SQL Azure copia tooan esistente o il database copiato. Per ulteriori informazioni, vedere [hello utilizzare Copia guidata Database](https://msdn.microsoft.com/library/ms188664.aspx).

Backup/ripristino di una schermata dei backup del Database hello opzioni da SQL Server Management Studio è illustrato di seguito.

![Strumento di importazione di SQL Server][1]

## <a name="resources"></a>Risorse
[Eseguire la migrazione di un tooSQL Database Server in una macchina virtuale di Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[Panoramica di SQL Server in macchine virtuali di Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
