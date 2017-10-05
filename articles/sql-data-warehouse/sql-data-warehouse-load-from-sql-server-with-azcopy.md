---
title: Caricare dati da SQL Server in Azure SQL Data Warehouse (PolyBase) | Documentazione Microsoft
description: Uso di bcp per esportare dati da SQL Server a file flat, di AZCopy per importare dati nell'archivio BLOB di Azure e di PolyBase per inserire i dati in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 08f94bc26d8b1e1f5a56dfccd41e394dbd721024
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="a9fe3-103">Caricare dati da SQL Server in Azure SQL Data Warehouse (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="a9fe3-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="a9fe3-104">Usare le utilità della riga di comando bcp e AZCopy per caricare dati da SQL Server all'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-104">Use bcp and AZCopy command-line utilities to load data from SQL Server to Azure blob storage.</span></span> <span data-ttu-id="a9fe3-105">Usare quindi PolyBase o Azure Data Factory per caricare i dati in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-105">Then use PolyBase or Azure Data Factory to load the data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a9fe3-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a9fe3-106">Prerequisites</span></span>
<span data-ttu-id="a9fe3-107">Per eseguire questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="a9fe3-107">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="a9fe3-108">Un database di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a9fe3-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="a9fe3-109">Utilità della riga di comando bcp installata</span><span class="sxs-lookup"><span data-stu-id="a9fe3-109">The bcp command line utility installed</span></span>
* <span data-ttu-id="a9fe3-110">Utilità della riga di comando SQLCMD installata</span><span class="sxs-lookup"><span data-stu-id="a9fe3-110">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="a9fe3-111">È possibile scaricare le utilità bcp e sqlcmd dall'[Area download Microsoft][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="a9fe3-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="a9fe3-112">Importare i dati in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a9fe3-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="a9fe3-113">In questa esercitazione verrà creata una tabella in Azure SQL Data Warehouse e verranno importati dati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="a9fe3-114">Passaggio 1: Creare una tabella in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a9fe3-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="a9fe3-115">Al prompt dei comandi usare sqlcmd per eseguire la query seguente per creare una tabella nell'istanza:</span><span class="sxs-lookup"><span data-stu-id="a9fe3-115">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

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
> <span data-ttu-id="a9fe3-116">Per altre informazioni sulla creazione di una tabella in SQL Data Warehouse e sulle opzioni disponibili con la clausola WITH, vedere [Panoramica delle tabelle][Table Overview] o la [sintassi di CREATE TABLE][CREATE TABLE syntax].</span><span class="sxs-lookup"><span data-stu-id="a9fe3-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="a9fe3-117">Passaggio 2: Creare un file di dati di origine</span><span class="sxs-lookup"><span data-stu-id="a9fe3-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="a9fe3-118">Aprire il Blocco note, copiare le righe di dati seguenti in un nuovo file di testo e quindi salvare il file nella directory temporanea locale, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-118">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="a9fe3-119">È importante ricordare che bcp.exe non supporta la codifica UTF-8 del file.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-119">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="a9fe3-120">Usare i file ASCII o con codifica UTF-16 quando si usa bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="a9fe3-121">Passaggio 3: Connettersi e importare i dati</span><span class="sxs-lookup"><span data-stu-id="a9fe3-121">Step 3: Connect and import the data</span></span>
<span data-ttu-id="a9fe3-122">bcp permette di connettersi e importare i dati usando il comando seguente, sostituendo i valori in base alla necessità:</span><span class="sxs-lookup"><span data-stu-id="a9fe3-122">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="a9fe3-123">È possibile verificare che i dati siano stati caricati eseguendo la query seguente con sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="a9fe3-123">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="a9fe3-124">Dovrebbero essere visualizzati i risultati seguenti:</span><span class="sxs-lookup"><span data-stu-id="a9fe3-124">This should return the following results:</span></span>

| <span data-ttu-id="a9fe3-125">DateId</span><span class="sxs-lookup"><span data-stu-id="a9fe3-125">DateId</span></span> | <span data-ttu-id="a9fe3-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="a9fe3-126">CalendarQuarter</span></span> | <span data-ttu-id="a9fe3-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="a9fe3-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9fe3-128">20150101</span><span class="sxs-lookup"><span data-stu-id="a9fe3-128">20150101</span></span> |<span data-ttu-id="a9fe3-129">1</span><span class="sxs-lookup"><span data-stu-id="a9fe3-129">1</span></span> |<span data-ttu-id="a9fe3-130">3</span><span class="sxs-lookup"><span data-stu-id="a9fe3-130">3</span></span> |
| <span data-ttu-id="a9fe3-131">20150201</span><span class="sxs-lookup"><span data-stu-id="a9fe3-131">20150201</span></span> |<span data-ttu-id="a9fe3-132">1</span><span class="sxs-lookup"><span data-stu-id="a9fe3-132">1</span></span> |<span data-ttu-id="a9fe3-133">3</span><span class="sxs-lookup"><span data-stu-id="a9fe3-133">3</span></span> |
| <span data-ttu-id="a9fe3-134">20150301</span><span class="sxs-lookup"><span data-stu-id="a9fe3-134">20150301</span></span> |<span data-ttu-id="a9fe3-135">1</span><span class="sxs-lookup"><span data-stu-id="a9fe3-135">1</span></span> |<span data-ttu-id="a9fe3-136">3</span><span class="sxs-lookup"><span data-stu-id="a9fe3-136">3</span></span> |
| <span data-ttu-id="a9fe3-137">20150401</span><span class="sxs-lookup"><span data-stu-id="a9fe3-137">20150401</span></span> |<span data-ttu-id="a9fe3-138">2</span><span class="sxs-lookup"><span data-stu-id="a9fe3-138">2</span></span> |<span data-ttu-id="a9fe3-139">4</span><span class="sxs-lookup"><span data-stu-id="a9fe3-139">4</span></span> |
| <span data-ttu-id="a9fe3-140">20150501</span><span class="sxs-lookup"><span data-stu-id="a9fe3-140">20150501</span></span> |<span data-ttu-id="a9fe3-141">2</span><span class="sxs-lookup"><span data-stu-id="a9fe3-141">2</span></span> |<span data-ttu-id="a9fe3-142">4</span><span class="sxs-lookup"><span data-stu-id="a9fe3-142">4</span></span> |
| <span data-ttu-id="a9fe3-143">20150601</span><span class="sxs-lookup"><span data-stu-id="a9fe3-143">20150601</span></span> |<span data-ttu-id="a9fe3-144">2</span><span class="sxs-lookup"><span data-stu-id="a9fe3-144">2</span></span> |<span data-ttu-id="a9fe3-145">4</span><span class="sxs-lookup"><span data-stu-id="a9fe3-145">4</span></span> |
| <span data-ttu-id="a9fe3-146">20150701</span><span class="sxs-lookup"><span data-stu-id="a9fe3-146">20150701</span></span> |<span data-ttu-id="a9fe3-147">3</span><span class="sxs-lookup"><span data-stu-id="a9fe3-147">3</span></span> |<span data-ttu-id="a9fe3-148">1</span><span class="sxs-lookup"><span data-stu-id="a9fe3-148">1</span></span> |
| <span data-ttu-id="a9fe3-149">20150801</span><span class="sxs-lookup"><span data-stu-id="a9fe3-149">20150801</span></span> |<span data-ttu-id="a9fe3-150">3</span><span class="sxs-lookup"><span data-stu-id="a9fe3-150">3</span></span> |<span data-ttu-id="a9fe3-151">1</span><span class="sxs-lookup"><span data-stu-id="a9fe3-151">1</span></span> |
| <span data-ttu-id="a9fe3-152">20150801</span><span class="sxs-lookup"><span data-stu-id="a9fe3-152">20150801</span></span> |<span data-ttu-id="a9fe3-153">3</span><span class="sxs-lookup"><span data-stu-id="a9fe3-153">3</span></span> |<span data-ttu-id="a9fe3-154">1</span><span class="sxs-lookup"><span data-stu-id="a9fe3-154">1</span></span> |
| <span data-ttu-id="a9fe3-155">20151001</span><span class="sxs-lookup"><span data-stu-id="a9fe3-155">20151001</span></span> |<span data-ttu-id="a9fe3-156">4</span><span class="sxs-lookup"><span data-stu-id="a9fe3-156">4</span></span> |<span data-ttu-id="a9fe3-157">2</span><span class="sxs-lookup"><span data-stu-id="a9fe3-157">2</span></span> |
| <span data-ttu-id="a9fe3-158">20151101</span><span class="sxs-lookup"><span data-stu-id="a9fe3-158">20151101</span></span> |<span data-ttu-id="a9fe3-159">4</span><span class="sxs-lookup"><span data-stu-id="a9fe3-159">4</span></span> |<span data-ttu-id="a9fe3-160">2</span><span class="sxs-lookup"><span data-stu-id="a9fe3-160">2</span></span> |
| <span data-ttu-id="a9fe3-161">20151201</span><span class="sxs-lookup"><span data-stu-id="a9fe3-161">20151201</span></span> |<span data-ttu-id="a9fe3-162">4</span><span class="sxs-lookup"><span data-stu-id="a9fe3-162">4</span></span> |<span data-ttu-id="a9fe3-163">2</span><span class="sxs-lookup"><span data-stu-id="a9fe3-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="a9fe3-164">Passaggio 4: creare le statistiche sui dati appena caricati</span><span class="sxs-lookup"><span data-stu-id="a9fe3-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="a9fe3-165">SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="a9fe3-166">Per ottenere le migliori prestazioni dalle query, è importante creare statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento o dopo eventuali modifiche sostanziali dei dati.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-166">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="a9fe3-167">Per una spiegazione dettagliata delle statistiche, vedere l'argomento [Statistiche][Statistics] nel gruppo di argomenti sullo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-167">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="a9fe3-168">Di seguito è possibile vedere un rapido esempio di come creare statistiche nella tabella caricata in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-168">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="a9fe3-169">Da un prompt di sqlcmd, eseguire le istruzioni CREATE STATISTICS seguenti:</span><span class="sxs-lookup"><span data-stu-id="a9fe3-169">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="a9fe3-170">Esportare i dati da SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a9fe3-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="a9fe3-171">In questa esercitazione verrà creato un file di dati da una tabella in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="a9fe3-172">I dati creati in precedenza verranno esportati in un nuovo file denominato DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-172">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="a9fe3-173">Passaggio 1: Esportare i dati</span><span class="sxs-lookup"><span data-stu-id="a9fe3-173">Step 1: Export the data</span></span>
<span data-ttu-id="a9fe3-174">L'utilità bcp permette di connettersi ed esportare i dati usando il comando seguente, sostituendo i valori in base alla necessità:</span><span class="sxs-lookup"><span data-stu-id="a9fe3-174">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="a9fe3-175">Per verificare che i dati siano stati esportati correttamente, aprire il nuovo file.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-175">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="a9fe3-176">I dati del file devono corrispondere al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="a9fe3-176">The data in the file should match the text below:</span></span>

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
> <span data-ttu-id="a9fe3-177">A causa della natura dei sistemi distribuiti, è possibile che l'ordine dei dati non sia uguale nei database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-177">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="a9fe3-178">Un'altra opzione consiste nell'usare la funzione **queryout** di bcp per scrivere un estratto di query invece di esportare l'intera tabella.</span><span class="sxs-lookup"><span data-stu-id="a9fe3-178">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a9fe3-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9fe3-179">Next steps</span></span>
<span data-ttu-id="a9fe3-180">Per una panoramica sul caricamento, vedere [Caricare i dati in SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a9fe3-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="a9fe3-181">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="a9fe3-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
