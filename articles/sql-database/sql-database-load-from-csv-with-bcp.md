---
title: Caricare dati da un file CSV al database SQL di Azure (bcp) | Microsoft Docs
description: Per dati di piccole dimensioni, usa bcp per importare dati nel database SQL di Azure.
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 84bebab7763bb21f73880a6c8b367a62b0c137d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="7b506-103">Caricare dati da CSV in un database SQL di Azure (file flat)</span><span class="sxs-lookup"><span data-stu-id="7b506-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="7b506-104">È possibile usare l'utilità della riga di comando bcp per importare dati da un file CSV in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b506-104">You can use the bcp command-line utility to import data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7b506-105">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="7b506-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="7b506-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7b506-106">Prerequisites</span></span>
<span data-ttu-id="7b506-107">Per seguire la procedura descritta in questo articolo, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="7b506-107">To complete the steps in this article, you need:</span></span>

* <span data-ttu-id="7b506-108">Un server logico e un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="7b506-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="7b506-109">Utilità della riga di comando bcp installata</span><span class="sxs-lookup"><span data-stu-id="7b506-109">The bcp command-line utility installed</span></span>
* <span data-ttu-id="7b506-110">Utilità della riga di comando sqlcmd installata</span><span class="sxs-lookup"><span data-stu-id="7b506-110">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="7b506-111">È possibile scaricare le utilità bcp e sqlcmd dall'[Area download Microsoft][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="7b506-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="7b506-112">Dati in formato ASCII o UTF-16</span><span class="sxs-lookup"><span data-stu-id="7b506-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="7b506-113">Se si prova a eseguire questa esercitazione con dati personalizzati, è necessario che i dati usino la codifica ASCII o UTF-16, perché bcp non supporta UTF-8.</span><span class="sxs-lookup"><span data-stu-id="7b506-113">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="7b506-114">1. Creare una tabella di destinazione</span><span class="sxs-lookup"><span data-stu-id="7b506-114">1. Create a destination table</span></span>
<span data-ttu-id="7b506-115">Definire una tabella nel database SQL come tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="7b506-115">Define a table in SQL Database as the destination table.</span></span> <span data-ttu-id="7b506-116">Le colonne della tabella devono corrispondere ai dati in ogni riga del file di dati.</span><span class="sxs-lookup"><span data-stu-id="7b506-116">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="7b506-117">Per creare una tabella, aprire un prompt dei comandi e usare sqlcmd.exe per eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7b506-117">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="7b506-118">2. Creare un file di dati di origine</span><span class="sxs-lookup"><span data-stu-id="7b506-118">2. Create a source data file</span></span>
<span data-ttu-id="7b506-119">Aprire il Blocco note, copiare le righe di dati seguenti in un nuovo file di testo e quindi salvare il file nella directory temporanea locale, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="7b506-119">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="7b506-120">I dati hanno formato ASCII.</span><span class="sxs-lookup"><span data-stu-id="7b506-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="7b506-121">(Facoltativo) Per esportare i dati personalizzati da un database di SQL Server, aprire un prompt dei comandi ed eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="7b506-121">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="7b506-122">Sostituire TableName, ServerName, DatabaseName, Username e Password con le informazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="7b506-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-the-data"></a><span data-ttu-id="7b506-123">3. Caricare i dati</span><span class="sxs-lookup"><span data-stu-id="7b506-123">3. Load the data</span></span>
<span data-ttu-id="7b506-124">Per caricare i dati, aprire un prompt dei comandi ed eseguire il comando seguente, sostituendo i valori per nome server, nome database, nome utente e password con le informazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="7b506-124">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="7b506-125">Usare questo comando per verificare che i dati siano stati caricati correttamente.</span><span class="sxs-lookup"><span data-stu-id="7b506-125">Use this command to verify the data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="7b506-126">I risultati dovrebbero avere l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="7b506-126">The results should look like this:</span></span>

| <span data-ttu-id="7b506-127">DateId</span><span class="sxs-lookup"><span data-stu-id="7b506-127">DateId</span></span> | <span data-ttu-id="7b506-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="7b506-128">CalendarQuarter</span></span> | <span data-ttu-id="7b506-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="7b506-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b506-130">20150101</span><span class="sxs-lookup"><span data-stu-id="7b506-130">20150101</span></span> |<span data-ttu-id="7b506-131">1</span><span class="sxs-lookup"><span data-stu-id="7b506-131">1</span></span> |<span data-ttu-id="7b506-132">3</span><span class="sxs-lookup"><span data-stu-id="7b506-132">3</span></span> |
| <span data-ttu-id="7b506-133">20150201</span><span class="sxs-lookup"><span data-stu-id="7b506-133">20150201</span></span> |<span data-ttu-id="7b506-134">1</span><span class="sxs-lookup"><span data-stu-id="7b506-134">1</span></span> |<span data-ttu-id="7b506-135">3</span><span class="sxs-lookup"><span data-stu-id="7b506-135">3</span></span> |
| <span data-ttu-id="7b506-136">20150301</span><span class="sxs-lookup"><span data-stu-id="7b506-136">20150301</span></span> |<span data-ttu-id="7b506-137">1</span><span class="sxs-lookup"><span data-stu-id="7b506-137">1</span></span> |<span data-ttu-id="7b506-138">3</span><span class="sxs-lookup"><span data-stu-id="7b506-138">3</span></span> |
| <span data-ttu-id="7b506-139">20150401</span><span class="sxs-lookup"><span data-stu-id="7b506-139">20150401</span></span> |<span data-ttu-id="7b506-140">2</span><span class="sxs-lookup"><span data-stu-id="7b506-140">2</span></span> |<span data-ttu-id="7b506-141">4</span><span class="sxs-lookup"><span data-stu-id="7b506-141">4</span></span> |
| <span data-ttu-id="7b506-142">20150501</span><span class="sxs-lookup"><span data-stu-id="7b506-142">20150501</span></span> |<span data-ttu-id="7b506-143">2</span><span class="sxs-lookup"><span data-stu-id="7b506-143">2</span></span> |<span data-ttu-id="7b506-144">4</span><span class="sxs-lookup"><span data-stu-id="7b506-144">4</span></span> |
| <span data-ttu-id="7b506-145">20150601</span><span class="sxs-lookup"><span data-stu-id="7b506-145">20150601</span></span> |<span data-ttu-id="7b506-146">2</span><span class="sxs-lookup"><span data-stu-id="7b506-146">2</span></span> |<span data-ttu-id="7b506-147">4</span><span class="sxs-lookup"><span data-stu-id="7b506-147">4</span></span> |
| <span data-ttu-id="7b506-148">20150701</span><span class="sxs-lookup"><span data-stu-id="7b506-148">20150701</span></span> |<span data-ttu-id="7b506-149">3</span><span class="sxs-lookup"><span data-stu-id="7b506-149">3</span></span> |<span data-ttu-id="7b506-150">1</span><span class="sxs-lookup"><span data-stu-id="7b506-150">1</span></span> |
| <span data-ttu-id="7b506-151">20150801</span><span class="sxs-lookup"><span data-stu-id="7b506-151">20150801</span></span> |<span data-ttu-id="7b506-152">3</span><span class="sxs-lookup"><span data-stu-id="7b506-152">3</span></span> |<span data-ttu-id="7b506-153">1</span><span class="sxs-lookup"><span data-stu-id="7b506-153">1</span></span> |
| <span data-ttu-id="7b506-154">20150801</span><span class="sxs-lookup"><span data-stu-id="7b506-154">20150801</span></span> |<span data-ttu-id="7b506-155">3</span><span class="sxs-lookup"><span data-stu-id="7b506-155">3</span></span> |<span data-ttu-id="7b506-156">1</span><span class="sxs-lookup"><span data-stu-id="7b506-156">1</span></span> |
| <span data-ttu-id="7b506-157">20151001</span><span class="sxs-lookup"><span data-stu-id="7b506-157">20151001</span></span> |<span data-ttu-id="7b506-158">4</span><span class="sxs-lookup"><span data-stu-id="7b506-158">4</span></span> |<span data-ttu-id="7b506-159">2</span><span class="sxs-lookup"><span data-stu-id="7b506-159">2</span></span> |
| <span data-ttu-id="7b506-160">20151101</span><span class="sxs-lookup"><span data-stu-id="7b506-160">20151101</span></span> |<span data-ttu-id="7b506-161">4</span><span class="sxs-lookup"><span data-stu-id="7b506-161">4</span></span> |<span data-ttu-id="7b506-162">2</span><span class="sxs-lookup"><span data-stu-id="7b506-162">2</span></span> |
| <span data-ttu-id="7b506-163">20151201</span><span class="sxs-lookup"><span data-stu-id="7b506-163">20151201</span></span> |<span data-ttu-id="7b506-164">4</span><span class="sxs-lookup"><span data-stu-id="7b506-164">4</span></span> |<span data-ttu-id="7b506-165">2</span><span class="sxs-lookup"><span data-stu-id="7b506-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7b506-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7b506-166">Next steps</span></span>
<span data-ttu-id="7b506-167">Per eseguire la migrazione di un database SQL Server, vedere [Migrazione di un database SQL Server al database SQL nel cloud](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="7b506-167">To migrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
