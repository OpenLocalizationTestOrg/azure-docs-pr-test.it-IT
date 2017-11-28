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
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="1c554-103">Spostare dati tooSQL Server in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="1c554-103">Move data tooSQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="1c554-104">In questo argomento vengono descritte le opzioni di hello per lo spostamento dei dati da file flat (formati CSV o TSV) o da un tooSQL di Server SQL Server locale in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c554-104">This topic outlines hello options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server tooSQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="1c554-105">Queste attività per lo spostamento dati nel cloud toohello fanno parte del processo di analisi scientifica dei dati di Team hello.</span><span class="sxs-lookup"><span data-stu-id="1c554-105">These tasks for moving data toohello cloud are part of hello Team Data Science Process.</span></span>

<span data-ttu-id="1c554-106">Per un argomento che descrive le opzioni di hello per lo spostamento dati tooan Database SQL di Azure per Machine Learning, vedere [spostare dati tooan Database SQL di Azure per Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="1c554-106">For a topic that outlines hello options for moving data tooan Azure SQL Database for Machine Learning, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="1c554-107">Hello **menu** seguito tootopics collegamenti che descrivono come dati tooingest in altri ambienti di destinazione in cui i dati hello possono essere archiviati ed elaborati durante hello Team Data Science processo (TDSP).</span><span class="sxs-lookup"><span data-stu-id="1c554-107">hello **menu** below links tootopics that describe how tooingest data into other target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="1c554-108">Hello nella tabella seguente sono riepilogate le opzioni di hello per lo spostamento dati tooSQL Server in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c554-108">hello following table summarizes hello options for moving data tooSQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="1c554-109"><b>SOURCE</b></span><span class="sxs-lookup"><span data-stu-id="1c554-109"><b>SOURCE</b></span></span> | <span data-ttu-id="1c554-110"><b>DESTINAZIONE: SQL Server in VM di Azure</b></span><span class="sxs-lookup"><span data-stu-id="1c554-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="1c554-111"><b>File Flat</b></span><span class="sxs-lookup"><span data-stu-id="1c554-111"><b>Flat File</b></span></span> |<span data-ttu-id="1c554-112">1. <a href="#insert-tables-bcp">Utilità copia di massa della riga di comando (BCP) </a></span><span class="sxs-lookup"><span data-stu-id="1c554-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="1c554-113">2. <a href="#insert-tables-bulkquery">Inserimento di massa query SQL </a></span><span class="sxs-lookup"><span data-stu-id="1c554-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="1c554-114">3. <a href="#sql-builtin-utilities">Utilità grafiche integrate in SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="1c554-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="1c554-115"><b>Server SQL locale</b></span><span class="sxs-lookup"><span data-stu-id="1c554-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="1c554-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Distribuzione guidata di Microsoft Azure VM tooa un Database di SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="1c554-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="1c554-117">2. <a href="#export-flat-file">Esportare tooa File flat</a></span><span class="sxs-lookup"><span data-stu-id="1c554-117">2. <a href="#export-flat-file">Export tooa flat File </a></span></span><br> <span data-ttu-id="1c554-118">3. <a href="#sql-migration">Migrazione guidata database SQL </a></span><span class="sxs-lookup"><span data-stu-id="1c554-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="1c554-119">4. <a href="#sql-backup">Backup e ripristino database </a></span><span class="sxs-lookup"><span data-stu-id="1c554-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="1c554-120">Tenere presente che il presente documento presuppone che i comandi SQL vengano eseguiti da SQL Server Management Studio o Visual Studio Database Explorer.</span><span class="sxs-lookup"><span data-stu-id="1c554-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="1c554-121">In alternativa, è possibile utilizzare [Data Factory di Azure](https://azure.microsoft.com/services/data-factory/) toocreate e pianificare una pipeline che sposta dati tooa macchina virtuale SQL Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="1c554-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate and schedule a pipeline that will move data tooa SQL Server VM on Azure.</span></span> <span data-ttu-id="1c554-122">Per altre informazioni, vedere [Copia di dati con Data factory di Azure (Attività di copia)](../data-factory/data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="1c554-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="1c554-123"><a name="prereqs"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1c554-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="1c554-124">Il tutorial presuppone:</span><span class="sxs-lookup"><span data-stu-id="1c554-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="1c554-125">Una **sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="1c554-125">An **Azure subscription**.</span></span> <span data-ttu-id="1c554-126">Se non si ha una sottoscrizione, è possibile iscriversi per provare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c554-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1c554-127">Un **account di archiviazione Azure**.</span><span class="sxs-lookup"><span data-stu-id="1c554-127">An **Azure storage account**.</span></span> <span data-ttu-id="1c554-128">Utilizzare un account di archiviazione di Azure per archiviare i dati di hello in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1c554-128">You will use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="1c554-129">Se non si dispone di un account di archiviazione di Azure, vedere hello [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) articolo.</span><span class="sxs-lookup"><span data-stu-id="1c554-129">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="1c554-130">Dopo aver creato l'account di archiviazione hello, occorrerà account hello tooobtain chiave utilizzata l'archiviazione di hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="1c554-130">After you have created hello storage account, you will need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="1c554-131">Vedere la sezione [Gestire le chiavi di accesso alle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="1c554-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="1c554-132">Provisioning di **SQL Server in una VM di Azure**.</span><span class="sxs-lookup"><span data-stu-id="1c554-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="1c554-133">Per le istruzioni, vedere [Configurare una macchina virtuale SQL Server di Azure come server IPython Notebook per l'analisi avanzata](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="1c554-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="1c554-134">Installazione e configurazione di **Azure PowerShell** in locale.</span><span class="sxs-lookup"><span data-stu-id="1c554-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="1c554-135">Per istruzioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1c554-135">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="1c554-136"><a name="filesource_to_sqlonazurevm"></a>Spostamento dei dati da un tooSQL origine file flat Server in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="1c554-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="1c554-137">Se i dati sono in un file flat (disposto in un formato di riga/colonna), può essere spostato tooSQL Server VM in Azure tramite hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="1c554-137">If your data is in a flat file (arranged in a row/column format), it can be moved tooSQL Server VM on Azure via hello following methods:</span></span>

1. [<span data-ttu-id="1c554-138">Utilità copia di massa della riga di comando (BCP)</span><span class="sxs-lookup"><span data-stu-id="1c554-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="1c554-139">Inserimento di massa query SQL </span><span class="sxs-lookup"><span data-stu-id="1c554-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="1c554-140">Utilità grafiche integrate in SQL Server (importazione/esportazione, SSIS)</span><span class="sxs-lookup"><span data-stu-id="1c554-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="1c554-141"><a name="insert-tables-bcp"></a>Utilità copia di massa della riga di comando (BCP)</span><span class="sxs-lookup"><span data-stu-id="1c554-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="1c554-142">BCP è un'utilità della riga di comando installata con SQL Server ed è uno dei dati di toomove modi più rapido hello.</span><span class="sxs-lookup"><span data-stu-id="1c554-142">BCP is a command-line utility installed with SQL Server and is one of hello quickest ways toomove data.</span></span> <span data-ttu-id="1c554-143">Funziona in tutte e tre le varianti di SQL Server (SQL Server locale, SQL Azure e macchine virtuali SQL Server in Azure).</span><span class="sxs-lookup"><span data-stu-id="1c554-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="1c554-144">**Dove devono trovarsi i dati per eseguire la copia BCP?**</span><span class="sxs-lookup"><span data-stu-id="1c554-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="1c554-145">Sebbene non obbligatorio, il file contenente dati di origine nello stesso computer di destinazione hello SQL Server consente i trasferimenti più veloci (velocità vs locale disco di rete la velocità dei / o) hello.</span><span class="sxs-lookup"><span data-stu-id="1c554-145">While it is not required, having files containing source data located on hello same machine as hello target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="1c554-146">È possibile spostare una macchina di toohello contenente dati di file flat hello in cui è installato SQL Server utilizzando la copia dei file vari strumenti, ad esempio [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) oppure copiare e incollare windows tramite remoto Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="1c554-146">You can move hello flat files containing data toohello machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="1c554-147">Verificare che i database di hello e tabelle hello vengono create nel database di SQL Server di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="1c554-147">Ensure that hello database and hello tables are created on hello target SQL Server database.</span></span> <span data-ttu-id="1c554-148">Di seguito è riportato un esempio di come toodo che l'utilizzo di hello `Create Database` e `Create Table` comandi:</span><span class="sxs-lookup"><span data-stu-id="1c554-148">Here is an example of how toodo that using hello `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="1c554-149">Generare hello file di formato che descrive lo schema di hello per tabella hello eseguendo hello comando seguente dalla riga di comando della macchina hello hello in cui è installato bcp.</span><span class="sxs-lookup"><span data-stu-id="1c554-149">Generate hello format file that describes hello schema for hello table by issuing hello following command from hello command-line of hello machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="1c554-150">Inserire dati hello database hello comando hello bcp come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1c554-150">Insert hello data into hello database using hello bcp command as follows.</span></span> <span data-ttu-id="1c554-151">Supponendo che hello è installato SQL Server nello stesso computer, questo dovrebbe funzionare da hello della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="1c554-151">This should work from hello command-line assuming that hello SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="1c554-152">**Ottimizzazione BCP inserisce** , vedere l'articolo seguente hello ['Linee guida per l'ottimizzazione dell'importazione Bulk'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) inserisce toooptimize questo tipo.</span><span class="sxs-lookup"><span data-stu-id="1c554-152">**Optimizing BCP Inserts** Please refer hello following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize such inserts.</span></span>
>
>

### <span data-ttu-id="1c554-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizzazione delle operazioni di inserimento per uno spostamento dei dati più veloce</span><span class="sxs-lookup"><span data-stu-id="1c554-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="1c554-154">Se si spostano dati di hello sono grandi, è possibile velocizzare il eseguendo contemporaneamente più comandi BCP in parallelo in uno Script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c554-154">If hello data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="1c554-155">**Inserimento di dati Big** toooptimize dati di caricamento per i set di dati di grandi, partizionare le tabelle di database logico e fisico con più tabelle di partizione e i filegroup.</span><span class="sxs-lookup"><span data-stu-id="1c554-155">**Big data Ingestion** toooptimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="1c554-156">Per ulteriori informazioni sulla creazione e caricamento di dati toopartition tabelle, vedere [tabelle delle partizioni SQL caricamento parallelo](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="1c554-156">For more information about creating and loading data toopartition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="1c554-157">Hello script di PowerShell di esempio riportato di seguito illustrano parallelo degli inserimenti tramite bcp:</span><span class="sxs-lookup"><span data-stu-id="1c554-157">hello sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

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


### <span data-ttu-id="1c554-158"><a name="insert-tables-bulkquery"></a>Inserimento di massa query SQL</span><span class="sxs-lookup"><span data-stu-id="1c554-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="1c554-159">[Bulk Insert Query SQL](https://msdn.microsoft.com/library/ms188365) possono essere utilizzati tooimport dati nel database di hello dai file basato su righe e colonne (tipi hello supportato sono trattate nel[prepara i dati per l'importazione (SQL Server) o l'esportazione Bulk](https://msdn.microsoft.com/library/ms188609)) argomento.</span><span class="sxs-lookup"><span data-stu-id="1c554-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used tooimport data into hello database from row/column based files (hello supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="1c554-160">Ecco alcuni comandi di esempio per l'inserimento di massa:</span><span class="sxs-lookup"><span data-stu-id="1c554-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="1c554-161">Analizzare i dati e impostare le opzioni personalizzate prima dell'importazione toomake che il database di SQL Server hello presuppone hello stesso formato per tutti i campi speciali, ad esempio le date.</span><span class="sxs-lookup"><span data-stu-id="1c554-161">Analyze your data and set any custom options before importing toomake sure that hello SQL Server database assumes hello same format for any special fields such as dates.</span></span> <span data-ttu-id="1c554-162">Di seguito è riportato un esempio di come tooset hello formato anno-mese-giorno (se i dati contengono date hello nel formato anno-mese-giorno):</span><span class="sxs-lookup"><span data-stu-id="1c554-162">Here is an example of how tooset hello date format as year-month-day (if your data contains hello date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="1c554-163">portare i dati utilizzando le istruzioni per eseguire importazioni di massa</span><span class="sxs-lookup"><span data-stu-id="1c554-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <span data-ttu-id="1c554-164"><a name="sql-builtin-utilities"></a>Utilità integrate in SQL Server</span><span class="sxs-lookup"><span data-stu-id="1c554-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="1c554-165">È possibile utilizzare i dati di SQL Server Integrations Services (SSIS) tooimport nella macchina virtuale di SQL Server in Azure da un file flat.</span><span class="sxs-lookup"><span data-stu-id="1c554-165">You can use SQL Server Integrations Services (SSIS) tooimport data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="1c554-166">SSIS è disponibile in due ambienti studio.</span><span class="sxs-lookup"><span data-stu-id="1c554-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="1c554-167">Per ulteriori informazioni, vedere [Integration Services (SSIS) e ambienti Studio](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="1c554-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="1c554-168">Per informazioni dettagliate su SQL Server Data Tools, vedere [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="1c554-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="1c554-169">Per informazioni dettagliate su hello importazione/esportazione guidata, vedere [SQL Server di importazione / esportazione guidata](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="1c554-169">For details on hello Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="1c554-170"><a name="sqlonprem_to_sqlonazurevm"></a>Spostamento dei dati da tooSQL di SQL Server on-premise Server in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="1c554-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="1c554-171">È inoltre possibile utilizzare hello strategie di migrazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="1c554-171">You can also use hello following migration strategies:</span></span>

1. [<span data-ttu-id="1c554-172">Distribuzione guidata di Microsoft Azure VM tooa un Database di SQL Server</span><span class="sxs-lookup"><span data-stu-id="1c554-172">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="1c554-173">Esportazione tooFlat File</span><span class="sxs-lookup"><span data-stu-id="1c554-173">Export tooFlat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="1c554-174">Migrazione guidata database SQL</span><span class="sxs-lookup"><span data-stu-id="1c554-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="1c554-175">Backup e ripristino database</span><span class="sxs-lookup"><span data-stu-id="1c554-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="1c554-176">Tali procedure vengono descritte qui di seguito:</span><span class="sxs-lookup"><span data-stu-id="1c554-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a><span data-ttu-id="1c554-177">Distribuzione guidata di Microsoft Azure VM tooa un Database di SQL Server</span><span class="sxs-lookup"><span data-stu-id="1c554-177">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>
<span data-ttu-id="1c554-178">Hello **distribuzione guidata di Microsoft Azure VM tooa un Database di SQL Server** è di tipo semplice e consigliato toomove data da un tooSQL di istanza di SQL Server on-premise Server in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c554-178">hello **Deploy a SQL Server Database tooa Microsoft Azure VM wizard** is a simple and recommended way toomove data from an on-premises SQL Server instance tooSQL Server on an Azure VM.</span></span> <span data-ttu-id="1c554-179">Per i passaggi dettagliati, nonché una descrizione delle altre alternative, vedere [eseguire la migrazione di un Server in una macchina virtuale Azure di tooSQL database](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="1c554-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database tooSQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="1c554-180"><a name="export-flat-file"></a>Esportazione tooFlat File</span><span class="sxs-lookup"><span data-stu-id="1c554-180"><a name="export-flat-file"></a>Export tooFlat File</span></span>
<span data-ttu-id="1c554-181">Vari metodi possono essere utilizzato toobulk esportazione dei dati da un Server SQL locale, come documentato in hello [Bulk importazione ed esportazione di dati (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) argomento.</span><span class="sxs-lookup"><span data-stu-id="1c554-181">Various methods can be used toobulk export data from an On-Premises SQL Server as documented in hello [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="1c554-182">Ad esempio, questo documento verrà illustrate hello del programma di copia Bulk (BCP).</span><span class="sxs-lookup"><span data-stu-id="1c554-182">This document will cover hello Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="1c554-183">Una volta che i dati vengono esportati in un file flat, può essere importato tooanother SQL server tramite l'importazione bulk.</span><span class="sxs-lookup"><span data-stu-id="1c554-183">Once data is exported into a flat file, it can be imported tooanother SQL server using bulk import.</span></span>

1. <span data-ttu-id="1c554-184">Esportare i dati di hello da tooa di SQL Server on-premise File utilizzando utilità bcp hello nel modo seguente</span><span class="sxs-lookup"><span data-stu-id="1c554-184">Export hello data from on-premises SQL Server tooa File using hello bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="1c554-185">Creare database hello e una tabella di hello nella macchina virtuale di SQL Server in Azure utilizzando hello `create database` e `create table` per schema della tabella hello esportato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="1c554-185">Create hello database and hello table on SQL Server VM on Azure using hello `create database` and `create table` for hello table schema exported in step 1.</span></span>
3. <span data-ttu-id="1c554-186">Creare un file di formato per la descrizione dello schema di tabella hello hello dati di esportazione/importazione.</span><span class="sxs-lookup"><span data-stu-id="1c554-186">Create a format file for describing hello table schema of hello data being exported/imported.</span></span> <span data-ttu-id="1c554-187">Sono descritti i dettagli del file di formato hello in [creare un File di formato (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c554-187">Details of hello format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="1c554-188">Generazione di file di formato quando esegue BCP da hello computer SQL Server</span><span class="sxs-lookup"><span data-stu-id="1c554-188">Format file generation when running BCP from hello SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="1c554-189">Creazione di file di formato quando si esegue BCP in remoto rispetto a SQL Server</span><span class="sxs-lookup"><span data-stu-id="1c554-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="1c554-190">Utilizzare uno dei metodi di hello descritti nella sezione [spostamento di dati da File di origine](#filesource_to_sqlonazurevm) dati hello toomove in file flat tooa SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1c554-190">Use any of hello methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) toomove hello data in flat files tooa SQL Server.</span></span>

### <span data-ttu-id="1c554-191"><a name="sql-migration"></a>Migrazione guidata database SQL</span><span class="sxs-lookup"><span data-stu-id="1c554-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="1c554-192">[Migrazione guidata Database di SQL Server](http://sqlazuremw.codeplex.com/) fornisce toomove un modo semplice i dati tra due istanze di SQL server.</span><span class="sxs-lookup"><span data-stu-id="1c554-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way toomove data between two SQL server instances.</span></span> <span data-ttu-id="1c554-193">Consente di hello utente toomap hello schema di dati tra origini e le tabelle di destinazione, scegliere i tipi di colonna e varie altre funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1c554-193">It allows hello user toomap hello data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="1c554-194">Usa la copia bulk (BCP) in copre hello.</span><span class="sxs-lookup"><span data-stu-id="1c554-194">It uses bulk copy (BCP) under hello covers.</span></span> <span data-ttu-id="1c554-195">Una schermata di hello Benvenuti schermata per la migrazione del Database SQL di seguito è riportata guidata hello.</span><span class="sxs-lookup"><span data-stu-id="1c554-195">A screenshot of hello welcome screen for hello SQL Database Migration wizard is shown below.</span></span>  

![Migrazione guidata in SQL Server][2]

### <span data-ttu-id="1c554-197"><a name="sql-backup"></a>Backup e ripristino database</span><span class="sxs-lookup"><span data-stu-id="1c554-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="1c554-198">SQL Server supporta:</span><span class="sxs-lookup"><span data-stu-id="1c554-198">SQL Server supports:</span></span>

1. <span data-ttu-id="1c554-199">[Back backup e ripristino dei database funzionalità](https://msdn.microsoft.com/library/ms187048.aspx) (entrambi tooa locale bacpac o file di esportazione tooblob) e [applicazioni livello dati](https://msdn.microsoft.com/library/ee210546.aspx) (tramite bacpac).</span><span class="sxs-lookup"><span data-stu-id="1c554-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both tooa local file or bacpac export tooblob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="1c554-200">Toodirectly possibilità di creare macchine virtuali di SQL Server in Azure con un database di SQL Azure copia tooan esistente o il database copiato.</span><span class="sxs-lookup"><span data-stu-id="1c554-200">Ability toodirectly create SQL Server VMs on Azure with a copied database or copy tooan existing SQL Azure database.</span></span> <span data-ttu-id="1c554-201">Per ulteriori informazioni, vedere [hello utilizzare Copia guidata Database](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c554-201">For more details, see [Use hello Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="1c554-202">Backup/ripristino di una schermata dei backup del Database hello opzioni da SQL Server Management Studio è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1c554-202">A screenshot of hello Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![Strumento di importazione di SQL Server][1]

## <a name="resources"></a><span data-ttu-id="1c554-204">Risorse</span><span class="sxs-lookup"><span data-stu-id="1c554-204">Resources</span></span>
[<span data-ttu-id="1c554-205">Eseguire la migrazione di un tooSQL Database Server in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="1c554-205">Migrate a Database tooSQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="1c554-206">Panoramica di SQL Server in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="1c554-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
