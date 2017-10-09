---
title: dati di tooload aaaUse bcp in SQL Data Warehouse | Documenti Microsoft
description: Informazioni su quali bcp e come toouse per scenari di data warehouse.
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
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="ef871-103">Caricare i dati con BCP</span><span class="sxs-lookup"><span data-stu-id="ef871-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef871-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="ef871-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="ef871-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="ef871-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="ef871-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="ef871-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="ef871-107">BCP</span><span class="sxs-lookup"><span data-stu-id="ef871-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="ef871-108">**[bcp] [ bcp]**  è un'utilità di caricamento bulk della riga di comando che consente di toocopy dati tra SQL Server, i file di dati e SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef871-108">**[bcp][bcp]** is a command-line bulk load utility that allows you toocopy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="ef871-109">Usare bcp tooimport un numero elevato di righe in tabelle di SQL Data Warehouse o tooexport dati dalle tabelle di SQL Server nei file di dati.</span><span class="sxs-lookup"><span data-stu-id="ef871-109">Use bcp tooimport large numbers of rows into SQL Data Warehouse tables or tooexport data from SQL Server tables into data files.</span></span> <span data-ttu-id="ef871-110">Tranne quando sono usati con l'opzione queryout hello, bcp richiede alcuna conoscenza di Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="ef871-110">Except when used with hello queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="ef871-111">bcp è un modo semplice e rapido toomove più piccoli set di dati dentro e fuori da un database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef871-111">bcp is a quick and easy way toomove smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="ef871-112">quantità esatta di Hello di dati che sono consigliabile tooload/estrazione tramite bcp variano di rete nella connessione toohello data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="ef871-112">hello exact amount of data that is recommended tooload/extract via bcp will depend on you network connection toohello Azure data center.</span></span>  <span data-ttu-id="ef871-113">In genere, le tabelle delle dimensioni possono essere caricate ed estratte facilmente con bcp, tuttavia bcp non è consigliato per il caricamento o l'estrazione di grandi volumi di dati.</span><span class="sxs-lookup"><span data-stu-id="ef871-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="ef871-114">Polybase è hello consigliato strumento per il caricamento e l'estrazione di grandi volumi di dati come un processo migliore sfruttando l'architettura di elaborazione parallela massiva hello di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef871-114">Polybase is hello recommended tool for loading and extracting large volumes of data as it does a better job leveraging hello massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="ef871-115">Con bcp è possibile:</span><span class="sxs-lookup"><span data-stu-id="ef871-115">With bcp you can:</span></span>

* <span data-ttu-id="ef871-116">Utilizzare una semplice utilità da riga di comando tooload di dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef871-116">Use a simple command-line utility tooload data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="ef871-117">Utilizzare un semplice utilità da riga di comando tooextract dati da SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef871-117">Use a simple command-line utility tooextract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="ef871-118">In questa esercitazione verranno illustrate le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="ef871-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="ef871-119">Importazione di dati in una tabella utilizzando bcp hello nella finestra di comando</span><span class="sxs-lookup"><span data-stu-id="ef871-119">Import data into a table using hello bcp in command</span></span>
* <span data-ttu-id="ef871-120">Esportare i dati da un piano di hello tabella abbonamento comando</span><span class="sxs-lookup"><span data-stu-id="ef871-120">Export data from a table uisng hello bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ef871-121">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ef871-121">Prerequisites</span></span>
<span data-ttu-id="ef871-122">toostep di questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="ef871-122">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="ef871-123">Un database di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ef871-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="ef871-124">utilità della riga di comando bcp Hello installato</span><span class="sxs-lookup"><span data-stu-id="ef871-124">hello bcp command line utility installed</span></span>
* <span data-ttu-id="ef871-125">utilità della riga di comando SQLCMD installato Hello</span><span class="sxs-lookup"><span data-stu-id="ef871-125">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="ef871-126">È possibile scaricare le utilità bcp e sqlcmd hello da hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="ef871-126">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="ef871-127">Importare i dati in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ef871-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="ef871-128">In questa esercitazione, verrà di creare una tabella in Azure SQL Data Warehouse e di importare dati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="ef871-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="ef871-129">Passaggio 1: Creare una tabella in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ef871-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="ef871-130">Da un prompt dei comandi, utilizzare sqlcmd toorun hello seguente query toocreate una tabella nell'istanza:</span><span class="sxs-lookup"><span data-stu-id="ef871-130">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="ef871-131">Vedere [Cenni preliminari su tabella] [ Table Overview] o [sintassi CREATE TABLE] [ CREATE TABLE syntax] per ulteriori informazioni sulla creazione di una tabella in SQL Data Warehouse e hello  opzioni disponibili nella clausola WITH hello.</span><span class="sxs-lookup"><span data-stu-id="ef871-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="ef871-132">Passaggio 2: Creare un file di dati di origine</span><span class="sxs-lookup"><span data-stu-id="ef871-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="ef871-133">Aprire Blocco note e copiare hello seguenti righe di dati in un nuovo file di testo e quindi salvare il file tooyour locale directory temporanea, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="ef871-133">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="ef871-134">È importante tooremember che bcp.exe non supporta la codifica file hello UTF-8.</span><span class="sxs-lookup"><span data-stu-id="ef871-134">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="ef871-135">Usare i file ASCII o con codifica UTF-16 quando si usa bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="ef871-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="ef871-136">Passaggio 3: Connettersi e importare i dati hello</span><span class="sxs-lookup"><span data-stu-id="ef871-136">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="ef871-137">Utilizzo di bcp, è possibile connettersi e importare i dati di hello tramite hello seguente comando sostituendo hello i valori appropriati:</span><span class="sxs-lookup"><span data-stu-id="ef871-137">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="ef871-138">È possibile verificare i dati sono stati caricati eseguendo la seguente query utilizzando sqlcmd hello hello:</span><span class="sxs-lookup"><span data-stu-id="ef871-138">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="ef871-139">Deve essere restituito hello seguenti risultati:</span><span class="sxs-lookup"><span data-stu-id="ef871-139">This should return hello following results:</span></span>

| <span data-ttu-id="ef871-140">DateId</span><span class="sxs-lookup"><span data-stu-id="ef871-140">DateId</span></span> | <span data-ttu-id="ef871-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="ef871-141">CalendarQuarter</span></span> | <span data-ttu-id="ef871-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="ef871-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ef871-143">20150101</span><span class="sxs-lookup"><span data-stu-id="ef871-143">20150101</span></span> |<span data-ttu-id="ef871-144">1</span><span class="sxs-lookup"><span data-stu-id="ef871-144">1</span></span> |<span data-ttu-id="ef871-145">3</span><span class="sxs-lookup"><span data-stu-id="ef871-145">3</span></span> |
| <span data-ttu-id="ef871-146">20150201</span><span class="sxs-lookup"><span data-stu-id="ef871-146">20150201</span></span> |<span data-ttu-id="ef871-147">1</span><span class="sxs-lookup"><span data-stu-id="ef871-147">1</span></span> |<span data-ttu-id="ef871-148">3</span><span class="sxs-lookup"><span data-stu-id="ef871-148">3</span></span> |
| <span data-ttu-id="ef871-149">20150301</span><span class="sxs-lookup"><span data-stu-id="ef871-149">20150301</span></span> |<span data-ttu-id="ef871-150">1</span><span class="sxs-lookup"><span data-stu-id="ef871-150">1</span></span> |<span data-ttu-id="ef871-151">3</span><span class="sxs-lookup"><span data-stu-id="ef871-151">3</span></span> |
| <span data-ttu-id="ef871-152">20150401</span><span class="sxs-lookup"><span data-stu-id="ef871-152">20150401</span></span> |<span data-ttu-id="ef871-153">2</span><span class="sxs-lookup"><span data-stu-id="ef871-153">2</span></span> |<span data-ttu-id="ef871-154">4</span><span class="sxs-lookup"><span data-stu-id="ef871-154">4</span></span> |
| <span data-ttu-id="ef871-155">20150501</span><span class="sxs-lookup"><span data-stu-id="ef871-155">20150501</span></span> |<span data-ttu-id="ef871-156">2</span><span class="sxs-lookup"><span data-stu-id="ef871-156">2</span></span> |<span data-ttu-id="ef871-157">4</span><span class="sxs-lookup"><span data-stu-id="ef871-157">4</span></span> |
| <span data-ttu-id="ef871-158">20150601</span><span class="sxs-lookup"><span data-stu-id="ef871-158">20150601</span></span> |<span data-ttu-id="ef871-159">2</span><span class="sxs-lookup"><span data-stu-id="ef871-159">2</span></span> |<span data-ttu-id="ef871-160">4</span><span class="sxs-lookup"><span data-stu-id="ef871-160">4</span></span> |
| <span data-ttu-id="ef871-161">20150701</span><span class="sxs-lookup"><span data-stu-id="ef871-161">20150701</span></span> |<span data-ttu-id="ef871-162">3</span><span class="sxs-lookup"><span data-stu-id="ef871-162">3</span></span> |<span data-ttu-id="ef871-163">1</span><span class="sxs-lookup"><span data-stu-id="ef871-163">1</span></span> |
| <span data-ttu-id="ef871-164">20150801</span><span class="sxs-lookup"><span data-stu-id="ef871-164">20150801</span></span> |<span data-ttu-id="ef871-165">3</span><span class="sxs-lookup"><span data-stu-id="ef871-165">3</span></span> |<span data-ttu-id="ef871-166">1</span><span class="sxs-lookup"><span data-stu-id="ef871-166">1</span></span> |
| <span data-ttu-id="ef871-167">20150801</span><span class="sxs-lookup"><span data-stu-id="ef871-167">20150801</span></span> |<span data-ttu-id="ef871-168">3</span><span class="sxs-lookup"><span data-stu-id="ef871-168">3</span></span> |<span data-ttu-id="ef871-169">1</span><span class="sxs-lookup"><span data-stu-id="ef871-169">1</span></span> |
| <span data-ttu-id="ef871-170">20151001</span><span class="sxs-lookup"><span data-stu-id="ef871-170">20151001</span></span> |<span data-ttu-id="ef871-171">4</span><span class="sxs-lookup"><span data-stu-id="ef871-171">4</span></span> |<span data-ttu-id="ef871-172">2</span><span class="sxs-lookup"><span data-stu-id="ef871-172">2</span></span> |
| <span data-ttu-id="ef871-173">20151101</span><span class="sxs-lookup"><span data-stu-id="ef871-173">20151101</span></span> |<span data-ttu-id="ef871-174">4</span><span class="sxs-lookup"><span data-stu-id="ef871-174">4</span></span> |<span data-ttu-id="ef871-175">2</span><span class="sxs-lookup"><span data-stu-id="ef871-175">2</span></span> |
| <span data-ttu-id="ef871-176">20151201</span><span class="sxs-lookup"><span data-stu-id="ef871-176">20151201</span></span> |<span data-ttu-id="ef871-177">4</span><span class="sxs-lookup"><span data-stu-id="ef871-177">4</span></span> |<span data-ttu-id="ef871-178">2</span><span class="sxs-lookup"><span data-stu-id="ef871-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="ef871-179">Passaggio 4: creare le statistiche sui dati appena caricati</span><span class="sxs-lookup"><span data-stu-id="ef871-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="ef871-180">SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.</span><span class="sxs-lookup"><span data-stu-id="ef871-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="ef871-181">Ordine tooget hello prestazioni migliori dalle query, è importante creare statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento hello o si verificano modifiche sostanziali in dati hello.</span><span class="sxs-lookup"><span data-stu-id="ef871-181">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="ef871-182">Per una spiegazione dettagliata delle statistiche, vedere hello [statistiche] [ Statistics] argomento nel gruppo di sviluppare hello degli argomenti.</span><span class="sxs-lookup"><span data-stu-id="ef871-182">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="ef871-183">Di seguito è riportato un esempio di come statistiche toocreate sulla tabella hello caricati in questo esempio</span><span class="sxs-lookup"><span data-stu-id="ef871-183">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="ef871-184">Hello seguendo le istruzioni CREATE STATISTICS sqlcmd al prompt dei comandi eseguire:</span><span class="sxs-lookup"><span data-stu-id="ef871-184">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="ef871-185">Esportare i dati da SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ef871-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="ef871-186">In questa esercitazione verrà creato un file di dati da una tabella in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef871-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="ef871-187">Si esporterà i dati di hello creato in precedenza tooa nuovo file di dati denominato DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="ef871-187">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="ef871-188">Passaggio 1: Esportare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="ef871-188">Step 1: Export hello data</span></span>
<span data-ttu-id="ef871-189">Utilità bcp hello, è possibile connettersi ed esportare dati utilizzando hello seguente comando sostituendo hello i valori appropriati:</span><span class="sxs-lookup"><span data-stu-id="ef871-189">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="ef871-190">È possibile verificare i dati è stati esportati correttamente aprendo hello nuovo file hello.</span><span class="sxs-lookup"><span data-stu-id="ef871-190">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="ef871-191">dati Hello nel file hello devono corrispondere testo hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ef871-191">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="ef871-192">A causa di natura toohello dei sistemi distribuiti, ordine dei dati hello potrebbe non essere hello uguali tra i database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef871-192">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="ef871-193">Un'altra opzione consiste hello toouse **queryout** funzione di bcp toowrite una query estrarre anziché di esportare l'intera tabella hello.</span><span class="sxs-lookup"><span data-stu-id="ef871-193">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ef871-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ef871-194">Next steps</span></span>
<span data-ttu-id="ef871-195">Per una panoramica sul caricamento, vedere [Caricare i dati in SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="ef871-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="ef871-196">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="ef871-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
