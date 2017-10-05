---
title: "Livello 130 di compatibilità del database - Database SQL di Azure | Documentazione Microsoft"
description: "In questo articolo vengono illustrati i vantaggi dell'esecuzione del database SQL di Azure al livello di compatibilità 130 e i vantaggi delle nuove funzionalità Query Optimizer e Query Processor. Vengono discussi anche i possibili effetti collaterali sulle prestazioni delle query per le applicazioni SQL esistenti."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: c08c0690df4f389416e4ed2e2df2dbb72d6fd567
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="acaa6-104">Miglioramento delle prestazioni delle query con il livello di compatibilità 130 nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="acaa6-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="acaa6-105">Il database SQL di Azure esegue in modo trasparente centinaia di migliaia di database a vari livelli di compatibilità diversi, mantenendo e garantendo la compatibilità con le versioni precedenti corrispondenti di Microsoft SQL Server per tutti i clienti.</span><span class="sxs-lookup"><span data-stu-id="acaa6-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing the backward compatibility to the corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="acaa6-106">In questo articolo, vengono illustrati i vantaggi dell'esecuzione del database SQL di Azure al livello di compatibilità 130 e dei vantaggi delle nuove funzionalità Query Optimizer e Query Processor.</span><span class="sxs-lookup"><span data-stu-id="acaa6-106">In this article, we explore the benefits of running your Azure SQL Databse at compatibility level 130, and leveraging the benefits of the new query optimizer and query processor features.</span></span> <span data-ttu-id="acaa6-107">Vengono discussi anche i possibili effetti collaterali sulle prestazioni delle query per le applicazioni SQL esistenti.</span><span class="sxs-lookup"><span data-stu-id="acaa6-107">We also address the possible side-effects on the query performance for the existing SQL applications.</span></span>

<span data-ttu-id="acaa6-108">Di seguito è riportato un promemoria relativo all'allineamento delle versioni di SQL ai livelli di compatibilità predefiniti.</span><span class="sxs-lookup"><span data-stu-id="acaa6-108">As a reminder of history, the alignment of SQL versions to default compatibility levels are as follows:</span></span>

* <span data-ttu-id="acaa6-109">100: in SQL Server 2008 e database SQL di Azure versione 11.</span><span class="sxs-lookup"><span data-stu-id="acaa6-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="acaa6-110">110: in SQL Server 2012 e database SQL di Azure versione 11.</span><span class="sxs-lookup"><span data-stu-id="acaa6-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="acaa6-111">120: in SQL Server 2014 e database SQL di Azure versione 12.</span><span class="sxs-lookup"><span data-stu-id="acaa6-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="acaa6-112">130: in SQL Server 2016 e database SQL di Azure versione 12.</span><span class="sxs-lookup"><span data-stu-id="acaa6-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="acaa6-113">A partire dalla **metà di giugno 2016**, nel database SQL di Azure il livello di compatibilità predefinito sarà 130 anziché 120 per i database **di nuova creazione**.</span><span class="sxs-lookup"><span data-stu-id="acaa6-113">Starting in **mid-June 2016**, in Azure SQL Database, the default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="acaa6-114">I database creati prima della metà di giugno 2016 *non* saranno interessati dalla modifica e manterranno il livello di compatibilità corrente (100, 110 o 120).</span><span class="sxs-lookup"><span data-stu-id="acaa6-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="acaa6-115">I database di cui viene eseguita la migrazione dalla versione 11 alla versione 12 del database SQL di Azure avranno un livello di compatibilità di 100 o 110.</span><span class="sxs-lookup"><span data-stu-id="acaa6-115">Databases that migrated from Azure SQL Database version V11 to V12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="acaa6-116">Informazioni sul livello di compatibilità 130</span><span class="sxs-lookup"><span data-stu-id="acaa6-116">About compatibility level 130</span></span>
<span data-ttu-id="acaa6-117">Per conoscere il livello di compatibilità corrente del database, eseguire prima di tutto l'istruzione Transact-SQL seguente.</span><span class="sxs-lookup"><span data-stu-id="acaa6-117">First, if you want to know the current compatibility level of your database, execute the following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="acaa6-118">Prima del passaggio al livello 130 per i database **di nuova creazione** , questo articolo esamina da vicino la modifica attraverso alcuni esempi di query molto semplici, per valutarne i vantaggi effettivi.</span><span class="sxs-lookup"><span data-stu-id="acaa6-118">Before this change to level 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="acaa6-119">L'elaborazione delle query nei database relazionali può risultare molto complessa e richiedere competenze informatiche e matematiche per comprendere le scelte di progettazione e i comportamenti intrinseci.</span><span class="sxs-lookup"><span data-stu-id="acaa6-119">Query processing in relational databases can be very complex and can lead to lots of computer science and mathematics to understand the inherent design choices and behaviors.</span></span> <span data-ttu-id="acaa6-120">In questo documento il contenuto è stato semplificato intenzionalmente perché che chiunque abbia una minima competenza tecnica possa comprendere l'impatto della modifica del livello di compatibilità e valutarne i vantaggi per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="acaa6-120">In this document, the content has been intentionally simplified to ensure that anyone with some minimum technical background can understand the impact of the compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="acaa6-121">Di seguito è riportato un breve riepilogo delle caratteristiche del livello di compatibilità 130.</span><span class="sxs-lookup"><span data-stu-id="acaa6-121">Let’s have a quick look at what the compatibility level 130 brings at the table.</span></span>  <span data-ttu-id="acaa6-122">Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx):</span><span class="sxs-lookup"><span data-stu-id="acaa6-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="acaa6-123">L'operazione INSERT di un'istruzione INSERT-SELECT può essere multithread o avere un piano parallelo. In precedenza l'operazione era a thread singolo.</span><span class="sxs-lookup"><span data-stu-id="acaa6-123">The Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="acaa6-124">Le tabelle con ottimizzazione per la memoria e le query sulle variabili di tabella ora possono avere piani paralleli. In precedenza l'operazione era a thread singolo.</span><span class="sxs-lookup"><span data-stu-id="acaa6-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="acaa6-125">Le statistiche per la tabella con ottimizzazione per la memoria ora possono essere campionate e vengono aggiornate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="acaa6-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="acaa6-126">Per altre informazioni, vedere [Novità (Motore di database): OLTP in memoria](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) .</span><span class="sxs-lookup"><span data-stu-id="acaa6-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="acaa6-127">Modifiche alla modalità batch rispetto alla modalità riga con gli indici columnstore:</span><span class="sxs-lookup"><span data-stu-id="acaa6-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="acaa6-128">L'ordinamento in una tabella con un indice columnstore viene ora eseguito in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="acaa6-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="acaa6-129">Le aggregazioni finestra ora vengono eseguite in modalità batch, ad esempio con istruzioni TSQL LAG/LEAD.</span><span class="sxs-lookup"><span data-stu-id="acaa6-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="acaa6-130">Le query sulle tabelle columnstore con più clausole distinte operano in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="acaa6-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="acaa6-131">Anche le query in esecuzione con DOP=1 o con un piano seriale vengono eseguite in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="acaa6-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="acaa6-132">I miglioramenti relativi alla stima di cardinalità sono legati effettivamente al livello di compatibilità 120, ma se si esegue un livello di compatibilità inferiore, ovvero 100 o 110, il passaggio al livello di compatibilità 130 porterà anche questi vantaggi, utili per le prestazioni di query delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="acaa6-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), the move to compatibility level 130 will also bring these improvements, and these can also benefit the query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="acaa6-133">Esercitazione sul livello di compatibilità 130</span><span class="sxs-lookup"><span data-stu-id="acaa6-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="acaa6-134">Preparare, prima di tutto, alcune tabelle, indici e dati casuali creati per provare alcune di queste nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="acaa6-134">First let’s get some tables, indexes and random data created to practice some of these new capabilities.</span></span> <span data-ttu-id="acaa6-135">Gli esempi di script TSQL possono essere eseguiti in SQL Server 2016 o nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="acaa6-135">The TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="acaa6-136">Tuttavia, quando si crea un database SQL di Azure, assicurarsi di scegliere come minimo un database P2. Sono necessari almeno due core per consentire il multithreading e poter trarre vantaggio da queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="acaa6-136">However, when creating an Azure SQL database, make sure you choose at the minimum a P2 database because you need at least a couple of cores to allow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- the second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


<span data-ttu-id="acaa6-137">Vengono ora prese in esame alcune delle funzionalità di elaborazione query offerte dal livello di compatibilità 130.</span><span class="sxs-lookup"><span data-stu-id="acaa6-137">Now, let’s have a look to some of the Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="acaa6-138">INSERT in parallelo</span><span class="sxs-lookup"><span data-stu-id="acaa6-138">Parallel INSERT</span></span>
<span data-ttu-id="acaa6-139">Le istruzioni TSQL seguenti permettono di eseguire l'operazione INSERT con i livelli di compatibilità 120 e 130. Questi eseguono l'operazione INSERT rispettivamente in un modello a thread singolo (120) e in un modello multithread (130).</span><span class="sxs-lookup"><span data-stu-id="acaa6-139">Executing the TSQL statements below executes the INSERT operation under compatibility level 120 and 130, which respectively executes the INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- The INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- The INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="acaa6-140">Richiedendo il piano di query effettivo ed esaminandone la rappresentazione grafica o il contenuto XML è possibile determinare la funzione di stima di cardinalità usata.</span><span class="sxs-lookup"><span data-stu-id="acaa6-140">By requesting the actual the query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="acaa6-141">La visualizzazione affiancata della figura 1 mostra chiaramente che l'esecuzione dell'operazione INSERT sull'indice columnstore passa da seriale, nel livello 120, a parallela, nel livello 130.</span><span class="sxs-lookup"><span data-stu-id="acaa6-141">Looking at the plans side-by-side on figure 1, we can clearly see that the Column Store INSERT execution goes from serial in 120 to parallel in 130.</span></span> <span data-ttu-id="acaa6-142">Si noti anche la modifica dell'icona iteratore nel piano 130, con due frecce parallele a indicare il fatto che ora l'esecuzione dell'iteratore è effettivamente parallela.</span><span class="sxs-lookup"><span data-stu-id="acaa6-142">Also, note that the change of the iterator icon in the 130 plan showing two parallel arrows, illustrating the fact that now the iterator execution is indeed parallel.</span></span> <span data-ttu-id="acaa6-143">Per il completamento di operazioni INSERT di grandi dimensioni, l'esecuzione parallela, collegata al numero di core disponibili per il database, offre prestazioni migliori e può risultare fino a un 100 volte più veloce, a seconda delle situazioni.</span><span class="sxs-lookup"><span data-stu-id="acaa6-143">If you have large INSERT operations to complete, the parallel execution, linked to the number of core you have at your disposal for the database, will perform better; up to a 100 times faster depending your situation!</span></span>

<span data-ttu-id="acaa6-144">*Figura 1: L'operazione INSERT passa da seriale a parallela con il livello di compatibilità 130.*</span><span class="sxs-lookup"><span data-stu-id="acaa6-144">*Figure 1: INSERT operation changes from serial to parallel with compatibility level 130.*</span></span>

![Figura 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="acaa6-146">Modalità batch seriale</span><span class="sxs-lookup"><span data-stu-id="acaa6-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="acaa6-147">Analogamente, il passaggio al livello di compatibilità 130 durante l'elaborazione di righe di dati consente l'elaborazione in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="acaa6-147">Similarly, moving to compatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="acaa6-148">In primo luogo, le operazioni in modalità batch sono disponibili solo in presenza di un indice columnstore.</span><span class="sxs-lookup"><span data-stu-id="acaa6-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="acaa6-149">In secondo luogo, un batch rappresenta in genere circa 900 righe e usa una logica del codice ottimizzata per una CPU multicore, ha una maggiore velocità effettiva della memoria e sfrutta direttamente i dati compressi dell'indice columnstore quando è possibile.</span><span class="sxs-lookup"><span data-stu-id="acaa6-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages the compressed data of the Column Store whenever possible.</span></span> <span data-ttu-id="acaa6-150">In queste condizioni SQL Server 2016 può elaborare circa 900 righe contemporaneamente, anziché 1 riga alla volta. Il costo generale dell'operazione viene quindi condiviso dall'intero batch, con conseguente riduzione del costo complessivo per riga.</span><span class="sxs-lookup"><span data-stu-id="acaa6-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at the time, and as a consequence, the overall overhead cost of the operation is now shared by the entire batch, reducing the overall cost by row.</span></span> <span data-ttu-id="acaa6-151">Questa quantità condivisa di operazioni, unita alla compressione dell'indice columnstore, riduce sostanzialmente la latenza legata a un'operazione SELECT in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="acaa6-151">This shared amount of operations combined with the column store compression basically reduces the latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="acaa6-152">Per altre informazioni sull'indice columnstore e la modalità batch, vedere la [descrizione degli indici columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="acaa6-152">You can find more details about the column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="acaa6-153">Come mostra la visualizzazione affiancata dei piani di query nella figura 2, anche la modalità di elaborazione è cambiata con il livello di compatibilità. Di conseguenza, quando si eseguono query in entrambi i livelli di compatibilità si vede come la maggior parte del tempo di elaborazione sia dedicata alla modalità riga (86%), rispetto alla modalità batch (14%) usata per elaborare due batch.</span><span class="sxs-lookup"><span data-stu-id="acaa6-153">As visible below, by observing the query plans side-by-side on figure 2, we can see that the processing mode has changed with the compatibility level, and as a consequence, when executing the queries in both compatibility level altogether, we can see that most of the processing time is spent in row mode (86%) compared to the batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="acaa6-154">Aumentando le dimensioni del set di dati, aumentano anche i vantaggi.</span><span class="sxs-lookup"><span data-stu-id="acaa6-154">Increase the dataset, the benefit will increase.</span></span>

<span data-ttu-id="acaa6-155">*Figura 2: L'operazione SELECT passa da seriale alla modalità batch con il livello di compatibilità 130.*</span><span class="sxs-lookup"><span data-stu-id="acaa6-155">*Figure 2: SELECT operation changes from serial to batch mode with compatibility level 130.*</span></span>

![Figura 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="acaa6-157">Modalità batch per l'esecuzione dell'ordinamento</span><span class="sxs-lookup"><span data-stu-id="acaa6-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="acaa6-158">Quanto appena visto si applica anche a un'operazione di ordinamento. La transizione dalla modalità riga nel livello di compatibilità 120 alla modalità batch nel livello di compatibilità 130 migliora le prestazioni dell'operazione SORT, per gli stessi motivi.</span><span class="sxs-lookup"><span data-stu-id="acaa6-158">Similar to the above, but applied to a sort operation, the transition from row mode (compatibility level 120) to batch mode (compatibility level 130) improves the performance of the SORT operation for the same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="acaa6-159">La visualizzazione affiancata nella figura 3 mostra che l'operazione di ordinamento in modalità riga rappresenta l'81% del costo, mentre la modalità batch rappresenta solo il 19% del costo. Rispettivamente, l'81% e il 56% dell'operazione di ordinamento.</span><span class="sxs-lookup"><span data-stu-id="acaa6-159">Visible side-by-side on figure 3, we can see that the sort operation in row mode represents 81% of the cost, while the batch mode only represents 19% of the cost (respectively 81% and 56% on the sort itself).</span></span>

<span data-ttu-id="acaa6-160">*Figura 3: L'operazione SORT passa dalla modalità riga alla modalità batch con il livello di compatibilità 130.*</span><span class="sxs-lookup"><span data-stu-id="acaa6-160">*Figure 3: SORT operation changes from row to batch mode with compatibility level 130.*</span></span>

![Figura 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="acaa6-162">Naturalmente, questi esempi contengono solo decine di migliaia di righe, che non sono nulla rispetto alla quantità di dati disponibili nella maggior parte delle istanze di SQL Server di oggi.</span><span class="sxs-lookup"><span data-stu-id="acaa6-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at the data available in most SQL Servers these days.</span></span> <span data-ttu-id="acaa6-163">Su milioni di righe, questo può tradursi in tempi di esecuzione inferiori di diversi minuti ogni giorno, in base alla natura del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="acaa6-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending the nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="acaa6-164">Miglioramenti apportati alla stima di cardinalità (CE)</span><span class="sxs-lookup"><span data-stu-id="acaa6-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="acaa6-165">La nuova funzionalità di stima di cardinalità è stata introdotta con SQL Server 2014 ed è inclusa in tutti i database in esecuzione a un livello di compatibilità 120 o superiore.</span><span class="sxs-lookup"><span data-stu-id="acaa6-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="acaa6-166">La stima di cardinalità è sostanzialmente la logica usata per determinare il modo in cui SQL Server deve eseguire una query in base al relativo costo stimato.</span><span class="sxs-lookup"><span data-stu-id="acaa6-166">Essentially, cardinality estimation is the logic used to determine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="acaa6-167">La stima viene calcolata usando informazioni basate sulle statistiche associate agli oggetti coinvolti nella query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-167">The estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="acaa6-168">In generale, le funzioni di stima di cardinalità sono costituite da stime dei conteggi delle righe, informazioni sulla distribuzione dei valori, conteggi dei valori distinct e conteggi duplicati contenuti in tabelle e oggetti a cui viene fatto riferimento nella query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about the distribution of the values, distinct value counts, and duplicate counts contained in the tables and objects referenced in the query.</span></span> <span data-ttu-id="acaa6-169">Un errore in queste stime può portare a operazioni di I/O sul disco non necessarie a causa di concessioni di memoria insufficienti, con conseguenti eventi di spill di TempDB, o alla scelta dell'esecuzione di un piano seriale anziché di un piano parallelo, per fare alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="acaa6-169">Getting these estimates wrong, can lead to unnecessary disk I/O due to insufficient memory grants (i.e. TempDB spills), or to a selection of a serial plan execution over a parallel plan execution, to name a few.</span></span> <span data-ttu-id="acaa6-170">In conclusione, stime non corrette possono portare a una riduzione del livello di prestazioni complessivo dell'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-170">Conclusion, incorrect estimates can lead to an overall performance degradation of the query execution.</span></span> <span data-ttu-id="acaa6-171">Stime corrette e più accurate, d'altro canto, migliorano notevolmente l'esecuzione delle query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-171">On the other side, better estimates, more accurate estimates, leads to better query executions!</span></span>

<span data-ttu-id="acaa6-172">Come accennato in precedenza, le stime e l'ottimizzazione delle query sono un argomento complesso. Per informazioni più approfondite sui piani di query e sulla stima di cardinalità, vedere il documento [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) (Ottimizzazione dei piani di query con la funzionalità di stima di cardinalità di SQL Server 2014).</span><span class="sxs-lookup"><span data-stu-id="acaa6-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want to learn more about query plans and cardinality estimator, you can refer to the document at [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="acaa6-173">Stima di cardinalità corrente</span><span class="sxs-lookup"><span data-stu-id="acaa6-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="acaa6-174">Per determinare la stima di cardinalità in cui vengono eseguite le query è possibile usare gli esempi di query seguenti.</span><span class="sxs-lookup"><span data-stu-id="acaa6-174">To determine under which Cardinality Estimation your queries are running, let’s just use the query samples below.</span></span> <span data-ttu-id="acaa6-175">Si noti che il primo esempio viene eseguito con il livello di compatibilità 110 e implica l'uso delle funzioni di stima di cardinalità precedenti.</span><span class="sxs-lookup"><span data-stu-id="acaa6-175">Note that this first example will run under compatibility level 110, implying the use of the old Cardinality Estimation functions.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="acaa6-176">Al termine dell'esecuzione, fare clic sul collegamento XML ed esaminare le proprietà del primo iteratore, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="acaa6-176">Once execution is complete, click on the XML link, and look at the properties of the first iterator as shown below.</span></span> <span data-ttu-id="acaa6-177">Si noti che il nome della proprietà CardinalityEstimationModelVersion attualmente è impostato su 70.</span><span class="sxs-lookup"><span data-stu-id="acaa6-177">Note the property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="acaa6-178">Questo non significa che il livello di compatibilità del database sia impostato su SQL Server versione 7.0. Come si può vedere nelle istruzioni TSQL precedenti, è impostato su 110. Il valore 70 rappresenta semplicemente la funzionalità di stima di cardinalità legacy disponibile a partire da SQL Server 7.0, che non ha subito modifiche importanti fino a SQL Server 2014 e al relativo livello di compatibilità 120.</span><span class="sxs-lookup"><span data-stu-id="acaa6-178">It does not mean that the database compatibility level is set to the SQL Server 7.0 version (it is set on 110 as visible in the TSQL statements above), but the value 70 simply represents the legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="acaa6-179">*Figura 4: CardinalityEstimationModelVersion impostato su 70 quando si usa un livello di compatibilità 110 o inferiore.*</span><span class="sxs-lookup"><span data-stu-id="acaa6-179">*Figure 4: The CardinalityEstimationModelVersion is set to 70 when using a compatibility level of 110 or below.*</span></span>

![Figura 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="acaa6-181">In alternativa, è possibile modificare il livello di compatibilità in 130 e disabilitare l'uso della nuova funzione di stima di cardinalità impostando LEGACY_CARDINALITY_ESTIMATION su ON con l'istruzione [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="acaa6-181">Alternatively, you can change the compatibility level to 130, and disable the use of the new Cardinality Estimation function by using the LEGACY_CARDINALITY_ESTIMATION set to ON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="acaa6-182">In termini di funzione di stima di cardinalità questo equivale a usare il livello 110, pur facendo uso del livello di compatibilità più recente per l'elaborazione delle query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-182">This will be exactly the same as using 110 from a Cardinality Estimation function point of view, while using the latest query processing compatibility level.</span></span> <span data-ttu-id="acaa6-183">Così facendo, è possibile sfruttare le nuove funzionalità di elaborazione query incluse nel livello di compatibilità più recente, ovvero la modalità batch, ma poter fare uso all'occorrenza della funzione di stima di cardinalità precedente.</span><span class="sxs-lookup"><span data-stu-id="acaa6-183">Doing so, you can benefit from the new query processing features coming with the latest compatibility level (i.e. batch mode), but still rely on the old Cardinality Estimation functionality if necessary.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="acaa6-184">Il semplice passaggio al livello di compatibilità 120 o 130 abilita la nuova funzionalità di stima di cardinalità.</span><span class="sxs-lookup"><span data-stu-id="acaa6-184">Simply moving to the compatibility level 120 or 130 enables the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="acaa6-185">In tal caso, il valore predefinito di CardinalityEstimationModelVersion sarà impostato su 120 o 130, come mostrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="acaa6-185">In such a case, the default CardinalityEstimationModelVersion will be set accordingly to 120 or 130 as visible below.</span></span>

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="acaa6-186">*Figura 5: CardinalityEstimationModelVersion impostato su 130 quando si usa un livello di compatibilità 130.*</span><span class="sxs-lookup"><span data-stu-id="acaa6-186">*Figure 5: The CardinalityEstimationModelVersion is set to 130 when using a compatibility level of 130.*</span></span>

![Figura 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-the-cardinality-estimation-differences"></a><span data-ttu-id="acaa6-188">Osservazione delle differenze nella stima di cardinalità</span><span class="sxs-lookup"><span data-stu-id="acaa6-188">Witnessing the Cardinality Estimation differences</span></span>
<span data-ttu-id="acaa6-189">A questo punto, provare a eseguire una query leggermente più complessa che preveda un INNER JOIN con una clausola WHERE e alcuni predicati. Esaminare prima di tutto la stima del conteggio delle righe ottenuta dalla funzione di stima di cardinalità precedente.</span><span class="sxs-lookup"><span data-stu-id="acaa6-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at the row count estimate from the old Cardinality Estimation function first.</span></span>

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="acaa6-190">L'esecuzione di questa query restituisce in effetti 200.704 righe, mentre la stima delle righe prodotta dalla funzione di stima di cardinalità precedente indica 194.284 righe.</span><span class="sxs-lookup"><span data-stu-id="acaa6-190">Executing this query effectively returns 200,704 rows, while the row estimate with the old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="acaa6-191">Come detto in precedenza, i risultati di conteggio delle righe variano anche in base alla frequenza con cui sono stati eseguiti gli esempi precedenti, che a ogni esecuzione popolano le tabelle di esempio.</span><span class="sxs-lookup"><span data-stu-id="acaa6-191">Obviously, as said before, these row count results will also depend how often you ran the previous samples, which populates the sample tables over and over again at each run.</span></span> <span data-ttu-id="acaa6-192">Anche i predicati della query hanno un effetto sulla stima effettiva, insieme alla forma della tabella, al contenuto dei dati e al modo in cui i dati sono effettivamente correlati tra loro.</span><span class="sxs-lookup"><span data-stu-id="acaa6-192">Obviously, the predicates in your query will also have an influence on the actual estimation aside from the table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="acaa6-193">*Figura 6: La stima del conteggio delle righe è 194.284. 6.000 righe di differenza rispetto alle 200.704 righe effettive.*</span><span class="sxs-lookup"><span data-stu-id="acaa6-193">*Figure 6: The row count estimate is 194,284 or 6,000 rows off from the 200,704 rows expected.*</span></span>

![Figura 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="acaa6-195">Eseguire ora la stessa query con la nuova funzione di stima di cardinalità.</span><span class="sxs-lookup"><span data-stu-id="acaa6-195">In the same way, let’s now execute the same query with the new Cardinality Estimation functionality.</span></span>

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="acaa6-196">Esaminando la figura seguente, si nota che la stima delle righe è ora 202.877. Molto più vicina al conteggio effettivo e superiore alla stima di cardinalità precedente.</span><span class="sxs-lookup"><span data-stu-id="acaa6-196">Looking at the below, we now see that the row estimate is 202,877, or much closer and higher than the old Cardinality Estimation.</span></span>

<span data-ttu-id="acaa6-197">*Figura 7: La stima del conteggio delle righe è ora 202.877 anziché 194.284.*</span><span class="sxs-lookup"><span data-stu-id="acaa6-197">*Figure 7: The row count estimate is now 202,877, instead of 194,284.*</span></span>

![Figura 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="acaa6-199">Il risultato effettivo è di 200.704 righe. Tale risultato dipende però dalla frequenza con cui sono state eseguite le query degli esempi precedenti. È importante sottolineare anche che dato l'uso dell'istruzione RAND() in TSQL, i valori effettivi restituiti possono variare da un'esecuzione all'altra.</span><span class="sxs-lookup"><span data-stu-id="acaa6-199">In reality, the result set is 200,704 rows (but all of it depends how often you did run the queries of the previous samples, but more importantly, because the TSQL uses the RAND() statement, the actual values returned can vary from one run to the next).</span></span> <span data-ttu-id="acaa6-200">In questo particolare esempio, quindi, con una stima del numero di righe pari a 202.877, la nuova stima di cardinalità si avvicina di più al risultato effettivo di 200.704, rispetto alle 194.284 della funzionalità precedente.</span><span class="sxs-lookup"><span data-stu-id="acaa6-200">Therefore, in this particular example, the new Cardinality Estimation does a better job at estimating the number of rows because 202,877 is much closer to 200,704, than 194,284!</span></span> <span data-ttu-id="acaa6-201">Infine, se si modificano i predicati della clausola WHERE in uguaglianze anziché usare, ad esempio, il simbolo ">", la differenza tra le stime della nuova funzione di cardinalità e di quella precedente può aumentare ancora di più, a seconda del numero di corrispondenze che è possibile ottenere.</span><span class="sxs-lookup"><span data-stu-id="acaa6-201">Last, if you change the WHERE clause predicates to equality (rather than “>” for instance), this could make the estimates between the old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="acaa6-202">In questo caso, naturalmente, una differenza di circa 6000 righe rispetto al conteggio effettivo non rappresenta una grande quantità di dati, in alcune situazioni.</span><span class="sxs-lookup"><span data-stu-id="acaa6-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="acaa6-203">Nella realtà si tratta spesso di milioni di righe su numerose tabelle e di query più complesse. In alcuni casi le stime possono sbagliare di milioni di righe e questo può portare a scegliere un piano di esecuzione sbagliato o a richiedere concessioni di memoria insufficienti, con conseguenti eventi di spill di TempDB e aumento delle operazioni di I/O.</span><span class="sxs-lookup"><span data-stu-id="acaa6-203">Now, transpose this to millions of rows across several tables and more complex queries, and at times the estimate can be off by millions of rows , and therefore, the risk of picking-up the wrong execution plan, or requesting insufficient memory grants leading to TempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="acaa6-204">Se possibile, provare a fare questo confronto con le query e i set di dati più usati, per scoprire le differenze tra le vecchie e le nuove stime. Alcune potrebbero discostarsi ancora di più dai valori effettivi, mentre altre potrebbero avvicinarsi di più al conteggio delle righe effettivamente restituito nei set di risultati.</span><span class="sxs-lookup"><span data-stu-id="acaa6-204">If you have the opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of the old and new estimates are affected, while some could just become more off from the reality, or some others just simply closer to the actual row counts actually returned in the result sets.</span></span> <span data-ttu-id="acaa6-205">Tutto dipende dalla forma delle query, dalle caratteristiche del database SQL di Azure, dalla natura e dalle dimensioni dei set di dati e dalle relative statistiche disponibili.</span><span class="sxs-lookup"><span data-stu-id="acaa6-205">All of it will depend of the shape of your queries, the Azure SQL database characteristics, the nature and the size of your datasets, and the statistics available about them.</span></span> <span data-ttu-id="acaa6-206">Se l'istanza di database SQL di Azure è stata appena creata, Query Optimizer dovrà compilare le informazioni da zero anziché riutilizzare le statistiche relative alle esecuzioni precedenti della query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-206">If you just created your Azure SQL Database instance, the query optimizer will have to build its knowledge from scratch instead of reusing statistics made of the previous query runs.</span></span> <span data-ttu-id="acaa6-207">Le stime, quindi, dipendono molto dal contesto sono quasi specifiche dei singoli server e delle situazioni relative alle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="acaa6-207">So, the estimates are very contextual and almost specific to every server and application situation.</span></span> <span data-ttu-id="acaa6-208">Questo è un aspetto importante da tenere presente.</span><span class="sxs-lookup"><span data-stu-id="acaa6-208">It is an important aspect to keep in mind!</span></span>

## <a name="some-considerations-to-take-into-account"></a><span data-ttu-id="acaa6-209">Alcune considerazioni importanti</span><span class="sxs-lookup"><span data-stu-id="acaa6-209">Some considerations to take into account</span></span>
<span data-ttu-id="acaa6-210">Anche se la maggior parte dei carichi di lavoro può trarre vantaggio dal livello di compatibilità 130, prima di adottare questo livello di compatibilità per l'ambiente di produzione occorre valutare le tre opzioni disponibili:</span><span class="sxs-lookup"><span data-stu-id="acaa6-210">Although most workloads would benefit from the compatibility level 130, before you adopting the compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="acaa6-211">Passare al livello di compatibilità 130 e osservare i risultati.</span><span class="sxs-lookup"><span data-stu-id="acaa6-211">You move to compatibility level 130, and see how things perform.</span></span> <span data-ttu-id="acaa6-212">Se si nota un peggioramento, è sufficiente impostare di nuovo il livello di compatibilità sul valore originale. In alternativa, è possibile lasciare il livello impostato su 130 ma ripristinare la modalità legacy della stima di cardinalità, come descritto in precedenza. Quest'ultima operazione potrebbe già risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="acaa6-212">In case you notice some regressions, you just simply set the compatibility level back to its original level, or keep 130, and only reverse the Cardinality Estimation back to the legacy mode (As explained above, this alone could address the issue).</span></span>
2. <span data-ttu-id="acaa6-213">Eseguire test approfonditi sulle applicazioni esistenti con un carico di produzione simile, ottimizzare e convalidare le prestazioni prima di passare all'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="acaa6-213">You thoroughly test your existing applications under similar production load, fine tune, and validate the performance before going to production.</span></span> <span data-ttu-id="acaa6-214">In caso di problemi, come per l'opzione precedente è possibile tornare al livello di compatibilità originale o semplicemente ripristinare la modalità legacy della stima di cardinalità.</span><span class="sxs-lookup"><span data-stu-id="acaa6-214">In case of issues, same as above, you can always go back to the original compatibility level, or simply reverse the Cardinality Estimation back to the legacy mode.</span></span>
3. <span data-ttu-id="acaa6-215">Usare Archivio query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-215">As a final option, and the most recent way to address these questions, is to leverage the Query Store.</span></span> <span data-ttu-id="acaa6-216">Quest'ultima opzione rappresenta il modo più recente di risolvere il problema ed è anche l'opzione consigliata.</span><span class="sxs-lookup"><span data-stu-id="acaa6-216">That’s today’s recommended option!</span></span> <span data-ttu-id="acaa6-217">Per semplificare l'analisi delle query al di sotto del livello di compatibilità 120 rispetto al livello 130, la soluzione più efficace è sicuramente Archivio query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-217">To assist the analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough to use Query Store.</span></span> <span data-ttu-id="acaa6-218">Archivio query è disponibile con la versione più recente del database SQL di Azure V12 ed è progettato per la risoluzione dei problemi di prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-218">Query Store is available with the latest version of Azure SQL Database V12, and it’s designed to help you with query performance troubleshooting.</span></span> <span data-ttu-id="acaa6-219">Archivio query agisce nel database come una scatola nera, che registra dati e raccoglie e presenta informazioni cronologiche dettagliate su tutte le query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-219">Think of the Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="acaa6-220">Questo semplifica notevolmente le analisi sulle prestazioni riducendo il tempo necessario per diagnosticare e risolvere i problemi.</span><span class="sxs-lookup"><span data-stu-id="acaa6-220">This greatly simplifies performance forensics by reducing the time to diagnose and resolve issues.</span></span> <span data-ttu-id="acaa6-221">Per altre informazioni, vedere il post di blog relativo ad [Archivio query, la scatola nera del database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span><span class="sxs-lookup"><span data-stu-id="acaa6-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="acaa6-222">A livello generale, se è già disponibile un set di database in esecuzione al livello di compatibilità 120 o inferiore e si prevede di impostare alcuni di essi sul livello 130, o se il carico di lavoro effettua automaticamente il provisioning di nuovi database che verranno presto impostati su 130 come valore predefinito, prendere in considerazione quanto segue:</span><span class="sxs-lookup"><span data-stu-id="acaa6-222">At the high-level, if you already have a set of databases running at compatibility level 120 or below, and plan to move some of them to 130, or because your workload automatically provision new databases that will be soon be set by default to 130, please consider the followings:</span></span>

* <span data-ttu-id="acaa6-223">Prima di passare al nuovo livello di compatibilità nell'ambiente di produzione, abilitare Archivio query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-223">Before changing to the new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="acaa6-224">Per altre informazioni, vedere l'articolo relativo alla [modifica della modalità di compatibilità del database e uso di Archivio query](https://msdn.microsoft.com/library/bb895281.aspx) .</span><span class="sxs-lookup"><span data-stu-id="acaa6-224">You can refer to [Change the Database Compatibility Mode and Use the Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="acaa6-225">Successivamente, testare tutti i carichi di lavoro critici con query e dati rappresentativi di un ambiente di produzione e confrontare le prestazioni registrate e segnalate da Archivio query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare the performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="acaa6-226">Se si verifica un peggioramento è possibile usare Archivio query per identificare le query peggiorate e usare l'opzione di Archivio query per l'uso forzato del piano, anche detta associazione del piano.</span><span class="sxs-lookup"><span data-stu-id="acaa6-226">If you experience some regressions, you can identify the regressed queries with the Query Store and use the plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="acaa6-227">In tal caso, si può lasciare il livello di compatibilità impostato su 130 e usare il piano di query precedente come indicato da Archivio query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-227">In such a case, you definitively stay with the compatibility level 130, and use the former query plan as suggested by the Query Store.</span></span>
* <span data-ttu-id="acaa6-228">Se si vuole sfruttare le nuove funzionalità del database SQL di Azure, che esegue SQL Server 2016, ma si preferisce evitare le modifiche introdotte con il livello di compatibilità 130, come ultima soluzione è possibile forzare il ripristino del livello di compatibilità al livello appropriato per il carico di lavoro tramite un'istruzione ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="acaa6-228">If you want to leverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive to changes brought by the compatibility level 130, as a last resort, you could consider forcing the compatibility level back to the level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="acaa6-229">Tenere presente, però, che l'opzione di Archivio query per l'uso forzato del piano rimane comunque la soluzione migliore. Questo perché usare un livello di compatibilità diverso da 130 significa sostanzialmente rimanere al livello di funzionalità di una versione precedente di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="acaa6-229">But first, be aware that the Query Store plan pinning option is your best option because not using 130 is basically staying at the functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="acaa6-230">Se sono presenti applicazioni multi-tenant in più database, potrebbe essere necessario aggiornare la logica di provisioning dei database per garantire la coerenza del livello di compatibilità in tutti i database di cui è stato eseguito il provisioning più di recente o meno.</span><span class="sxs-lookup"><span data-stu-id="acaa6-230">If you have multitenant applications spanning multiple databases, it may be necessary to update the provisioning logic of your databases to ensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="acaa6-231">Le prestazioni del carico di lavoro dell'applicazione potrebbero risentire del fatto che alcuni database vengono eseguiti a livelli di compatibilità diversi. La coerenza del livello di compatibilità in tutti i database potrebbe quindi essere necessaria per fornire la stessa esperienza a tutti i clienti.</span><span class="sxs-lookup"><span data-stu-id="acaa6-231">Your application workload performance could be sensitive to the fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order to provide the same experience to your customers all across the board.</span></span> <span data-ttu-id="acaa6-232">Si noti che la coerenza non è obbligatoria. Dipende unicamente dall'effetto del livello di compatibilità sull'applicazione.</span><span class="sxs-lookup"><span data-stu-id="acaa6-232">Note that it is not a mandate, it really depends on how your application is affected by the compatibility level.</span></span>
* <span data-ttu-id="acaa6-233">Riguardo alla stima di cardinalità, come per la modifica del livello di compatibilità, prima di procedere nell'ambiente di produzione è consigliabile testare il carico di lavoro di produzione con le nuove condizioni, per determinare se l'applicazione trae vantaggio dai miglioramenti alla stima di cardinalità.</span><span class="sxs-lookup"><span data-stu-id="acaa6-233">Last, regarding the Cardinality Estimation, and just like changing the compatibility level, before proceeding in production, it is recommended to test your production workload under the new conditions to determine if your application benefits from the Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="acaa6-234">Conclusione</span><span class="sxs-lookup"><span data-stu-id="acaa6-234">Conclusion</span></span>
<span data-ttu-id="acaa6-235">L'uso del database SQL di Azure per sfruttare i vantaggi dei miglioramenti di SQL Server 2016 può migliorare notevolmente l'esecuzione delle query.</span><span class="sxs-lookup"><span data-stu-id="acaa6-235">Using Azure SQL Database to benefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="acaa6-236">È un dato di fatto.</span><span class="sxs-lookup"><span data-stu-id="acaa6-236">Just as-is!</span></span> <span data-ttu-id="acaa6-237">Naturalmente, come per qualsiasi nuova funzionalità è necessaria un'attenta valutazione per determinare le condizioni esatte in cui il carico di lavoro del database funziona al meglio.</span><span class="sxs-lookup"><span data-stu-id="acaa6-237">Of course, like any new feature, a proper evaluation must be done to determine the exact conditions under which your database workload operates the best.</span></span> <span data-ttu-id="acaa6-238">L'esperienza dimostra che, al livello di compatibilità 130, la maggior parte dei carichi di lavoro viene eseguita almeno in modo trasparente, sfruttando le nuove funzioni di elaborazione delle query e la nuova stima di cardinalità.</span><span class="sxs-lookup"><span data-stu-id="acaa6-238">Experience shows that most workload are expected to at least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="acaa6-239">Ciò detto, esistono sempre alcune eccezioni ed è importante eseguire le opportune verifiche per quantificare il vantaggio effettivo di tali miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="acaa6-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment to determine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="acaa6-240">Anche in questo caso Archivio query può rivelarsi una risorsa molto utile.</span><span class="sxs-lookup"><span data-stu-id="acaa6-240">And again, the Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="acaa6-241">Con l'evoluzione di SQL Azure, si arriverà probabilmente a un livello di compatibilità 140.</span><span class="sxs-lookup"><span data-stu-id="acaa6-241">As SQL Azure evolves, you can expect a compatibility level 140 in the future.</span></span> <span data-ttu-id="acaa6-242">Al momento opportuno verranno trattate anche le nuove caratteristiche del futuro livello di compatibilità 140, come si è fatto brevemente in questo articolo per il livello di compatibilità 130.</span><span class="sxs-lookup"><span data-stu-id="acaa6-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="acaa6-243">Per ora è importante sottolineare ancora una volta che, a partire da giugno 2016, il livello di compatibilità predefinito nel database SQL di Azure per i database di nuova creazione passerà da 120 a 130.</span><span class="sxs-lookup"><span data-stu-id="acaa6-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change the default compatibility level from 120 to 130 for newly created databases.</span></span> <span data-ttu-id="acaa6-244">Tenere presente questa informazione.</span><span class="sxs-lookup"><span data-stu-id="acaa6-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="acaa6-245">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="acaa6-245">References</span></span>
* [<span data-ttu-id="acaa6-246">Novità (Motore di database)</span><span class="sxs-lookup"><span data-stu-id="acaa6-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="acaa6-247">Post di blog: Archivio query, la scatola nera del database, di Borko Novakovic, 8 giugno 2016</span><span class="sxs-lookup"><span data-stu-id="acaa6-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="acaa6-248">Livello di compatibilità ALTER TABLE (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="acaa6-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="acaa6-249">ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="acaa6-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="acaa6-250">Livello di compatibilità 130 per il database SQL di Azure versione 12</span><span class="sxs-lookup"><span data-stu-id="acaa6-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="acaa6-251">Ottimizzazione dei piani di query con la funzionalità di stima di cardinalità di SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="acaa6-251">Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="acaa6-252">Descrizione degli indici columnstore</span><span class="sxs-lookup"><span data-stu-id="acaa6-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="acaa6-253">Post di blog: Miglioramento delle prestazioni delle query con il livello di compatibilità 130 nel database SQL di Azure, di Alain Lissoir, 6 maggio 2016</span><span class="sxs-lookup"><span data-stu-id="acaa6-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
