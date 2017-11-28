---
title: dati aaaLoad da SQL Server in Azure SQL Data Warehouse (PolyBase) | Documenti Microsoft
description: Utilizza bcp tooexport dati da file tooflat di SQL Server, archiviazione blob di AZCopy tooimport dati tooAzure e dati di PolyBase tooingest hello in Azure SQL Data Warehouse.
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
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="a3cdf-103">Caricare dati da SQL Server in Azure SQL Data Warehouse (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="a3cdf-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="a3cdf-104">Utilizzare bcp e dati tooload utilità della riga di comando di AZCopy dall'archiviazione blob tooAzure di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-104">Use bcp and AZCopy command-line utilities tooload data from SQL Server tooAzure blob storage.</span></span> <span data-ttu-id="a3cdf-105">Quindi utilizzare i dati di hello tooload PolyBase o Data Factory di Azure in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-105">Then use PolyBase or Azure Data Factory tooload hello data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a3cdf-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a3cdf-106">Prerequisites</span></span>
<span data-ttu-id="a3cdf-107">toostep di questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="a3cdf-107">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="a3cdf-108">Un database di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a3cdf-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="a3cdf-109">utilità della riga di comando bcp Hello installato</span><span class="sxs-lookup"><span data-stu-id="a3cdf-109">hello bcp command line utility installed</span></span>
* <span data-ttu-id="a3cdf-110">utilità della riga di comando SQLCMD installato Hello</span><span class="sxs-lookup"><span data-stu-id="a3cdf-110">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="a3cdf-111">È possibile scaricare le utilità bcp e sqlcmd hello da hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="a3cdf-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="a3cdf-112">Importare i dati in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a3cdf-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="a3cdf-113">In questa esercitazione, verrà di creare una tabella in Azure SQL Data Warehouse e di importare dati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="a3cdf-114">Passaggio 1: Creare una tabella in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a3cdf-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="a3cdf-115">Da un prompt dei comandi, utilizzare sqlcmd toorun hello seguente query toocreate una tabella nell'istanza:</span><span class="sxs-lookup"><span data-stu-id="a3cdf-115">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="a3cdf-116">Vedere [Cenni preliminari su tabella] [ Table Overview] o [sintassi CREATE TABLE] [ CREATE TABLE syntax] per ulteriori informazioni sulla creazione di una tabella in SQL Data Warehouse e hello  opzioni disponibili nella clausola WITH hello.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="a3cdf-117">Passaggio 2: Creare un file di dati di origine</span><span class="sxs-lookup"><span data-stu-id="a3cdf-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="a3cdf-118">Aprire Blocco note e copiare hello seguenti righe di dati in un nuovo file di testo e quindi salvare il file tooyour locale directory temporanea, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-118">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="a3cdf-119">È importante tooremember che bcp.exe non supporta la codifica file hello UTF-8.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-119">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="a3cdf-120">Usare i file ASCII o con codifica UTF-16 quando si usa bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="a3cdf-121">Passaggio 3: Connettersi e importare i dati hello</span><span class="sxs-lookup"><span data-stu-id="a3cdf-121">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="a3cdf-122">Utilizzo di bcp, è possibile connettersi e importare i dati di hello tramite hello seguente comando sostituendo hello i valori appropriati:</span><span class="sxs-lookup"><span data-stu-id="a3cdf-122">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="a3cdf-123">È possibile verificare i dati sono stati caricati eseguendo la seguente query utilizzando sqlcmd hello hello:</span><span class="sxs-lookup"><span data-stu-id="a3cdf-123">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="a3cdf-124">Deve essere restituito hello seguenti risultati:</span><span class="sxs-lookup"><span data-stu-id="a3cdf-124">This should return hello following results:</span></span>

| <span data-ttu-id="a3cdf-125">DateId</span><span class="sxs-lookup"><span data-stu-id="a3cdf-125">DateId</span></span> | <span data-ttu-id="a3cdf-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="a3cdf-126">CalendarQuarter</span></span> | <span data-ttu-id="a3cdf-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="a3cdf-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3cdf-128">20150101</span><span class="sxs-lookup"><span data-stu-id="a3cdf-128">20150101</span></span> |<span data-ttu-id="a3cdf-129">1</span><span class="sxs-lookup"><span data-stu-id="a3cdf-129">1</span></span> |<span data-ttu-id="a3cdf-130">3</span><span class="sxs-lookup"><span data-stu-id="a3cdf-130">3</span></span> |
| <span data-ttu-id="a3cdf-131">20150201</span><span class="sxs-lookup"><span data-stu-id="a3cdf-131">20150201</span></span> |<span data-ttu-id="a3cdf-132">1</span><span class="sxs-lookup"><span data-stu-id="a3cdf-132">1</span></span> |<span data-ttu-id="a3cdf-133">3</span><span class="sxs-lookup"><span data-stu-id="a3cdf-133">3</span></span> |
| <span data-ttu-id="a3cdf-134">20150301</span><span class="sxs-lookup"><span data-stu-id="a3cdf-134">20150301</span></span> |<span data-ttu-id="a3cdf-135">1</span><span class="sxs-lookup"><span data-stu-id="a3cdf-135">1</span></span> |<span data-ttu-id="a3cdf-136">3</span><span class="sxs-lookup"><span data-stu-id="a3cdf-136">3</span></span> |
| <span data-ttu-id="a3cdf-137">20150401</span><span class="sxs-lookup"><span data-stu-id="a3cdf-137">20150401</span></span> |<span data-ttu-id="a3cdf-138">2</span><span class="sxs-lookup"><span data-stu-id="a3cdf-138">2</span></span> |<span data-ttu-id="a3cdf-139">4</span><span class="sxs-lookup"><span data-stu-id="a3cdf-139">4</span></span> |
| <span data-ttu-id="a3cdf-140">20150501</span><span class="sxs-lookup"><span data-stu-id="a3cdf-140">20150501</span></span> |<span data-ttu-id="a3cdf-141">2</span><span class="sxs-lookup"><span data-stu-id="a3cdf-141">2</span></span> |<span data-ttu-id="a3cdf-142">4</span><span class="sxs-lookup"><span data-stu-id="a3cdf-142">4</span></span> |
| <span data-ttu-id="a3cdf-143">20150601</span><span class="sxs-lookup"><span data-stu-id="a3cdf-143">20150601</span></span> |<span data-ttu-id="a3cdf-144">2</span><span class="sxs-lookup"><span data-stu-id="a3cdf-144">2</span></span> |<span data-ttu-id="a3cdf-145">4</span><span class="sxs-lookup"><span data-stu-id="a3cdf-145">4</span></span> |
| <span data-ttu-id="a3cdf-146">20150701</span><span class="sxs-lookup"><span data-stu-id="a3cdf-146">20150701</span></span> |<span data-ttu-id="a3cdf-147">3</span><span class="sxs-lookup"><span data-stu-id="a3cdf-147">3</span></span> |<span data-ttu-id="a3cdf-148">1</span><span class="sxs-lookup"><span data-stu-id="a3cdf-148">1</span></span> |
| <span data-ttu-id="a3cdf-149">20150801</span><span class="sxs-lookup"><span data-stu-id="a3cdf-149">20150801</span></span> |<span data-ttu-id="a3cdf-150">3</span><span class="sxs-lookup"><span data-stu-id="a3cdf-150">3</span></span> |<span data-ttu-id="a3cdf-151">1</span><span class="sxs-lookup"><span data-stu-id="a3cdf-151">1</span></span> |
| <span data-ttu-id="a3cdf-152">20150801</span><span class="sxs-lookup"><span data-stu-id="a3cdf-152">20150801</span></span> |<span data-ttu-id="a3cdf-153">3</span><span class="sxs-lookup"><span data-stu-id="a3cdf-153">3</span></span> |<span data-ttu-id="a3cdf-154">1</span><span class="sxs-lookup"><span data-stu-id="a3cdf-154">1</span></span> |
| <span data-ttu-id="a3cdf-155">20151001</span><span class="sxs-lookup"><span data-stu-id="a3cdf-155">20151001</span></span> |<span data-ttu-id="a3cdf-156">4</span><span class="sxs-lookup"><span data-stu-id="a3cdf-156">4</span></span> |<span data-ttu-id="a3cdf-157">2</span><span class="sxs-lookup"><span data-stu-id="a3cdf-157">2</span></span> |
| <span data-ttu-id="a3cdf-158">20151101</span><span class="sxs-lookup"><span data-stu-id="a3cdf-158">20151101</span></span> |<span data-ttu-id="a3cdf-159">4</span><span class="sxs-lookup"><span data-stu-id="a3cdf-159">4</span></span> |<span data-ttu-id="a3cdf-160">2</span><span class="sxs-lookup"><span data-stu-id="a3cdf-160">2</span></span> |
| <span data-ttu-id="a3cdf-161">20151201</span><span class="sxs-lookup"><span data-stu-id="a3cdf-161">20151201</span></span> |<span data-ttu-id="a3cdf-162">4</span><span class="sxs-lookup"><span data-stu-id="a3cdf-162">4</span></span> |<span data-ttu-id="a3cdf-163">2</span><span class="sxs-lookup"><span data-stu-id="a3cdf-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="a3cdf-164">Passaggio 4: creare le statistiche sui dati appena caricati</span><span class="sxs-lookup"><span data-stu-id="a3cdf-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="a3cdf-165">SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="a3cdf-166">Ordine tooget hello prestazioni migliori dalle query, è importante creare statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento hello o si verificano modifiche sostanziali in dati hello.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-166">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="a3cdf-167">Per una spiegazione dettagliata delle statistiche, vedere hello [statistiche] [ Statistics] argomento nel gruppo di sviluppare hello degli argomenti.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-167">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="a3cdf-168">Di seguito è riportato un esempio di come statistiche toocreate sulla tabella hello caricati in questo esempio</span><span class="sxs-lookup"><span data-stu-id="a3cdf-168">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="a3cdf-169">Hello seguendo le istruzioni CREATE STATISTICS sqlcmd al prompt dei comandi eseguire:</span><span class="sxs-lookup"><span data-stu-id="a3cdf-169">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="a3cdf-170">Esportare i dati da SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a3cdf-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="a3cdf-171">In questa esercitazione verrà creato un file di dati da una tabella in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="a3cdf-172">Si esporterà i dati di hello creato in precedenza tooa nuovo file di dati denominato DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-172">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="a3cdf-173">Passaggio 1: Esportare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="a3cdf-173">Step 1: Export hello data</span></span>
<span data-ttu-id="a3cdf-174">Utilità bcp hello, è possibile connettersi ed esportare dati utilizzando hello seguente comando sostituendo hello i valori appropriati:</span><span class="sxs-lookup"><span data-stu-id="a3cdf-174">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="a3cdf-175">È possibile verificare i dati è stati esportati correttamente aprendo hello nuovo file hello.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-175">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="a3cdf-176">dati Hello nel file hello devono corrispondere testo hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a3cdf-176">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="a3cdf-177">A causa di natura toohello dei sistemi distribuiti, ordine dei dati hello potrebbe non essere hello uguali tra i database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-177">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="a3cdf-178">Un'altra opzione consiste hello toouse **queryout** funzione di bcp toowrite una query estrarre anziché di esportare l'intera tabella hello.</span><span class="sxs-lookup"><span data-stu-id="a3cdf-178">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a3cdf-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3cdf-179">Next steps</span></span>
<span data-ttu-id="a3cdf-180">Per una panoramica sul caricamento, vedere [Caricare i dati in SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a3cdf-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="a3cdf-181">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="a3cdf-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
