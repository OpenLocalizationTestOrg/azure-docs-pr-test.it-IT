---
title: Linee guida di progettazione per tabelle replicate - Azure SQL Data Warehouse | Microsoft Docs
description: Consigli per la progettazione di tabelle replicate nello schema Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 437a4f628a343312984d1fa2981df7fa01459e26
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="961ee-103">Linee guida di progettazione per l'uso di tabelle replicate in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="961ee-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="961ee-104">Questo articolo offre alcuni consigli per la progettazione di tabelle replicate nello schema Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="961ee-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="961ee-105">Usare questi consigli per migliorare le prestazioni delle query riducendo lo spostamento dei dati e la complessità delle query stesse.</span><span class="sxs-lookup"><span data-stu-id="961ee-105">Use these recommendations to improve query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="961ee-106">La funzionalità delle tabelle replicate è attualmente disponibile in anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="961ee-106">The replicated table feature is currently in public preview.</span></span> <span data-ttu-id="961ee-107">Alcuni comportamenti sono soggetti a modifiche.</span><span class="sxs-lookup"><span data-stu-id="961ee-107">Some behaviors are subject to change.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="961ee-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="961ee-108">Prerequisites</span></span>
<span data-ttu-id="961ee-109">Questo articolo presuppone una certa familiarità con i concetti di distribuzione e spostamento dei dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="961ee-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="961ee-110">Per altre informazioni, vedere [Dati distribuiti](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="961ee-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="961ee-111">Come parte della progettazione di tabelle, è necessario comprendere quanto più possibile i propri dati e il modo in cui vengono eseguite query sui dati.</span><span class="sxs-lookup"><span data-stu-id="961ee-111">As part of table design, understand as much as possible about your data and how the data is queried.</span></span>  <span data-ttu-id="961ee-112">Ad esempio, considerare queste domande:</span><span class="sxs-lookup"><span data-stu-id="961ee-112">For example, consider these questions:</span></span>

- <span data-ttu-id="961ee-113">Quali sono le dimensioni della tabella?</span><span class="sxs-lookup"><span data-stu-id="961ee-113">How large is the table?</span></span>   
- <span data-ttu-id="961ee-114">Quanto spesso viene aggiornata la tabella?</span><span class="sxs-lookup"><span data-stu-id="961ee-114">How often is the table refreshed?</span></span>   
- <span data-ttu-id="961ee-115">Sono presenti tabelle dei fatti e delle dimensioni in un data warehouse?</span><span class="sxs-lookup"><span data-stu-id="961ee-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="961ee-116">Che cos'è una tabella replicata?</span><span class="sxs-lookup"><span data-stu-id="961ee-116">What is a replicated table?</span></span>
<span data-ttu-id="961ee-117">Una tabella replicata include una copia completa della tabella accessibile in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="961ee-117">A replicated table has a full copy of the table accessible on each Compute node.</span></span> <span data-ttu-id="961ee-118">La replica di una tabella elimina la necessità di trasferire dati tra i nodi di calcolo prima di un join o un'aggregazione.</span><span class="sxs-lookup"><span data-stu-id="961ee-118">Replicating a table removes the need to transfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="961ee-119">Poiché la tabella ha più copie, le tabelle replicate funzionano meglio quando le dimensioni delle tabelle sono inferiori a 2 GB, già compresse.</span><span class="sxs-lookup"><span data-stu-id="961ee-119">Since the table has multiple copies, replicated tables work best when the table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="961ee-120">Il diagramma seguente mostra una tabella replicata accessibile in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="961ee-120">The following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="961ee-121">In SQL Data Warehouse la tabella replicata viene interamente copiata in un database di distribuzione in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="961ee-121">In SQL Data Warehouse, the replicated table is fully copied to a distribution database on each Compute node.</span></span> 

<span data-ttu-id="961ee-122">![Tabella replicata](media/guidance-for-using-replicated-tables/replicated-table.png "Tabella replicata")</span><span class="sxs-lookup"><span data-stu-id="961ee-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="961ee-123">Le tabelle replicate sono più adatte per piccole tabelle delle dimensioni in uno schema star.</span><span class="sxs-lookup"><span data-stu-id="961ee-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="961ee-124">Le tabelle delle dimensioni hanno in genere dimensioni tali da rendere possibile l'archiviazione e la conservazione di più copie.</span><span class="sxs-lookup"><span data-stu-id="961ee-124">Dimension tables are usually of a size that makes it feasible to store and maintain multiple copies.</span></span> <span data-ttu-id="961ee-125">Nelle dimensioni sono archiviati dati descrittivi che cambiano raramente, come il nome e l'indirizzo di un cliente e i dettagli del prodotto.</span><span class="sxs-lookup"><span data-stu-id="961ee-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="961ee-126">La rarità delle modifiche dei dati comporta un numero minore di ricompilazioni della tabella replicata.</span><span class="sxs-lookup"><span data-stu-id="961ee-126">The slowly changing nature of the data leads to fewer rebuilds of the replicated table.</span></span> 

<span data-ttu-id="961ee-127">Provare a usare una tabella replicata nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="961ee-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="961ee-128">La dimensione della tabella su disco è inferiore a 2 GB, indipendentemente dal numero di righe.</span><span class="sxs-lookup"><span data-stu-id="961ee-128">The table size on disk is less than 2 GB, regardless of the number of rows.</span></span> <span data-ttu-id="961ee-129">Per individuare la dimensione di una tabella, usare il comando [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql): `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="961ee-129">To find the size of a table, you can use the [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="961ee-130">La tabella viene usata in join che richiederebbero altrimenti lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="961ee-130">The table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="961ee-131">Ad esempio, un join in tabelle con distribuzione hash richiede lo spostamento dei dati quando le colonne di join non si trovano nella stessa colonna di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="961ee-131">For example, a join on hash-distributed tables requires data movement when the joining columns are not the same distribution column.</span></span> <span data-ttu-id="961ee-132">Se una delle tabelle con distribuzione hash ha dimensioni ridotte, provare una tabella replicata.</span><span class="sxs-lookup"><span data-stu-id="961ee-132">If one of the hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="961ee-133">Un join in una tabella round robin richiede lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="961ee-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="961ee-134">È consigliabile usare tabelle replicate invece di tabelle round robin nella maggior parte dei casi.</span><span class="sxs-lookup"><span data-stu-id="961ee-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="961ee-135">Provare a convertire una tabella distribuita esistente in una tabella replicata nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="961ee-135">Consider converting an existing distributed table to a replicated table when:</span></span>

- <span data-ttu-id="961ee-136">I piani di query usano operazioni di spostamento dei dati che trasmettono i dati a tutti i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="961ee-136">Query plans use data movement operations that broadcast the data to all the Compute nodes.</span></span> <span data-ttu-id="961ee-137">L'operazione BroadcastMoveOperation è costosa e rallenta le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="961ee-137">The BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="961ee-138">Per visualizzare le operazioni di spostamento dei dati nei piani di query, usare [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="961ee-138">To view data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="961ee-139">Le tabelle replicate possono essere causa di prestazioni delle query non ottimali nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="961ee-139">Replicated tables may not yield the best query performance when:</span></span>

- <span data-ttu-id="961ee-140">La tabella prevede frequenti operazioni di inserimento, aggiornamento ed eliminazione.</span><span class="sxs-lookup"><span data-stu-id="961ee-140">The table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="961ee-141">Queste operazioni di Data Manipulation Language (DML) richiedono una ricompilazione della tabella replicata.</span><span class="sxs-lookup"><span data-stu-id="961ee-141">These data manipulation language (DML) operations require a rebuild of the replicated table.</span></span> <span data-ttu-id="961ee-142">La ricompilazione causa spesso un rallentamento delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="961ee-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="961ee-143">Il data warehouse viene ridimensionato spesso.</span><span class="sxs-lookup"><span data-stu-id="961ee-143">The data warehouse is scaled frequently.</span></span> <span data-ttu-id="961ee-144">Il ridimensionamento di un data warehouse comporta la modifica del numero dei nodi di calcolo, che richiede una ricompilazione.</span><span class="sxs-lookup"><span data-stu-id="961ee-144">Scaling a data warehouse changes the number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="961ee-145">La tabella include un numero elevato di colonne, ma le operazioni sui dati accedono in genere solo a una quantità ridotta di colonne.</span><span class="sxs-lookup"><span data-stu-id="961ee-145">The table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="961ee-146">In questo scenario, invece di replicare l'intera tabella, può essere più efficace eseguire una distribuzione hash della tabella e quindi creare un indice per le colonne cui si accede di frequente.</span><span class="sxs-lookup"><span data-stu-id="961ee-146">In this scenario, instead of replicating the entire table, it might be more effective to hash distribute the table, and then create an index on the frequently accessed columns.</span></span> <span data-ttu-id="961ee-147">Quando una query richiede lo spostamento dei dati, SQL Data Warehouse sposta solo i dati presenti nelle colonne richieste.</span><span class="sxs-lookup"><span data-stu-id="961ee-147">When a query requires data movement, SQL Data Warehouse only moves data in the requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="961ee-148">Usare tabelle replicate con predicati di query semplici</span><span class="sxs-lookup"><span data-stu-id="961ee-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="961ee-149">Prima di scegliere di distribuire o replicare una tabella, considerare i tipi di query che si prevede di eseguire sulla tabella.</span><span class="sxs-lookup"><span data-stu-id="961ee-149">Before you choose to distribute or replicate a table, think about the types of queries you plan to run against the table.</span></span> <span data-ttu-id="961ee-150">Se possibile:</span><span class="sxs-lookup"><span data-stu-id="961ee-150">Whenever possible,</span></span>

- <span data-ttu-id="961ee-151">Usare tabelle replicate per query con predicati di query semplici, come le query di uguaglianza o disuguaglianza.</span><span class="sxs-lookup"><span data-stu-id="961ee-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="961ee-152">Usare tabelle distribuite per query con predicati di query complessi, come LIKE o NOT LIKE.</span><span class="sxs-lookup"><span data-stu-id="961ee-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="961ee-153">Le query che richiedono un uso intensivo della CPU hanno prestazioni migliori quando il lavoro viene distribuito tra tutti i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="961ee-153">CPU-intensive queries perform best when the work is distributed across all of the Compute nodes.</span></span> <span data-ttu-id="961ee-154">Ad esempio, le query che eseguono calcoli in ogni riga di una tabella hanno prestazioni migliori nelle tabelle distribuite che non nelle tabelle replicate.</span><span class="sxs-lookup"><span data-stu-id="961ee-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="961ee-155">Poiché una tabella replicata viene completamente archiviata in ogni nodo di calcolo, una query che richiede un uso intensivo di CPU su una tabella replicata viene eseguita sull'intera tabella in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="961ee-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against the entire table on every Compute node.</span></span> <span data-ttu-id="961ee-156">Il calcolo aggiuntivo può rallentare le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="961ee-156">The extra computation can slow query performance.</span></span>

<span data-ttu-id="961ee-157">Questa query, ad esempio, ha un predicato complesso.</span><span class="sxs-lookup"><span data-stu-id="961ee-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="961ee-158">Viene eseguita più rapidamente quando il fornitore è una tabella distribuita invece di una tabella replicata.</span><span class="sxs-lookup"><span data-stu-id="961ee-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="961ee-159">In questo esempio il fornitore può avere una distribuzione hash o una distribuzione round robin.</span><span class="sxs-lookup"><span data-stu-id="961ee-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-to-replicated-tables"></a><span data-ttu-id="961ee-160">Convertire le tabelle round robin esistenti in tabelle replicate</span><span class="sxs-lookup"><span data-stu-id="961ee-160">Convert existing round-robin tables to replicated tables</span></span>
<span data-ttu-id="961ee-161">Se sono già presenti tabelle round robin, è consigliabile convertirle in tabelle replicate se soddisfano i criteri specificati in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="961ee-161">If you already have round-robin tables, we recommend converting them to replicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="961ee-162">Le tabelle replicate migliorano le prestazioni rispetto alle tabelle round robin, perché eliminano la necessità di spostare i dati.</span><span class="sxs-lookup"><span data-stu-id="961ee-162">Replicated tables improve performance over round-robin tables because they eliminate the need for data movement.</span></span>  <span data-ttu-id="961ee-163">Una tabella round robin richiede lo spostamento dei dati per i join.</span><span class="sxs-lookup"><span data-stu-id="961ee-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="961ee-164">Questo esempio usa [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) per modificare la tabella DimSalesTerritory in una tabella replicata.</span><span class="sxs-lookup"><span data-stu-id="961ee-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) to change the DimSalesTerritory table to a replicated table.</span></span> <span data-ttu-id="961ee-165">Questo esempio funziona indipendentemente dal fatto che per DimSalesTerritory sia stata eseguita una distribuzione hash o round robin.</span><span class="sxs-lookup"><span data-stu-id="961ee-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="961ee-166">Esempio di prestazioni delle query delle tabelle round robin rispetto alle tabelle replicate</span><span class="sxs-lookup"><span data-stu-id="961ee-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="961ee-167">Una tabella replicata non richiede lo spostamento dei dati per i join, perché l'intera tabella è già presente in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="961ee-167">A replicated table does not require any data movement for joins because the entire table is already present on each Compute node.</span></span> <span data-ttu-id="961ee-168">Se viene eseguita una distribuzione round robin delle tabelle delle dimensioni, un join copia interamente la tabella delle dimensioni in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="961ee-168">If the dimension tables are round-robin distributed, a join copies the dimension table in full to each Compute node.</span></span> <span data-ttu-id="961ee-169">Per spostare i dati, il piano di query contiene un'operazione chiamata BroadcastMoveOperation.</span><span class="sxs-lookup"><span data-stu-id="961ee-169">To move the data, the query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="961ee-170">Questo tipo di operazione di spostamento dei dati rallenta le prestazioni delle query e viene eliminato usando tabelle replicate.</span><span class="sxs-lookup"><span data-stu-id="961ee-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="961ee-171">Per visualizzare i passaggi del piano di query, usare la vista del catalogo di sistema [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="961ee-171">To view query plan steps, use the [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="961ee-172">Nella query seguente sullo schema AdventureWorks, ad esempio, la tabella ` FactInternetSales` è con distribuzione hash.</span><span class="sxs-lookup"><span data-stu-id="961ee-172">For example, in following query against the AdventureWorks schema, the ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="961ee-173">Le tabelle `DimDate` e `DimSalesTerritory` sono tabelle delle dimensioni più piccole.</span><span class="sxs-lookup"><span data-stu-id="961ee-173">The `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="961ee-174">Questa query restituisce le vendite totali in America del Nord per l'anno fiscale 2004:</span><span class="sxs-lookup"><span data-stu-id="961ee-174">This query returns the total sales in North America for fiscal year 2004:</span></span>
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
<span data-ttu-id="961ee-175">`DimDate` e `DimSalesTerritory` sono state ricreate come tabelle round robin.</span><span class="sxs-lookup"><span data-stu-id="961ee-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="961ee-176">Di conseguenza, la query ha mostrato il piano di query seguente, che prevede più operazioni di spostamento di trasmissione:</span><span class="sxs-lookup"><span data-stu-id="961ee-176">As a result, the query showed the following query plan, which has multiple broadcast move operations:</span></span> 
 
![Piano di query round robin](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="961ee-178">`DimDate` e `DimSalesTerritory` sono state ricreate come tabelle replicate e su di esse è stata eseguita una query.</span><span class="sxs-lookup"><span data-stu-id="961ee-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran the query again.</span></span> <span data-ttu-id="961ee-179">Il piano di query risultante è molto più breve e non include spostamenti di trasmissione.</span><span class="sxs-lookup"><span data-stu-id="961ee-179">The resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![Piano di query di tabelle replicate](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="961ee-181">Considerazioni sulle prestazioni per la modifica di tabelle replicate</span><span class="sxs-lookup"><span data-stu-id="961ee-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="961ee-182">SQL Data Warehouse implementa una tabella replicata mantenendo una versione master della tabella.</span><span class="sxs-lookup"><span data-stu-id="961ee-182">SQL Data Warehouse implements a replicated table by maintaining a master version of the table.</span></span> <span data-ttu-id="961ee-183">Il servizio copia la versione master in un database di distribuzione in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="961ee-183">It copies the master version to one distribution database on each Compute node.</span></span> <span data-ttu-id="961ee-184">Quando viene apportata una modifica, SQL Data Warehouse aggiorna prima la tabella master.</span><span class="sxs-lookup"><span data-stu-id="961ee-184">When there is a change, SQL Data Warehouse first updates the master table.</span></span> <span data-ttu-id="961ee-185">Richiede quindi una ricompilazione delle tabelle in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="961ee-185">Then it requires a rebuild of the tables on each Compute node.</span></span> <span data-ttu-id="961ee-186">Una ricompilazione di una tabella replicata include la copia della tabella in ogni nodo di calcolo e quindi la ricompilazione degli indici.</span><span class="sxs-lookup"><span data-stu-id="961ee-186">A rebuild of a replicated table includes copying the table to each Compute node and then rebuilding the indexes.</span></span>

<span data-ttu-id="961ee-187">Le compilazioni sono necessarie dopo le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="961ee-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="961ee-188">Vengono caricati o modificati dati</span><span class="sxs-lookup"><span data-stu-id="961ee-188">Data is loaded or modified</span></span>
- <span data-ttu-id="961ee-189">Il data warehouse viene ridimensionato in base a un'impostazione DWU diversa</span><span class="sxs-lookup"><span data-stu-id="961ee-189">The data warehouse is scaled to a different DWU setting</span></span>
- <span data-ttu-id="961ee-190">Viene aggiornata la definizione di tabella</span><span class="sxs-lookup"><span data-stu-id="961ee-190">Table definition is updated</span></span>

<span data-ttu-id="961ee-191">Le ricompilazioni non sono necessarie dopo le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="961ee-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="961ee-192">Operazione di sospensione</span><span class="sxs-lookup"><span data-stu-id="961ee-192">Pause operation</span></span>
- <span data-ttu-id="961ee-193">Operazione di ripresa</span><span class="sxs-lookup"><span data-stu-id="961ee-193">Resume operation</span></span>

<span data-ttu-id="961ee-194">La ricompilazione non viene eseguita immediatamente dopo la modifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="961ee-194">The rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="961ee-195">Al contrario, la ricompilazione viene attivata la prima volta che una query esegue una selezione dalla tabella.</span><span class="sxs-lookup"><span data-stu-id="961ee-195">Instead, the rebuild is triggered the first time a query selects from the table.</span></span>  <span data-ttu-id="961ee-196">Nell'istruzione di selezione iniziale dalla tabella sono inclusi i passaggi per ricompilare la tabella replicata.</span><span class="sxs-lookup"><span data-stu-id="961ee-196">Within the initial select statement from the table are steps to rebuild the replicated table.</span></span>  <span data-ttu-id="961ee-197">Poiché la ricompilazione viene eseguita all'interno della query, l'impatto dell'istruzione di selezione iniziale può essere significativo, a seconda delle dimensioni della tabella.</span><span class="sxs-lookup"><span data-stu-id="961ee-197">Because the rebuild is done within the query, the impact to the initial select statement could be significant depending on the size of the table.</span></span>  <span data-ttu-id="961ee-198">Se sono interessate più tabelle replicate che richiedono una ricompilazione, ogni copia viene ricompilata in serie come passaggi all'interno dell'istruzione.</span><span class="sxs-lookup"><span data-stu-id="961ee-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within the statement.</span></span>  <span data-ttu-id="961ee-199">Per mantenere la coerenza dei dati durante la ricompilazione della tabella replicata, viene applicato un blocco esclusivo alla tabella.</span><span class="sxs-lookup"><span data-stu-id="961ee-199">To maintain data consistency during the rebuild of the replicated table an exclusive lock is taken on the table.</span></span>  <span data-ttu-id="961ee-200">Il blocco impedisce qualsiasi accesso alla tabella durante la ricompilazione.</span><span class="sxs-lookup"><span data-stu-id="961ee-200">The lock prevents all access to the table for the duration of the rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="961ee-201">Usare gli indici con moderazione</span><span class="sxs-lookup"><span data-stu-id="961ee-201">Use indexes conservatively</span></span>
<span data-ttu-id="961ee-202">Alle tabelle replicate si applicano le procedure di indicizzazione standard.</span><span class="sxs-lookup"><span data-stu-id="961ee-202">Standard indexing practices apply to replicated tables.</span></span> <span data-ttu-id="961ee-203">SQL Data Warehouse ricompila ogni indice di tabella replicata come parte della ricompilazione.</span><span class="sxs-lookup"><span data-stu-id="961ee-203">SQL Data Warehouse rebuilds each replicated table index as part of the rebuild.</span></span> <span data-ttu-id="961ee-204">Usare gli indici solo quando le prestazioni sono più importanti del costo della ricompilazione degli indici.</span><span class="sxs-lookup"><span data-stu-id="961ee-204">Only use indexes when the performance gain outweighs the cost of rebuilding the indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="961ee-205">Caricare in batch i dati</span><span class="sxs-lookup"><span data-stu-id="961ee-205">Batch data loads</span></span>
<span data-ttu-id="961ee-206">Quando si caricano dati in tabelle replicate, provare a ridurre al minimo le ricompilazioni eseguendo i caricamenti in batch.</span><span class="sxs-lookup"><span data-stu-id="961ee-206">When loading data into replicated tables, try to minimize rebuilds by batching loads together.</span></span> <span data-ttu-id="961ee-207">Eseguire tutti i caricamenti in batch prima di eseguire istruzioni di selezione.</span><span class="sxs-lookup"><span data-stu-id="961ee-207">Perform all the batched loads before running select statements.</span></span>

<span data-ttu-id="961ee-208">Ad esempio, questo modello di carico carica dati da quattro origini e richiama quattro ricompilazioni.</span><span class="sxs-lookup"><span data-stu-id="961ee-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="961ee-209">Caricamento dall'origine 1.</span><span class="sxs-lookup"><span data-stu-id="961ee-209">Load from source 1.</span></span>
- <span data-ttu-id="961ee-210">L'istruzione di selezione attiva la ricompilazione 1.</span><span class="sxs-lookup"><span data-stu-id="961ee-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="961ee-211">Caricamento dall'origine 2.</span><span class="sxs-lookup"><span data-stu-id="961ee-211">Load from source 2.</span></span>
- <span data-ttu-id="961ee-212">L'istruzione di selezione attiva la ricompilazione 2.</span><span class="sxs-lookup"><span data-stu-id="961ee-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="961ee-213">Caricamento dall'origine 3.</span><span class="sxs-lookup"><span data-stu-id="961ee-213">Load from source 3.</span></span>
- <span data-ttu-id="961ee-214">L'istruzione di selezione attiva la ricompilazione 3.</span><span class="sxs-lookup"><span data-stu-id="961ee-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="961ee-215">Caricamento dall'origine 4.</span><span class="sxs-lookup"><span data-stu-id="961ee-215">Load from source 4.</span></span>
- <span data-ttu-id="961ee-216">L'istruzione di selezione attiva la ricompilazione 4.</span><span class="sxs-lookup"><span data-stu-id="961ee-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="961ee-217">Ad esempio, questo modello di carico carica dati da quattro origini, ma richiama una sola ricompilazione.</span><span class="sxs-lookup"><span data-stu-id="961ee-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="961ee-218">Caricamento dall'origine 1.</span><span class="sxs-lookup"><span data-stu-id="961ee-218">Load from source 1.</span></span>
- <span data-ttu-id="961ee-219">Caricamento dall'origine 2.</span><span class="sxs-lookup"><span data-stu-id="961ee-219">Load from source 2.</span></span>
- <span data-ttu-id="961ee-220">Caricamento dall'origine 3.</span><span class="sxs-lookup"><span data-stu-id="961ee-220">Load from source 3.</span></span>
- <span data-ttu-id="961ee-221">Caricamento dall'origine 4.</span><span class="sxs-lookup"><span data-stu-id="961ee-221">Load from source 4.</span></span>
- <span data-ttu-id="961ee-222">L'istruzione di selezione attiva la ricompilazione.</span><span class="sxs-lookup"><span data-stu-id="961ee-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="961ee-223">Ricompilare una tabella replicata dopo un caricamento in batch</span><span class="sxs-lookup"><span data-stu-id="961ee-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="961ee-224">Per garantire tempi di esecuzione di query coerenti, è consigliabile forzare un aggiornamento delle tabelle replicate dopo un caricamento in batch.</span><span class="sxs-lookup"><span data-stu-id="961ee-224">To ensure consistent query execution times, we recommend forcing a refresh of the replicated tables after a batch load.</span></span> <span data-ttu-id="961ee-225">In caso contrario, la prima query deve attendere l'aggiornamento delle tabelle, che include la ricompilazione degli indici.</span><span class="sxs-lookup"><span data-stu-id="961ee-225">Otherwise, the first query must wait for the tables to refresh, which includes rebuilding the indexes.</span></span> <span data-ttu-id="961ee-226">A seconda delle dimensioni e del numero di tabelle replicate interessate, l'impatto sulle prestazioni può essere significativo.</span><span class="sxs-lookup"><span data-stu-id="961ee-226">Depending on the size and number of replicated tables affected, the performance impact can be significant.</span></span>  

<span data-ttu-id="961ee-227">Questa query usa la DMV [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) per elencare le tabelle replicate che sono state modificate, ma non ricompilate.</span><span class="sxs-lookup"><span data-stu-id="961ee-227">This query uses the [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV to list the replicated tables that have been modified, but not rebuilt.</span></span>

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
<span data-ttu-id="961ee-228">Per forzare una ricompilazione, eseguire l'istruzione seguente in ogni tabella nell'output precedente.</span><span class="sxs-lookup"><span data-stu-id="961ee-228">To force a rebuild, run the following statement on each table in the preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="961ee-229">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="961ee-229">Next steps</span></span> 
<span data-ttu-id="961ee-230">Per creare una tabella replicata, usare una di queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="961ee-230">To create a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="961ee-231">CREATE TABLE (Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="961ee-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="961ee-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="961ee-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="961ee-233">Per una panoramica delle tabelle distribuite, vedere [Tabelle distribuite](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="961ee-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



