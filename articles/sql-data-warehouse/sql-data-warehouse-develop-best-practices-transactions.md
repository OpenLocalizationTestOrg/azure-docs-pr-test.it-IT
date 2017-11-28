---
title: le transazioni aaaOptimizing per SQL Data Warehouse | Documenti Microsoft
description: Indicazioni sulle procedure consigliate per la scrittura di aggiornamenti di transazioni efficienti in Azure SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="535a0-103">Ottimizzazione delle transazioni per SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="535a0-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="535a0-104">Questo articolo spiega come toooptimize hello prestazioni del codice transazionale riducendo i rischi per i ripristini lungo.</span><span class="sxs-lookup"><span data-stu-id="535a0-104">This article explains how toooptimize hello performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="535a0-105">Transazioni e registrazione</span><span class="sxs-lookup"><span data-stu-id="535a0-105">Transactions and logging</span></span>
<span data-ttu-id="535a0-106">Le transazioni sono un componente importante in un motore di database relazionale.</span><span class="sxs-lookup"><span data-stu-id="535a0-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="535a0-107">SQL Data Warehouse usa le transazioni durante la modifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="535a0-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="535a0-108">Queste operazioni possono essere esplicite o implicite.</span><span class="sxs-lookup"><span data-stu-id="535a0-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="535a0-109">Le istruzioni singole `INSERT`, `UPDATE` e `DELETE` sono esempi di transazioni implicite.</span><span class="sxs-lookup"><span data-stu-id="535a0-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="535a0-110">Le transazioni esplicite sono scritti in modo esplicito da uno sviluppatore utilizzando `BEGIN TRAN`, `COMMIT TRAN` o `ROLLBACK TRAN` e vengono in genere usate quando le istruzioni di modifica più necessario toobe collegati in un'unica unità atomica.</span><span class="sxs-lookup"><span data-stu-id="535a0-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need toobe tied together in a single atomic unit.</span></span> 

<span data-ttu-id="535a0-111">Azure SQL Data Warehouse viene eseguito il commit del database toohello modifiche utilizzando i log delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="535a0-111">Azure SQL Data Warehouse commits changes toohello database using transaction logs.</span></span> <span data-ttu-id="535a0-112">Ogni distribuzione ha un proprio log delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="535a0-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="535a0-113">Le scritture del log delle transazioni avvengono in modo automatico</span><span class="sxs-lookup"><span data-stu-id="535a0-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="535a0-114">e non è richiesta alcuna configurazione.</span><span class="sxs-lookup"><span data-stu-id="535a0-114">There is no configuration required.</span></span> <span data-ttu-id="535a0-115">Tuttavia, durante questo processo garantisce la scrittura di hello introdurre un sovraccarico nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="535a0-115">However, whilst this process guarantees hello write it does introduce an overhead in hello system.</span></span> <span data-ttu-id="535a0-116">È possibile ridurre al minimo tale impatto scrivendo codice efficiente a livello transazionale.</span><span class="sxs-lookup"><span data-stu-id="535a0-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="535a0-117">Il codice efficiente a livello transazionale rientra in due categorie generali.</span><span class="sxs-lookup"><span data-stu-id="535a0-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="535a0-118">Sfruttare costrutti di registrazione minima, dove possibile.</span><span class="sxs-lookup"><span data-stu-id="535a0-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="535a0-119">Elaborazione di dati con la forma singolare tooavoid con ambito batch transazioni a esecuzione prolungata</span><span class="sxs-lookup"><span data-stu-id="535a0-119">Process data using scoped batches tooavoid singular long running transactions</span></span>
* <span data-ttu-id="535a0-120">Adottare una modello per la partizione specificata tooa di grandi dimensioni modifiche del cambio di partizione</span><span class="sxs-lookup"><span data-stu-id="535a0-120">Adopt a partition switching pattern for large modifications tooa given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="535a0-121">Confronto tra registrazione minima e registrazione completa</span><span class="sxs-lookup"><span data-stu-id="535a0-121">Minimal vs. full logging</span></span>
<span data-ttu-id="535a0-122">A differenza delle operazioni con registrazione completa, che utilizzano traccia tookeep di hello transaction log di ogni modifica della riga, operazioni con registrazione minima tenere traccia delle allocazioni di extent e solo le modifiche dei metadati.</span><span class="sxs-lookup"><span data-stu-id="535a0-122">Unlike fully logged operations, which use hello transaction log tookeep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="535a0-123">Di conseguenza, la registrazione minima implica la registrazione solo informazioni hello sono obbligatorio toorollback hello di transazione nell'evento hello di un errore o di una richiesta esplicita (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="535a0-123">Therefore, minimal logging involves logging only hello information that is required toorollback hello transaction in hello event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="535a0-124">Come molto meno informazioni vengono rilevate nel log delle transazioni hello, un'operazione con registrazione minima offre prestazioni migliori rispetto a un'operazione completamente registrata con dimensione simili.</span><span class="sxs-lookup"><span data-stu-id="535a0-124">As much less information is tracked in hello transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="535a0-125">Inoltre, in quanto un minor numero di scritture log delle transazioni hello, una minore quantità di dati di log viene generata e pertanto i/o più efficiente.</span><span class="sxs-lookup"><span data-stu-id="535a0-125">Furthermore, because fewer writes go hello transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="535a0-126">limiti di sicurezza delle transazioni Hello si applicano solo operazioni toofully registrati.</span><span class="sxs-lookup"><span data-stu-id="535a0-126">hello transaction safety limits only apply toofully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="535a0-127">le operazioni con registrazione minima possono partecipare alle transazioni esplicite.</span><span class="sxs-lookup"><span data-stu-id="535a0-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="535a0-128">Come vengono rilevate tutte le modifiche in strutture di allocazione, è possibile tooroll back minima operazioni registrate.</span><span class="sxs-lookup"><span data-stu-id="535a0-128">As all changes in allocation structures are tracked, it is possible tooroll back minimally logged operations.</span></span> <span data-ttu-id="535a0-129">È importante registrato toounderstand che modifica hello è "minima" non è non registrato.</span><span class="sxs-lookup"><span data-stu-id="535a0-129">It is important toounderstand that hello change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="535a0-130">Operazioni con registrazione minima</span><span class="sxs-lookup"><span data-stu-id="535a0-130">Minimally logged operations</span></span>
<span data-ttu-id="535a0-131">Hello operazioni indicate di seguito sono in grado di corso la registrazione minima:</span><span class="sxs-lookup"><span data-stu-id="535a0-131">hello following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="535a0-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="535a0-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="535a0-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="535a0-133">INSERT..SELECT</span></span>
* <span data-ttu-id="535a0-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="535a0-134">CREATE INDEX</span></span>
* <span data-ttu-id="535a0-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="535a0-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="535a0-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="535a0-136">DROP INDEX</span></span>
* <span data-ttu-id="535a0-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="535a0-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="535a0-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="535a0-138">DROP TABLE</span></span>
* <span data-ttu-id="535a0-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="535a0-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="535a0-140">Operazioni di spostamento dei dati interni (ad esempio `BROADCAST` e `SHUFFLE`) non sono interessati da limite di sicurezza delle transazioni hello.</span><span class="sxs-lookup"><span data-stu-id="535a0-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by hello transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="535a0-141">Registrazione minima con caricamento bulk</span><span class="sxs-lookup"><span data-stu-id="535a0-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="535a0-142">`CTAS` e `INSERT...SELECT` sono entrambe operazioni di caricamento bulk.</span><span class="sxs-lookup"><span data-stu-id="535a0-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="535a0-143">Tuttavia, entrambi sono influenzate dalla definizione di tabella di destinazione hello e dipendono da uno scenario di carico hello.</span><span class="sxs-lookup"><span data-stu-id="535a0-143">However, both are influenced by hello target table definition and depend on hello load scenario.</span></span> <span data-ttu-id="535a0-144">La tabella riportata di seguito indica la registrazione completa o minima delle operazioni bulk elencate:</span><span class="sxs-lookup"><span data-stu-id="535a0-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="535a0-145">Indice primario</span><span class="sxs-lookup"><span data-stu-id="535a0-145">Primary Index</span></span> | <span data-ttu-id="535a0-146">Scenario di caricamento</span><span class="sxs-lookup"><span data-stu-id="535a0-146">Load Scenario</span></span> | <span data-ttu-id="535a0-147">Modalità di registrazione</span><span class="sxs-lookup"><span data-stu-id="535a0-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="535a0-148">Heap</span><span class="sxs-lookup"><span data-stu-id="535a0-148">Heap</span></span> |<span data-ttu-id="535a0-149">Qualsiasi</span><span class="sxs-lookup"><span data-stu-id="535a0-149">Any</span></span> |<span data-ttu-id="535a0-150">**Minima**</span><span class="sxs-lookup"><span data-stu-id="535a0-150">**Minimal**</span></span> |
| <span data-ttu-id="535a0-151">Indice cluster</span><span class="sxs-lookup"><span data-stu-id="535a0-151">Clustered Index</span></span> |<span data-ttu-id="535a0-152">Tabella di destinazione vuota</span><span class="sxs-lookup"><span data-stu-id="535a0-152">Empty target table</span></span> |<span data-ttu-id="535a0-153">**Minima**</span><span class="sxs-lookup"><span data-stu-id="535a0-153">**Minimal**</span></span> |
| <span data-ttu-id="535a0-154">Indice cluster</span><span class="sxs-lookup"><span data-stu-id="535a0-154">Clustered Index</span></span> |<span data-ttu-id="535a0-155">Le righe caricate non si sovrappongono alle pagine esistenti nella destinazione</span><span class="sxs-lookup"><span data-stu-id="535a0-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="535a0-156">**Minima**</span><span class="sxs-lookup"><span data-stu-id="535a0-156">**Minimal**</span></span> |
| <span data-ttu-id="535a0-157">Indice cluster</span><span class="sxs-lookup"><span data-stu-id="535a0-157">Clustered Index</span></span> |<span data-ttu-id="535a0-158">Le righe caricate si sovrappongono alle pagine esistenti nella destinazione</span><span class="sxs-lookup"><span data-stu-id="535a0-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="535a0-159">Completa</span><span class="sxs-lookup"><span data-stu-id="535a0-159">Full</span></span> |
| <span data-ttu-id="535a0-160">Indice columnstore cluster</span><span class="sxs-lookup"><span data-stu-id="535a0-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="535a0-161">Dimensioni batch >= 102.400 per ogni distribuzione allineata alle partizioni</span><span class="sxs-lookup"><span data-stu-id="535a0-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="535a0-162">**Minima**</span><span class="sxs-lookup"><span data-stu-id="535a0-162">**Minimal**</span></span> |
| <span data-ttu-id="535a0-163">Indice columnstore cluster</span><span class="sxs-lookup"><span data-stu-id="535a0-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="535a0-164">Dimensioni batch < 102.400 per ogni distribuzione allineata alle partizioni</span><span class="sxs-lookup"><span data-stu-id="535a0-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="535a0-165">Completa</span><span class="sxs-lookup"><span data-stu-id="535a0-165">Full</span></span> |

<span data-ttu-id="535a0-166">Vale la pena notare che eventuali scritture gli indici secondari o non cluster tooupdate sarà sempre completamente operazioni registrate.</span><span class="sxs-lookup"><span data-stu-id="535a0-166">It is worth noting that any writes tooupdate secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="535a0-167">SQL Data Warehouse ha 60 distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="535a0-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="535a0-168">Di conseguenza, presupponendo che tutte le righe sono distribuite uniformemente e di destinazione in una singola partizione, il batch sarà necessario righe toocontain 6,144,000 o toobe maggiore minima registrate durante la scrittura tooa indice Columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="535a0-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need toocontain 6,144,000 rows or larger toobe minimally logged when writing tooa Clustered Columnstore Index.</span></span> <span data-ttu-id="535a0-169">Se viene partizionata hello e righe hello inserite span dei limiti delle partizioni, è necessario 6,144,000 righe al limite della partizione presupponendo che anche la distribuzione dei dati.</span><span class="sxs-lookup"><span data-stu-id="535a0-169">If hello table is partitioned and hello rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="535a0-170">Ogni partizione in ogni distribuzione deve superare in modo indipendente soglia di righe per hello insert toobe registrazione minima in distribuzione hello 102.400 hello.</span><span class="sxs-lookup"><span data-stu-id="535a0-170">Each partition in each distribution must independently exceed hello 102,400 row threshold for hello insert toobe minimally logged into hello distribution.</span></span>
> 
> 

<span data-ttu-id="535a0-171">Il caricamento di dati in una tabella non vuota con un indice cluster può spesso contenere una combinazione di righe con registrazione completa e con registrazione minima.</span><span class="sxs-lookup"><span data-stu-id="535a0-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="535a0-172">Un indice cluster è un albero B (bilanciato) di pagine.</span><span class="sxs-lookup"><span data-stu-id="535a0-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="535a0-173">Se la pagina hello scritti tooalready contiene le righe da un'altra transazione, quindi tali operazioni di scrittura verrà registrate completamente.</span><span class="sxs-lookup"><span data-stu-id="535a0-173">If hello page being written tooalready contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="535a0-174">Tuttavia, se la pagina hello è vuota quindi pagina toothat di scrittura hello verrà minima registrato.</span><span class="sxs-lookup"><span data-stu-id="535a0-174">However, if hello page is empty then hello write toothat page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="535a0-175">Ottimizzazione delle eliminazioni</span><span class="sxs-lookup"><span data-stu-id="535a0-175">Optimizing deletes</span></span>
<span data-ttu-id="535a0-176">`DELETE` è un'operazione con registrazione completa.</span><span class="sxs-lookup"><span data-stu-id="535a0-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="535a0-177">Se è necessario toodelete una grande quantità di dati in una tabella o una partizione, è spesso opportuno troppo`SELECT` dati hello desiderato tookeep, che può essere eseguito come un'operazione con registrazione minima.</span><span class="sxs-lookup"><span data-stu-id="535a0-177">If you need toodelete a large amount of data in a table or a partition, it often makes more sense too`SELECT` hello data you wish tookeep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="535a0-178">tooaccomplish, creare una nuova tabella con [un'istruzione CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="535a0-178">tooaccomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="535a0-179">Una volta creata, utilizzare [RINOMINARE] [ RENAME] tooswap la tabella precedente con la tabella hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="535a0-179">Once created, use [RENAME][RENAME] tooswap out your old table with hello newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="535a0-180">Ottimizzazione degli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="535a0-180">Optimizing updates</span></span>
<span data-ttu-id="535a0-181">`UPDATE` è un'operazione con registrazione completa.</span><span class="sxs-lookup"><span data-stu-id="535a0-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="535a0-182">Se è necessario tooupdate un numero elevato di righe in una tabella o una partizione può essere spesso molto più efficiente toouse un'operazione con registrazione minima, ad esempio [un'istruzione CTAS] [ CTAS] toodo in modo.</span><span class="sxs-lookup"><span data-stu-id="535a0-182">If you need tooupdate a large number of rows in a table or a partition it can often be far more efficient toouse a minimally logged operation such as [CTAS][CTAS] toodo so.</span></span>

<span data-ttu-id="535a0-183">In hello esempio riportato di seguito un aggiornamento di tabelle complete è stato convertito tooa `CTAS` in modo che sia possibile la registrazione minima.</span><span class="sxs-lookup"><span data-stu-id="535a0-183">In hello example below a full table update has been converted tooa `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="535a0-184">In questo caso aggiungiamo posteriori vendite toohello importo dello sconto nella tabella hello:</span><span class="sxs-lookup"><span data-stu-id="535a0-184">In this case we are retrospectively adding a discount amount toohello sales in hello table:</span></span>

```sql
--Step 01. Create a new table containing hello "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="535a0-185">Per creare nuovamente tabelle di grandi dimensioni è possibile sfruttare le funzionalità di gestione del carico di lavoro di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="535a0-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="535a0-186">Per ulteriori informazioni, vedere toohello sezione relativa alla gestione del carico di lavoro in hello [concorrenza] [ concurrency] articolo.</span><span class="sxs-lookup"><span data-stu-id="535a0-186">For more details please refer toohello workload management section in hello [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="535a0-187">Ottimizzazione con cambio della partizione</span><span class="sxs-lookup"><span data-stu-id="535a0-187">Optimizing with partition switching</span></span>
<span data-ttu-id="535a0-188">In caso di modifiche su larga scala in una [partizione di tabella][table partition] può risultare molto utile adottare un modello di cambio di partizione.</span><span class="sxs-lookup"><span data-stu-id="535a0-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="535a0-189">Se hello la modifica dei dati è significativa e intervalli di più partizioni, quindi scorrere semplicemente partizioni hello raggiunge hello stesso risultato.</span><span class="sxs-lookup"><span data-stu-id="535a0-189">If hello data modification is significant and spans multiple partitions, then simply iterating over hello partitions achieves hello same result.</span></span>

<span data-ttu-id="535a0-190">di seguito sono riportati i passaggi di Hello tooperform un cambio di partizione:</span><span class="sxs-lookup"><span data-stu-id="535a0-190">hello steps tooperform a partition switch are as follows:</span></span>

1. <span data-ttu-id="535a0-191">Creare una partizione di disattivazione vuota.</span><span class="sxs-lookup"><span data-stu-id="535a0-191">Create an empty out partition</span></span>
2. <span data-ttu-id="535a0-192">Eseguire l'aggiornamento"hello" come una istruzione CTAS</span><span class="sxs-lookup"><span data-stu-id="535a0-192">Perform hello 'update' as a CTAS</span></span>
3. <span data-ttu-id="535a0-193">Hello esistente dati toohello la tabella di disattivazione</span><span class="sxs-lookup"><span data-stu-id="535a0-193">Switch out hello existing data toohello out table</span></span>
4. <span data-ttu-id="535a0-194">Passare a nuovi dati hello</span><span class="sxs-lookup"><span data-stu-id="535a0-194">Switch in hello new data</span></span>
5. <span data-ttu-id="535a0-195">Pulizia dei dati hello</span><span class="sxs-lookup"><span data-stu-id="535a0-195">Clean up hello data</span></span>

<span data-ttu-id="535a0-196">Tuttavia, toohelp identificare hello tooswitch di partizioni è necessario innanzitutto toobuild una routine di supporto, ad esempio hello uno riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="535a0-196">However, toohelp identify hello partitions tooswitch we will first need toobuild a helper procedure such as hello one below.</span></span> 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

<span data-ttu-id="535a0-197">Questa procedura consente di ottimizzare riutilizzo del codice e mantiene esempio più compatto del cambio di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="535a0-197">This procedure maximizes code re-use and keeps hello partition switching example more compact.</span></span>

<span data-ttu-id="535a0-198">Hello di codice riportato di seguito cinque passaggi hello indicato in precedenza tooachieve una routine di cambio della partizione completa.</span><span class="sxs-lookup"><span data-stu-id="535a0-198">hello code below demonstrates hello five steps mentioned above tooachieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="535a0-199">Riduzione della registrazione con batch di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="535a0-199">Minimize logging with small batches</span></span>
<span data-ttu-id="535a0-200">Per le operazioni di modifica di dati di grandi dimensioni, può avere senso toodivide hello operazione in unità di hello tooscope blocchi o i batch di lavoro.</span><span class="sxs-lookup"><span data-stu-id="535a0-200">For large data modification operations, it may make sense toodivide hello operation into chunks or batches tooscope hello unit of work.</span></span>

<span data-ttu-id="535a0-201">Di seguito viene fornito un esempio funzionante.</span><span class="sxs-lookup"><span data-stu-id="535a0-201">A working example is provided below.</span></span> <span data-ttu-id="535a0-202">dimensioni del batch Hello sono stata impostata una semplice numero tecnica di hello toohighlight tooa.</span><span class="sxs-lookup"><span data-stu-id="535a0-202">hello batch size has been set tooa trivial number toohighlight hello technique.</span></span> <span data-ttu-id="535a0-203">In realtà la dimensione del batch hello sarebbe notevolmente maggiore.</span><span class="sxs-lookup"><span data-stu-id="535a0-203">In reality hello batch size would be significantly larger.</span></span> 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="535a0-204">Linee guida per la sospensione e il ridimensionamento</span><span class="sxs-lookup"><span data-stu-id="535a0-204">Pause and scaling guidance</span></span>
<span data-ttu-id="535a0-205">Azure SQL Data Warehouse permette di sospendere, riprendere e ridimensionare il data warehouse su richiesta.</span><span class="sxs-lookup"><span data-stu-id="535a0-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="535a0-206">Quando si sospende o ridimensionare il Data Warehouse di SQL è importante toounderstand che qualsiasi pertanto le transazioni vengono terminate immediatamente. causa toobe eventuali transazioni aperte a rollback.</span><span class="sxs-lookup"><span data-stu-id="535a0-206">When you pause or scale your SQL Data Warehouse it is important toounderstand that any in-flight transactions are terminated immediately; causing any open transactions toobe rolled back.</span></span> <span data-ttu-id="535a0-207">Se il carico di lavoro ha rilasciato una lunga esecuzione e la modifica di dati incompleti precedente toohello sospensione o dell'operazione di ridimensionamento, quindi questo lavoro sarà necessario toobe annullata.</span><span class="sxs-lookup"><span data-stu-id="535a0-207">If your workload had issued a long running and incomplete data modification prior toohello pause or scale operation, then this work will need toobe undone.</span></span> <span data-ttu-id="535a0-208">Questo potrebbe influire sulle hello tempo toopause o ridimensionare il database di Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="535a0-208">This may impact hello time it takes toopause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="535a0-209">`UPDATE` e `DELETE` sono operazioni con registrazione completa e qualsiasi operazione di annullamento o ripristino può richiedere molto più tempo rispetto alle operazioni con registrazione minima equivalenti.</span><span class="sxs-lookup"><span data-stu-id="535a0-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="535a0-210">scenario migliore Hello è toolet in fase di trasferimento dati Modifica transazioni completo precedente toopausing o ridimensionamento SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="535a0-210">hello best scenario is toolet in flight data modification transactions complete prior toopausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="535a0-211">Tuttavia, questo potrebbe non essere sempre possibile.</span><span class="sxs-lookup"><span data-stu-id="535a0-211">However, this may not always be practical.</span></span> <span data-ttu-id="535a0-212">rischio hello toomitigate di un rollback lungo considerare una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="535a0-212">toomitigate hello risk of a long rollback, consider one of hello following options:</span></span>

* <span data-ttu-id="535a0-213">Riscrivere le operazioni a esecuzione prolungata con [CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="535a0-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="535a0-214">Suddividere operazione hello in blocchi. opera su un subset di righe hello</span><span class="sxs-lookup"><span data-stu-id="535a0-214">Break hello operation down into chunks; operating on a subset of hello rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="535a0-215">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="535a0-215">Next steps</span></span>
<span data-ttu-id="535a0-216">Vedere [transazioni in SQL Data Warehouse] [ Transactions in SQL Data Warehouse] toolearn informazioni sui livelli di isolamento e i limiti transazionali.</span><span class="sxs-lookup"><span data-stu-id="535a0-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] toolearn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="535a0-217">Per una panoramica delle altre procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="535a0-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

