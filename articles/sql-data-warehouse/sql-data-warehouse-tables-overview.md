---
title: Panoramica delle tabelle in SQL Data Warehouse | Microsoft Docs
description: Introduzione alle tabelle di SQL Data Warehouse di Azure.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 2114d9ad-c113-43da-859f-419d72604bdf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/29/2016
ms.author: shigu;jrj
ms.openlocfilehash: c16fef2f302dbc56f257eaf2f0d2b68b6a3c1852
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a><span data-ttu-id="d3ee9-103">Panoramica delle tabelle in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d3ee9-103">Overview of tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="d3ee9-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="d3ee9-105">[Tipi di dati][Data Types]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="d3ee9-106">[Distribuzione][Distribute]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="d3ee9-107">[Indice][Index]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-107">[Index][Index]</span></span>
> * <span data-ttu-id="d3ee9-108">[Partizione][Partition]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="d3ee9-109">[Statistiche][Statistics]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="d3ee9-110">[Temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="d3ee9-111">Iniziare a creare tabelle in SQL Data Warehouse è facile.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-111">Getting started with creating tables in SQL Data Warehouse is simple.</span></span>  <span data-ttu-id="d3ee9-112">La sintassi di base [CREATE TABLE][CREATE TABLE] segue la sintassi comune che probabilmente è già nota perché usata in altri database.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-112">The basic [CREATE TABLE][CREATE TABLE] syntax follows the common syntax you are most likely already familiar with from working with other databases.</span></span>  <span data-ttu-id="d3ee9-113">Per creare una tabella, è sufficiente assegnarle un nome, assegnare un nome alle colonne e definire i tipi di dati per ogni colonna.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-113">To create a table, you simply need to name your table, name your columns and define data types for each column.</span></span>  <span data-ttu-id="d3ee9-114">Se sono state create tabelle in altri database, si dovrebbe avere già familiarità con la procedura.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-114">If you've create tables in other databases, this should look very familiar to you.</span></span>

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

<span data-ttu-id="d3ee9-115">Nell'esempio sopra riportato viene creata una tabella di nome Customers con due colonne: FirstName e LastName.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-115">The above example creates a table named Customers with two columns, FirstName and LastName.</span></span>  <span data-ttu-id="d3ee9-116">Ogni colonna è definita con un tipo di dati VARCHAR(25), che limita i dati a 25 caratteri.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-116">Each column is defined with a data type of VARCHAR(25), which limits the data to 25 characters.</span></span>  <span data-ttu-id="d3ee9-117">Questi e altri attributi fondamentali di una tabella sono praticamente identici a quelli di altri database.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-117">These fundamental attributes of a table, as well as others, are mostly the same as other databases.</span></span>  <span data-ttu-id="d3ee9-118">I tipi di dati vengono definiti per ogni colonna e garantiscono l'integrità dei dati.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-118">Data types are defined for each column and ensure the integrity of your data.</span></span>  <span data-ttu-id="d3ee9-119">È possibile aggiungere indici per aumentare le prestazioni riducendo l'I/O.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-119">Indexes can be added to improve performance by reducing I/O.</span></span>  <span data-ttu-id="d3ee9-120">È possibile aggiungere il partizionamento per migliorare le prestazioni quando è necessario modificare i dati.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-120">Partitioning can be added to improve performance when you need to modify data.</span></span>

<span data-ttu-id="d3ee9-121">La [ridenominazione][RENAME] di una tabella di SQL Data Warehouse sarà simile alle seguente:</span><span class="sxs-lookup"><span data-stu-id="d3ee9-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span></span>

```sql  
RENAME OBJECT Customer TO CustomerOrig; 
 ```

## <a name="distributed-tables"></a><span data-ttu-id="d3ee9-122">Tabelle con distribuzione</span><span class="sxs-lookup"><span data-stu-id="d3ee9-122">Distributed tables</span></span>
<span data-ttu-id="d3ee9-123">Un nuovo attributo fondamentale introdotto da sistemi distribuiti come SQL Data Warehouse è la **colonna di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is the **distribution column**.</span></span>  <span data-ttu-id="d3ee9-124">Il nome stesso è indicativo di cosa sia una colonna di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-124">The distribution column is very much what it sounds like.</span></span>  <span data-ttu-id="d3ee9-125">Si tratta della colonna che determina come distribuire, o dividere, i dati in background.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-125">It is the column that determines how to distribute, or divide, your data behind the scenes.</span></span>  <span data-ttu-id="d3ee9-126">Quando si crea una tabella senza specificare la colonna di distribuzione, la tabella viene automaticamente distribuita mediante **round robin**.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-126">When you create a table without specifying the distribution column, the table is automatically distributed using **round robin**.</span></span>  <span data-ttu-id="d3ee9-127">Sebbene le tabelle round robin possano essere sufficiente in alcuni scenari, definire le colonne di distribuzione può ridurre considerevolmente lo spostamento dei dati durante le query, ottimizzando così le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span></span>  <span data-ttu-id="d3ee9-128">In situazioni in cui esiste una piccola quantità di dati in una tabella, scegliendo di creare la tabella con il tipo di distribuzione di **replica** si copiano i dati in ogni nodo di calcolo e si evita di spostare i dati in fase di esecuzione della query.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-128">In situations where there is a small amount of data in a table, choosing to create the table with the **replicate** distribution type copies data to each compute node and saves data movement at query execution time.</span></span> <span data-ttu-id="d3ee9-129">Per altre informazioni su come selezionare una colonna di distribuzione, vedere [Distribuzione di una tabella][Distribute].</span><span class="sxs-lookup"><span data-stu-id="d3ee9-129">See [Distributing a Table][Distribute] to learn more about how to select a distribution column.</span></span>

## <a name="indexing-and-partitioning-tables"></a><span data-ttu-id="d3ee9-130">Indicizzazione e partizionamento delle tabelle</span><span class="sxs-lookup"><span data-stu-id="d3ee9-130">Indexing and partitioning tables</span></span>
<span data-ttu-id="d3ee9-131">Con l'acquisizione di maggiore esperienza nell'uso di SQL Data Warehouse e il desiderio di ottimizzare le prestazioni, l'utente vorrà trovare ulteriori informazioni sulla progettazione della tabella.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-131">As you become more advanced in using SQL Data Warehouse and want to optimize performance, you'll want to learn more about Table Design.</span></span>  <span data-ttu-id="d3ee9-132">Per altre informazioni, vedere gli articoli su [tipi di dati di una tabella][Data Types], [distribuzione di una tabella][Distribute], [indicizzazione di una tabella][Index] e [partizionamento di una tabella][Partition].</span><span class="sxs-lookup"><span data-stu-id="d3ee9-132">To learn more, see the articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span></span>

## <a name="table-statistics"></a><span data-ttu-id="d3ee9-133">Statistiche della tabella</span><span class="sxs-lookup"><span data-stu-id="d3ee9-133">Table statistics</span></span>
<span data-ttu-id="d3ee9-134">Le statistiche sono estremamente importanti per ottenere le migliori prestazioni da SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-134">Statistics are an extremely important to getting the best performance out of your SQL Data Warehouse.</span></span>  <span data-ttu-id="d3ee9-135">Poiché SQL Data Warehouse ancora non crea e non aggiorna automaticamente le statistiche per l'utente, come ci si potrebbe aspettare dal database SQL di Azure, l'articolo sulle [statistiche][Statistics] potrebbe essere una delle fonti più importanti da cui imparare a ottenere prestazioni ottimali dalle query.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-135">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come to expect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of the most important articles you read to ensure that you get the best performance from your queries.</span></span>

## <a name="temporary-tables"></a><span data-ttu-id="d3ee9-136">Tabelle temporanee</span><span class="sxs-lookup"><span data-stu-id="d3ee9-136">Temporary tables</span></span>
<span data-ttu-id="d3ee9-137">Le tabelle temporanee sono tabelle che esistono solo per la durata dell'accesso e che non possono essere visualizzate da altri utenti.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-137">Temporary tables are tables which only exist for the duration of your logon and cannot be seen by other users.</span></span>  <span data-ttu-id="d3ee9-138">Le tabelle temporanee possono essere un ottimo modo per impedire ad altri utenti di visualizzare i risultati temporanei e per ridurre la necessità di pulizia.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-138">Temporary tables can be a good way to prevent others from seeing temporary results and also reduce the need for cleanup.</span></span>  <span data-ttu-id="d3ee9-139">Poiché le tabelle temporanee utilizzano anche archiviazione locale, possono offrire prestazioni più veloci per alcune operazioni.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-139">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span></span>  <span data-ttu-id="d3ee9-140">Per altre informazioni sulle tabelle temporanee, vedere l'articolo [Tabelle temporanee in SQL Data Warehouse][Temporary].</span><span class="sxs-lookup"><span data-stu-id="d3ee9-140">See the [Temporary Table][Temporary] articles for more details about temporary tables.</span></span>

## <a name="external-tables"></a><span data-ttu-id="d3ee9-141">Tabelle esterne</span><span class="sxs-lookup"><span data-stu-id="d3ee9-141">External tables</span></span>
<span data-ttu-id="d3ee9-142">Le tabelle esterne, note anche come tabelle Polybase, sono tabelle in cui è possibile eseguire query da SQL Data Warehouse, ma che puntano a dati esterni da SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-142">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point to data external from SQL Data Warehouse.</span></span>  <span data-ttu-id="d3ee9-143">Ad esempio, è possibile creare una tabella esterna che punta ai file nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-143">For example, you can create an external table which points to files on Azure Blob Storage.</span></span>  <span data-ttu-id="d3ee9-144">Per altre informazioni su come creare ed eseguire query in una tabella esterna, vedere [Caricare dati con Polybase][Load data with Polybase].</span><span class="sxs-lookup"><span data-stu-id="d3ee9-144">For more details on how to create and query an external table, see [Load data with Polybase][Load data with Polybase].</span></span>  

## <a name="unsupported-table-features"></a><span data-ttu-id="d3ee9-145">Funzionalità non supportate delle tabelle</span><span class="sxs-lookup"><span data-stu-id="d3ee9-145">Unsupported table features</span></span>
<span data-ttu-id="d3ee9-146">Mentre SQL Data Warehouse contiene molte delle stesse funzionalità delle tabelle offerte da altri database, esistono alcune funzionalità che non sono ancora supportate.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-146">While SQL Data Warehouse contains many of the same table features offered by other databases, there are some features which are not yet supported.</span></span>  <span data-ttu-id="d3ee9-147">Di seguito è riportato un elenco di alcune funzionalità non ancora supportate.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-147">Below is a list of some of the table features which are not yet supported.</span></span>

| <span data-ttu-id="d3ee9-148">Funzionalità non supportate</span><span class="sxs-lookup"><span data-stu-id="d3ee9-148">Unsupported features</span></span> |
| --- |
| <span data-ttu-id="d3ee9-149">[Vincoli di tabella][Table Constraints] Primary key, Foreign key, Unique e Check</span><span class="sxs-lookup"><span data-stu-id="d3ee9-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span></span> |
| <span data-ttu-id="d3ee9-150">[Indici univoci][Unique Indexes]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-150">[Unique Indexes][Unique Indexes]</span></span> |
| <span data-ttu-id="d3ee9-151">[Colonne calcolate][Computed Columns]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-151">[Computed Columns][Computed Columns]</span></span> |
| <span data-ttu-id="d3ee9-152">[Colonne di tipo sparse][Sparse Columns]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-152">[Sparse Columns][Sparse Columns]</span></span> |
| <span data-ttu-id="d3ee9-153">[Tipi definiti dall'utente][User-Defined Types]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-153">[User-Defined Types][User-Defined Types]</span></span> |
| <span data-ttu-id="d3ee9-154">[Sequenza][Sequence]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-154">[Sequence][Sequence]</span></span> |
| <span data-ttu-id="d3ee9-155">[Trigger][Triggers]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-155">[Triggers][Triggers]</span></span> |
| <span data-ttu-id="d3ee9-156">[Viste indicizzate][Indexed Views]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-156">[Indexed Views][Indexed Views]</span></span> |
| <span data-ttu-id="d3ee9-157">[Sinonimi][Synonyms]</span><span class="sxs-lookup"><span data-stu-id="d3ee9-157">[Synonyms][Synonyms]</span></span> |

## <a name="table-size-queries"></a><span data-ttu-id="d3ee9-158">Query di dimensioni della tabella</span><span class="sxs-lookup"><span data-stu-id="d3ee9-158">Table size queries</span></span>
<span data-ttu-id="d3ee9-159">Un modo semplice per identificare lo spazio e le righe usati da una tabella in ognuna delle 60 distribuzioni consiste nell'usare [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span><span class="sxs-lookup"><span data-stu-id="d3ee9-159">One simple way to identify space and rows consumed by a table in each of the 60 distributions, is to use [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span></span>

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="d3ee9-160">Tuttavia, l'utilizzo dei comandi DBCC può essere abbastanza restrittivo.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-160">However, using DBCC commands can be quite limiting.</span></span>  <span data-ttu-id="d3ee9-161">Le viste a gestione dinamica (DMV) consentono di visualizzare molti più dettagli, nonché di fornire un controllo di gran lunga superiore sui risultati della query.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-161">Dynamic management views (DMVs) will allow you to see much more detail as well as give you much greater control over the query results.</span></span>  <span data-ttu-id="d3ee9-162">Per iniziare, creare questa vista, a cui si farà riferimento in molti esempi di questo e di altri articoli.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-162">Start by creating this view, which will be referred to by many of our examples in this and other articles.</span></span>

```sql
CREATE VIEW dbo.vTableSizes
AS
WITH base
AS
(
SELECT 
 GETDATE()                                                             AS  [execution_time]
, DB_NAME()                                                            AS  [database_name]
, s.name                                                               AS  [schema_name]
, t.name                                                               AS  [table_name]
, QUOTENAME(s.name)+'.'+QUOTENAME(t.name)                              AS  [two_part_name]
, nt.[name]                                                            AS  [node_table_name]
, ROW_NUMBER() OVER(PARTITION BY nt.[name] ORDER BY (SELECT NULL))     AS  [node_table_name_seq]
, tp.[distribution_policy_desc]                                        AS  [distribution_policy_name]
, c.[name]                                                             AS  [distribution_column]
, nt.[distribution_id]                                                 AS  [distribution_id]
, i.[type]                                                             AS  [index_type]
, i.[type_desc]                                                        AS  [index_type_desc]
, nt.[pdw_node_id]                                                     AS  [pdw_node_id]
, pn.[type]                                                            AS  [pdw_node_type]
, pn.[name]                                                            AS  [pdw_node_name]
, di.name                                                              AS  [dist_name]
, di.position                                                          AS  [dist_position]
, nps.[partition_number]                                               AS  [partition_nmbr]
, nps.[reserved_page_count]                                            AS  [reserved_space_page_count]
, nps.[reserved_page_count] - nps.[used_page_count]                    AS  [unused_space_page_count]
, nps.[in_row_data_page_count] 
    + nps.[row_overflow_used_page_count] 
    + nps.[lob_used_page_count]                                        AS  [data_space_page_count]
, nps.[reserved_page_count] 
 - (nps.[reserved_page_count] - nps.[used_page_count]) 
 - ([in_row_data_page_count] 
         + [row_overflow_used_page_count]+[lob_used_page_count])       AS  [index_space_page_count]
, nps.[row_count]                                                      AS  [row_count]
from 
    sys.schemas s
INNER JOIN sys.tables t
    ON s.[schema_id] = t.[schema_id]
INNER JOIN sys.indexes i
    ON  t.[object_id] = i.[object_id]
    AND i.[index_id] <= 1
INNER JOIN sys.pdw_table_distribution_properties tp
    ON t.[object_id] = tp.[object_id]
INNER JOIN sys.pdw_table_mappings tm
    ON t.[object_id] = tm.[object_id]
INNER JOIN sys.pdw_nodes_tables nt
    ON tm.[physical_name] = nt.[name]
INNER JOIN sys.dm_pdw_nodes pn
    ON  nt.[pdw_node_id] = pn.[pdw_node_id]
INNER JOIN sys.pdw_distributions di
    ON  nt.[distribution_id] = di.[distribution_id]
INNER JOIN sys.dm_pdw_nodes_db_partition_stats nps
    ON nt.[object_id] = nps.[object_id]
    AND nt.[pdw_node_id] = nps.[pdw_node_id]
    AND nt.[distribution_id] = nps.[distribution_id]
LEFT OUTER JOIN (select * from sys.pdw_column_distribution_properties where distribution_ordinal = 1) cdp
    ON t.[object_id] = cdp.[object_id]
LEFT OUTER JOIN sys.columns c
    ON cdp.[object_id] = c.[object_id]
    AND cdp.[column_id] = c.[column_id]
)
, size
AS
(
SELECT
   [execution_time]
,  [database_name]
,  [schema_name]
,  [table_name]
,  [two_part_name]
,  [node_table_name]
,  [node_table_name_seq]
,  [distribution_policy_name]
,  [distribution_column]
,  [distribution_id]
,  [index_type]
,  [index_type_desc]
,  [pdw_node_id]
,  [pdw_node_type]
,  [pdw_node_name]
,  [dist_name]
,  [dist_position]
,  [partition_nmbr]
,  [reserved_space_page_count]
,  [unused_space_page_count]
,  [data_space_page_count]
,  [index_space_page_count]
,  [row_count]
,  ([reserved_space_page_count] * 8.0)                                 AS [reserved_space_KB]
,  ([reserved_space_page_count] * 8.0)/1000                            AS [reserved_space_MB]
,  ([reserved_space_page_count] * 8.0)/1000000                         AS [reserved_space_GB]
,  ([reserved_space_page_count] * 8.0)/1000000000                      AS [reserved_space_TB]
,  ([unused_space_page_count]   * 8.0)                                 AS [unused_space_KB]
,  ([unused_space_page_count]   * 8.0)/1000                            AS [unused_space_MB]
,  ([unused_space_page_count]   * 8.0)/1000000                         AS [unused_space_GB]
,  ([unused_space_page_count]   * 8.0)/1000000000                      AS [unused_space_TB]
,  ([data_space_page_count]     * 8.0)                                 AS [data_space_KB]
,  ([data_space_page_count]     * 8.0)/1000                            AS [data_space_MB]
,  ([data_space_page_count]     * 8.0)/1000000                         AS [data_space_GB]
,  ([data_space_page_count]     * 8.0)/1000000000                      AS [data_space_TB]
,  ([index_space_page_count]  * 8.0)                                   AS [index_space_KB]
,  ([index_space_page_count]  * 8.0)/1000                              AS [index_space_MB]
,  ([index_space_page_count]  * 8.0)/1000000                           AS [index_space_GB]
,  ([index_space_page_count]  * 8.0)/1000000000                        AS [index_space_TB]
FROM base
)
SELECT * 
FROM size
;
```

### <a name="table-space-summary"></a><span data-ttu-id="d3ee9-163">Riepilogo dello spazio della tabella</span><span class="sxs-lookup"><span data-stu-id="d3ee9-163">Table space summary</span></span>
<span data-ttu-id="d3ee9-164">Questa query restituisce le righe e lo spazio per singola tabella.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-164">This query returns the rows and space by table.</span></span>  <span data-ttu-id="d3ee9-165">È una query molto utile per verificare quali sono le tabelle più grandi e se sono con distribuzione hash, replicata o round robin.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-165">It is a great query to see which tables are your largest tables and whether they are round robin, replicated or hash distributed.</span></span>  <span data-ttu-id="d3ee9-166">Per le tabelle con distribuzione hash viene mostrata anche la colonna di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-166">For hash distributed tables it also shows the distribution column.</span></span>  <span data-ttu-id="d3ee9-167">Nella maggior parte dei casi le tabelle più grandi devono essere con distribuzione hash e avere un indice columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="d3ee9-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span></span>

```sql
SELECT 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
,    COUNT(distinct partition_nmbr) as nbr_partitions
,    SUM(row_count)                 as table_row_count
,    SUM(reserved_space_GB)         as table_reserved_space_GB
,    SUM(data_space_GB)             as table_data_space_GB
,    SUM(index_space_GB)            as table_index_space_GB
,    SUM(unused_space_GB)           as table_unused_space_GB
FROM 
    dbo.vTableSizes
GROUP BY 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
ORDER BY
    table_reserved_space_GB desc
;
```

### <a name="table-space-by-distribution-type"></a><span data-ttu-id="d3ee9-168">Spazio della tabella per tipo di distribuzione</span><span class="sxs-lookup"><span data-stu-id="d3ee9-168">Table space by distribution type</span></span>
```sql
SELECT 
     distribution_policy_name
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY distribution_policy_name
;
```

### <a name="table-space-by-index-type"></a><span data-ttu-id="d3ee9-169">Spazio della tabella per tipo di indice</span><span class="sxs-lookup"><span data-stu-id="d3ee9-169">Table space by index type</span></span>
```sql
SELECT 
     index_type_desc
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY index_type_desc
;
```

### <a name="distribution-space-summary"></a><span data-ttu-id="d3ee9-170">Riepilogo dello spazio di distribuzione</span><span class="sxs-lookup"><span data-stu-id="d3ee9-170">Distribution space summary</span></span>
```sql
SELECT 
    distribution_id
,    SUM(row_count)                as total_node_distribution_row_count
,    SUM(reserved_space_MB)        as total_node_distribution_reserved_space_MB
,    SUM(data_space_MB)            as total_node_distribution_data_space_MB
,    SUM(index_space_MB)           as total_node_distribution_index_space_MB
,    SUM(unused_space_MB)          as total_node_distribution_unused_space_MB
FROM dbo.vTableSizes
GROUP BY     distribution_id
ORDER BY    distribution_id
;
```

## <a name="next-steps"></a><span data-ttu-id="d3ee9-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3ee9-171">Next steps</span></span>
<span data-ttu-id="d3ee9-172">Per altre informazioni, vedere gli articoli su [tipi di dati di una tabella][Data Types], [distribuzione di una tabella][Distribute], [indicizzazione di una tabella][Index], [partizionamento di una tabella][Partition], [gestione delle statistiche di una tabella][Statistics] e [tabelle temporanee][Temporary].</span><span class="sxs-lookup"><span data-stu-id="d3ee9-172">To learn more, see the articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="d3ee9-173">Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="d3ee9-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Load data with Polybase]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md

<!--MSDN references-->
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx
[DBCC PDW_SHOWSPACEUSED]: https://msdn.microsoft.com/library/mt204028.aspx
[Table Constraints]: https://msdn.microsoft.com/library/ms188066.aspx
[Computed Columns]: https://msdn.microsoft.com/library/ms186241.aspx
[Sparse Columns]: https://msdn.microsoft.com/library/cc280604.aspx
[User-Defined Types]: https://msdn.microsoft.com/library/ms131694.aspx
[Sequence]: https://msdn.microsoft.com/library/ff878091.aspx
[Triggers]: https://msdn.microsoft.com/library/ms189799.aspx
[Indexed Views]: https://msdn.microsoft.com/library/ms191432.aspx
[Synonyms]: https://msdn.microsoft.com/library/ms177544.aspx
[Unique Indexes]: https://msdn.microsoft.com/library/ms188783.aspx

<!--Other Web references-->
