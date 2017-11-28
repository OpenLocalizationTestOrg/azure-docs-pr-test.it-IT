---
title: Usare bcp per caricare i dati in SQL Data Warehouse | Documentazione Microsoft
description: Informazioni su bcp e sul relativo uso per scenari di data warehousing.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 7596eac10fdf53380d85128265430ce07b551fe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="e8b81-103">Caricare i dati con BCP</span><span class="sxs-lookup"><span data-stu-id="e8b81-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e8b81-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="e8b81-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="e8b81-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="e8b81-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="e8b81-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="e8b81-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="e8b81-107">BCP</span><span class="sxs-lookup"><span data-stu-id="e8b81-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="e8b81-108">**[bcp][bcp]** è un'utilità di caricamento bulk da riga di comando che permette di copiare dati tra SQL Server, file di dati e SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e8b81-108">**[bcp][bcp]** is a command-line bulk load utility that allows you to copy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="e8b81-109">Usare bcp per importare numeri elevati di righe nelle tabelle di SQL Data Warehouse o per esportare i dati dalle tabelle di SQL Server ai file di dati.</span><span class="sxs-lookup"><span data-stu-id="e8b81-109">Use bcp to import large numbers of rows into SQL Data Warehouse tables or to export data from SQL Server tables into data files.</span></span> <span data-ttu-id="e8b81-110">bcp richiede competenze in ambito di Transact-SQL solo quando viene usato con l'opzione queryout.</span><span class="sxs-lookup"><span data-stu-id="e8b81-110">Except when used with the queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="e8b81-111">bcp costituisce un modo semplice e rapido per spostare set di dati di dimensioni ridotte da e verso un database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e8b81-111">bcp is a quick and easy way to move smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="e8b81-112">La quantità esatta di dati che è consigliabile caricare/estrarre tramite bcp dipenderà dalla connessione di rete per il data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8b81-112">The exact amount of data that is recommended to load/extract via bcp will depend on you network connection to the Azure data center.</span></span>  <span data-ttu-id="e8b81-113">In genere, le tabelle delle dimensioni possono essere caricate ed estratte facilmente con bcp, tuttavia bcp non è consigliato per il caricamento o l'estrazione di grandi volumi di dati.</span><span class="sxs-lookup"><span data-stu-id="e8b81-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="e8b81-114">Lo strumento consigliato per il caricamento e l'estrazione di grandi volumi di dati è Polybase, perché offre risultati migliori con l'architettura MPP (Massively Parallel Processing, elaborazione parallela massiva) di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e8b81-114">Polybase is the recommended tool for loading and extracting large volumes of data as it does a better job leveraging the massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="e8b81-115">Con bcp è possibile:</span><span class="sxs-lookup"><span data-stu-id="e8b81-115">With bcp you can:</span></span>

* <span data-ttu-id="e8b81-116">Utilizzare una semplice utilità della riga di comando per caricare dati nell’SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e8b81-116">Use a simple command-line utility to load data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="e8b81-117">Utilizzare una semplice utilità della riga di comando per estrarre dati dall’SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e8b81-117">Use a simple command-line utility to extract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="e8b81-118">In questa esercitazione verranno illustrate le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8b81-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="e8b81-119">Importare dati in una tabella tramite l'utilità bcp nel comando</span><span class="sxs-lookup"><span data-stu-id="e8b81-119">Import data into a table using the bcp in command</span></span>
* <span data-ttu-id="e8b81-120">Esportare dati da una tabella tramite l'utilità bcp dal comando</span><span class="sxs-lookup"><span data-stu-id="e8b81-120">Export data from a table uisng the bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e8b81-121">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e8b81-121">Prerequisites</span></span>
<span data-ttu-id="e8b81-122">Per eseguire questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="e8b81-122">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="e8b81-123">Un database di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e8b81-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="e8b81-124">Utilità della riga di comando bcp installata</span><span class="sxs-lookup"><span data-stu-id="e8b81-124">The bcp command line utility installed</span></span>
* <span data-ttu-id="e8b81-125">Utilità della riga di comando SQLCMD installata</span><span class="sxs-lookup"><span data-stu-id="e8b81-125">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="e8b81-126">È possibile scaricare le utilità bcp e sqlcmd dall'[Area download Microsoft][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="e8b81-126">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="e8b81-127">Importare i dati in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e8b81-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="e8b81-128">In questa esercitazione verrà creata una tabella in Azure SQL Data Warehouse e verranno importati dati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="e8b81-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="e8b81-129">Passaggio 1: Creare una tabella in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e8b81-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="e8b81-130">Al prompt dei comandi usare sqlcmd per eseguire la query seguente per creare una tabella nell'istanza:</span><span class="sxs-lookup"><span data-stu-id="e8b81-130">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```

> [!NOTE]
> <span data-ttu-id="e8b81-131">Per altre informazioni sulla creazione di una tabella in SQL Data Warehouse e sulle opzioni disponibili con la clausola WITH, vedere [Panoramica delle tabelle][Table Overview] o la [sintassi di CREATE TABLE][CREATE TABLE syntax].</span><span class="sxs-lookup"><span data-stu-id="e8b81-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="e8b81-132">Passaggio 2: Creare un file di dati di origine</span><span class="sxs-lookup"><span data-stu-id="e8b81-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="e8b81-133">Aprire il Blocco note, copiare le righe di dati seguenti in un nuovo file di testo e quindi salvare il file nella directory temporanea locale, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="e8b81-133">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> <span data-ttu-id="e8b81-134">È importante ricordare che bcp.exe non supporta la codifica UTF-8 del file.</span><span class="sxs-lookup"><span data-stu-id="e8b81-134">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="e8b81-135">Usare i file ASCII o con codifica UTF-16 quando si usa bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="e8b81-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="e8b81-136">Passaggio 3: Connettersi e importare i dati</span><span class="sxs-lookup"><span data-stu-id="e8b81-136">Step 3: Connect and import the data</span></span>
<span data-ttu-id="e8b81-137">bcp permette di connettersi e importare i dati usando il comando seguente, sostituendo i valori in base alla necessità:</span><span class="sxs-lookup"><span data-stu-id="e8b81-137">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="e8b81-138">È possibile verificare che i dati siano stati caricati eseguendo la query seguente con sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="e8b81-138">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="e8b81-139">Dovrebbero essere visualizzati i risultati seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8b81-139">This should return the following results:</span></span>

| <span data-ttu-id="e8b81-140">DateId</span><span class="sxs-lookup"><span data-stu-id="e8b81-140">DateId</span></span> | <span data-ttu-id="e8b81-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="e8b81-141">CalendarQuarter</span></span> | <span data-ttu-id="e8b81-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="e8b81-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8b81-143">20150101</span><span class="sxs-lookup"><span data-stu-id="e8b81-143">20150101</span></span> |<span data-ttu-id="e8b81-144">1</span><span class="sxs-lookup"><span data-stu-id="e8b81-144">1</span></span> |<span data-ttu-id="e8b81-145">3</span><span class="sxs-lookup"><span data-stu-id="e8b81-145">3</span></span> |
| <span data-ttu-id="e8b81-146">20150201</span><span class="sxs-lookup"><span data-stu-id="e8b81-146">20150201</span></span> |<span data-ttu-id="e8b81-147">1</span><span class="sxs-lookup"><span data-stu-id="e8b81-147">1</span></span> |<span data-ttu-id="e8b81-148">3</span><span class="sxs-lookup"><span data-stu-id="e8b81-148">3</span></span> |
| <span data-ttu-id="e8b81-149">20150301</span><span class="sxs-lookup"><span data-stu-id="e8b81-149">20150301</span></span> |<span data-ttu-id="e8b81-150">1</span><span class="sxs-lookup"><span data-stu-id="e8b81-150">1</span></span> |<span data-ttu-id="e8b81-151">3</span><span class="sxs-lookup"><span data-stu-id="e8b81-151">3</span></span> |
| <span data-ttu-id="e8b81-152">20150401</span><span class="sxs-lookup"><span data-stu-id="e8b81-152">20150401</span></span> |<span data-ttu-id="e8b81-153">2</span><span class="sxs-lookup"><span data-stu-id="e8b81-153">2</span></span> |<span data-ttu-id="e8b81-154">4</span><span class="sxs-lookup"><span data-stu-id="e8b81-154">4</span></span> |
| <span data-ttu-id="e8b81-155">20150501</span><span class="sxs-lookup"><span data-stu-id="e8b81-155">20150501</span></span> |<span data-ttu-id="e8b81-156">2</span><span class="sxs-lookup"><span data-stu-id="e8b81-156">2</span></span> |<span data-ttu-id="e8b81-157">4</span><span class="sxs-lookup"><span data-stu-id="e8b81-157">4</span></span> |
| <span data-ttu-id="e8b81-158">20150601</span><span class="sxs-lookup"><span data-stu-id="e8b81-158">20150601</span></span> |<span data-ttu-id="e8b81-159">2</span><span class="sxs-lookup"><span data-stu-id="e8b81-159">2</span></span> |<span data-ttu-id="e8b81-160">4</span><span class="sxs-lookup"><span data-stu-id="e8b81-160">4</span></span> |
| <span data-ttu-id="e8b81-161">20150701</span><span class="sxs-lookup"><span data-stu-id="e8b81-161">20150701</span></span> |<span data-ttu-id="e8b81-162">3</span><span class="sxs-lookup"><span data-stu-id="e8b81-162">3</span></span> |<span data-ttu-id="e8b81-163">1</span><span class="sxs-lookup"><span data-stu-id="e8b81-163">1</span></span> |
| <span data-ttu-id="e8b81-164">20150801</span><span class="sxs-lookup"><span data-stu-id="e8b81-164">20150801</span></span> |<span data-ttu-id="e8b81-165">3</span><span class="sxs-lookup"><span data-stu-id="e8b81-165">3</span></span> |<span data-ttu-id="e8b81-166">1</span><span class="sxs-lookup"><span data-stu-id="e8b81-166">1</span></span> |
| <span data-ttu-id="e8b81-167">20150801</span><span class="sxs-lookup"><span data-stu-id="e8b81-167">20150801</span></span> |<span data-ttu-id="e8b81-168">3</span><span class="sxs-lookup"><span data-stu-id="e8b81-168">3</span></span> |<span data-ttu-id="e8b81-169">1</span><span class="sxs-lookup"><span data-stu-id="e8b81-169">1</span></span> |
| <span data-ttu-id="e8b81-170">20151001</span><span class="sxs-lookup"><span data-stu-id="e8b81-170">20151001</span></span> |<span data-ttu-id="e8b81-171">4</span><span class="sxs-lookup"><span data-stu-id="e8b81-171">4</span></span> |<span data-ttu-id="e8b81-172">2</span><span class="sxs-lookup"><span data-stu-id="e8b81-172">2</span></span> |
| <span data-ttu-id="e8b81-173">20151101</span><span class="sxs-lookup"><span data-stu-id="e8b81-173">20151101</span></span> |<span data-ttu-id="e8b81-174">4</span><span class="sxs-lookup"><span data-stu-id="e8b81-174">4</span></span> |<span data-ttu-id="e8b81-175">2</span><span class="sxs-lookup"><span data-stu-id="e8b81-175">2</span></span> |
| <span data-ttu-id="e8b81-176">20151201</span><span class="sxs-lookup"><span data-stu-id="e8b81-176">20151201</span></span> |<span data-ttu-id="e8b81-177">4</span><span class="sxs-lookup"><span data-stu-id="e8b81-177">4</span></span> |<span data-ttu-id="e8b81-178">2</span><span class="sxs-lookup"><span data-stu-id="e8b81-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="e8b81-179">Passaggio 4: creare le statistiche sui dati appena caricati</span><span class="sxs-lookup"><span data-stu-id="e8b81-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="e8b81-180">SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.</span><span class="sxs-lookup"><span data-stu-id="e8b81-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="e8b81-181">Per ottenere le migliori prestazioni dalle query, è importante creare statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento o dopo eventuali modifiche sostanziali dei dati.</span><span class="sxs-lookup"><span data-stu-id="e8b81-181">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="e8b81-182">Per una spiegazione dettagliata delle statistiche, vedere l'argomento [Statistiche][Statistics] nel gruppo di argomenti sullo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="e8b81-182">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="e8b81-183">Di seguito è possibile vedere un rapido esempio di come creare statistiche nella tabella caricata in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="e8b81-183">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="e8b81-184">Da un prompt di sqlcmd, eseguire le istruzioni CREATE STATISTICS seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8b81-184">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="e8b81-185">Esportare i dati da SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e8b81-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="e8b81-186">In questa esercitazione verrà creato un file di dati da una tabella in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e8b81-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="e8b81-187">I dati creati in precedenza verranno esportati in un nuovo file denominato DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="e8b81-187">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="e8b81-188">Passaggio 1: Esportare i dati</span><span class="sxs-lookup"><span data-stu-id="e8b81-188">Step 1: Export the data</span></span>
<span data-ttu-id="e8b81-189">L'utilità bcp permette di connettersi ed esportare i dati usando il comando seguente, sostituendo i valori in base alla necessità:</span><span class="sxs-lookup"><span data-stu-id="e8b81-189">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="e8b81-190">Per verificare che i dati siano stati esportati correttamente, aprire il nuovo file.</span><span class="sxs-lookup"><span data-stu-id="e8b81-190">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="e8b81-191">I dati del file devono corrispondere al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="e8b81-191">The data in the file should match the text below:</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> <span data-ttu-id="e8b81-192">A causa della natura dei sistemi distribuiti, è possibile che l'ordine dei dati non sia uguale nei database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e8b81-192">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="e8b81-193">Un'altra opzione consiste nell'usare la funzione **queryout** di bcp per scrivere un estratto di query invece di esportare l'intera tabella.</span><span class="sxs-lookup"><span data-stu-id="e8b81-193">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e8b81-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8b81-194">Next steps</span></span>
<span data-ttu-id="e8b81-195">Per una panoramica sul caricamento, vedere [Caricare i dati in SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="e8b81-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="e8b81-196">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="e8b81-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
