---
title: Caricare dati da SQL Server in Azure SQL Data Warehouse (bcp) | Documentazione Microsoft
description: "Per dimensioni ridotte dei dati è possibile usare bcp per esportare i dati da SQL Server a file flat e importare i dati direttamente in Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: dae7b5f7456f4ec0daf60d55f9c38b780896ff83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="5434b-103">Caricare dati da SQL Server in Azure SQL Data Warehouse (file flat)</span><span class="sxs-lookup"><span data-stu-id="5434b-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5434b-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="5434b-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="5434b-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="5434b-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="5434b-106">bcp</span><span class="sxs-lookup"><span data-stu-id="5434b-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="5434b-107">Per set di dati di piccole dimensioni è possibile usare l'utilità della riga di comando bcp per esportare i dati da SQL Server e quindi caricarli direttamente in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5434b-107">For small data sets, you can use the bcp command-line utility to export data from SQL Server and then load it directly to Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="5434b-108">In questa esercitazione si userà bcp per eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="5434b-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="5434b-109">Esportare una tabella da SQL Server usando il comando bcp out oppure creare un semplice file di esempio.</span><span class="sxs-lookup"><span data-stu-id="5434b-109">Export a table from from SQL Server by using the bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="5434b-110">Importare la tabella da un file flat in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5434b-110">Import the table from a flat file to SQL Data Warehouse.</span></span>
* <span data-ttu-id="5434b-111">Creare statistiche sui dati caricati.</span><span class="sxs-lookup"><span data-stu-id="5434b-111">Create statistics on the loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="5434b-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="5434b-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="5434b-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5434b-113">Prerequisites</span></span>
<span data-ttu-id="5434b-114">Per eseguire questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="5434b-114">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="5434b-115">Un database di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5434b-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="5434b-116">Utilità della riga di comando bcp installata</span><span class="sxs-lookup"><span data-stu-id="5434b-116">The bcp command-line utility installed</span></span>
* <span data-ttu-id="5434b-117">Utilità della riga di comando sqlcmd installata</span><span class="sxs-lookup"><span data-stu-id="5434b-117">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="5434b-118">È possibile scaricare le utilità bcp e sqlcmd dall'[Area download Microsoft][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="5434b-118">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="5434b-119">Dati in formato ASCII o UTF-16</span><span class="sxs-lookup"><span data-stu-id="5434b-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="5434b-120">Se si prova a eseguire questa esercitazione con dati personalizzati, è necessario che i dati usino la codifica ASCII o UTF-16, perché bcp non supporta UTF-8.</span><span class="sxs-lookup"><span data-stu-id="5434b-120">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="5434b-121">PolyBase supporta UTF-8 ma non supporta ancora UTF-16.</span><span class="sxs-lookup"><span data-stu-id="5434b-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="5434b-122">Si noti che se si vuole associare bcp con PolyBase, sarà necessario trasformare i dati in UTF-8 dopo l'esportazione da SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5434b-122">Note that if you want to combine bcp with PolyBase you will need to transform the data to UTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="5434b-123">1. Creare una tabella di destinazione</span><span class="sxs-lookup"><span data-stu-id="5434b-123">1. Create a destination table</span></span>
<span data-ttu-id="5434b-124">Definire una tabella in SQL Data Warehouse da usare come tabella di destinazione per il caricamento.</span><span class="sxs-lookup"><span data-stu-id="5434b-124">Define a table in SQL Data Warehouse that will be the destination table for the load.</span></span> <span data-ttu-id="5434b-125">Le colonne della tabella devono corrispondere ai dati in ogni riga del file di dati.</span><span class="sxs-lookup"><span data-stu-id="5434b-125">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="5434b-126">Per creare una tabella, aprire un prompt dei comandi e usare sqlcmd.exe per eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5434b-126">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="5434b-127">2. Creare un file di dati di origine</span><span class="sxs-lookup"><span data-stu-id="5434b-127">2. Create a source data file</span></span>
<span data-ttu-id="5434b-128">Aprire il Blocco note, copiare le righe di dati seguenti in un nuovo file di testo e quindi salvare il file nella directory temporanea locale, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="5434b-128">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="5434b-129">I dati hanno formato ASCII.</span><span class="sxs-lookup"><span data-stu-id="5434b-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="5434b-130">(Facoltativo) Per esportare i dati personalizzati da un database di SQL Server, aprire un prompt dei comandi ed eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5434b-130">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="5434b-131">Sostituire TableName, ServerName, DatabaseName, Username e Password con le informazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="5434b-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-the-data"></a><span data-ttu-id="5434b-132">3. Caricare i dati</span><span class="sxs-lookup"><span data-stu-id="5434b-132">3. Load the data</span></span>
<span data-ttu-id="5434b-133">Per caricare i dati, aprire un prompt dei comandi ed eseguire il comando seguente, sostituendo i valori per nome server, nome database, nome utente e password con le informazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="5434b-133">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="5434b-134">Usare questo comando per verificare che i dati siano stati caricati correttamente.</span><span class="sxs-lookup"><span data-stu-id="5434b-134">Use this command to verify the data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="5434b-135">I risultati dovrebbero avere l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="5434b-135">The results should look like this:</span></span>

| <span data-ttu-id="5434b-136">DateId</span><span class="sxs-lookup"><span data-stu-id="5434b-136">DateId</span></span> | <span data-ttu-id="5434b-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="5434b-137">CalendarQuarter</span></span> | <span data-ttu-id="5434b-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="5434b-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5434b-139">20150101</span><span class="sxs-lookup"><span data-stu-id="5434b-139">20150101</span></span> |<span data-ttu-id="5434b-140">1</span><span class="sxs-lookup"><span data-stu-id="5434b-140">1</span></span> |<span data-ttu-id="5434b-141">3</span><span class="sxs-lookup"><span data-stu-id="5434b-141">3</span></span> |
| <span data-ttu-id="5434b-142">20150201</span><span class="sxs-lookup"><span data-stu-id="5434b-142">20150201</span></span> |<span data-ttu-id="5434b-143">1</span><span class="sxs-lookup"><span data-stu-id="5434b-143">1</span></span> |<span data-ttu-id="5434b-144">3</span><span class="sxs-lookup"><span data-stu-id="5434b-144">3</span></span> |
| <span data-ttu-id="5434b-145">20150301</span><span class="sxs-lookup"><span data-stu-id="5434b-145">20150301</span></span> |<span data-ttu-id="5434b-146">1</span><span class="sxs-lookup"><span data-stu-id="5434b-146">1</span></span> |<span data-ttu-id="5434b-147">3</span><span class="sxs-lookup"><span data-stu-id="5434b-147">3</span></span> |
| <span data-ttu-id="5434b-148">20150401</span><span class="sxs-lookup"><span data-stu-id="5434b-148">20150401</span></span> |<span data-ttu-id="5434b-149">2</span><span class="sxs-lookup"><span data-stu-id="5434b-149">2</span></span> |<span data-ttu-id="5434b-150">4</span><span class="sxs-lookup"><span data-stu-id="5434b-150">4</span></span> |
| <span data-ttu-id="5434b-151">20150501</span><span class="sxs-lookup"><span data-stu-id="5434b-151">20150501</span></span> |<span data-ttu-id="5434b-152">2</span><span class="sxs-lookup"><span data-stu-id="5434b-152">2</span></span> |<span data-ttu-id="5434b-153">4</span><span class="sxs-lookup"><span data-stu-id="5434b-153">4</span></span> |
| <span data-ttu-id="5434b-154">20150601</span><span class="sxs-lookup"><span data-stu-id="5434b-154">20150601</span></span> |<span data-ttu-id="5434b-155">2</span><span class="sxs-lookup"><span data-stu-id="5434b-155">2</span></span> |<span data-ttu-id="5434b-156">4</span><span class="sxs-lookup"><span data-stu-id="5434b-156">4</span></span> |
| <span data-ttu-id="5434b-157">20150701</span><span class="sxs-lookup"><span data-stu-id="5434b-157">20150701</span></span> |<span data-ttu-id="5434b-158">3</span><span class="sxs-lookup"><span data-stu-id="5434b-158">3</span></span> |<span data-ttu-id="5434b-159">1</span><span class="sxs-lookup"><span data-stu-id="5434b-159">1</span></span> |
| <span data-ttu-id="5434b-160">20150801</span><span class="sxs-lookup"><span data-stu-id="5434b-160">20150801</span></span> |<span data-ttu-id="5434b-161">3</span><span class="sxs-lookup"><span data-stu-id="5434b-161">3</span></span> |<span data-ttu-id="5434b-162">1</span><span class="sxs-lookup"><span data-stu-id="5434b-162">1</span></span> |
| <span data-ttu-id="5434b-163">20150801</span><span class="sxs-lookup"><span data-stu-id="5434b-163">20150801</span></span> |<span data-ttu-id="5434b-164">3</span><span class="sxs-lookup"><span data-stu-id="5434b-164">3</span></span> |<span data-ttu-id="5434b-165">1</span><span class="sxs-lookup"><span data-stu-id="5434b-165">1</span></span> |
| <span data-ttu-id="5434b-166">20151001</span><span class="sxs-lookup"><span data-stu-id="5434b-166">20151001</span></span> |<span data-ttu-id="5434b-167">4</span><span class="sxs-lookup"><span data-stu-id="5434b-167">4</span></span> |<span data-ttu-id="5434b-168">2</span><span class="sxs-lookup"><span data-stu-id="5434b-168">2</span></span> |
| <span data-ttu-id="5434b-169">20151101</span><span class="sxs-lookup"><span data-stu-id="5434b-169">20151101</span></span> |<span data-ttu-id="5434b-170">4</span><span class="sxs-lookup"><span data-stu-id="5434b-170">4</span></span> |<span data-ttu-id="5434b-171">2</span><span class="sxs-lookup"><span data-stu-id="5434b-171">2</span></span> |
| <span data-ttu-id="5434b-172">20151201</span><span class="sxs-lookup"><span data-stu-id="5434b-172">20151201</span></span> |<span data-ttu-id="5434b-173">4</span><span class="sxs-lookup"><span data-stu-id="5434b-173">4</span></span> |<span data-ttu-id="5434b-174">2</span><span class="sxs-lookup"><span data-stu-id="5434b-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="5434b-175">4. Creare le statistiche</span><span class="sxs-lookup"><span data-stu-id="5434b-175">4. Create statistics</span></span>
<span data-ttu-id="5434b-176">SQL Data Warehouse non supporta ancora la creazione automatica o l'aggiornamento automatico delle statistiche.</span><span class="sxs-lookup"><span data-stu-id="5434b-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="5434b-177">Per ottenere le prestazioni migliori per le query, è importante creare statistiche su tutte le colonne di tutte le tabelle dopo il primo caricamento o dopo qualsiasi modifica significativa ai dati.</span><span class="sxs-lookup"><span data-stu-id="5434b-177">To get the best query performance, it's important to create statistics on all columns of all tables after the first load or after any substantial changes occur in the data.</span></span> <span data-ttu-id="5434b-178">Per una spiegazione dettagliata delle statistiche, vedere [Statistiche][Statistics].</span><span class="sxs-lookup"><span data-stu-id="5434b-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="5434b-179">Eseguire il comando seguente per creare le statistiche nella tabella appena caricata.</span><span class="sxs-lookup"><span data-stu-id="5434b-179">Run the following command to create statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="5434b-180">5. Esportare i dati da SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5434b-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="5434b-181">Se si vuole, è possibile esportare i dati appena caricati da SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5434b-181">For fun, you can export the data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="5434b-182">Il comando per l'esportazione corrisponde esattamente all'esportazione da SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5434b-182">The command to export is exactly the same as exporting from SQL Server.</span></span>

<span data-ttu-id="5434b-183">I risultati presentano tuttavia una differenza.</span><span class="sxs-lookup"><span data-stu-id="5434b-183">However, there is a difference in the results.</span></span> <span data-ttu-id="5434b-184">Poiché i dati vengono archiviati in posizioni distribuite in SQL Data Warehouse, quando si esportano i dati ogni nodo di calcolo scrive i rispettivi dati nel file di output.</span><span class="sxs-lookup"><span data-stu-id="5434b-184">Since the data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data to the output file.</span></span> <span data-ttu-id="5434b-185">L'ordine dei dati nel file di output sarà probabilmente diverso dall'ordine dei dati nel file di input.</span><span class="sxs-lookup"><span data-stu-id="5434b-185">The order of the data in the output file is likely to be different than the order of the data in the input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="5434b-186">Esportare una tabella e confrontare i risultati esportati</span><span class="sxs-lookup"><span data-stu-id="5434b-186">Export a table and compare exported results</span></span>
<span data-ttu-id="5434b-187">Per visualizzare i dati esportati, aprire un prompt dei comandi ed eseguire questo comando usando parametri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="5434b-187">To see the exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="5434b-188">ServerName è il nome del server SQL logico di Azure.</span><span class="sxs-lookup"><span data-stu-id="5434b-188">ServerName is the name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="5434b-189">Per verificare che i dati siano stati esportati correttamente, aprire il nuovo file.</span><span class="sxs-lookup"><span data-stu-id="5434b-189">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="5434b-190">I dati nel file devono corrispondere al testo seguente, ma è probabile che abbiano un ordinamento diverso:</span><span class="sxs-lookup"><span data-stu-id="5434b-190">The data in the file should match the text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-the-results-of-a-query"></a><span data-ttu-id="5434b-191">Esportare i risultati di una query</span><span class="sxs-lookup"><span data-stu-id="5434b-191">Export the results of a query</span></span>
<span data-ttu-id="5434b-192">È possibile usare la funzione **queryout** di bcp per esportare i risultati di una query invece di esportare l'intera tabella.</span><span class="sxs-lookup"><span data-stu-id="5434b-192">You can use the **queryout** function of bcp to export the results of a query instead of exporting the entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5434b-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5434b-193">Next steps</span></span>
<span data-ttu-id="5434b-194">Per una panoramica sul caricamento, vedere [Caricare i dati in SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="5434b-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="5434b-195">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="5434b-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="5434b-196">Per altre informazioni sulla creazione di una tabella in SQL Data Warehouse, vedere [Panoramica delle tabelle][Table Overview] o la sintassi di [CREATE TABLE][CREATE TABLE syntax].</span><span class="sxs-lookup"><span data-stu-id="5434b-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

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
