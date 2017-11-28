---
title: Tabelle di partizionamento in SQL Data Warehouse | Documentazione Microsoft
description: Introduzione al partizionamento delle tabelle di SQL Data Warehouse di Azure.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 3edfd34d368228be32afef48688739639a3b03ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="3f607-103">Tabelle di partizionamento in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3f607-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="3f607-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="3f607-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="3f607-105">[Tipi di dati][Data Types]</span><span class="sxs-lookup"><span data-stu-id="3f607-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="3f607-106">[Distribuzione][Distribute]</span><span class="sxs-lookup"><span data-stu-id="3f607-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="3f607-107">[Indice][Index]</span><span class="sxs-lookup"><span data-stu-id="3f607-107">[Index][Index]</span></span>
> * <span data-ttu-id="3f607-108">[Partizione][Partition]</span><span class="sxs-lookup"><span data-stu-id="3f607-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="3f607-109">[Statistiche][Statistics]</span><span class="sxs-lookup"><span data-stu-id="3f607-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="3f607-110">[Temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="3f607-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="3f607-111">Il partizionamento è supportato in tutti i tipi di tabella di SQL Data Warehouse, tra cui columnstore cluster, indice cluster e heap.</span><span class="sxs-lookup"><span data-stu-id="3f607-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="3f607-112">Il partizionamento è supportato anche in tutti i tipi di distribuzione, sia hash che round robin.</span><span class="sxs-lookup"><span data-stu-id="3f607-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="3f607-113">Il partizionamento consente di dividere i dati in gruppi di dati più piccoli e nella maggior parte dei casi il partizionamento viene effettuato su una colonna relativa alla data.</span><span class="sxs-lookup"><span data-stu-id="3f607-113">Partitioning enables you to divide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="3f607-114">Vantaggi del partizionamento</span><span class="sxs-lookup"><span data-stu-id="3f607-114">Benefits of partitioning</span></span>
<span data-ttu-id="3f607-115">Il partizionamento può recare vantaggio alle prestazioni di query e di conservazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="3f607-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="3f607-116">Il fatto di recare vantaggio a entrambi i tipi di prestazioni o solo a uno dei due dipende dalla modalità di caricamento dei dati e dalla possibilità di usare la stessa colonna per entrambi gli scopi, poiché il partizionamento può essere eseguito solo su una colonna.</span><span class="sxs-lookup"><span data-stu-id="3f607-116">Whether it benefits both or just one is dependent on how data is loaded and whether the same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-to-loads"></a><span data-ttu-id="3f607-117">Vantaggi in termini di caricamento</span><span class="sxs-lookup"><span data-stu-id="3f607-117">Benefits to loads</span></span>
<span data-ttu-id="3f607-118">Il vantaggio principale del partizionamento in SQL Data Warehouse è aumentare l'efficienza e le prestazioni di caricamento dei dati usando l'eliminazione, il cambio e l'unione delle partizioni.</span><span class="sxs-lookup"><span data-stu-id="3f607-118">The primary benefit of partitioning in SQL Data Warehouse is improve the efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="3f607-119">Nella maggior parte dei casi viene eseguito il partizionamento dei dati in una colonna di date strettamente legata alla sequenza in cui i dati vengono caricati nel database.</span><span class="sxs-lookup"><span data-stu-id="3f607-119">In most cases data is partitioned on a date column that is closely tied to the sequence which the data is loaded to the database.</span></span>  <span data-ttu-id="3f607-120">Uno dei principali vantaggi dell'uso di partizioni per conservare i dati è che evita la registrazione delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="3f607-120">One of the greatest benefits of using partitions to maintain data it the avoidance of transaction logging.</span></span>  <span data-ttu-id="3f607-121">Mentre le semplici operazioni di inserimento, aggiornamento o eliminazione dei dati possono rappresentare l'approccio più semplice, con un po' di impegno e di ragionamento, l'uso del partizionamento durante il processo di caricamento può migliorare notevolmente le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="3f607-121">While simply inserting, updating or deleting data can be the most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="3f607-122">Il cambio di partizioni consente di rimuovere o sostituire rapidamente una sezione di tabella.</span><span class="sxs-lookup"><span data-stu-id="3f607-122">Partition switching can be used to quickly remove or replace a section of a table.</span></span>  <span data-ttu-id="3f607-123">Ad esempio, una tabella dei fatti delle vendite potrebbe contenere solo i dati relativi agli ultimi 36 mesi.</span><span class="sxs-lookup"><span data-stu-id="3f607-123">For example, a sales fact table might contain just data for the past 36 months.</span></span>  <span data-ttu-id="3f607-124">Alla fine di ogni mese, il mese dei dati di vendita meno recenti viene eliminato dalla tabella.</span><span class="sxs-lookup"><span data-stu-id="3f607-124">At the end of every month, the oldest month of sales data is deleted from the table.</span></span>  <span data-ttu-id="3f607-125">Questi dati potrebbero essere eliminati tramite un'istruzione delete per eliminare i dati relativi al mese meno recente.</span><span class="sxs-lookup"><span data-stu-id="3f607-125">This data could be deleted by using a delete statement to delete the data for the oldest month.</span></span>  <span data-ttu-id="3f607-126">Tuttavia, l'eliminazione di una grande quantità di dati riga per riga con un'istruzione delete può richiedere molto tempo e inoltre creare il rischio di transazioni di grandi dimensioni il cui rollback potrebbe richiedere molto tempo nel caso in cui qualcosa andasse storto.</span><span class="sxs-lookup"><span data-stu-id="3f607-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create the risk of large transactions which could take a long time to rollback if something goes wrong.</span></span>  <span data-ttu-id="3f607-127">Un approccio più appropriato consiste semplicemente nel rilasciare la partizione dei dati meno recente.</span><span class="sxs-lookup"><span data-stu-id="3f607-127">A more optimal approach is to simply drop the oldest partition of data.</span></span>  <span data-ttu-id="3f607-128">Nei casi in cui l'eliminazione delle singole righe arrivasse a richiedere alcune ore, l'eliminazione di un'intera partizione potrebbe richiedere pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="3f607-128">Where deleting the individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-to-queries"></a><span data-ttu-id="3f607-129">Vantaggi in termini di query</span><span class="sxs-lookup"><span data-stu-id="3f607-129">Benefits to queries</span></span>
<span data-ttu-id="3f607-130">Il partizionamento può essere usato anche per aumentare le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="3f607-130">Partitioning can also be used to improve query performance.</span></span>  <span data-ttu-id="3f607-131">Se una query applica un filtro in una colonna con partizionamento, questo può limitare l'analisi solo alle partizioni idonee che potrebbero rappresentare un sottoinsieme di dati molto più ridotto, evitando un'analisi completa della tabella.</span><span class="sxs-lookup"><span data-stu-id="3f607-131">If a query applies a filter on a partitioned column, this can limit the scan to only the qualifying partitions which may be a much smaller subset of the data, avoiding a full table scan.</span></span>  <span data-ttu-id="3f607-132">Con l'introduzione di indici columnstore cluster, i vantaggi delle prestazioni di eliminazione del predicato sono meno utili, ma in alcuni casi possono esserci vantaggi per le query.</span><span class="sxs-lookup"><span data-stu-id="3f607-132">With the introduction of clustered columnstore indexes, the predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit to queries.</span></span>  <span data-ttu-id="3f607-133">Ad esempio, se la tabella dei fatti delle vendite è suddivisa in 36 mesi tramite il campo della data di vendita, le query che filtrano la data di vendita possono ignorare la ricerca nelle partizioni che non corrispondono al filtro.</span><span class="sxs-lookup"><span data-stu-id="3f607-133">For example, if the sales fact table is partitioned into 36 months using the sales date field, then queries that filter on the sale date can skip searching in partitions that don’t match the filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="3f607-134">Indicazioni sul dimensionamento delle partizioni</span><span class="sxs-lookup"><span data-stu-id="3f607-134">Partition sizing guidance</span></span>
<span data-ttu-id="3f607-135">Mentre il partizionamento può essere usato per aumentare le prestazioni di alcuni scenari, in alcune circostanze la creazione di una tabella con **troppe** partizioni può influire negativamente sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="3f607-135">While partitioning can be used to improve performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="3f607-136">Questi problemi valgono soprattutto per le tabelle columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="3f607-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="3f607-137">Affinché il partizionamento sia utile, per un amministratore di database è importante capire quando usare il partizionamento e il numero di partizioni da creare.</span><span class="sxs-lookup"><span data-stu-id="3f607-137">For partitioning to be helpful, it is important to understand when to use partitioning and the number of partitions to create.</span></span>  <span data-ttu-id="3f607-138">Non esiste una regola assoluta che chiarisca cosa si intende per troppe partizioni, perché dipende dai dati e dal numero di partizioni caricate contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="3f607-138">There is no hard fast rule as to how many partitions are too many, it depends on your data and how many partitions you are loading to simultaneously.</span></span>  <span data-ttu-id="3f607-139">Tuttavia, come regola empirica generale, è consigliabile aggiungere alcune decine o centinaia di partizioni, non migliaia.</span><span class="sxs-lookup"><span data-stu-id="3f607-139">But as a general rule of thumb, think of adding 10s to 100s of partitions, not 1000s.</span></span>

<span data-ttu-id="3f607-140">Quando si crea il partizionamento in tabelle **columnstore cluster** , è importante tenere in considerazione il numero di righe visualizzate in ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="3f607-140">When creating partitioning on **clustered columnstore** tables, it is important to consider how many rows will land in each partition.</span></span>  <span data-ttu-id="3f607-141">Per ottenere risultati ottimali in termini di compressione e prestazioni delle tabelle columnstore cluster, è necessario almeno 1 milione di righe per distribuzione e partizione.</span><span class="sxs-lookup"><span data-stu-id="3f607-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="3f607-142">Prima della creazione delle partizioni, SQL Data Warehouse divide già ogni tabella in 60 database distribuiti.</span><span class="sxs-lookup"><span data-stu-id="3f607-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="3f607-143">Eventuali partizionamenti aggiunti a una tabella sono in più rispetto alle distribuzioni create in background.</span><span class="sxs-lookup"><span data-stu-id="3f607-143">Any partitioning added to a table is in addition to the distributions created behind the scenes.</span></span>  <span data-ttu-id="3f607-144">Utilizzando questo esempio, se la tabella dei fatti delle vendite contenesse 36 partizioni mensili e dato che SQL Data Warehouse dispone di 60 distribuzioni, la tabella dei fatti delle vendite dovrebbe contenere 60 milioni di righe al mese o 2,1 milioni di righe quando tutti i mesi sono popolati.</span><span class="sxs-lookup"><span data-stu-id="3f607-144">Using this example, if the sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then the sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="3f607-145">Se una tabella contiene un numero di righe significativamente inferiore a quello minimo consigliato per partizione, è necessario prendere in considerazione l'uso di un minor numero di partizioni per aumentare il numero di righe per partizione.</span><span class="sxs-lookup"><span data-stu-id="3f607-145">If a table contains significantly less rows than the recommended minimum number of rows per partition, consider using fewer partitions in order to make increase the number of rows per partition.</span></span>  <span data-ttu-id="3f607-146">Vedere anche l'articolo sull'[indicizzazione][Index], che include le query che possono essere eseguite in SQL Data Warehouse per valutare la qualità degli indici columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="3f607-146">Also see the [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse to assess the quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="3f607-147">Differenze di sintassi rispetto a SQL Server</span><span class="sxs-lookup"><span data-stu-id="3f607-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="3f607-148">SQL Data Warehouse introduce una definizione semplificata delle partizioni, leggermente diversa da SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3f607-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="3f607-149">Le funzioni e gli schemi di partizionamento non vengono usati in SQL Data Warehouse come in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3f607-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="3f607-150">Piuttosto, è necessario identificare la colonna partizionata e le delimitazioni.</span><span class="sxs-lookup"><span data-stu-id="3f607-150">Instead, all you need to do is identify partitioned column and the boundary points.</span></span>  <span data-ttu-id="3f607-151">Mentre la sintassi del partizionamento può essere leggermente diversa da quella di SQL Server, i concetti di base sono gli stessi.</span><span class="sxs-lookup"><span data-stu-id="3f607-151">While the syntax of partitioning may be slightly different from SQL Server, the basic concepts are the same.</span></span>  <span data-ttu-id="3f607-152">SQL Server e SQL Data Warehouse supportano una colonna di partizione per tabella, che può essere il partizionamento con intervallo.</span><span class="sxs-lookup"><span data-stu-id="3f607-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="3f607-153">Per altre informazioni sul partizionamento, vedere [Tabelle e indici partizionati][Partitioned Tables and Indexes].</span><span class="sxs-lookup"><span data-stu-id="3f607-153">To learn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="3f607-154">Il seguente esempio di istruzione [CREATE TABLE][CREATE TABLE] con partizionamento di SQL Data Warehouse esegue il partizionamento della tabella FactInternetSales nella colonna OrderDateKey:</span><span class="sxs-lookup"><span data-stu-id="3f607-154">The below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions the FactInternetSales table on the OrderDateKey column:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="3f607-155">Migrazione del partizionamento da SQL Server</span><span class="sxs-lookup"><span data-stu-id="3f607-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="3f607-156">Per eseguire la migrazione delle definizioni delle partizioni di SQL Server a SQL Data Warehouse, è necessario semplicemente:</span><span class="sxs-lookup"><span data-stu-id="3f607-156">To migrate SQL Server partition definitions to SQL Data Warehouse simply:</span></span>

* <span data-ttu-id="3f607-157">Eliminare lo [schema di partizione][partition scheme] di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3f607-157">Eliminate the SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="3f607-158">Aggiungere la definizione di [funzione di partizione][partition function] all'istruzione CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="3f607-158">Add the [partition function][partition function] definition to your CREATE TABLE.</span></span>

<span data-ttu-id="3f607-159">Se si sta migrando una tabella con partizionamento da un'istanza di SQL Server, l'SQL di seguito è utile per interrogare il numero di righe in ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="3f607-159">If you are migrating a partitioned table from a SQL Server instance the below SQL can help you to interrogate the number of rows that are in each partition.</span></span>  <span data-ttu-id="3f607-160">È necessario tenere presente che se viene usata la stessa granularità di partizionamento in SQL Data Warehouse, il numero di righe per partizione diminuirà di un fattore pari a 60.</span><span class="sxs-lookup"><span data-stu-id="3f607-160">Keep in mind that if the same partitioning granularity is used on SQL Data Warehouse, the number of rows per partition will decrease by a factor of 60.</span></span>  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a><span data-ttu-id="3f607-161">Gestione del carico di lavoro</span><span class="sxs-lookup"><span data-stu-id="3f607-161">Workload management</span></span>
<span data-ttu-id="3f607-162">Un'ultima considerazione da tenere presente nella decisione relativa alla partizione della tabella riguarda la [gestione del carico di lavoro][workload management].</span><span class="sxs-lookup"><span data-stu-id="3f607-162">One final piece consideration to factor in to the table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="3f607-163">La gestione del carico di lavoro in SQL Data Warehouse è principalmente la gestione di memoria e concorrenza.</span><span class="sxs-lookup"><span data-stu-id="3f607-163">Workload management in SQL Data Warehouse is primarily the management of memory and concurrency.</span></span>  <span data-ttu-id="3f607-164">In SQL Data Warehouse la memoria massima allocata a ogni distribuzione durante l'esecuzione della query è controllata dalle classi di risorse.</span><span class="sxs-lookup"><span data-stu-id="3f607-164">In SQL Data Warehouse the maximum memory allocated to each distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="3f607-165">In teoria le dimensioni delle partizioni devono tenere in considerazione altri fattori come la memoria necessaria per creare indici columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="3f607-165">Ideally your partitions will be sized in consideration of other factors like the memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="3f607-166">Gli indici columnstore cluster traggono importanti vantaggi quando la memoria allocata è maggiore.</span><span class="sxs-lookup"><span data-stu-id="3f607-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="3f607-167">È quindi opportuno verificare che la ricompilazione dell'indice della partizione non esaurisca la memoria.</span><span class="sxs-lookup"><span data-stu-id="3f607-167">Therefore, you will want to ensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="3f607-168">Per ottenere l'aumento della memoria disponibile per la query, è possibile passare dal ruolo predefinito, smallrc, a uno degli altri ruoli, ad esempio largerc.</span><span class="sxs-lookup"><span data-stu-id="3f607-168">Increasing the amount of memory available to your query can be achieved by switching from the default role, smallrc, to one of the other roles such as largerc.</span></span>

<span data-ttu-id="3f607-169">Le informazioni sull'allocazione di memoria per ogni distribuzione sono disponibili mediante l'esecuzione di una query sulle viste a gestione dinamica di Resource Governor.</span><span class="sxs-lookup"><span data-stu-id="3f607-169">Information on the allocation of memory per distribution is available by querying the resource governor dynamic management views.</span></span> <span data-ttu-id="3f607-170">In realtà la concessione di memoria sarà inferiore rispetto alle cifre seguenti.</span><span class="sxs-lookup"><span data-stu-id="3f607-170">In reality your memory grant will be less than the figures below.</span></span> <span data-ttu-id="3f607-171">Fornisce tuttavia un livello di indicazioni che è possibile usare durante il dimensionamento delle partizioni per le operazioni di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="3f607-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="3f607-172">Evitare se possibile di dimensionare le partizioni oltre la concessione di memoria fornita dalla classe di risorse molto grande.</span><span class="sxs-lookup"><span data-stu-id="3f607-172">Try to avoid sizing your partitions beyond the memory grant provided by the extra large resource class.</span></span> <span data-ttu-id="3f607-173">Se le partizioni aumentano oltre questa cifra, si rischia un utilizzo elevato di memoria che a sua volta determina una compressione non ottimale.</span><span class="sxs-lookup"><span data-stu-id="3f607-173">If your partitions grow beyond this figure you run the risk of memory pressure which in turn leads to less optimal compression.</span></span>

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a><span data-ttu-id="3f607-174">Cambio di partizione</span><span class="sxs-lookup"><span data-stu-id="3f607-174">Partition switching</span></span>
<span data-ttu-id="3f607-175">SQL Data Warehouse supporta la suddivisione, l'unione e il cambio di partizioni.</span><span class="sxs-lookup"><span data-stu-id="3f607-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="3f607-176">Ognuna di queste funzioni viene eseguita usando l'istruzione [ALTER TABLE][ALTER TABLE].</span><span class="sxs-lookup"><span data-stu-id="3f607-176">Each of these functions is excuted using the [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="3f607-177">Per il cambio di partizione tra due tabelle, è necessario verificare che le partizioni siano allineate sui rispettivi limiti e che le definizioni delle tabelle corrispondano.</span><span class="sxs-lookup"><span data-stu-id="3f607-177">To switch partitions between two tables you must ensure that the partitions align on their respective boundaries and that the table definitions match.</span></span> <span data-ttu-id="3f607-178">Poiché non sono disponibili vincoli CHECK per imporre l'intervallo di valori in una tabella, la tabella di origine deve contenere gli stessi limiti di partizione della tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="3f607-178">As check constraints are not available to enforce the range of values in a table the source table must contain the same partition boundaries as the target table.</span></span> <span data-ttu-id="3f607-179">In caso contrario, il cambio di partizione non riuscirà, perché i metadati della partizione non verranno sincronizzati.</span><span class="sxs-lookup"><span data-stu-id="3f607-179">If this is not the case, then the partition switch will fail as the partition metadata will not be synchronized.</span></span>

### <a name="how-to-split-a-partition-that-contains-data"></a><span data-ttu-id="3f607-180">Come suddividere una partizione che contiene dati</span><span class="sxs-lookup"><span data-stu-id="3f607-180">How to split a partition that contains data</span></span>
<span data-ttu-id="3f607-181">Il metodo più efficiente per suddividere una partizione che contiene già dati, consiste nell'usare un'istruzione `CTAS` .</span><span class="sxs-lookup"><span data-stu-id="3f607-181">The most efficient method to split a partition that already contains data is to use a `CTAS` statement.</span></span> <span data-ttu-id="3f607-182">Se la tabella partizionata è un columnstore cluster, la partizione della tabella deve essere vuota per poterla suddividere.</span><span class="sxs-lookup"><span data-stu-id="3f607-182">If the partitioned table is a clustered columnstore then the table partition must be empty before it can be split.</span></span>

<span data-ttu-id="3f607-183">Di seguito è riportato un esempio di tabella columnstore contenente una riga in ogni partizione:</span><span class="sxs-lookup"><span data-stu-id="3f607-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
    ,   [OrderDateKey]          int          NOT NULL
    ,   [CustomerKey]           int          NOT NULL
    ,   [PromotionKey]          int          NOT NULL
    ,   [SalesOrderNumber]      nvarchar(20) NOT NULL
    ,   [OrderQuantity]         smallint     NOT NULL
    ,   [UnitPrice]             money        NOT NULL
    ,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> <span data-ttu-id="3f607-184">Con la creazione dell'oggetto Statistic, si assicura una maggiore accuratezza dei metadati della tabella.</span><span class="sxs-lookup"><span data-stu-id="3f607-184">By Creating the statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="3f607-185">Se si omette la creazione di statistiche, SQL Data Warehouse userà i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="3f607-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="3f607-186">Per altre informazioni, vedere l'articolo relativo alla gestione delle [statistiche][statistics].</span><span class="sxs-lookup"><span data-stu-id="3f607-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="3f607-187">È quindi possibile eseguire una query per il conteggio delle righe usando la vista del catalogo `sys.partitions` :</span><span class="sxs-lookup"><span data-stu-id="3f607-187">We can then query for the row count using the `sys.partitions` catalog view:</span></span>

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

<span data-ttu-id="3f607-188">Se si tenta di suddividere questa tabella, verrà restituito un errore:</span><span class="sxs-lookup"><span data-stu-id="3f607-188">If we try to split this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="3f607-189">Messaggio 35346, livello 15, stato 1, riga 44 Clausola SPLIT dell'istruzione ALTER PARTITION non riuscita perché la partizione non è vuota.</span><span class="sxs-lookup"><span data-stu-id="3f607-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because the partition is not empty.</span></span>  <span data-ttu-id="3f607-190">Solo le partizioni vuote possono essere suddivise quando nella tabella è presente un indice columnstore.</span><span class="sxs-lookup"><span data-stu-id="3f607-190">Only empty partitions can be split in when a columnstore index exists on the table.</span></span> <span data-ttu-id="3f607-191">Provare a disabilitare l'indice columnstore prima di eseguire l'istruzione ALTER PARTITION, quindi ricompilare l'indice columnstore dopo il completamento di ALTER PARTITION.</span><span class="sxs-lookup"><span data-stu-id="3f607-191">Consider disabling the columnstore index before issuing the ALTER PARTITION statement, then rebuilding the columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="3f607-192">È tuttavia possibile usare `CTAS` per creare una nuova tabella per contenere i dati.</span><span class="sxs-lookup"><span data-stu-id="3f607-192">However, we can use `CTAS` to create a new table to hold our data.</span></span>

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

<span data-ttu-id="3f607-193">Poiché i limiti della partizione sono allineati, il cambio è consentito.</span><span class="sxs-lookup"><span data-stu-id="3f607-193">As the partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="3f607-194">In questo modo la tabella di origine avrà una partizione vuota che in seguito si potrà suddividere.</span><span class="sxs-lookup"><span data-stu-id="3f607-194">This will leave the source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 TO  FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="3f607-195">A questo punto è sufficiente allineare i dati ai nuovi limiti di partizione usando `CTAS` e ritrasferire i dati nella tabella principale.</span><span class="sxs-lookup"><span data-stu-id="3f607-195">All that is left to do is to align our data to the new partition boundaries using `CTAS` and switch our data back in to the main table</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 TO dbo.FactInternetSales PARTITION 2;
```

<span data-ttu-id="3f607-196">Dopo aver completato lo spostamento dei dati, è consigliabile aggiornare le statistiche nella tabella di destinazione per assicurare che riflettano accuratamente la nuova distribuzione dei dati nelle rispettive partizioni:</span><span class="sxs-lookup"><span data-stu-id="3f607-196">Once you have completed the movement of the data it is a good idea to refresh the statistics on the target table to ensure they accurately reflect the new distribution of the data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="3f607-197">Controllo del codice sorgente del partizionamento della tabella</span><span class="sxs-lookup"><span data-stu-id="3f607-197">Table partitioning source control</span></span>
<span data-ttu-id="3f607-198">Per evitare che la definizione della tabella si **stabilisca** nel sistema di controllo del codice sorgente, è possibile considerare l'approccio seguente:</span><span class="sxs-lookup"><span data-stu-id="3f607-198">To avoid your table definition from **rusting** in your source control system you may want to consider the following approach:</span></span>

1. <span data-ttu-id="3f607-199">Creare la tabella come tabella partizionata, ma senza valori di partizione.</span><span class="sxs-lookup"><span data-stu-id="3f607-199">Create the table as a partitioned table but with no partition values</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. <span data-ttu-id="3f607-200">`SPLIT` per suddividere la tabella come parte del processo di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="3f607-200">`SPLIT` the table as part of the deployment process:</span></span>

```sql
-- Create a table containing the partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over the partition boundaries and split the table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

<span data-ttu-id="3f607-201">Con questo approccio, il codice nel controllo del codice sorgente rimane statico, mentre i valori dei limiti del partizionamento possono essere dinamici, evolvendo con il warehouse nel tempo.</span><span class="sxs-lookup"><span data-stu-id="3f607-201">With this approach the code in source control remains static and the partitioning boundary values are allowed to be dynamic; evolving with the warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f607-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3f607-202">Next steps</span></span>
<span data-ttu-id="3f607-203">Per altre informazioni, vedere gli articoli su [panoramica delle tabelle][Overview], [tipi di dati delle tabelle][Data Types], [distribuzione di una tabella][Distribute], [indicizzazione di una tabella][Index], [conservazione delle statistiche delle tabelle][Statistics] e [tabelle temporanee][Temporary].</span><span class="sxs-lookup"><span data-stu-id="3f607-203">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="3f607-204">Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="3f607-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
