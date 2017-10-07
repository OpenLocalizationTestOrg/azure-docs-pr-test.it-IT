---
title: "il livello di compatibilità aaaDatabase 130 - Database SQL di Azure | Documenti Microsoft"
description: "In questo articolo, è esplorare hello vantaggi offerti dall'esecuzione di Database SQL di Azure a livello di compatibilità 130 e sfruttando i vantaggi di hello nuovo query Optimizer è hello e funzionalità del processore di query. Vengono inoltre affrontati hello possibili effetti collaterali sulle prestazioni delle query hello per le applicazioni SQL hello esistenti."
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
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="cef58-104">Miglioramento delle prestazioni delle query con il livello di compatibilità 130 nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="cef58-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="cef58-105">Database SQL di Azure è in esecuzione in modo trasparente centinaia di migliaia di database con molti livelli di compatibilità diversi, mantenendo e garantendo hello compatibilità toohello corrispondente versione di Microsoft SQL Server per tutti i clienti!</span><span class="sxs-lookup"><span data-stu-id="cef58-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing hello backward compatibility toohello corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="cef58-106">In questo articolo, è esplorare vantaggi hello in esecuzione il database SQL di Azure a livello di compatibilità 130 e sfruttare i vantaggi di hello nuovo query Optimizer è hello e funzionalità del processore di query.</span><span class="sxs-lookup"><span data-stu-id="cef58-106">In this article, we explore hello benefits of running your Azure SQL Databse at compatibility level 130, and leveraging hello benefits of hello new query optimizer and query processor features.</span></span> <span data-ttu-id="cef58-107">Vengono inoltre affrontati hello possibili effetti collaterali sulle prestazioni delle query hello per le applicazioni SQL hello esistenti.</span><span class="sxs-lookup"><span data-stu-id="cef58-107">We also address hello possible side-effects on hello query performance for hello existing SQL applications.</span></span>

<span data-ttu-id="cef58-108">Come promemoria della cronologia, l'allineamento di hello di livelli di compatibilità toodefault versioni SQL sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="cef58-108">As a reminder of history, hello alignment of SQL versions toodefault compatibility levels are as follows:</span></span>

* <span data-ttu-id="cef58-109">100: in SQL Server 2008 e database SQL di Azure versione 11.</span><span class="sxs-lookup"><span data-stu-id="cef58-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="cef58-110">110: in SQL Server 2012 e database SQL di Azure versione 11.</span><span class="sxs-lookup"><span data-stu-id="cef58-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="cef58-111">120: in SQL Server 2014 e database SQL di Azure versione 12.</span><span class="sxs-lookup"><span data-stu-id="cef58-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="cef58-112">130: in SQL Server 2016 e database SQL di Azure versione 12.</span><span class="sxs-lookup"><span data-stu-id="cef58-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cef58-113">A partire da **mid-giugno 2016**, nel Database di SQL Azure, il livello di compatibilità predefinito hello sarà 130 anziché 120 per **appena creato** database.</span><span class="sxs-lookup"><span data-stu-id="cef58-113">Starting in **mid-June 2016**, in Azure SQL Database, hello default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="cef58-114">I database creati prima della metà di giugno 2016 *non* saranno interessati dalla modifica e manterranno il livello di compatibilità corrente (100, 110 o 120).</span><span class="sxs-lookup"><span data-stu-id="cef58-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="cef58-115">I database migrati da Database SQL di Azure versione V11 tooV12 avranno un livello di compatibilità pari a 100 o 110.</span><span class="sxs-lookup"><span data-stu-id="cef58-115">Databases that migrated from Azure SQL Database version V11 tooV12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="cef58-116">Informazioni sul livello di compatibilità 130</span><span class="sxs-lookup"><span data-stu-id="cef58-116">About compatibility level 130</span></span>
<span data-ttu-id="cef58-117">Se si desidera tooknow hello livello di compatibilità corrente del database, eseguire innanzitutto hello seguente istruzione Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="cef58-117">First, if you want tooknow hello current compatibility level of your database, execute hello following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="cef58-118">Prima di questa modifica toolevel 130 accade per **appena** create database, si esaminare questa modifica novità su alcuni esempi di query molto semplice e vedere come tutti gli utenti possono trarre vantaggio da esso.</span><span class="sxs-lookup"><span data-stu-id="cef58-118">Before this change toolevel 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="cef58-119">L'elaborazione delle query nei database relazionali possono essere molto complessi e può causare toolots computer scienza e matematiche toounderstand hello inerente scelte di progettazione e i comportamenti.</span><span class="sxs-lookup"><span data-stu-id="cef58-119">Query processing in relational databases can be very complex and can lead toolots of computer science and mathematics toounderstand hello inherent design choices and behaviors.</span></span> <span data-ttu-id="cef58-120">In questo documento, contenuto hello è stato intenzionalmente semplificate tooensure che chiunque concetti tecnici minima può comprendere hello impatto della modifica del livello di compatibilità hello e determinare come è possibile trarre vantaggio di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="cef58-120">In this document, hello content has been intentionally simplified tooensure that anyone with some minimum technical background can understand hello impact of hello compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="cef58-121">Di seguito hanno una sintesi quale livello di compatibilità 130 hello visualizzata nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="cef58-121">Let’s have a quick look at what hello compatibility level 130 brings at hello table.</span></span>  <span data-ttu-id="cef58-122">Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx):</span><span class="sxs-lookup"><span data-stu-id="cef58-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="cef58-123">può essere multithreading Hello operazione di inserimento di un'istruzione Insert select o può avere un piano parallelo, mentre prima dell'operazione a thread singolo.</span><span class="sxs-lookup"><span data-stu-id="cef58-123">hello Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="cef58-124">Le tabelle con ottimizzazione per la memoria e le query sulle variabili di tabella ora possono avere piani paralleli. In precedenza l'operazione era a thread singolo.</span><span class="sxs-lookup"><span data-stu-id="cef58-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="cef58-125">Le statistiche per la tabella con ottimizzazione per la memoria ora possono essere campionate e vengono aggiornate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cef58-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="cef58-126">Per altre informazioni, vedere [Novità (Motore di database): OLTP in memoria](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) .</span><span class="sxs-lookup"><span data-stu-id="cef58-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="cef58-127">Modifiche alla modalità batch rispetto alla modalità riga con gli indici columnstore:</span><span class="sxs-lookup"><span data-stu-id="cef58-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="cef58-128">L'ordinamento in una tabella con un indice columnstore viene ora eseguito in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="cef58-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="cef58-129">Le aggregazioni finestra ora vengono eseguite in modalità batch, ad esempio con istruzioni TSQL LAG/LEAD.</span><span class="sxs-lookup"><span data-stu-id="cef58-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="cef58-130">Le query sulle tabelle columnstore con più clausole distinte operano in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="cef58-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="cef58-131">Anche le query in esecuzione con DOP=1 o con un piano seriale vengono eseguite in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="cef58-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="cef58-132">Miglioramenti di stima della cardinalità provengano effettivamente con livello di compatibilità 120, ma se si esegue in un livello di compatibilità inferiore (ad esempio 100 o 110), hello spostamento toocompatibility livello 130 anche porterà questi miglioramenti e questi possono anche per ultimo, sfruttare le prestazioni di query hello delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="cef58-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), hello move toocompatibility level 130 will also bring these improvements, and these can also benefit hello query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="cef58-133">Esercitazione sul livello di compatibilità 130</span><span class="sxs-lookup"><span data-stu-id="cef58-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="cef58-134">Primo entriamo alcune tabelle, indici e dati casuali creati toopractice alcune di queste nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cef58-134">First let’s get some tables, indexes and random data created toopractice some of these new capabilities.</span></span> <span data-ttu-id="cef58-135">esempi di script TSQL Hello possono essere eseguiti in SQL Server 2016 o in Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="cef58-135">hello TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="cef58-136">Tuttavia, quando si crea un database SQL di Azure, assicurarsi scegliere un minimo di hello P2 database perché è necessario almeno un paio di core tooallow multithreading e quindi sfruttare queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cef58-136">However, when creating an Azure SQL database, make sure you choose at hello minimum a P2 database because you need at least a couple of cores tooallow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

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


<span data-ttu-id="cef58-137">A questo punto, si dispone di un toosome aspetto delle funzionalità di elaborazione delle Query hello in arrivo con livello di compatibilità 130.</span><span class="sxs-lookup"><span data-stu-id="cef58-137">Now, let’s have a look toosome of hello Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="cef58-138">INSERT in parallelo</span><span class="sxs-lookup"><span data-stu-id="cef58-138">Parallel INSERT</span></span>
<span data-ttu-id="cef58-139">L'esecuzione di istruzioni TSQL hello seguente esegue hello dell'operazione di inserimento nel livello di compatibilità 120 e 130, che consente di eseguire rispettivamente hello operazione di inserimento in un modello a thread singolo (120) e in un modello a thread multipli (130).</span><span class="sxs-lookup"><span data-stu-id="cef58-139">Executing hello TSQL statements below executes hello INSERT operation under compatibility level 120 and 130, which respectively executes hello INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="cef58-140">Richiedendo piano di query effettivo hello hello, esaminando la rappresentazione grafica o il relativo contenuto XML, è possibile determinare quale funzione è organo la stima della cardinalità.</span><span class="sxs-lookup"><span data-stu-id="cef58-140">By requesting hello actual hello query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="cef58-141">Esaminando i piani hello side-by-side in figura 1, si vede chiaramente che hello colonna Store inserire esecuzione passa dalla seriale in 120 tooparallel 130.</span><span class="sxs-lookup"><span data-stu-id="cef58-141">Looking at hello plans side-by-side on figure 1, we can clearly see that hello Column Store INSERT execution goes from serial in 120 tooparallel in 130.</span></span> <span data-ttu-id="cef58-142">Inoltre, poiché tale modifica hello dell'icona di hello iteratore nel piano di 130 hello con due frecce parallele, viene effettivamente parallela relativa fatto hello che ora hello esecuzione iteratore.</span><span class="sxs-lookup"><span data-stu-id="cef58-142">Also, note that hello change of hello iterator icon in hello 130 plan showing two parallel arrows, illustrating hello fact that now hello iterator execution is indeed parallel.</span></span> <span data-ttu-id="cef58-143">Se si dispone di grandi dimensioni toocomplete di operazioni di inserimento, l'esecuzione parallela hello, collegato toohello numero di core, che hai a disposizione per il database di hello, offre prestazioni migliori; backup tooa 100 volte più veloce in base alla situazione specifica.</span><span class="sxs-lookup"><span data-stu-id="cef58-143">If you have large INSERT operations toocomplete, hello parallel execution, linked toohello number of core you have at your disposal for hello database, will perform better; up tooa 100 times faster depending your situation!</span></span>

<span data-ttu-id="cef58-144">*Figura 1: Inserire modifiche apportate all'operazione seriale tooparallel con livello di compatibilità 130.*</span><span class="sxs-lookup"><span data-stu-id="cef58-144">*Figure 1: INSERT operation changes from serial tooparallel with compatibility level 130.*</span></span>

![Figura 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="cef58-146">Modalità batch seriale</span><span class="sxs-lookup"><span data-stu-id="cef58-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="cef58-147">Analogamente, lo spostamento di livello toocompatibility 130 durante l'elaborazione delle righe di dati consente l'elaborazione in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="cef58-147">Similarly, moving toocompatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="cef58-148">In primo luogo, le operazioni in modalità batch sono disponibili solo in presenza di un indice columnstore.</span><span class="sxs-lookup"><span data-stu-id="cef58-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="cef58-149">In secondo luogo, un batch in genere rappresenta ~ 900 righe e utilizza una logica di codice ottimizzata per la CPU multicore, velocità effettiva più elevata di memoria e direttamente sfrutta hello dati compressi di hello archivio colonne se possibile.</span><span class="sxs-lookup"><span data-stu-id="cef58-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages hello compressed data of hello Column Store whenever possible.</span></span> <span data-ttu-id="cef58-150">In queste condizioni, SQL Server 2016 può elaborare ~ 900 righe in una sola volta, anziché la 1 riga in fase di hello e di conseguenza, hello costo complessivo generale dell'operazione hello ora condiviso da hello dell'intero batch, riducendo costi riga hello complessiva.</span><span class="sxs-lookup"><span data-stu-id="cef58-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at hello time, and as a consequence, hello overall overhead cost of hello operation is now shared by hello entire batch, reducing hello overall cost by row.</span></span> <span data-ttu-id="cef58-151">La quantità di operazioni combinate con compressione dell'archivio colonne hello fondamentalmente condivisa riduce la latenza di hello coinvolto in un'operazione in modalità batch selezionare.</span><span class="sxs-lookup"><span data-stu-id="cef58-151">This shared amount of operations combined with hello column store compression basically reduces hello latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="cef58-152">È possibile trovare ulteriori informazioni sull'archivio colonna hello e modalità al batch [Guida agli indici Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="cef58-152">You can find more details about hello column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="cef58-153">Come viene visualizzata di sotto, osservando hello query piani side-by-side nella figura 2, possiamo vedere che la modalità di elaborazione hello è stato modificato con il livello di compatibilità di hello e di conseguenza, quando si eseguono query hello in sia a livello di compatibilità del tutto, possiamo vedere che la maggior parte del tempo di elaborazione hello viene impiegato per riga (% 86) confrontati toohello batch una modalità (% 14), in cui sono stati elaborati 2 batch.</span><span class="sxs-lookup"><span data-stu-id="cef58-153">As visible below, by observing hello query plans side-by-side on figure 2, we can see that hello processing mode has changed with hello compatibility level, and as a consequence, when executing hello queries in both compatibility level altogether, we can see that most of hello processing time is spent in row mode (86%) compared toohello batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="cef58-154">Aumentare i set di dati hello, hello vantaggio aumenterà.</span><span class="sxs-lookup"><span data-stu-id="cef58-154">Increase hello dataset, hello benefit will increase.</span></span>

<span data-ttu-id="cef58-155">*Figura 2: Selezionare le modifiche di operazione dalla modalità seriale toobatch con livello di compatibilità 130.*</span><span class="sxs-lookup"><span data-stu-id="cef58-155">*Figure 2: SELECT operation changes from serial toobatch mode with compatibility level 130.*</span></span>

![Figura 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="cef58-157">Modalità batch per l'esecuzione dell'ordinamento</span><span class="sxs-lookup"><span data-stu-id="cef58-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="cef58-158">Transizione di hello simile toohello precedente, ma l'operazione di ordinamento applicati tooa, dalla riga (livello di compatibilità 120) toobatch modalità (livello di compatibilità 130) consente di migliorare le prestazioni hello dell'operazione di ordinamento per hello hello gli stessi motivi.</span><span class="sxs-lookup"><span data-stu-id="cef58-158">Similar toohello above, but applied tooa sort operation, hello transition from row mode (compatibility level 120) toobatch mode (compatibility level 130) improves hello performance of hello SORT operation for hello same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="cef58-159">Visibile side-by-side nella figura 3, possiamo vedere che l'operazione di ordinamento hello in modalità riga rappresenta 81% di hello costo, mentre la modalità batch hello rappresenta solo % 19 del costo di hello (rispettivamente 81% e % 56 Ordina hello stesso).</span><span class="sxs-lookup"><span data-stu-id="cef58-159">Visible side-by-side on figure 3, we can see that hello sort operation in row mode represents 81% of hello cost, while hello batch mode only represents 19% of hello cost (respectively 81% and 56% on hello sort itself).</span></span>

<span data-ttu-id="cef58-160">*Figura 3: Operazione di ordinamento viene modificata dalla modalità a riga toobatch con livello di compatibilità 130.*</span><span class="sxs-lookup"><span data-stu-id="cef58-160">*Figure 3: SORT operation changes from row toobatch mode with compatibility level 130.*</span></span>

![Figura 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="cef58-162">Ovviamente, questi esempi solo contengono decine di migliaia di righe, ovvero nulla quando si esaminano i dati di hello disponibili nella maggior parte dei server SQL questi giorni.</span><span class="sxs-lookup"><span data-stu-id="cef58-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at hello data available in most SQL Servers these days.</span></span> <span data-ttu-id="cef58-163">Solo questi su milioni di righe invece progetto, e questo può essere convertita in corso di esecuzione per ogni giorno in sospeso di natura hello del carico di lavoro di altri.</span><span class="sxs-lookup"><span data-stu-id="cef58-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending hello nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="cef58-164">Miglioramenti apportati alla stima di cardinalità (CE)</span><span class="sxs-lookup"><span data-stu-id="cef58-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="cef58-165">Introdotti con SQL Server 2014, qualsiasi database in esecuzione in un livello di compatibilità 120 sopra renderà hello nuove funzionalità di stima della cardinalità.</span><span class="sxs-lookup"><span data-stu-id="cef58-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="cef58-166">In pratica, la stima della cardinalità è logica hello utilizzato toodetermine come SQL server eseguirà una query in base al suo costo stimato.</span><span class="sxs-lookup"><span data-stu-id="cef58-166">Essentially, cardinality estimation is hello logic used toodetermine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="cef58-167">stima Hello viene calcolata utilizzando input da statistiche associate agli oggetti coinvolti nella query.</span><span class="sxs-lookup"><span data-stu-id="cef58-167">hello estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="cef58-168">In pratica, a livello generale, le funzioni di stima della cardinalità riga conteggio stime insieme alle informazioni sulla distribuzione dei valori hello, Conteggio valori distinct, hello e conteggi duplicati contenuti in hello tabelle e gli oggetti a cui fa riferimento nella query hello.</span><span class="sxs-lookup"><span data-stu-id="cef58-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about hello distribution of hello values, distinct value counts, and duplicate counts contained in hello tables and objects referenced in hello query.</span></span> <span data-ttu-id="cef58-169">Commette queste stime, può causare i/o disco toounnecessary scadenza tooinsufficient concessioni di memoria (ad esempio TempDB spill) o tooa selezione di un'esecuzione del piano seriale in una parallela alcuni esecuzione, tooname del piano.</span><span class="sxs-lookup"><span data-stu-id="cef58-169">Getting these estimates wrong, can lead toounnecessary disk I/O due tooinsufficient memory grants (i.e. TempDB spills), or tooa selection of a serial plan execution over a parallel plan execution, tooname a few.</span></span> <span data-ttu-id="cef58-170">Conclusione, le stime non corrette possono causare tooan un calo delle prestazioni complessive hello di esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="cef58-170">Conclusion, incorrect estimates can lead tooan overall performance degradation of hello query execution.</span></span> <span data-ttu-id="cef58-171">In hello altri lato, stime migliori, eseguire stime più accurate, le esecuzioni di query toobetter lead!</span><span class="sxs-lookup"><span data-stu-id="cef58-171">On hello other side, better estimates, more accurate estimates, leads toobetter query executions!</span></span>

<span data-ttu-id="cef58-172">Come accennato in precedenza, le ottimizzazioni query e le stime sono pochi complessi, ma se si desidera toolearn informazioni sui piani di query e stima della cardinalità, è possibile fare riferimento documento toohello [l'ottimizzazione di piani di Query con hello SQL Server 2014 Strumento di stima della cardinalità](https://msdn.microsoft.com/library/dn673537.aspx) per un approfondimento.</span><span class="sxs-lookup"><span data-stu-id="cef58-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want toolearn more about query plans and cardinality estimator, you can refer toohello document at [Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="cef58-173">Stima di cardinalità corrente</span><span class="sxs-lookup"><span data-stu-id="cef58-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="cef58-174">toodetermine in cui la stima della cardinalità delle query sono in esecuzione, si solo query di utilizzare hello esempi di seguito.</span><span class="sxs-lookup"><span data-stu-id="cef58-174">toodetermine under which Cardinality Estimation your queries are running, let’s just use hello query samples below.</span></span> <span data-ttu-id="cef58-175">Si noti che questo primo esempio verrà eseguiti a livello di compatibilità 110, pertanto l'utilizzo di hello delle funzioni di stima della cardinalità precedente hello.</span><span class="sxs-lookup"><span data-stu-id="cef58-175">Note that this first example will run under compatibility level 110, implying hello use of hello old Cardinality Estimation functions.</span></span>

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


<span data-ttu-id="cef58-176">Al termine dell'esecuzione, fare clic sul collegamento di hello XML ed esaminare le proprietà di hello del primo iteratore hello come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="cef58-176">Once execution is complete, click on hello XML link, and look at hello properties of hello first iterator as shown below.</span></span> <span data-ttu-id="cef58-177">Annotare il nome di proprietà hello chiamato CardinalityEstimationModelVersion attualmente impostato su 70.</span><span class="sxs-lookup"><span data-stu-id="cef58-177">Note hello property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="cef58-178">Questo non significa che il livello di compatibilità database hello è impostato toohello versione di SQL Server 7.0 (è impostato su 110 come visibile nelle istruzioni TSQL hello precedente), ma il valore di hello 70 rappresenta semplicemente hello legacy stima della cardinalità funzionalità disponibili a partire da SQL Server 7.0, con cui non erano revisioni principali fino a SQL Server 2014 (che viene fornito con un livello di compatibilità pari a 120).</span><span class="sxs-lookup"><span data-stu-id="cef58-178">It does not mean that hello database compatibility level is set toohello SQL Server 7.0 version (it is set on 110 as visible in hello TSQL statements above), but hello value 70 simply represents hello legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="cef58-179">*Figura 4: hello CardinalityEstimationModelVersion è impostato too70 quando si utilizza un livello di compatibilità 110 o inferiore.*</span><span class="sxs-lookup"><span data-stu-id="cef58-179">*Figure 4: hello CardinalityEstimationModelVersion is set too70 when using a compatibility level of 110 or below.*</span></span>

![Figura 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="cef58-181">In alternativa, è possibile modificare too130 livello di compatibilità hello e disabilitare l'uso di hello della nuova funzione di stima della cardinalità hello utilizzando hello LEGACY_CARDINALITY_ESTIMATION impostare tooON con [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="cef58-181">Alternatively, you can change hello compatibility level too130, and disable hello use of hello new Cardinality Estimation function by using hello LEGACY_CARDINALITY_ESTIMATION set tooON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="cef58-182">Questo verrà essere esattamente hello come utilizzando 110 da un punto di vista della funzione di stima della cardinalità, utilizzando il livello di compatibilità di elaborazione delle query più recente hello.</span><span class="sxs-lookup"><span data-stu-id="cef58-182">This will be exactly hello same as using 110 from a Cardinality Estimation function point of view, while using hello latest query processing compatibility level.</span></span> <span data-ttu-id="cef58-183">In questo modo, è possibile trarre vantaggio dalla nuova query hello l'elaborazione delle funzionalità con livello di compatibilità più recente di hello (vale a dire la modalità batch), ma comunque si basano sulla funzionalità di stima della cardinalità precedente hello, se necessario.</span><span class="sxs-lookup"><span data-stu-id="cef58-183">Doing so, you can benefit from hello new query processing features coming with hello latest compatibility level (i.e. batch mode), but still rely on hello old Cardinality Estimation functionality if necessary.</span></span>

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


<span data-ttu-id="cef58-184">Il semplice spostamento toohello livello di compatibilità 120 o 130 abilita la funzionalità di hello nuova stima della cardinalità.</span><span class="sxs-lookup"><span data-stu-id="cef58-184">Simply moving toohello compatibility level 120 or 130 enables hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="cef58-185">In tal caso, predefinito hello CardinalityEstimationModelVersion verrà impostato di conseguenza too120 o 130 come viene visualizzata di seguito.</span><span class="sxs-lookup"><span data-stu-id="cef58-185">In such a case, hello default CardinalityEstimationModelVersion will be set accordingly too120 or 130 as visible below.</span></span>

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


<span data-ttu-id="cef58-186">*Figura 5: hello CardinalityEstimationModelVersion è impostato too130 quando si utilizza un livello di compatibilità di 130.*</span><span class="sxs-lookup"><span data-stu-id="cef58-186">*Figure 5: hello CardinalityEstimationModelVersion is set too130 when using a compatibility level of 130.*</span></span>

![Figura 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a><span data-ttu-id="cef58-188">Differenze di stima della cardinalità hello che</span><span class="sxs-lookup"><span data-stu-id="cef58-188">Witnessing hello Cardinality Estimation differences</span></span>
<span data-ttu-id="cef58-189">A questo punto, eseguire leggermente più complesso di query che includono un INNER JOIN con una clausola WHERE con alcuni predicati e diamo un'occhiata hello stima del conteggio delle righe da una funzione di stima della cardinalità precedente hello prima.</span><span class="sxs-lookup"><span data-stu-id="cef58-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at hello row count estimate from hello old Cardinality Estimation function first.</span></span>

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


<span data-ttu-id="cef58-190">In modo efficace per eseguire questa query restituisce 200,704 righe, mentre hello riga stima con funzionalità di stima della cardinalità precedente hello attestazioni 194,284 righe.</span><span class="sxs-lookup"><span data-stu-id="cef58-190">Executing this query effectively returns 200,704 rows, while hello row estimate with hello old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="cef58-191">Ovviamente, come accennato prima, questi risultati conteggio righe variano la frequenza con cui è stato eseguito hello degli esempi precedenti, che consente di popolare le tabelle di esempio hello in ogni esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cef58-191">Obviously, as said before, these row count results will also depend how often you ran hello previous samples, which populates hello sample tables over and over again at each run.</span></span> <span data-ttu-id="cef58-192">Ovviamente, predicati di hello nella query avrà inoltre influire sulla stima effettivo di hello oltre a forma di tabella hello, il contenuto dei dati e come questi dati sono effettivamente correlati tra loro.</span><span class="sxs-lookup"><span data-stu-id="cef58-192">Obviously, hello predicates in your query will also have an influence on hello actual estimation aside from hello table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="cef58-193">*Figura 6: stima del conteggio delle righe hello è 194,284 o 6.000 righe disattivata dalle righe di hello 200,704 previsto.*</span><span class="sxs-lookup"><span data-stu-id="cef58-193">*Figure 6: hello row count estimate is 194,284 or 6,000 rows off from hello 200,704 rows expected.*</span></span>

![Figura 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="cef58-195">In hello allo stesso modo, verrà ora eseguire hello stessa query con nuove funzionalità di stima della cardinalità hello.</span><span class="sxs-lookup"><span data-stu-id="cef58-195">In hello same way, let’s now execute hello same query with hello new Cardinality Estimation functionality.</span></span>

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


<span data-ttu-id="cef58-196">Analizzando hello riportato di seguito, è ora visualizzare che tale stima riga hello è 202,877, o molto inferiore e superiore a quello hello la stima della cardinalità precedente.</span><span class="sxs-lookup"><span data-stu-id="cef58-196">Looking at hello below, we now see that hello row estimate is 202,877, or much closer and higher than hello old Cardinality Estimation.</span></span>

<span data-ttu-id="cef58-197">*Figura 7: stima del conteggio delle righe hello è 202,877, anziché 194,284.*</span><span class="sxs-lookup"><span data-stu-id="cef58-197">*Figure 7: hello row count estimate is now 202,877, instead of 194,284.*</span></span>

![Figura 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="cef58-199">In realtà, il set di risultati di hello è 200,704 righe (tutti i relativi a seconda dei casi la frequenza con cui è stato eseguito nelle query hello hello degli esempi precedenti, ma ancora più importante, poiché hello TSQL utilizza l'istruzione di hello rand (), i valori effettivi hello restituiti possono variare da toohello esecuzione uno accanto).</span><span class="sxs-lookup"><span data-stu-id="cef58-199">In reality, hello result set is 200,704 rows (but all of it depends how often you did run hello queries of hello previous samples, but more importantly, because hello TSQL uses hello RAND() statement, hello actual values returned can vary from one run toohello next).</span></span> <span data-ttu-id="cef58-200">Pertanto, in questo particolare esempio hello nuova stima della cardinalità consente valutare il numero di hello di righe perché 202,877 è molto più simile too200, 704, rispetto a 194,284!</span><span class="sxs-lookup"><span data-stu-id="cef58-200">Therefore, in this particular example, hello new Cardinality Estimation does a better job at estimating hello number of rows because 202,877 is much closer too200,704, than 194,284!</span></span> <span data-ttu-id="cef58-201">Infine, se si modifica una clausola WHERE predicati tooequality hello (invece di ">" per l'istanza), questo esegua stime hello tra hello vecchia e nuova funzione di cardinalità più diversi, a seconda di come numero massimo di corrispondenze è possibile ottenere.</span><span class="sxs-lookup"><span data-stu-id="cef58-201">Last, if you change hello WHERE clause predicates tooequality (rather than “>” for instance), this could make hello estimates between hello old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="cef58-202">In questo caso, naturalmente, una differenza di circa 6000 righe rispetto al conteggio effettivo non rappresenta una grande quantità di dati, in alcune situazioni.</span><span class="sxs-lookup"><span data-stu-id="cef58-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="cef58-203">A questo punto, trasporre questo toomillions di righe tra più tabelle e query più complesse e a volte hello stima possa essere spostate di milioni di righe e pertanto hello rischio di prelievo-up hello errato piano di esecuzione, o la richiesta di memoria insufficiente concede iniziali tooTempDB spill e pertanto più i/o, sono molto più elevate.</span><span class="sxs-lookup"><span data-stu-id="cef58-203">Now, transpose this toomillions of rows across several tables and more complex queries, and at times hello estimate can be off by millions of rows , and therefore, hello risk of picking-up hello wrong execution plan, or requesting insufficient memory grants leading tooTempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="cef58-204">Se si hanno l'opportunità di hello, esercitarsi a confronto con le query più comuni e di un set di dati e visualizzare autonomamente di quanto alcune delle stime di hello nuovi e precedenti sono interessate, mentre alcuni potrebbe diventare semplicemente più esterno dalla realtà hello o alcuni altri solo semplicemente più vicino toohello effettivo delle righe conta effettivamente restituiti in set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="cef58-204">If you have hello opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of hello old and new estimates are affected, while some could just become more off from hello reality, or some others just simply closer toohello actual row counts actually returned in hello result sets.</span></span> <span data-ttu-id="cef58-205">Tutti i relativi a seconda della forma hello di query, le caratteristiche del database SQL di Azure hello, natura hello e dimensioni hello del set di dati e le statistiche di hello disponibili su di essi.</span><span class="sxs-lookup"><span data-stu-id="cef58-205">All of it will depend of hello shape of your queries, hello Azure SQL database characteristics, hello nature and hello size of your datasets, and hello statistics available about them.</span></span> <span data-ttu-id="cef58-206">Se è stata creata l'istanza di Database SQL di Azure, la query hello optimizer disporrà toobuild viene eseguita la conoscenza da zero anziché riutilizzo delle statistiche di query precedente hello.</span><span class="sxs-lookup"><span data-stu-id="cef58-206">If you just created your Azure SQL Database instance, hello query optimizer will have toobuild its knowledge from scratch instead of reusing statistics made of hello previous query runs.</span></span> <span data-ttu-id="cef58-207">In tal caso, le stime hello sono molto contestuali e quasi specifico tooevery situazione di server e dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cef58-207">So, hello estimates are very contextual and almost specific tooevery server and application situation.</span></span> <span data-ttu-id="cef58-208">È un aspetto importante di tookeep presente.</span><span class="sxs-lookup"><span data-stu-id="cef58-208">It is an important aspect tookeep in mind!</span></span>

## <a name="some-considerations-tootake-into-account"></a><span data-ttu-id="cef58-209">Tootake alcune considerazioni in considerazione</span><span class="sxs-lookup"><span data-stu-id="cef58-209">Some considerations tootake into account</span></span>
<span data-ttu-id="cef58-210">Sebbene la maggior parte dei carichi di lavoro può costituire un vantaggio a livello di compatibilità di hello 130, prima di adottare il livello di compatibilità hello per l'ambiente di produzione, fondamentalmente sono disponibili 3 opzioni:</span><span class="sxs-lookup"><span data-stu-id="cef58-210">Although most workloads would benefit from hello compatibility level 130, before you adopting hello compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="cef58-211">Si sposta il livello di toocompatibility 130 e vedere modalità di esecuzione delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="cef58-211">You move toocompatibility level 130, and see how things perform.</span></span> <span data-ttu-id="cef58-212">Nel caso in cui si nota che alcuni regressioni, è appena sufficiente impostare tooits indietro di hello compatibilità livello livello originale, o mantenere 130 e annullare solo la modalità legacy di hello stima della cardinalità toohello indietro (come descritto in precedenza, questo singolarmente potrebbe risolvere il problema di hello).</span><span class="sxs-lookup"><span data-stu-id="cef58-212">In case you notice some regressions, you just simply set hello compatibility level back tooits original level, or keep 130, and only reverse hello Cardinality Estimation back toohello legacy mode (As explained above, this alone could address hello issue).</span></span>
2. <span data-ttu-id="cef58-213">Testare le applicazioni esistenti in carico di produzione simile, ottimizzare e convalidare le prestazioni di hello prima di passare tooproduction.</span><span class="sxs-lookup"><span data-stu-id="cef58-213">You thoroughly test your existing applications under similar production load, fine tune, and validate hello performance before going tooproduction.</span></span> <span data-ttu-id="cef58-214">In caso di problemi, stesso come sopra, è possibile sempre tornare indietro a livello di compatibilità originale toohello o sufficiente invertire la modalità legacy di hello stima della cardinalità toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="cef58-214">In case of issues, same as above, you can always go back toohello original compatibility level, or simply reverse hello Cardinality Estimation back toohello legacy mode.</span></span>
3. <span data-ttu-id="cef58-215">Come opzione finale e hello funzionalità archivio Query hello tooleverage queste domande, è più recente tooaddress modo.</span><span class="sxs-lookup"><span data-stu-id="cef58-215">As a final option, and hello most recent way tooaddress these questions, is tooleverage hello Query Store.</span></span> <span data-ttu-id="cef58-216">Quest'ultima opzione rappresenta il modo più recente di risolvere il problema ed è anche l'opzione consigliata.</span><span class="sxs-lookup"><span data-stu-id="cef58-216">That’s today’s recommended option!</span></span> <span data-ttu-id="cef58-217">analisi di hello tooassist delle query in compatibilità livello 120 o inferiore rispetto a 130, non consiglia sufficiente toouse archivio Query.</span><span class="sxs-lookup"><span data-stu-id="cef58-217">tooassist hello analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough toouse Query Store.</span></span> <span data-ttu-id="cef58-218">Archivio query è disponibile con la versione più recente di hello del Database SQL di Azure V12, ed è concepita toohelp è la risoluzione dei problemi di prestazioni di query.</span><span class="sxs-lookup"><span data-stu-id="cef58-218">Query Store is available with hello latest version of Azure SQL Database V12, and it’s designed toohelp you with query performance troubleshooting.</span></span> <span data-ttu-id="cef58-219">Hello archivio Query può essere paragonato a un'utilità di traccia eventi per il database di raccogliere e presentare informazioni cronologiche su tutte le query.</span><span class="sxs-lookup"><span data-stu-id="cef58-219">Think of hello Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="cef58-220">Questo semplifica l'analisi forense prestazioni riducendo hello ora toodiagnose notevolmente più semplice e risolve i problemi.</span><span class="sxs-lookup"><span data-stu-id="cef58-220">This greatly simplifies performance forensics by reducing hello time toodiagnose and resolve issues.</span></span> <span data-ttu-id="cef58-221">Per altre informazioni, vedere il post di blog relativo ad [Archivio query, la scatola nera del database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span><span class="sxs-lookup"><span data-stu-id="cef58-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="cef58-222">In generale, se già associato un set di database in esecuzione a livello di compatibilità 120 o di sotto e pianificare la toomove hello alcuni di essi too130, o perché il carico di lavoro automaticamente il provisioning di nuovi database che verrà presto impostazione too130 predefinito, provare a segue Hello:</span><span class="sxs-lookup"><span data-stu-id="cef58-222">At hello high-level, if you already have a set of databases running at compatibility level 120 or below, and plan toomove some of them too130, or because your workload automatically provision new databases that will be soon be set by default too130, please consider hello followings:</span></span>

* <span data-ttu-id="cef58-223">Prima di modificare toohello nuovo livello di compatibilità nell'ambiente di produzione, abilitare l'archivio Query.</span><span class="sxs-lookup"><span data-stu-id="cef58-223">Before changing toohello new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="cef58-224">È possibile fare riferimento troppo[modificare hello archivio Query hello modalità di compatibilità del Database e utilizzare](https://msdn.microsoft.com/library/bb895281.aspx) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="cef58-224">You can refer too[Change hello Database Compatibility Mode and Use hello Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="cef58-225">Testare quindi i carichi di lavoro sono di importanza critica con dati rappresentativi e query di un ambiente di produzione e confrontare così le prestazioni hello si è verificato e come indicato dall'archivio Query.</span><span class="sxs-lookup"><span data-stu-id="cef58-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare hello performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="cef58-226">Se si verificano alcuni regressioni, è possibile identificare hello query regredite con archivio Query hello e utilizzare l'opzione dall'archivio Query di forzatura del piano hello (noto anche come prevede il blocco).</span><span class="sxs-lookup"><span data-stu-id="cef58-226">If you experience some regressions, you can identify hello regressed queries with hello Query Store and use hello plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="cef58-227">In tal caso, si definitivamente rimanere con livello di compatibilità hello 130 e utilizza il piano di query precedente hello come suggerito dal hello archivio Query.</span><span class="sxs-lookup"><span data-stu-id="cef58-227">In such a case, you definitively stay with hello compatibility level 130, and use hello former query plan as suggested by hello Query Store.</span></span>
* <span data-ttu-id="cef58-228">Se si desidera tooleverage nuove caratteristiche e funzionalità di Database SQL di Azure (che è in esecuzione SQL Server 2016), ma che sono sensibili toochanges dovuta a livello di compatibilità di hello 130, come ultima risorsa, è possibile forzare il nuovo livello di compatibilità di hello livello toohello che soddisfi il carico di lavoro utilizzando un'istruzione ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="cef58-228">If you want tooleverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive toochanges brought by hello compatibility level 130, as a last resort, you could consider forcing hello compatibility level back toohello level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="cef58-229">Ma prima di tutto, tale piano di archivio Query hello aggiunta l'opzione è la migliore opzione perché non si utilizza 130 è fondamentalmente sempre al livello di funzionalità hello di una versione precedente di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cef58-229">But first, be aware that hello Query Store plan pinning option is your best option because not using 130 is basically staying at hello functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="cef58-230">Se si dispone di applicazioni multi-tenant che si estende su più database, potrebbe essere necessario tooupdate hello provisioning logica del tooensure database un livello di compatibilità coerente in tutti i database; quelle precedenti e appena sottoposti a provisioning.</span><span class="sxs-lookup"><span data-stu-id="cef58-230">If you have multitenant applications spanning multiple databases, it may be necessary tooupdate hello provisioning logic of your databases tooensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="cef58-231">Le prestazioni del carico di lavoro dell'applicazione potrebbe essere fatto toohello sensibili che alcuni database sono in esecuzione con livelli di compatibilità diversi e pertanto la coerenza a livello di compatibilità in qualsiasi database potrebbe essere necessarie in ordine tooprovide hello stesso esperienza clienti tooyour tutti tra Lavagna hello.</span><span class="sxs-lookup"><span data-stu-id="cef58-231">Your application workload performance could be sensitive toohello fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order tooprovide hello same experience tooyour customers all across hello board.</span></span> <span data-ttu-id="cef58-232">Si noti che non è un Imponi la risposta dipende influenza l'applicazione dal livello di compatibilità hello.</span><span class="sxs-lookup"><span data-stu-id="cef58-232">Note that it is not a mandate, it really depends on how your application is affected by hello compatibility level.</span></span>
* <span data-ttu-id="cef58-233">Infine, hello stima della cardinalità, nonché come modifica livello di compatibilità hello, prima di procedere nell'ambiente di produzione, è consigliabile tootest il carico di lavoro di produzione in hello nuove condizioni toodetermine se l'applicazione trae vantaggio da miglioramenti di stima della cardinalità Hello.</span><span class="sxs-lookup"><span data-stu-id="cef58-233">Last, regarding hello Cardinality Estimation, and just like changing hello compatibility level, before proceeding in production, it is recommended tootest your production workload under hello new conditions toodetermine if your application benefits from hello Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="cef58-234">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="cef58-234">Conclusion</span></span>
<span data-ttu-id="cef58-235">L'utilizzo di Database SQL di Azure toobenefit da tutti i miglioramenti di SQL Server 2016 può migliorare chiaramente le esecuzioni delle query.</span><span class="sxs-lookup"><span data-stu-id="cef58-235">Using Azure SQL Database toobenefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="cef58-236">È un dato di fatto.</span><span class="sxs-lookup"><span data-stu-id="cef58-236">Just as-is!</span></span> <span data-ttu-id="cef58-237">Come qualsiasi nuova funzionalità, naturalmente, una corretta valutazione deve essere effettuata toodetermine hello esattamente le condizioni in cui il carico di lavoro del database funziona meglio hello.</span><span class="sxs-lookup"><span data-stu-id="cef58-237">Of course, like any new feature, a proper evaluation must be done toodetermine hello exact conditions under which your database workload operates hello best.</span></span> <span data-ttu-id="cef58-238">Esperienza mostra che la maggior parte delle carico di lavoro sono tooat previsto almeno eseguiti in modo trasparente il livello di compatibilità 130, sfruttando la nuova query di elaborazione, funzioni e nuova stima della cardinalità.</span><span class="sxs-lookup"><span data-stu-id="cef58-238">Experience shows that most workload are expected tooat least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="cef58-239">Ovvero Ciò premesso, in realtà, sono sempre presenti alcune eccezioni e l'esecuzione di scadenza appropriata molta attenzione toodetermine una valutazione importante quanto è possibile trarre vantaggio da tali miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="cef58-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment toodetermine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="cef58-240">E nuovamente, archivio Query hello può essere di grande aiuto in questo modo.</span><span class="sxs-lookup"><span data-stu-id="cef58-240">And again, hello Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="cef58-241">Come si evolve SQL Azure, è possibile prevedere un livello di compatibilità 140 in hello future.</span><span class="sxs-lookup"><span data-stu-id="cef58-241">As SQL Azure evolves, you can expect a compatibility level 140 in hello future.</span></span> <span data-ttu-id="cef58-242">Al momento opportuno verranno trattate anche le nuove caratteristiche del futuro livello di compatibilità 140, come si è fatto brevemente in questo articolo per il livello di compatibilità 130.</span><span class="sxs-lookup"><span data-stu-id="cef58-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="cef58-243">Per il momento opportuno non dimenticare, a partire da giugno 2016, Database SQL di Azure passerà il livello di compatibilità predefinito hello da 120 too130 per i database appena creati.</span><span class="sxs-lookup"><span data-stu-id="cef58-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change hello default compatibility level from 120 too130 for newly created databases.</span></span> <span data-ttu-id="cef58-244">Tenere presente questa informazione.</span><span class="sxs-lookup"><span data-stu-id="cef58-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="cef58-245">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="cef58-245">References</span></span>
* [<span data-ttu-id="cef58-246">Novità (Motore di database)</span><span class="sxs-lookup"><span data-stu-id="cef58-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="cef58-247">Post di blog: Archivio query, la scatola nera del database, di Borko Novakovic, 8 giugno 2016</span><span class="sxs-lookup"><span data-stu-id="cef58-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="cef58-248">Livello di compatibilità ALTER TABLE (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="cef58-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="cef58-249">ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="cef58-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="cef58-250">Livello di compatibilità 130 per il database SQL di Azure versione 12</span><span class="sxs-lookup"><span data-stu-id="cef58-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="cef58-251">Ottimizzazione del piani di Query con hello stima della cardinalità di SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="cef58-251">Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="cef58-252">Descrizione degli indici columnstore</span><span class="sxs-lookup"><span data-stu-id="cef58-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="cef58-253">Post di blog: Miglioramento delle prestazioni delle query con il livello di compatibilità 130 nel database SQL di Azure, di Alain Lissoir, 6 maggio 2016</span><span class="sxs-lookup"><span data-stu-id="cef58-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

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
