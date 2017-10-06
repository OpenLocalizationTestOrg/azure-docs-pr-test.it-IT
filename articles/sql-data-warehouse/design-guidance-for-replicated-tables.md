---
title: materiale sussidiario aaaDesign per tabelle replicate al fine - Azure SQL Data Warehouse | Documenti Microsoft
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
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="86cdd-103">Linee guida di progettazione per l'uso di tabelle replicate in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="86cdd-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="86cdd-104">Questo articolo offre alcuni consigli per la progettazione di tabelle replicate nello schema Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="86cdd-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="86cdd-105">Utilizzare le prestazioni delle query tooimprove queste indicazioni per ridurre la complessità di query e lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="86cdd-105">Use these recommendations tooimprove query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="86cdd-106">funzionalità di tabella replicata Hello è attualmente in anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="86cdd-106">hello replicated table feature is currently in public preview.</span></span> <span data-ttu-id="86cdd-107">Alcuni comportamenti sono toochange soggetto.</span><span class="sxs-lookup"><span data-stu-id="86cdd-107">Some behaviors are subject toochange.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="86cdd-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="86cdd-108">Prerequisites</span></span>
<span data-ttu-id="86cdd-109">Questo articolo presuppone una certa familiarità con i concetti di distribuzione e spostamento dei dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="86cdd-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="86cdd-110">Per altre informazioni, vedere [Dati distribuiti](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="86cdd-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="86cdd-111">Come parte della struttura di tabella, comprendere il più possibile sulle modalità con cui viene eseguita una query di dati hello e dei dati.</span><span class="sxs-lookup"><span data-stu-id="86cdd-111">As part of table design, understand as much as possible about your data and how hello data is queried.</span></span>  <span data-ttu-id="86cdd-112">Ad esempio, considerare queste domande:</span><span class="sxs-lookup"><span data-stu-id="86cdd-112">For example, consider these questions:</span></span>

- <span data-ttu-id="86cdd-113">Le dimensioni è tabella hello?</span><span class="sxs-lookup"><span data-stu-id="86cdd-113">How large is hello table?</span></span>   
- <span data-ttu-id="86cdd-114">Frequenza di aggiornamento tabella hello?</span><span class="sxs-lookup"><span data-stu-id="86cdd-114">How often is hello table refreshed?</span></span>   
- <span data-ttu-id="86cdd-115">Sono presenti tabelle dei fatti e delle dimensioni in un data warehouse?</span><span class="sxs-lookup"><span data-stu-id="86cdd-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="86cdd-116">Che cos'è una tabella replicata?</span><span class="sxs-lookup"><span data-stu-id="86cdd-116">What is a replicated table?</span></span>
<span data-ttu-id="86cdd-117">Una tabella replicata è una copia completa della tabella hello accessibile su ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="86cdd-117">A replicated table has a full copy of hello table accessible on each Compute node.</span></span> <span data-ttu-id="86cdd-118">La replica di una tabella rimuove i dati di tootransfer necessità di hello tra i nodi di calcolo prima di un'operazione join o aggregazione.</span><span class="sxs-lookup"><span data-stu-id="86cdd-118">Replicating a table removes hello need tootransfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="86cdd-119">Poiché la tabella hello dispone di più copie, le tabelle replicate funzionano meglio quando dimensioni della tabella hello sono minore di 2 GB compressi.</span><span class="sxs-lookup"><span data-stu-id="86cdd-119">Since hello table has multiple copies, replicated tables work best when hello table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="86cdd-120">Hello diagramma seguente mostra una tabella replicata è accessibile in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="86cdd-120">hello following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="86cdd-121">In SQL Data Warehouse, tabella replicata hello è il database di distribuzione tooa completamente copiato in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="86cdd-121">In SQL Data Warehouse, hello replicated table is fully copied tooa distribution database on each Compute node.</span></span> 

<span data-ttu-id="86cdd-122">![Tabella replicata](media/guidance-for-using-replicated-tables/replicated-table.png "Tabella replicata")</span><span class="sxs-lookup"><span data-stu-id="86cdd-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="86cdd-123">Le tabelle replicate sono più adatte per piccole tabelle delle dimensioni in uno schema star.</span><span class="sxs-lookup"><span data-stu-id="86cdd-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="86cdd-124">Le tabelle delle dimensioni sono generalmente di dimensioni che rende possibile toostore e mantengono più copie.</span><span class="sxs-lookup"><span data-stu-id="86cdd-124">Dimension tables are usually of a size that makes it feasible toostore and maintain multiple copies.</span></span> <span data-ttu-id="86cdd-125">Nelle dimensioni sono archiviati dati descrittivi che cambiano raramente, come il nome e l'indirizzo di un cliente e i dettagli del prodotto.</span><span class="sxs-lookup"><span data-stu-id="86cdd-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="86cdd-126">Hello a modifica lenta natura dei dati hello comporta la ricompilazione di una tabella replicata hello toofewer.</span><span class="sxs-lookup"><span data-stu-id="86cdd-126">hello slowly changing nature of hello data leads toofewer rebuilds of hello replicated table.</span></span> 

<span data-ttu-id="86cdd-127">Provare a usare una tabella replicata nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="86cdd-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="86cdd-128">dimensioni tabella Hello su disco sono inferiore a 2 GB, indipendentemente dal numero di hello di righe.</span><span class="sxs-lookup"><span data-stu-id="86cdd-128">hello table size on disk is less than 2 GB, regardless of hello number of rows.</span></span> <span data-ttu-id="86cdd-129">dimensioni di hello toofind di una tabella, è possibile utilizzare hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) comando: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="86cdd-129">toofind hello size of a table, you can use hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="86cdd-130">Hello tabella viene utilizzata nelle operazioni di join che altrimenti richiederebbero lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="86cdd-130">hello table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="86cdd-131">Ad esempio, un join sulle tabelle hash distribuita richiede lo spostamento dei dati quando le colonne di join hello non sono hello stessa colonna di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="86cdd-131">For example, a join on hash-distributed tables requires data movement when hello joining columns are not hello same distribution column.</span></span> <span data-ttu-id="86cdd-132">Se una delle tabelle hash distribuita hello è ridotta, si consideri una tabella replicata.</span><span class="sxs-lookup"><span data-stu-id="86cdd-132">If one of hello hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="86cdd-133">Un join in una tabella round robin richiede lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="86cdd-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="86cdd-134">È consigliabile usare tabelle replicate invece di tabelle round robin nella maggior parte dei casi.</span><span class="sxs-lookup"><span data-stu-id="86cdd-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="86cdd-135">Prendere in considerazione la conversione di un oggetto esistente distribuito tooa tabella replicata tabella quando:</span><span class="sxs-lookup"><span data-stu-id="86cdd-135">Consider converting an existing distributed table tooa replicated table when:</span></span>

- <span data-ttu-id="86cdd-136">Operazioni di spostamento dati di utilizzo che trasmettono i nodi di calcolo di hello dati tooall hello piani di query.</span><span class="sxs-lookup"><span data-stu-id="86cdd-136">Query plans use data movement operations that broadcast hello data tooall hello Compute nodes.</span></span> <span data-ttu-id="86cdd-137">Hello BroadcastMoveOperation è costoso e rallenta le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="86cdd-137">hello BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="86cdd-138">operazioni di spostamento dei dati tooview nei piani di query, utilizzare [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="86cdd-138">tooview data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="86cdd-139">Le tabelle replicate non possono produrre migliori prestazioni di query hello quando:</span><span class="sxs-lookup"><span data-stu-id="86cdd-139">Replicated tables may not yield hello best query performance when:</span></span>

- <span data-ttu-id="86cdd-140">tabella Hello è inserimento frequenti, aggiornamento ed eliminazione.</span><span class="sxs-lookup"><span data-stu-id="86cdd-140">hello table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="86cdd-141">Queste operazioni di data manipulation language (DML) richiedono una ricompilazione della tabella replicata hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-141">These data manipulation language (DML) operations require a rebuild of hello replicated table.</span></span> <span data-ttu-id="86cdd-142">La ricompilazione causa spesso un rallentamento delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="86cdd-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="86cdd-143">data warehouse di Hello viene ridotto di frequente.</span><span class="sxs-lookup"><span data-stu-id="86cdd-143">hello data warehouse is scaled frequently.</span></span> <span data-ttu-id="86cdd-144">Ridimensionamento di un data warehouse Modifica numero hello dei nodi di calcolo, che comporta una ricompilazione.</span><span class="sxs-lookup"><span data-stu-id="86cdd-144">Scaling a data warehouse changes hello number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="86cdd-145">tabella Hello è un numero elevato di colonne, ma in genere, le operazioni sui dati accedere solo un numero limitato di colonne.</span><span class="sxs-lookup"><span data-stu-id="86cdd-145">hello table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="86cdd-146">In questo scenario, anziché replicare hello dell'intera tabella, potrebbe essere più efficace toohash distribuire tabella hello e quindi creare un indice sulle colonne hello si accede di frequente.</span><span class="sxs-lookup"><span data-stu-id="86cdd-146">In this scenario, instead of replicating hello entire table, it might be more effective toohash distribute hello table, and then create an index on hello frequently accessed columns.</span></span> <span data-ttu-id="86cdd-147">Quando una query richiede lo spostamento dei dati, SQL Data Warehouse solo Sposta i dati in hello richieste colonne.</span><span class="sxs-lookup"><span data-stu-id="86cdd-147">When a query requires data movement, SQL Data Warehouse only moves data in hello requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="86cdd-148">Usare tabelle replicate con predicati di query semplici</span><span class="sxs-lookup"><span data-stu-id="86cdd-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="86cdd-149">Prima di scegliere toodistribute o replicare una tabella, considerare i tipi di hello di query toorun tabella hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-149">Before you choose toodistribute or replicate a table, think about hello types of queries you plan toorun against hello table.</span></span> <span data-ttu-id="86cdd-150">Se possibile:</span><span class="sxs-lookup"><span data-stu-id="86cdd-150">Whenever possible,</span></span>

- <span data-ttu-id="86cdd-151">Usare tabelle replicate per query con predicati di query semplici, come le query di uguaglianza o disuguaglianza.</span><span class="sxs-lookup"><span data-stu-id="86cdd-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="86cdd-152">Usare tabelle distribuite per query con predicati di query complessi, come LIKE o NOT LIKE.</span><span class="sxs-lookup"><span data-stu-id="86cdd-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="86cdd-153">Query di utilizzo elevato di CPU risultare migliori se lavoro hello è distribuito in tutti i nodi di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-153">CPU-intensive queries perform best when hello work is distributed across all of hello Compute nodes.</span></span> <span data-ttu-id="86cdd-154">Ad esempio, le query che eseguono calcoli in ogni riga di una tabella hanno prestazioni migliori nelle tabelle distribuite che non nelle tabelle replicate.</span><span class="sxs-lookup"><span data-stu-id="86cdd-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="86cdd-155">Tabella intera hello viene eseguita una query con utilizzo intensivo della CPU rispetto a una tabella replicata in ogni nodo di calcolo poiché una tabella replicata verrà archiviata in modo completo in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="86cdd-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against hello entire table on every Compute node.</span></span> <span data-ttu-id="86cdd-156">Hello calcolo supplementare può rallentare le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="86cdd-156">hello extra computation can slow query performance.</span></span>

<span data-ttu-id="86cdd-157">Questa query, ad esempio, ha un predicato complesso.</span><span class="sxs-lookup"><span data-stu-id="86cdd-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="86cdd-158">Viene eseguita più rapidamente quando il fornitore è una tabella distribuita invece di una tabella replicata.</span><span class="sxs-lookup"><span data-stu-id="86cdd-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="86cdd-159">In questo esempio il fornitore può avere una distribuzione hash o una distribuzione round robin.</span><span class="sxs-lookup"><span data-stu-id="86cdd-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a><span data-ttu-id="86cdd-160">Convertire le tabelle tooreplicated round-robin tabelle esistenti</span><span class="sxs-lookup"><span data-stu-id="86cdd-160">Convert existing round-robin tables tooreplicated tables</span></span>
<span data-ttu-id="86cdd-161">Se si dispongono già di tabelle algoritmo round-robin, è consigliabile convertire in tabelle tooreplicated se soddisfano i criteri descritti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="86cdd-161">If you already have round-robin tables, we recommend converting them tooreplicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="86cdd-162">Le tabelle replicate migliorare le prestazioni rispetto alle tabelle algoritmo round-robin perché eliminano hello necessario per lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="86cdd-162">Replicated tables improve performance over round-robin tables because they eliminate hello need for data movement.</span></span>  <span data-ttu-id="86cdd-163">Una tabella round robin richiede lo spostamento dei dati per i join.</span><span class="sxs-lookup"><span data-stu-id="86cdd-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="86cdd-164">Questo esempio viene utilizzato [un'istruzione CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory tabella tooa tabella replicata.</span><span class="sxs-lookup"><span data-stu-id="86cdd-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory table tooa replicated table.</span></span> <span data-ttu-id="86cdd-165">Questo esempio funziona indipendentemente dal fatto che per DimSalesTerritory sia stata eseguita una distribuzione hash o round robin.</span><span class="sxs-lookup"><span data-stu-id="86cdd-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

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
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="86cdd-166">Esempio di prestazioni delle query delle tabelle round robin rispetto alle tabelle replicate</span><span class="sxs-lookup"><span data-stu-id="86cdd-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="86cdd-167">Una tabella replicata non richiede alcuno spostamento dei dati per i join perché l'intera tabella hello è già presente in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="86cdd-167">A replicated table does not require any data movement for joins because hello entire table is already present on each Compute node.</span></span> <span data-ttu-id="86cdd-168">Se le tabelle delle dimensioni hello sono round-robin distribuito, un join copia tabella della dimensione hello tooeach completo del nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="86cdd-168">If hello dimension tables are round-robin distributed, a join copies hello dimension table in full tooeach Compute node.</span></span> <span data-ttu-id="86cdd-169">dati hello toomove, piano di query hello contiene un'operazione denominata BroadcastMoveOperation.</span><span class="sxs-lookup"><span data-stu-id="86cdd-169">toomove hello data, hello query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="86cdd-170">Questo tipo di operazione di spostamento dei dati rallenta le prestazioni delle query e viene eliminato usando tabelle replicate.</span><span class="sxs-lookup"><span data-stu-id="86cdd-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="86cdd-171">passaggi di piano di query tooview, utilizzare hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) vista del catalogo sys.</span><span class="sxs-lookup"><span data-stu-id="86cdd-171">tooview query plan steps, use hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="86cdd-172">Ad esempio, nella query seguente in base allo schema AdventureWorks hello, hello ` FactInternetSales` tabella è distribuita hash.</span><span class="sxs-lookup"><span data-stu-id="86cdd-172">For example, in following query against hello AdventureWorks schema, hello ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="86cdd-173">Hello `DimDate` e `DimSalesTerritory` le tabelle sono tabelle delle dimensioni più piccole.</span><span class="sxs-lookup"><span data-stu-id="86cdd-173">hello `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="86cdd-174">Questa query restituisce le vendite totali hello in Nord America per l'anno fiscale 2004:</span><span class="sxs-lookup"><span data-stu-id="86cdd-174">This query returns hello total sales in North America for fiscal year 2004:</span></span>
 
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
<span data-ttu-id="86cdd-175">`DimDate` e `DimSalesTerritory` sono state ricreate come tabelle round robin.</span><span class="sxs-lookup"><span data-stu-id="86cdd-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="86cdd-176">Di conseguenza, query hello ha dimostrato hello piano di query che ha più trasmissione spostare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="86cdd-176">As a result, hello query showed hello following query plan, which has multiple broadcast move operations:</span></span> 
 
![Piano di query round robin](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="86cdd-178">È stato creato nuovamente `DimDate` e `DimSalesTerritory` come tabelle duplicate ed è stato eseguito query hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="86cdd-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran hello query again.</span></span> <span data-ttu-id="86cdd-179">piano di query risultante Hello è molto più breve e non hanno uno trasmette passa.</span><span class="sxs-lookup"><span data-stu-id="86cdd-179">hello resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![Piano di query di tabelle replicate](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="86cdd-181">Considerazioni sulle prestazioni per la modifica di tabelle replicate</span><span class="sxs-lookup"><span data-stu-id="86cdd-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="86cdd-182">SQL Data Warehouse implementa una tabella replicata dal mantenimento di una versione principale della tabella di hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-182">SQL Data Warehouse implements a replicated table by maintaining a master version of hello table.</span></span> <span data-ttu-id="86cdd-183">Copia database di distribuzione tooone versione master hello in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="86cdd-183">It copies hello master version tooone distribution database on each Compute node.</span></span> <span data-ttu-id="86cdd-184">Quando viene apportata una modifica, SQL Data Warehouse prima Aggiorna tabella master hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-184">When there is a change, SQL Data Warehouse first updates hello master table.</span></span> <span data-ttu-id="86cdd-185">Richiede quindi una ricompilazione delle tabelle di hello in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="86cdd-185">Then it requires a rebuild of hello tables on each Compute node.</span></span> <span data-ttu-id="86cdd-186">Una ricompilazione di una tabella replicata include la copia del nodo di calcolo tooeach hello tabella e quindi ricompilare gli indici di hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-186">A rebuild of a replicated table includes copying hello table tooeach Compute node and then rebuilding hello indexes.</span></span>

<span data-ttu-id="86cdd-187">Le compilazioni sono necessarie dopo le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="86cdd-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="86cdd-188">Vengono caricati o modificati dati</span><span class="sxs-lookup"><span data-stu-id="86cdd-188">Data is loaded or modified</span></span>
- <span data-ttu-id="86cdd-189">Hello data warehouse è l'impostazione DWU diversa scalato tooa</span><span class="sxs-lookup"><span data-stu-id="86cdd-189">hello data warehouse is scaled tooa different DWU setting</span></span>
- <span data-ttu-id="86cdd-190">Viene aggiornata la definizione di tabella</span><span class="sxs-lookup"><span data-stu-id="86cdd-190">Table definition is updated</span></span>

<span data-ttu-id="86cdd-191">Le ricompilazioni non sono necessarie dopo le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="86cdd-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="86cdd-192">Operazione di sospensione</span><span class="sxs-lookup"><span data-stu-id="86cdd-192">Pause operation</span></span>
- <span data-ttu-id="86cdd-193">Operazione di ripresa</span><span class="sxs-lookup"><span data-stu-id="86cdd-193">Resume operation</span></span>

<span data-ttu-id="86cdd-194">ricompilazione di Hello non avviene immediatamente dopo la modifica di dati.</span><span class="sxs-lookup"><span data-stu-id="86cdd-194">hello rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="86cdd-195">Invece di attivazione di ricompilazione hello hello prima volta una query vengono selezionati dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-195">Instead, hello rebuild is triggered hello first time a query selects from hello table.</span></span>  <span data-ttu-id="86cdd-196">All'interno di hello iniziale from dell'istruzione select nella tabella hello sono tabella replicata di passaggi toorebuild hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-196">Within hello initial select statement from hello table are steps toorebuild hello replicated table.</span></span>  <span data-ttu-id="86cdd-197">Poiché hello ricompilazione viene eseguita all'interno di query hello, istruzione select iniziale toohello hello impatto potrebbe essere significativo a seconda delle dimensioni di hello della tabella hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-197">Because hello rebuild is done within hello query, hello impact toohello initial select statement could be significant depending on hello size of hello table.</span></span>  <span data-ttu-id="86cdd-198">Se più tabelle replicate sono coinvolte che richiedono la ricompilazione, ogni copia viene ricompilato in serie di passaggi all'interno di istruzione hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within hello statement.</span></span>  <span data-ttu-id="86cdd-199">la coerenza dei dati durante la ricompilazione hello di hello toomaintain replicati tabella che acquisizione di un blocco esclusivo sulla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-199">toomaintain data consistency during hello rebuild of hello replicated table an exclusive lock is taken on hello table.</span></span>  <span data-ttu-id="86cdd-200">blocco di Hello impedisce tutte tabella toohello di accesso per la durata di hello di ricompilazione hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-200">hello lock prevents all access toohello table for hello duration of hello rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="86cdd-201">Usare gli indici con moderazione</span><span class="sxs-lookup"><span data-stu-id="86cdd-201">Use indexes conservatively</span></span>
<span data-ttu-id="86cdd-202">Procedure consigliate di indicizzazione standard si applicano tooreplicated tabelle.</span><span class="sxs-lookup"><span data-stu-id="86cdd-202">Standard indexing practices apply tooreplicated tables.</span></span> <span data-ttu-id="86cdd-203">Ogni indice di tabella replicata come parte di ricompilazione hello viene ricompilato SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="86cdd-203">SQL Data Warehouse rebuilds each replicated table index as part of hello rebuild.</span></span> <span data-ttu-id="86cdd-204">Utilizzare solo indici quando miglioramento delle prestazioni hello supera il costo di hello di ricompilazione di indici hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-204">Only use indexes when hello performance gain outweighs hello cost of rebuilding hello indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="86cdd-205">Caricare in batch i dati</span><span class="sxs-lookup"><span data-stu-id="86cdd-205">Batch data loads</span></span>
<span data-ttu-id="86cdd-206">Quando si caricano dati in tabelle replicate, provare la ricompilazione toominimize da inviare in batch carica.</span><span class="sxs-lookup"><span data-stu-id="86cdd-206">When loading data into replicated tables, try toominimize rebuilds by batching loads together.</span></span> <span data-ttu-id="86cdd-207">Eseguire tutti i carichi di hello in batch prima di eseguire le istruzioni select.</span><span class="sxs-lookup"><span data-stu-id="86cdd-207">Perform all hello batched loads before running select statements.</span></span>

<span data-ttu-id="86cdd-208">Ad esempio, questo modello di carico carica dati da quattro origini e richiama quattro ricompilazioni.</span><span class="sxs-lookup"><span data-stu-id="86cdd-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="86cdd-209">Caricamento dall'origine 1.</span><span class="sxs-lookup"><span data-stu-id="86cdd-209">Load from source 1.</span></span>
- <span data-ttu-id="86cdd-210">L'istruzione di selezione attiva la ricompilazione 1.</span><span class="sxs-lookup"><span data-stu-id="86cdd-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="86cdd-211">Caricamento dall'origine 2.</span><span class="sxs-lookup"><span data-stu-id="86cdd-211">Load from source 2.</span></span>
- <span data-ttu-id="86cdd-212">L'istruzione di selezione attiva la ricompilazione 2.</span><span class="sxs-lookup"><span data-stu-id="86cdd-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="86cdd-213">Caricamento dall'origine 3.</span><span class="sxs-lookup"><span data-stu-id="86cdd-213">Load from source 3.</span></span>
- <span data-ttu-id="86cdd-214">L'istruzione di selezione attiva la ricompilazione 3.</span><span class="sxs-lookup"><span data-stu-id="86cdd-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="86cdd-215">Caricamento dall'origine 4.</span><span class="sxs-lookup"><span data-stu-id="86cdd-215">Load from source 4.</span></span>
- <span data-ttu-id="86cdd-216">L'istruzione di selezione attiva la ricompilazione 4.</span><span class="sxs-lookup"><span data-stu-id="86cdd-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="86cdd-217">Ad esempio, questo modello di carico carica dati da quattro origini, ma richiama una sola ricompilazione.</span><span class="sxs-lookup"><span data-stu-id="86cdd-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="86cdd-218">Caricamento dall'origine 1.</span><span class="sxs-lookup"><span data-stu-id="86cdd-218">Load from source 1.</span></span>
- <span data-ttu-id="86cdd-219">Caricamento dall'origine 2.</span><span class="sxs-lookup"><span data-stu-id="86cdd-219">Load from source 2.</span></span>
- <span data-ttu-id="86cdd-220">Caricamento dall'origine 3.</span><span class="sxs-lookup"><span data-stu-id="86cdd-220">Load from source 3.</span></span>
- <span data-ttu-id="86cdd-221">Caricamento dall'origine 4.</span><span class="sxs-lookup"><span data-stu-id="86cdd-221">Load from source 4.</span></span>
- <span data-ttu-id="86cdd-222">L'istruzione di selezione attiva la ricompilazione.</span><span class="sxs-lookup"><span data-stu-id="86cdd-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="86cdd-223">Ricompilare una tabella replicata dopo un caricamento in batch</span><span class="sxs-lookup"><span data-stu-id="86cdd-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="86cdd-224">tempi di esecuzione di query coerente tooensure, è consigliabile forzare un aggiornamento di tabelle hello replicata dopo un carico batch.</span><span class="sxs-lookup"><span data-stu-id="86cdd-224">tooensure consistent query execution times, we recommend forcing a refresh of hello replicated tables after a batch load.</span></span> <span data-ttu-id="86cdd-225">In caso contrario, prima query hello deve attendere hello tabelle toorefresh, che include la ricompilazione degli indici hello.</span><span class="sxs-lookup"><span data-stu-id="86cdd-225">Otherwise, hello first query must wait for hello tables toorefresh, which includes rebuilding hello indexes.</span></span> <span data-ttu-id="86cdd-226">A seconda delle dimensioni di hello e numero di tabelle replicate interessati, l'impatto sulle prestazioni di hello può essere significativo.</span><span class="sxs-lookup"><span data-stu-id="86cdd-226">Depending on hello size and number of replicated tables affected, hello performance impact can be significant.</span></span>  

<span data-ttu-id="86cdd-227">Questa query utilizza hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) hello toolist DMV replicati tabelle modificate, ma non è state ricompilate.</span><span class="sxs-lookup"><span data-stu-id="86cdd-227">This query uses hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello replicated tables that have been modified, but not rebuilt.</span></span>

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
 
<span data-ttu-id="86cdd-228">tooforce una ricompilazione, eseguire hello successiva istruzione di ciascuna tabella hello output precedente.</span><span class="sxs-lookup"><span data-stu-id="86cdd-228">tooforce a rebuild, run hello following statement on each table in hello preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="86cdd-229">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86cdd-229">Next steps</span></span> 
<span data-ttu-id="86cdd-230">toocreate una tabella replicata, utilizzare una di queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="86cdd-230">toocreate a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="86cdd-231">CREATE TABLE (Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="86cdd-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="86cdd-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="86cdd-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="86cdd-233">Per una panoramica delle tabelle distribuite, vedere [Tabelle distribuite](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="86cdd-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



