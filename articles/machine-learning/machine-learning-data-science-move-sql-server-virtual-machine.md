---
title: Spostamento dei dati in SQL Server in una macchina virtuale di Azure | Documentazione Microsoft
description: Spostare i dati da file flat o da un Server SQL locale a SQL Server su VM di Azure
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
ms.openlocfilehash: aa0cbba6bdb4cfdfe6ceee50c94f706aa0974924
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-sql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="9c08b-103">Spostamento dei dati in SQL Server in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="9c08b-103">Move data to SQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="9c08b-104">Questo argomento descrive le opzioni per lo spostamento dei dati da file flat con estensione csv o tsv o da SQL Server locale a SQL Server in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c08b-104">This topic outlines the options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server to SQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="9c08b-105">Queste attività per lo spostamento dei dati nel cloud fanno parte del Processo di analisi scientifica dei dati per i team.</span><span class="sxs-lookup"><span data-stu-id="9c08b-105">These tasks for moving data to the cloud are part of the Team Data Science Process.</span></span>

<span data-ttu-id="9c08b-106">Per un argomento che descrive le opzioni per lo spostamento dei dati a un database SQL Azure per Machine Learning, vedere [Spostare i dati a un Database di SQL Azure per Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="9c08b-106">For a topic that outlines the options for moving data to an Azure SQL Database for Machine Learning, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="9c08b-107">Il **menu** seguente si collega ad argomenti che descrivono come inserire dati in altri ambienti di destinazione in cui i dati possono essere archiviati ed elaborati durante il Processo di analisi scientifica dei dati per i team (TDSP).</span><span class="sxs-lookup"><span data-stu-id="9c08b-107">The **menu** below links to topics that describe how to ingest data into other target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="9c08b-108">Nella tabella seguente vengono riepilogate le opzioni per lo spostamento dei dati in SQL Server in una macchina virtuale Azure.</span><span class="sxs-lookup"><span data-stu-id="9c08b-108">The following table summarizes the options for moving data to SQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="9c08b-109"><b>SOURCE</b></span><span class="sxs-lookup"><span data-stu-id="9c08b-109"><b>SOURCE</b></span></span> | <span data-ttu-id="9c08b-110"><b>DESTINAZIONE: SQL Server in VM di Azure</b></span><span class="sxs-lookup"><span data-stu-id="9c08b-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="9c08b-111"><b>File Flat</b></span><span class="sxs-lookup"><span data-stu-id="9c08b-111"><b>Flat File</b></span></span> |<span data-ttu-id="9c08b-112">1. <a href="#insert-tables-bcp">Utilità copia di massa della riga di comando (BCP) </a></span><span class="sxs-lookup"><span data-stu-id="9c08b-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="9c08b-113">2. <a href="#insert-tables-bulkquery">Inserimento di massa query SQL </a></span><span class="sxs-lookup"><span data-stu-id="9c08b-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="9c08b-114">3. <a href="#sql-builtin-utilities">Utilità grafiche integrate in SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="9c08b-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="9c08b-115"><b>Server SQL locale</b></span><span class="sxs-lookup"><span data-stu-id="9c08b-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="9c08b-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Distribuzione di un database di SQL Server a una macchina virtuale di Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="9c08b-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database to a Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="9c08b-117">2. <a href="#export-flat-file">Esportazione in un file flat </a></span><span class="sxs-lookup"><span data-stu-id="9c08b-117">2. <a href="#export-flat-file">Export to a flat File </a></span></span><br> <span data-ttu-id="9c08b-118">3. <a href="#sql-migration">Migrazione guidata database SQL </a></span><span class="sxs-lookup"><span data-stu-id="9c08b-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="9c08b-119">4. <a href="#sql-backup">Backup e ripristino database </a></span><span class="sxs-lookup"><span data-stu-id="9c08b-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="9c08b-120">Tenere presente che il presente documento presuppone che i comandi SQL vengano eseguiti da SQL Server Management Studio o Visual Studio Database Explorer.</span><span class="sxs-lookup"><span data-stu-id="9c08b-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="9c08b-121">In alternativa, è possibile usare [Data factory di Azure](https://azure.microsoft.com/services/data-factory/) per creare e pianificare una pipeline che sposta i dati a una macchina virtuale di SQL Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="9c08b-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to create and schedule a pipeline that will move data to a SQL Server VM on Azure.</span></span> <span data-ttu-id="9c08b-122">Per altre informazioni, vedere [Copia di dati con Data factory di Azure (Attività di copia)](../data-factory/data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9c08b-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="9c08b-123"><a name="prereqs"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9c08b-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="9c08b-124">Il tutorial presuppone:</span><span class="sxs-lookup"><span data-stu-id="9c08b-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="9c08b-125">Una **sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c08b-125">An **Azure subscription**.</span></span> <span data-ttu-id="9c08b-126">Se non si ha una sottoscrizione, è possibile iscriversi per provare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9c08b-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9c08b-127">Un **account di archiviazione Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c08b-127">An **Azure storage account**.</span></span> <span data-ttu-id="9c08b-128">In questa esercitazione si userà un account di archiviazione di Azure per archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="9c08b-128">You will use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="9c08b-129">Se non si dispone di un account di archiviazione di Azure, vedere l'articolo [Creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="9c08b-129">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="9c08b-130">Dopo avere creato l'account di archiviazione, sarà necessario ottenere la chiave dell'account usata per accedere alla risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9c08b-130">After you have created the storage account, you will need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="9c08b-131">Vedere la sezione [Gestire le chiavi di accesso alle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="9c08b-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="9c08b-132">Provisioning di **SQL Server in una VM di Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c08b-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="9c08b-133">Per le istruzioni, vedere [Configurare una macchina virtuale SQL Server di Azure come server IPython Notebook per l'analisi avanzata](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="9c08b-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="9c08b-134">Installazione e configurazione di **Azure PowerShell** in locale.</span><span class="sxs-lookup"><span data-stu-id="9c08b-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="9c08b-135">Per istruzioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9c08b-135">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="9c08b-136"><a name="filesource_to_sqlonazurevm"></a> Spostamento di dati da un'origine di file flat a SQL Server su una VM di Azure</span><span class="sxs-lookup"><span data-stu-id="9c08b-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source to SQL Server on an Azure VM</span></span>
<span data-ttu-id="9c08b-137">Se i dati si trovano in un file flat (organizzati in un formato righe/colonne), possono essere spostati a una macchina virtuale di SQL Server attraverso i seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="9c08b-137">If your data is in a flat file (arranged in a row/column format), it can be moved to SQL Server VM on Azure via the following methods:</span></span>

1. [<span data-ttu-id="9c08b-138">Utilità copia di massa della riga di comando (BCP)</span><span class="sxs-lookup"><span data-stu-id="9c08b-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="9c08b-139">Inserimento di massa query SQL </span><span class="sxs-lookup"><span data-stu-id="9c08b-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="9c08b-140">Utilità grafiche integrate in SQL Server (importazione/esportazione, SSIS)</span><span class="sxs-lookup"><span data-stu-id="9c08b-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="9c08b-141"><a name="insert-tables-bcp"></a>Utilità copia di massa della riga di comando (BCP)</span><span class="sxs-lookup"><span data-stu-id="9c08b-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="9c08b-142">BCP è un'utilità della riga di comando installata con SQL Server e rappresenta uno dei metodi più rapidi per spostare i dati.</span><span class="sxs-lookup"><span data-stu-id="9c08b-142">BCP is a command-line utility installed with SQL Server and is one of the quickest ways to move data.</span></span> <span data-ttu-id="9c08b-143">Funziona in tutte e tre le varianti di SQL Server (SQL Server locale, SQL Azure e macchine virtuali SQL Server in Azure).</span><span class="sxs-lookup"><span data-stu-id="9c08b-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="9c08b-144">**Dove devono trovarsi i dati per eseguire la copia BCP?**</span><span class="sxs-lookup"><span data-stu-id="9c08b-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="9c08b-145">Anche se non è obbligatorio che i file contenenti i dati di origine si trovino nello stesso computer del server SQL di destinazione, questo garantisce trasferimenti più rapidi, a causa della differenza tra velocità di rete e velocità di I/O dei dischi locali.</span><span class="sxs-lookup"><span data-stu-id="9c08b-145">While it is not required, having files containing source data located on the same machine as the target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="9c08b-146">È possibile spostare i file flat contenenti i dati nel computer dove è installato SQL Server usando diversi strumenti per la copia dei file quali [AZCopy](../storage/common/storage-use-azcopy.md), [Esplora archivi di Azure](http://storageexplorer.com/) o la funzione di copia/incolla di Windows tramite Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="9c08b-146">You can move the flat files containing data to the machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="9c08b-147">Assicurarsi che il database e le tabelle vengano create nel database di SQL Server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9c08b-147">Ensure that the database and the tables are created on the target SQL Server database.</span></span> <span data-ttu-id="9c08b-148">Ecco un esempio di come procedere utilizzando i comandi `Create Database` e `Create Table`:</span><span class="sxs-lookup"><span data-stu-id="9c08b-148">Here is an example of how to do that using the `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="9c08b-149">Generare il file di formato che descrive lo schema per la tabella eseguendo il comando seguente dalla riga di comando del computer in cui è installato bcp.</span><span class="sxs-lookup"><span data-stu-id="9c08b-149">Generate the format file that describes the schema for the table by issuing the following command from the command-line of the machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="9c08b-150">Inserire i dati nel database utilizzando il comando bcp come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9c08b-150">Insert the data into the database using the bcp command as follows.</span></span> <span data-ttu-id="9c08b-151">Dovrebbe funzionare dalla riga di comando, presupponendo che SQL Server sia installato nello stesso computer:</span><span class="sxs-lookup"><span data-stu-id="9c08b-151">This should work from the command-line assuming that the SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="9c08b-152">**Ottimizzazione inserimenti BCP** Per ottimizzare gli inserimenti, fare riferimento al seguente articolo ["Linee guida per ottimizzare l'importazione di massa"](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="9c08b-152">**Optimizing BCP Inserts** Please refer the following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) to optimize such inserts.</span></span>
>
>

### <span data-ttu-id="9c08b-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizzazione delle operazioni di inserimento per uno spostamento dei dati più veloce</span><span class="sxs-lookup"><span data-stu-id="9c08b-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="9c08b-154">Se i dati che si stanno spostando sono grandi, è possibile velocizzare l'operazione eseguendo contemporaneamente più comandi BCP in uno script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9c08b-154">If the data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="9c08b-155">**Inserimento di Big Data** Per ottimizzare il caricamento dei dati per set di dati grandi e molto grandi, partizionare le tabelle dei database logici e fisici mediante più filegroup e tabelle di partizione.</span><span class="sxs-lookup"><span data-stu-id="9c08b-155">**Big data Ingestion** To optimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="9c08b-156">Per ulteriori informazioni sulla creazione e sul caricamento dei dati in tabelle di partizione, vedere [Caricamento parallelo di tabelle di partizione SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="9c08b-156">For more information about creating and loading data to partition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="9c08b-157">Lo script PowerShell di esempio illustra gli inserimenti mediante bcp:</span><span class="sxs-lookup"><span data-stu-id="9c08b-157">The sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for the script to execute
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


    # Wait for it all to complete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting the information back from the jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset the execution policy


### <span data-ttu-id="9c08b-158"><a name="insert-tables-bulkquery"></a>Inserimento di massa query SQL</span><span class="sxs-lookup"><span data-stu-id="9c08b-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="9c08b-159">L'[inserimento di massa di query SQL](https://msdn.microsoft.com/library/ms188365) può essere usato per importare dati nel database da file basati su righe/colonne (i tipi supportati sono indicati nell'argomento [Preparazione dei dati per l'importazione o l'esportazione bulk (SQL Server)](https://msdn.microsoft.com/library/ms188609)).</span><span class="sxs-lookup"><span data-stu-id="9c08b-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used to import data into the database from row/column based files (the supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="9c08b-160">Ecco alcuni comandi di esempio per l'inserimento di massa:</span><span class="sxs-lookup"><span data-stu-id="9c08b-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="9c08b-161">Analizzare i dati e impostare le opzioni personalizzate prima dell'importazione per assicurarsi che il database SQL Server presupponga lo stesso formato per tutti i campi speciali, ad esempio le date.</span><span class="sxs-lookup"><span data-stu-id="9c08b-161">Analyze your data and set any custom options before importing to make sure that the SQL Server database assumes the same format for any special fields such as dates.</span></span> <span data-ttu-id="9c08b-162">Ecco un esempio di come impostare il formato della data come anno-mese-giorno (se i dati contengono la data in formato anno-mese-giorno):</span><span class="sxs-lookup"><span data-stu-id="9c08b-162">Here is an example of how to set the date format as year-month-day (if your data contains the date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="9c08b-163">portare i dati utilizzando le istruzioni per eseguire importazioni di massa</span><span class="sxs-lookup"><span data-stu-id="9c08b-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be the row separator in your data
        )

### <span data-ttu-id="9c08b-164"><a name="sql-builtin-utilities"></a>Utilità integrate in SQL Server</span><span class="sxs-lookup"><span data-stu-id="9c08b-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="9c08b-165">È possibile utilizzare SQL Server Integrations Services (SSIS) per importare i dati nelle macchine virtuali SQL Server in Azure da un file flat.</span><span class="sxs-lookup"><span data-stu-id="9c08b-165">You can use SQL Server Integrations Services (SSIS) to import data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="9c08b-166">SSIS è disponibile in due ambienti studio.</span><span class="sxs-lookup"><span data-stu-id="9c08b-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="9c08b-167">Per ulteriori informazioni, vedere [Integration Services (SSIS) e ambienti Studio](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="9c08b-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="9c08b-168">Per informazioni dettagliate su SQL Server Data Tools, vedere [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="9c08b-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="9c08b-169">Per informazioni dettagliate sull'importazione/esportazione guidata, vedere [Importazione/esportazione guidata di SQL Server](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="9c08b-169">For details on the Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="9c08b-170"><a name="sqlonprem_to_sqlonazurevm"></a>Spostamento dei dati da SQL Server locale a SQL Server in una VM di Azure</span><span class="sxs-lookup"><span data-stu-id="9c08b-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server to SQL Server on an Azure VM</span></span>
<span data-ttu-id="9c08b-171">È inoltre possibile utilizzare le strategie di migrazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c08b-171">You can also use the following migration strategies:</span></span>

1. [<span data-ttu-id="9c08b-172">Distribuzione di un database di SQL Server a una macchina virtuale di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9c08b-172">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="9c08b-173">Esportazione in un file flat</span><span class="sxs-lookup"><span data-stu-id="9c08b-173">Export to Flat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="9c08b-174">Migrazione guidata database SQL</span><span class="sxs-lookup"><span data-stu-id="9c08b-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="9c08b-175">Backup e ripristino database</span><span class="sxs-lookup"><span data-stu-id="9c08b-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="9c08b-176">Tali procedure vengono descritte qui di seguito:</span><span class="sxs-lookup"><span data-stu-id="9c08b-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard"></a><span data-ttu-id="9c08b-177">Distribuzione di un database di SQL Server a una macchina virtuale di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9c08b-177">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>
<span data-ttu-id="9c08b-178">La **Distribuzione di un Database SQL Server in una macchina virtuale di Microsoft Azure** è un modo semplice e consigliato per spostare dati da un'istanza di SQL Server locale a un SQL Server in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c08b-178">The **Deploy a SQL Server Database to a Microsoft Azure VM wizard** is a simple and recommended way to move data from an on-premises SQL Server instance to SQL Server on an Azure VM.</span></span> <span data-ttu-id="9c08b-179">Per passaggi dettagliati, nonché per una descrizione delle altre alternative, vedere [Migrazione di un database a SQL Server su una macchina virtuale di Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="9c08b-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database to SQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="9c08b-180"><a name="export-flat-file"></a>Esportazione in un file flat</span><span class="sxs-lookup"><span data-stu-id="9c08b-180"><a name="export-flat-file"></a>Export to Flat File</span></span>
<span data-ttu-id="9c08b-181">È possibile usare diversi metodi per l'esportazione di massa dei dati dal Server locale SQL come descritto nell'argomento [Importazione ed esportazione dei dati in massa (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) .</span><span class="sxs-lookup"><span data-stu-id="9c08b-181">Various methods can be used to bulk export data from an On-Premises SQL Server as documented in the [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="9c08b-182">In questo documento si parla di Bulk Copy Program (BCP) come esempio.</span><span class="sxs-lookup"><span data-stu-id="9c08b-182">This document will cover the Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="9c08b-183">Una volta che i dati sono esportati in un file flat, possono essere importati in un altro server SQL mediante l'importazione di massa.</span><span class="sxs-lookup"><span data-stu-id="9c08b-183">Once data is exported into a flat file, it can be imported to another SQL server using bulk import.</span></span>

1. <span data-ttu-id="9c08b-184">Esportare i dati dal Server locale SQL in un file mediante l'utilità bcp come indicato di seguito</span><span class="sxs-lookup"><span data-stu-id="9c08b-184">Export the data from on-premises SQL Server to a File using the bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="9c08b-185">Creare il database e la tabella nella macchina virtuale di SQL Server in Azure tramite `create database` e `create table` per lo schema della tabella esportato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="9c08b-185">Create the database and the table on SQL Server VM on Azure using the `create database` and `create table` for the table schema exported in step 1.</span></span>
3. <span data-ttu-id="9c08b-186">Creare un file di formato per la descrizione dello schema della tabella dei dati da importare/esportare.</span><span class="sxs-lookup"><span data-stu-id="9c08b-186">Create a format file for describing the table schema of the data being exported/imported.</span></span> <span data-ttu-id="9c08b-187">I dettagli del file di formato sono descritti in [Creazione di un file di formato (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c08b-187">Details of the format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="9c08b-188">Creazione di file di formato quando si esegue BCP dal computer SQL Server</span><span class="sxs-lookup"><span data-stu-id="9c08b-188">Format file generation when running BCP from the SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="9c08b-189">Creazione di file di formato quando si esegue BCP in remoto rispetto a SQL Server</span><span class="sxs-lookup"><span data-stu-id="9c08b-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="9c08b-190">Utilizzare uno dei metodi descritti nella sezione [Spostamento dei dati dall'origine file](#filesource_to_sqlonazurevm) per spostare i dati dai file flat in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9c08b-190">Use any of the methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) to move the data in flat files to a SQL Server.</span></span>

### <span data-ttu-id="9c08b-191"><a name="sql-migration"></a>Migrazione guidata database SQL</span><span class="sxs-lookup"><span data-stu-id="9c08b-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="9c08b-192">[Migrazione guidata database SQL Server](http://sqlazuremw.codeplex.com/) fornisce un modo semplice per spostare i dati tra due istanze del server SQL.</span><span class="sxs-lookup"><span data-stu-id="9c08b-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way to move data between two SQL server instances.</span></span> <span data-ttu-id="9c08b-193">Consente all'utente di mappare lo schema dei dati tra origini e tabelle di destinazione, scegliere i tipi di colonna e varie altre funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9c08b-193">It allows the user to map the data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="9c08b-194">Utilizza la copia di massa (BCP) dietro le quinte.</span><span class="sxs-lookup"><span data-stu-id="9c08b-194">It uses bulk copy (BCP) under the covers.</span></span> <span data-ttu-id="9c08b-195">Di seguito è riportata una schermata della schermata iniziale della procedura guidata di migrazione del database SQL.</span><span class="sxs-lookup"><span data-stu-id="9c08b-195">A screenshot of the welcome screen for the SQL Database Migration wizard is shown below.</span></span>  

![Migrazione guidata in SQL Server][2]

### <span data-ttu-id="9c08b-197"><a name="sql-backup"></a>Backup e ripristino database</span><span class="sxs-lookup"><span data-stu-id="9c08b-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="9c08b-198">SQL Server supporta:</span><span class="sxs-lookup"><span data-stu-id="9c08b-198">SQL Server supports:</span></span>

1. <span data-ttu-id="9c08b-199">La [funzionalità di backup e ripristino del database](https://msdn.microsoft.com/library/ms187048.aspx) (sia in un file locale o in un'esportazione bacpac in un BLOB) e [applicazioni livello dati](https://msdn.microsoft.com/library/ee210546.aspx) (tramite bacpac).</span><span class="sxs-lookup"><span data-stu-id="9c08b-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both to a local file or bacpac export to blob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="9c08b-200">Possibilità di creare direttamente le macchine virtuali SQL Server in Azure con un database copiato o di copiare in un database esistente di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9c08b-200">Ability to directly create SQL Server VMs on Azure with a copied database or copy to an existing SQL Azure database.</span></span> <span data-ttu-id="9c08b-201">Per ulteriori informazioni, vedere [Utilizzo della procedura guidata di copia del database](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c08b-201">For more details, see [Use the Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="9c08b-202">Di seguito è riportata una schermata delle opzioni di backup e ripristino del database da SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="9c08b-202">A screenshot of the Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![Strumento di importazione di SQL Server][1]

## <a name="resources"></a><span data-ttu-id="9c08b-204">Risorse</span><span class="sxs-lookup"><span data-stu-id="9c08b-204">Resources</span></span>
[<span data-ttu-id="9c08b-205">Migrazione di un database a SQL Server su una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="9c08b-205">Migrate a Database to SQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="9c08b-206">Panoramica di SQL Server in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="9c08b-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
