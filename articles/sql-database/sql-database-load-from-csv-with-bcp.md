---
title: file di dati di aaaLoad da file CSV nel Database di SQL Azure (bcp) | Documenti Microsoft
description: Per una dimensione dei dati di piccole dimensioni, utilizza bcp tooimport dati in Database SQL di Azure.
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
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="7202e-103">Caricare dati da CSV in un database SQL di Azure (file flat)</span><span class="sxs-lookup"><span data-stu-id="7202e-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="7202e-104">È possibile utilizzare hello bcp utilità della riga di comando tooimport dati da un file CSV nel Database di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7202e-104">You can use hello bcp command-line utility tooimport data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7202e-105">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="7202e-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="7202e-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7202e-106">Prerequisites</span></span>
<span data-ttu-id="7202e-107">hello toocomplete i passaggi in questo articolo, è necessario:</span><span class="sxs-lookup"><span data-stu-id="7202e-107">toocomplete hello steps in this article, you need:</span></span>

* <span data-ttu-id="7202e-108">Un server logico e un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="7202e-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="7202e-109">utilità della riga di comando bcp Hello installato</span><span class="sxs-lookup"><span data-stu-id="7202e-109">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="7202e-110">utilità della riga di comando sqlcmd Hello installato</span><span class="sxs-lookup"><span data-stu-id="7202e-110">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="7202e-111">È possibile scaricare le utilità bcp e sqlcmd hello da hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="7202e-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="7202e-112">Dati in formato ASCII o UTF-16</span><span class="sxs-lookup"><span data-stu-id="7202e-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="7202e-113">Se si sta provando questa esercitazione con i propri dati, i dati devono toouse hello ASCII o UTF-16 codifica poiché bcp non supportano UTF-8.</span><span class="sxs-lookup"><span data-stu-id="7202e-113">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="7202e-114">1. Creare una tabella di destinazione</span><span class="sxs-lookup"><span data-stu-id="7202e-114">1. Create a destination table</span></span>
<span data-ttu-id="7202e-115">Definire una tabella nel Database SQL come tabella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="7202e-115">Define a table in SQL Database as hello destination table.</span></span> <span data-ttu-id="7202e-116">colonne di Hello nella tabella hello devono corrispondere toohello dati in ogni riga del file di dati.</span><span class="sxs-lookup"><span data-stu-id="7202e-116">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="7202e-117">toocreate una tabella, aprire un prompt dei comandi e utilizzare hello toorun sqlcmd.exe comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7202e-117">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="7202e-118">2. Creare un file di dati di origine</span><span class="sxs-lookup"><span data-stu-id="7202e-118">2. Create a source data file</span></span>
<span data-ttu-id="7202e-119">Aprire Blocco note e copiare hello seguenti righe di dati in un nuovo file di testo e quindi salvare il file tooyour locale directory temporanea, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="7202e-119">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="7202e-120">I dati hanno formato ASCII.</span><span class="sxs-lookup"><span data-stu-id="7202e-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="7202e-121">(Facoltativo) tooexport i propri dati da un database di SQL Server, aprire un prompt dei comandi ed eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="7202e-121">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="7202e-122">Sostituire TableName, ServerName, DatabaseName, Username e Password con le informazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="7202e-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a><span data-ttu-id="7202e-123">3. Caricare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="7202e-123">3. Load hello data</span></span>
<span data-ttu-id="7202e-124">dati hello tooload, aprire un prompt dei comandi ed eseguire hello comando seguente, sostituendo valori hello per il nome del Server, nome di Database, nome utente e Password con le proprie informazioni di.</span><span class="sxs-lookup"><span data-stu-id="7202e-124">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="7202e-125">Utilizzare questo comando tooverify hello di dati è stati caricati correttamente</span><span class="sxs-lookup"><span data-stu-id="7202e-125">Use this command tooverify hello data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="7202e-126">risultati Hello dovrebbero essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="7202e-126">hello results should look like this:</span></span>

| <span data-ttu-id="7202e-127">DateId</span><span class="sxs-lookup"><span data-stu-id="7202e-127">DateId</span></span> | <span data-ttu-id="7202e-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="7202e-128">CalendarQuarter</span></span> | <span data-ttu-id="7202e-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="7202e-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7202e-130">20150101</span><span class="sxs-lookup"><span data-stu-id="7202e-130">20150101</span></span> |<span data-ttu-id="7202e-131">1</span><span class="sxs-lookup"><span data-stu-id="7202e-131">1</span></span> |<span data-ttu-id="7202e-132">3</span><span class="sxs-lookup"><span data-stu-id="7202e-132">3</span></span> |
| <span data-ttu-id="7202e-133">20150201</span><span class="sxs-lookup"><span data-stu-id="7202e-133">20150201</span></span> |<span data-ttu-id="7202e-134">1</span><span class="sxs-lookup"><span data-stu-id="7202e-134">1</span></span> |<span data-ttu-id="7202e-135">3</span><span class="sxs-lookup"><span data-stu-id="7202e-135">3</span></span> |
| <span data-ttu-id="7202e-136">20150301</span><span class="sxs-lookup"><span data-stu-id="7202e-136">20150301</span></span> |<span data-ttu-id="7202e-137">1</span><span class="sxs-lookup"><span data-stu-id="7202e-137">1</span></span> |<span data-ttu-id="7202e-138">3</span><span class="sxs-lookup"><span data-stu-id="7202e-138">3</span></span> |
| <span data-ttu-id="7202e-139">20150401</span><span class="sxs-lookup"><span data-stu-id="7202e-139">20150401</span></span> |<span data-ttu-id="7202e-140">2</span><span class="sxs-lookup"><span data-stu-id="7202e-140">2</span></span> |<span data-ttu-id="7202e-141">4</span><span class="sxs-lookup"><span data-stu-id="7202e-141">4</span></span> |
| <span data-ttu-id="7202e-142">20150501</span><span class="sxs-lookup"><span data-stu-id="7202e-142">20150501</span></span> |<span data-ttu-id="7202e-143">2</span><span class="sxs-lookup"><span data-stu-id="7202e-143">2</span></span> |<span data-ttu-id="7202e-144">4</span><span class="sxs-lookup"><span data-stu-id="7202e-144">4</span></span> |
| <span data-ttu-id="7202e-145">20150601</span><span class="sxs-lookup"><span data-stu-id="7202e-145">20150601</span></span> |<span data-ttu-id="7202e-146">2</span><span class="sxs-lookup"><span data-stu-id="7202e-146">2</span></span> |<span data-ttu-id="7202e-147">4</span><span class="sxs-lookup"><span data-stu-id="7202e-147">4</span></span> |
| <span data-ttu-id="7202e-148">20150701</span><span class="sxs-lookup"><span data-stu-id="7202e-148">20150701</span></span> |<span data-ttu-id="7202e-149">3</span><span class="sxs-lookup"><span data-stu-id="7202e-149">3</span></span> |<span data-ttu-id="7202e-150">1</span><span class="sxs-lookup"><span data-stu-id="7202e-150">1</span></span> |
| <span data-ttu-id="7202e-151">20150801</span><span class="sxs-lookup"><span data-stu-id="7202e-151">20150801</span></span> |<span data-ttu-id="7202e-152">3</span><span class="sxs-lookup"><span data-stu-id="7202e-152">3</span></span> |<span data-ttu-id="7202e-153">1</span><span class="sxs-lookup"><span data-stu-id="7202e-153">1</span></span> |
| <span data-ttu-id="7202e-154">20150801</span><span class="sxs-lookup"><span data-stu-id="7202e-154">20150801</span></span> |<span data-ttu-id="7202e-155">3</span><span class="sxs-lookup"><span data-stu-id="7202e-155">3</span></span> |<span data-ttu-id="7202e-156">1</span><span class="sxs-lookup"><span data-stu-id="7202e-156">1</span></span> |
| <span data-ttu-id="7202e-157">20151001</span><span class="sxs-lookup"><span data-stu-id="7202e-157">20151001</span></span> |<span data-ttu-id="7202e-158">4</span><span class="sxs-lookup"><span data-stu-id="7202e-158">4</span></span> |<span data-ttu-id="7202e-159">2</span><span class="sxs-lookup"><span data-stu-id="7202e-159">2</span></span> |
| <span data-ttu-id="7202e-160">20151101</span><span class="sxs-lookup"><span data-stu-id="7202e-160">20151101</span></span> |<span data-ttu-id="7202e-161">4</span><span class="sxs-lookup"><span data-stu-id="7202e-161">4</span></span> |<span data-ttu-id="7202e-162">2</span><span class="sxs-lookup"><span data-stu-id="7202e-162">2</span></span> |
| <span data-ttu-id="7202e-163">20151201</span><span class="sxs-lookup"><span data-stu-id="7202e-163">20151201</span></span> |<span data-ttu-id="7202e-164">4</span><span class="sxs-lookup"><span data-stu-id="7202e-164">4</span></span> |<span data-ttu-id="7202e-165">2</span><span class="sxs-lookup"><span data-stu-id="7202e-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7202e-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7202e-166">Next steps</span></span>
<span data-ttu-id="7202e-167">toomigrate un database di SQL Server, vedere [la migrazione di database di SQL Server](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="7202e-167">toomigrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
