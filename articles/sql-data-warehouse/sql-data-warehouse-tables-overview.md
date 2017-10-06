---
title: aaaOverview delle tabelle in SQL Data Warehouse | Documenti Microsoft
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
ms.openlocfilehash: 4edabcb4b0754bf6c99c2b6b3f0c077749051d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a><span data-ttu-id="20c29-103">Panoramica delle tabelle in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="20c29-103">Overview of tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="20c29-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="20c29-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="20c29-105">[Tipi di dati][Data Types]</span><span class="sxs-lookup"><span data-stu-id="20c29-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="20c29-106">[Distribuzione][Distribute]</span><span class="sxs-lookup"><span data-stu-id="20c29-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="20c29-107">[Indice][Index]</span><span class="sxs-lookup"><span data-stu-id="20c29-107">[Index][Index]</span></span>
> * <span data-ttu-id="20c29-108">[Partizione][Partition]</span><span class="sxs-lookup"><span data-stu-id="20c29-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="20c29-109">[Statistiche][Statistics]</span><span class="sxs-lookup"><span data-stu-id="20c29-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="20c29-110">[Temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="20c29-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="20c29-111">Iniziare a creare tabelle in SQL Data Warehouse è facile.</span><span class="sxs-lookup"><span data-stu-id="20c29-111">Getting started with creating tables in SQL Data Warehouse is simple.</span></span>  <span data-ttu-id="20c29-112">Hello base [CREATE TABLE] [ CREATE TABLE] sintassi sintassi hello comuni si è probabilmente già familiarità con dall'utilizzo di altri database.</span><span class="sxs-lookup"><span data-stu-id="20c29-112">hello basic [CREATE TABLE][CREATE TABLE] syntax follows hello common syntax you are most likely already familiar with from working with other databases.</span></span>  <span data-ttu-id="20c29-113">toocreate una tabella, è sufficiente tooname la tabella, un nome delle colonne e definire i tipi di dati per ogni colonna.</span><span class="sxs-lookup"><span data-stu-id="20c29-113">toocreate a table, you simply need tooname your table, name your columns and define data types for each column.</span></span>  <span data-ttu-id="20c29-114">Se crei tabelle di altri database, questo dovrebbe essere tooyou molto familiare.</span><span class="sxs-lookup"><span data-stu-id="20c29-114">If you've create tables in other databases, this should look very familiar tooyou.</span></span>

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

<span data-ttu-id="20c29-115">Hello sopra riportato di seguito viene creata una tabella denominata Customers con due colonne, FirstName e LastName.</span><span class="sxs-lookup"><span data-stu-id="20c29-115">hello above example creates a table named Customers with two columns, FirstName and LastName.</span></span>  <span data-ttu-id="20c29-116">Ogni colonna viene definita con un tipo di dati di VARCHAR(25), che limita i caratteri di too25 hello dei dati.</span><span class="sxs-lookup"><span data-stu-id="20c29-116">Each column is defined with a data type of VARCHAR(25), which limits hello data too25 characters.</span></span>  <span data-ttu-id="20c29-117">Questi attributi fondamentali di una tabella, nonché altri, sono principalmente hello come gli altri database.</span><span class="sxs-lookup"><span data-stu-id="20c29-117">These fundamental attributes of a table, as well as others, are mostly hello same as other databases.</span></span>  <span data-ttu-id="20c29-118">Tipi di dati definiti per ogni colonna e verificare l'integrità dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="20c29-118">Data types are defined for each column and ensure hello integrity of your data.</span></span>  <span data-ttu-id="20c29-119">È possibile aggiungere indici tooimprove prestazioni riducendo i/o.</span><span class="sxs-lookup"><span data-stu-id="20c29-119">Indexes can be added tooimprove performance by reducing I/O.</span></span>  <span data-ttu-id="20c29-120">Partizionamento può essere aggiunto tooimprove prestazioni quando è necessario toomodify dati.</span><span class="sxs-lookup"><span data-stu-id="20c29-120">Partitioning can be added tooimprove performance when you need toomodify data.</span></span>

<span data-ttu-id="20c29-121">La [ridenominazione][RENAME] di una tabella di SQL Data Warehouse sarà simile alle seguente:</span><span class="sxs-lookup"><span data-stu-id="20c29-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span></span>

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a><span data-ttu-id="20c29-122">Tabelle con distribuzione</span><span class="sxs-lookup"><span data-stu-id="20c29-122">Distributed tables</span></span>
<span data-ttu-id="20c29-123">Un nuovo attributo fondamentale introdotto da sistemi distribuiti, ad esempio SQL Data Warehouse è hello **colonna distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="20c29-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is hello **distribution column**.</span></span>  <span data-ttu-id="20c29-124">colonna di distribuzione Hello è molto cosa può sembrare.</span><span class="sxs-lookup"><span data-stu-id="20c29-124">hello distribution column is very much what it sounds like.</span></span>  <span data-ttu-id="20c29-125">Si tratta di colonna hello che determina come toodistribute, o di divisione, i dati in background hello.</span><span class="sxs-lookup"><span data-stu-id="20c29-125">It is hello column that determines how toodistribute, or divide, your data behind hello scenes.</span></span>  <span data-ttu-id="20c29-126">Quando si crea una tabella senza specificare la colonna di distribuzione hello, tabella hello viene distribuita automaticamente utilizzando **round robin**.</span><span class="sxs-lookup"><span data-stu-id="20c29-126">When you create a table without specifying hello distribution column, hello table is automatically distributed using **round robin**.</span></span>  <span data-ttu-id="20c29-127">Sebbene le tabelle round robin possano essere sufficiente in alcuni scenari, definire le colonne di distribuzione può ridurre considerevolmente lo spostamento dei dati durante le query, ottimizzando così le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="20c29-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span></span>  <span data-ttu-id="20c29-128">In situazioni in cui è presente una piccola quantità di dati in una tabella, la scelta tabella hello toocreate con hello **replicare** copia del nodo di calcolo tooeach dati di tipo di distribuzione e Salva lo spostamento dei dati in fase di esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="20c29-128">In situations where there is a small amount of data in a table, choosing toocreate hello table with hello **replicate** distribution type copies data tooeach compute node and saves data movement at query execution time.</span></span> <span data-ttu-id="20c29-129">Vedere [la distribuzione di una tabella] [ Distribute] toolearn altre informazioni su come tooselect una colonna di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="20c29-129">See [Distributing a Table][Distribute] toolearn more about how tooselect a distribution column.</span></span>

## <a name="indexing-and-partitioning-tables"></a><span data-ttu-id="20c29-130">Indicizzazione e partizionamento delle tabelle</span><span class="sxs-lookup"><span data-stu-id="20c29-130">Indexing and partitioning tables</span></span>
<span data-ttu-id="20c29-131">Come si desidera toooptimize prestazioni diventano più avanzate utilizzando SQL Data Warehouse, è opportuno toolearn ulteriori informazioni sulla progettazione della tabella.</span><span class="sxs-lookup"><span data-stu-id="20c29-131">As you become more advanced in using SQL Data Warehouse and want toooptimize performance, you'll want toolearn more about Table Design.</span></span>  <span data-ttu-id="20c29-132">toolearn, vedere gli articoli di hello in [tipi di dati tabella][Data Types], [la distribuzione di una tabella][Distribute], [l'indicizzazione di una tabella] [ Index] e [il partizionamento di una tabella][Partition].</span><span class="sxs-lookup"><span data-stu-id="20c29-132">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span></span>

## <a name="table-statistics"></a><span data-ttu-id="20c29-133">Statistiche della tabella</span><span class="sxs-lookup"><span data-stu-id="20c29-133">Table statistics</span></span>
<span data-ttu-id="20c29-134">Le statistiche sono un'aspetto estremamente importante toogetting hello migliori prestazioni con il Data Warehouse di SQL.</span><span class="sxs-lookup"><span data-stu-id="20c29-134">Statistics are an extremely important toogetting hello best performance out of your SQL Data Warehouse.</span></span>  <span data-ttu-id="20c29-135">Poiché SQL Data Warehouse non è ancora automaticamente creare e aggiornare le statistiche, ad esempio, si potrebbe provenire tooexpect nel Database di SQL Azure, leggere l'articolo su [statistiche] [ Statistics] potrebbe essere uno dei hello articoli più importanti è leggere tooensure di ottenere prestazioni ottimali hello dalla query.</span><span class="sxs-lookup"><span data-stu-id="20c29-135">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come tooexpect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of hello most important articles you read tooensure that you get hello best performance from your queries.</span></span>

## <a name="temporary-tables"></a><span data-ttu-id="20c29-136">Tabelle temporanee</span><span class="sxs-lookup"><span data-stu-id="20c29-136">Temporary tables</span></span>
<span data-ttu-id="20c29-137">Tabelle temporanee sono tabelle che solo esistono per la durata di hello del sito di accesso e non possono essere visualizzate da altri utenti.</span><span class="sxs-lookup"><span data-stu-id="20c29-137">Temporary tables are tables which only exist for hello duration of your logon and cannot be seen by other users.</span></span>  <span data-ttu-id="20c29-138">Tabelle temporanee sono tooprevent un ottimo modo ad altri utenti di visualizzare i risultati temporanei e ridurre inoltre hello necessario per la pulizia.</span><span class="sxs-lookup"><span data-stu-id="20c29-138">Temporary tables can be a good way tooprevent others from seeing temporary results and also reduce hello need for cleanup.</span></span>  <span data-ttu-id="20c29-139">Poiché le tabelle temporanee utilizzano anche archiviazione locale, possono offrire prestazioni più veloci per alcune operazioni.</span><span class="sxs-lookup"><span data-stu-id="20c29-139">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span></span>  <span data-ttu-id="20c29-140">Vedere hello [tabella temporanea] [ Temporary] articoli per ulteriori informazioni sulle tabelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="20c29-140">See hello [Temporary Table][Temporary] articles for more details about temporary tables.</span></span>

## <a name="external-tables"></a><span data-ttu-id="20c29-141">Tabelle esterne</span><span class="sxs-lookup"><span data-stu-id="20c29-141">External tables</span></span>
<span data-ttu-id="20c29-142">Le tabelle esterne, noto anche come tabelle di Polybase, sono tabelle che è possibile eseguire query di SQL Data Warehouse, ma toodata punto esterno da SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="20c29-142">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point toodata external from SQL Data Warehouse.</span></span>  <span data-ttu-id="20c29-143">Ad esempio, è possibile creare una tabella esterna che toofiles punti nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="20c29-143">For example, you can create an external table which points toofiles on Azure Blob Storage.</span></span>  <span data-ttu-id="20c29-144">Per ulteriori informazioni su come toocreate e query di una tabella esterna, vedere [caricano dati con Polybase][Load data with Polybase].</span><span class="sxs-lookup"><span data-stu-id="20c29-144">For more details on how toocreate and query an external table, see [Load data with Polybase][Load data with Polybase].</span></span>  

## <a name="unsupported-table-features"></a><span data-ttu-id="20c29-145">Funzionalità non supportate delle tabelle</span><span class="sxs-lookup"><span data-stu-id="20c29-145">Unsupported table features</span></span>
<span data-ttu-id="20c29-146">Benché SQL Data Warehouse contiene molte delle stesse funzionalità di tabella offerti da altri database hello, sono disponibili alcune funzionalità che non sono ancora supportati.</span><span class="sxs-lookup"><span data-stu-id="20c29-146">While SQL Data Warehouse contains many of hello same table features offered by other databases, there are some features which are not yet supported.</span></span>  <span data-ttu-id="20c29-147">Di seguito è un elenco di alcune delle hello caratteristiche della tabella che non sono ancora supportati.</span><span class="sxs-lookup"><span data-stu-id="20c29-147">Below is a list of some of hello table features which are not yet supported.</span></span>

| <span data-ttu-id="20c29-148">Funzionalità non supportate</span><span class="sxs-lookup"><span data-stu-id="20c29-148">Unsupported features</span></span> |
| --- |
| <span data-ttu-id="20c29-149">[Vincoli di tabella][Table Constraints] Primary key, Foreign key, Unique e Check</span><span class="sxs-lookup"><span data-stu-id="20c29-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span></span> |
| <span data-ttu-id="20c29-150">[Indici univoci][Unique Indexes]</span><span class="sxs-lookup"><span data-stu-id="20c29-150">[Unique Indexes][Unique Indexes]</span></span> |
| <span data-ttu-id="20c29-151">[Colonne calcolate][Computed Columns]</span><span class="sxs-lookup"><span data-stu-id="20c29-151">[Computed Columns][Computed Columns]</span></span> |
| <span data-ttu-id="20c29-152">[Colonne di tipo sparse][Sparse Columns]</span><span class="sxs-lookup"><span data-stu-id="20c29-152">[Sparse Columns][Sparse Columns]</span></span> |
| <span data-ttu-id="20c29-153">[Tipi definiti dall'utente][User-Defined Types]</span><span class="sxs-lookup"><span data-stu-id="20c29-153">[User-Defined Types][User-Defined Types]</span></span> |
| <span data-ttu-id="20c29-154">[Sequenza][Sequence]</span><span class="sxs-lookup"><span data-stu-id="20c29-154">[Sequence][Sequence]</span></span> |
| <span data-ttu-id="20c29-155">[Trigger][Triggers]</span><span class="sxs-lookup"><span data-stu-id="20c29-155">[Triggers][Triggers]</span></span> |
| <span data-ttu-id="20c29-156">[Viste indicizzate][Indexed Views]</span><span class="sxs-lookup"><span data-stu-id="20c29-156">[Indexed Views][Indexed Views]</span></span> |
| <span data-ttu-id="20c29-157">[Sinonimi][Synonyms]</span><span class="sxs-lookup"><span data-stu-id="20c29-157">[Synonyms][Synonyms]</span></span> |

## <a name="table-size-queries"></a><span data-ttu-id="20c29-158">Query di dimensioni della tabella</span><span class="sxs-lookup"><span data-stu-id="20c29-158">Table size queries</span></span>
<span data-ttu-id="20c29-159">Uno spazio tooidentify in modo semplice e utilizzate da una tabella in ognuno dei tipi di distribuzione, hello 60 righe è toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span><span class="sxs-lookup"><span data-stu-id="20c29-159">One simple way tooidentify space and rows consumed by a table in each of hello 60 distributions, is toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span></span>

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="20c29-160">Tuttavia, l'utilizzo dei comandi DBCC può essere abbastanza restrittivo.</span><span class="sxs-lookup"><span data-stu-id="20c29-160">However, using DBCC commands can be quite limiting.</span></span>  <span data-ttu-id="20c29-161">Viste a gestione dinamica (DMV) consentirà toosee molto più in dettaglio come offrono molto maggiore controllo sui risultati di query hello.</span><span class="sxs-lookup"><span data-stu-id="20c29-161">Dynamic management views (DMVs) will allow you toosee much more detail as well as give you much greater control over hello query results.</span></span>  <span data-ttu-id="20c29-162">Avviare la creazione di questa visualizzazione, che sarà tooby cui molti degli esempi in questo e altri articoli.</span><span class="sxs-lookup"><span data-stu-id="20c29-162">Start by creating this view, which will be referred tooby many of our examples in this and other articles.</span></span>

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

### <a name="table-space-summary"></a><span data-ttu-id="20c29-163">Riepilogo dello spazio della tabella</span><span class="sxs-lookup"><span data-stu-id="20c29-163">Table space summary</span></span>
<span data-ttu-id="20c29-164">Questa query restituisce righe hello e lo spazio dalla tabella.</span><span class="sxs-lookup"><span data-stu-id="20c29-164">This query returns hello rows and space by table.</span></span>  <span data-ttu-id="20c29-165">È un toosee grande query le tabelle sono le tabelle più grandi e se sono round robin, replicati o distribuiti hash.</span><span class="sxs-lookup"><span data-stu-id="20c29-165">It is a great query toosee which tables are your largest tables and whether they are round robin, replicated or hash distributed.</span></span>  <span data-ttu-id="20c29-166">Per le tabelle hash distribuita Mostra anche la colonna di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="20c29-166">For hash distributed tables it also shows hello distribution column.</span></span>  <span data-ttu-id="20c29-167">Nella maggior parte dei casi le tabelle più grandi devono essere con distribuzione hash e avere un indice columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="20c29-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span></span>

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

### <a name="table-space-by-distribution-type"></a><span data-ttu-id="20c29-168">Spazio della tabella per tipo di distribuzione</span><span class="sxs-lookup"><span data-stu-id="20c29-168">Table space by distribution type</span></span>
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

### <a name="table-space-by-index-type"></a><span data-ttu-id="20c29-169">Spazio della tabella per tipo di indice</span><span class="sxs-lookup"><span data-stu-id="20c29-169">Table space by index type</span></span>
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

### <a name="distribution-space-summary"></a><span data-ttu-id="20c29-170">Riepilogo dello spazio di distribuzione</span><span class="sxs-lookup"><span data-stu-id="20c29-170">Distribution space summary</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="20c29-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20c29-171">Next steps</span></span>
<span data-ttu-id="20c29-172">toolearn, vedere gli articoli di hello in [tipi di dati tabella][Data Types], [la distribuzione di una tabella][Distribute], [l'indicizzazione di una tabella] [ Index], [Il partizionamento di una tabella][Partition], [gestione delle statistiche sulla tabella] [ Statistics] e [ Tabelle temporanee][Temporary].</span><span class="sxs-lookup"><span data-stu-id="20c29-172">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="20c29-173">Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="20c29-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
