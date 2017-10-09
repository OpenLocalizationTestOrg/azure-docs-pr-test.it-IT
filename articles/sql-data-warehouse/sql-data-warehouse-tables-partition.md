---
title: aaaPartitioning nelle tabelle SQL Data Warehouse | Documenti Microsoft
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
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="b8380-103">Tabelle di partizionamento in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b8380-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="b8380-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="b8380-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="b8380-105">[Tipi di dati][Data Types]</span><span class="sxs-lookup"><span data-stu-id="b8380-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="b8380-106">[Distribuzione][Distribute]</span><span class="sxs-lookup"><span data-stu-id="b8380-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="b8380-107">[Indice][Index]</span><span class="sxs-lookup"><span data-stu-id="b8380-107">[Index][Index]</span></span>
> * <span data-ttu-id="b8380-108">[Partizione][Partition]</span><span class="sxs-lookup"><span data-stu-id="b8380-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="b8380-109">[Statistiche][Statistics]</span><span class="sxs-lookup"><span data-stu-id="b8380-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="b8380-110">[Temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="b8380-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="b8380-111">Il partizionamento è supportato in tutti i tipi di tabella di SQL Data Warehouse, tra cui columnstore cluster, indice cluster e heap.</span><span class="sxs-lookup"><span data-stu-id="b8380-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="b8380-112">Il partizionamento è supportato anche in tutti i tipi di distribuzione, sia hash che round robin.</span><span class="sxs-lookup"><span data-stu-id="b8380-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="b8380-113">Partizionamento consente toodivide i dati in gruppi più piccoli dei dati e nella maggior parte dei casi, il partizionamento viene effettuati su una colonna di date.</span><span class="sxs-lookup"><span data-stu-id="b8380-113">Partitioning enables you toodivide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="b8380-114">Vantaggi del partizionamento</span><span class="sxs-lookup"><span data-stu-id="b8380-114">Benefits of partitioning</span></span>
<span data-ttu-id="b8380-115">Il partizionamento può recare vantaggio alle prestazioni di query e di conservazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="b8380-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="b8380-116">Se si avvantaggia entrambi o solo uno è dipendono dalla modalità di caricamento di dati e se hello stessa colonna può essere utilizzata per entrambi gli scopi, poiché il partizionamento può essere eseguito solo in una colonna.</span><span class="sxs-lookup"><span data-stu-id="b8380-116">Whether it benefits both or just one is dependent on how data is loaded and whether hello same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-tooloads"></a><span data-ttu-id="b8380-117">Vantaggi tooloads</span><span class="sxs-lookup"><span data-stu-id="b8380-117">Benefits tooloads</span></span>
<span data-ttu-id="b8380-118">Il vantaggio principale Hello di partizionamento in SQL Data Warehouse è migliorare hello efficienza e prestazioni di caricamento dati da utilizzare dell'eliminazione di una partizione, passaggio e unione.</span><span class="sxs-lookup"><span data-stu-id="b8380-118">hello primary benefit of partitioning in SQL Data Warehouse is improve hello efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="b8380-119">Nella maggior parte dei casi i dati sono partizionati in una data colonna che è strettamente legata sequenza toohello quali dati hello sono caricato toohello database.</span><span class="sxs-lookup"><span data-stu-id="b8380-119">In most cases data is partitioned on a date column that is closely tied toohello sequence which hello data is loaded toohello database.</span></span>  <span data-ttu-id="b8380-120">Uno dei principali vantaggi di hello dell'utilizzo di partizioni toomaintain dati hello prevenzione di registrazione delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="b8380-120">One of hello greatest benefits of using partitions toomaintain data it hello avoidance of transaction logging.</span></span>  <span data-ttu-id="b8380-121">Mentre semplicemente l'inserimento, aggiornamento o eliminazione di dati può essere l'approccio più semplice di hello, con una piccola pensiero e impegno, tramite il partizionamento durante il processo di caricamento può migliorare notevolmente le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b8380-121">While simply inserting, updating or deleting data can be hello most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="b8380-122">Cambio della partizione, è possibile rimuovere tooquickly usato o sostituire una sezione di una tabella.</span><span class="sxs-lookup"><span data-stu-id="b8380-122">Partition switching can be used tooquickly remove or replace a section of a table.</span></span>  <span data-ttu-id="b8380-123">Ad esempio, una tabella dei fatti vendite potrebbe contenere solo i dati per hello ultimi 36 mesi.</span><span class="sxs-lookup"><span data-stu-id="b8380-123">For example, a sales fact table might contain just data for hello past 36 months.</span></span>  <span data-ttu-id="b8380-124">Alla fine di hello di ogni mese, hello mese meno recente dei dati di vendita viene eliminato dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="b8380-124">At hello end of every month, hello oldest month of sales data is deleted from hello table.</span></span>  <span data-ttu-id="b8380-125">È stato possibile eliminare i dati utilizzando una data di hello toodelete istruzione delete per hello mese meno recente.</span><span class="sxs-lookup"><span data-stu-id="b8380-125">This data could be deleted by using a delete statement toodelete hello data for hello oldest month.</span></span>  <span data-ttu-id="b8380-126">Tuttavia, l'eliminazione di una grande quantità di dati riga per riga con un'istruzione delete può richiedere molto tempo, nonché creare rischio hello di transazioni di grandi dimensioni può richiedere un toorollback molto tempo se si verificano problemi.</span><span class="sxs-lookup"><span data-stu-id="b8380-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create hello risk of large transactions which could take a long time toorollback if something goes wrong.</span></span>  <span data-ttu-id="b8380-127">Un approccio più appropriato è toosimply partizione meno recente hello rilascio dei dati.</span><span class="sxs-lookup"><span data-stu-id="b8380-127">A more optimal approach is toosimply drop hello oldest partition of data.</span></span>  <span data-ttu-id="b8380-128">In cui le singole righe hello di eliminazione potrebbe richiedere ore, l'eliminazione di un'intera partizione potrebbe richiedere secondi.</span><span class="sxs-lookup"><span data-stu-id="b8380-128">Where deleting hello individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-tooqueries"></a><span data-ttu-id="b8380-129">Vantaggi tooqueries</span><span class="sxs-lookup"><span data-stu-id="b8380-129">Benefits tooqueries</span></span>
<span data-ttu-id="b8380-130">Partizionamento può essere anche usato tooimprove le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="b8380-130">Partitioning can also be used tooimprove query performance.</span></span>  <span data-ttu-id="b8380-131">Se una query che applica un filtro in una colonna di partizionamento, si può limitare hello tooonly di analisi hello qualificazione di partizioni che possono essere un subset molto più piccolo di dati di hello, evitando un'analisi completa della tabella.</span><span class="sxs-lookup"><span data-stu-id="b8380-131">If a query applies a filter on a partitioned column, this can limit hello scan tooonly hello qualifying partitions which may be a much smaller subset of hello data, avoiding a full table scan.</span></span>  <span data-ttu-id="b8380-132">Con l'introduzione di hello degli indici columnstore cluster, prestazioni hello come predicato di eliminazione sono meno utile, ma in alcuni casi può essere tooqueries un vantaggio.</span><span class="sxs-lookup"><span data-stu-id="b8380-132">With hello introduction of clustered columnstore indexes, hello predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit tooqueries.</span></span>  <span data-ttu-id="b8380-133">Ad esempio, se nella tabella dei fatti di vendita hello è suddiviso in mesi 36 mediante il campo di data di vendita hello, quindi query per filtrare nella data di vendita hello possibile ignorare la ricerca in partizioni che non corrispondono a filtro hello.</span><span class="sxs-lookup"><span data-stu-id="b8380-133">For example, if hello sales fact table is partitioned into 36 months using hello sales date field, then queries that filter on hello sale date can skip searching in partitions that don’t match hello filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="b8380-134">Indicazioni sul dimensionamento delle partizioni</span><span class="sxs-lookup"><span data-stu-id="b8380-134">Partition sizing guidance</span></span>
<span data-ttu-id="b8380-135">Durante il partizionamento possono essere utilizzato tooimprove prestazioni alcuni scenari, la creazione di una tabella con **troppi** partizioni possono influire negativamente sulle prestazioni in alcune circostanze.</span><span class="sxs-lookup"><span data-stu-id="b8380-135">While partitioning can be used tooimprove performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="b8380-136">Questi problemi valgono soprattutto per le tabelle columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="b8380-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="b8380-137">Per il partizionamento toobe utile, è importante toounderstand quando toouse partizionamento e hello il numero di partizioni toocreate.</span><span class="sxs-lookup"><span data-stu-id="b8380-137">For partitioning toobe helpful, it is important toounderstand when toouse partitioning and hello number of partitions toocreate.</span></span>  <span data-ttu-id="b8380-138">Vi è alcuna regola disco rigido veloce come toohow molte partizioni sono troppi, dipende dai dati e il numero di partizioni si sta caricando toosimultaneously.</span><span class="sxs-lookup"><span data-stu-id="b8380-138">There is no hard fast rule as toohow many partitions are too many, it depends on your data and how many partitions you are loading toosimultaneously.</span></span>  <span data-ttu-id="b8380-139">Ma come una regola empirica generale, considerare l'aggiunta di 10s too100s di partizioni, non 1000s.</span><span class="sxs-lookup"><span data-stu-id="b8380-139">But as a general rule of thumb, think of adding 10s too100s of partitions, not 1000s.</span></span>

<span data-ttu-id="b8380-140">Durante la creazione di partizionamento in **columnstore cluster** tabelle, è importante tooconsider quante righe verranno inserite in ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="b8380-140">When creating partitioning on **clustered columnstore** tables, it is important tooconsider how many rows will land in each partition.</span></span>  <span data-ttu-id="b8380-141">Per ottenere risultati ottimali in termini di compressione e prestazioni delle tabelle columnstore cluster, è necessario almeno 1 milione di righe per distribuzione e partizione.</span><span class="sxs-lookup"><span data-stu-id="b8380-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="b8380-142">Prima della creazione delle partizioni, SQL Data Warehouse divide già ogni tabella in 60 database distribuiti.</span><span class="sxs-lookup"><span data-stu-id="b8380-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="b8380-143">Qualsiasi tabella aggiunta tooa partizionamento è inoltre distribuzioni toohello create background hello.</span><span class="sxs-lookup"><span data-stu-id="b8380-143">Any partitioning added tooa table is in addition toohello distributions created behind hello scenes.</span></span>  <span data-ttu-id="b8380-144">Utilizzo di questo esempio, se nella tabella dei fatti di vendita hello contenuto 36 partizioni mensili e dato che SQL Data Warehouse è 60 distribuzioni, quindi hello dei fatti di vendita nella tabella deve contenere 60 milioni di righe al mese o 2.1 miliardi di righe quando vengono popolati tutti i mesi.</span><span class="sxs-lookup"><span data-stu-id="b8380-144">Using this example, if hello sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then hello sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="b8380-145">Se una tabella contiene molto meno righe rispetto al hello consigliato numero minimo di righe per partizione, utilizzare un minor numero di partizioni in ordine toomake aumento hello numerose righe per partizione.</span><span class="sxs-lookup"><span data-stu-id="b8380-145">If a table contains significantly less rows than hello recommended minimum number of rows per partition, consider using fewer partitions in order toomake increase hello number of rows per partition.</span></span>  <span data-ttu-id="b8380-146">Vedere anche hello [indicizzazione] [ Index] articolo che include le query che possono essere eseguite in qualità di hello tooassess SQL Data Warehouse di indici columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="b8380-146">Also see hello [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse tooassess hello quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="b8380-147">Differenze di sintassi rispetto a SQL Server</span><span class="sxs-lookup"><span data-stu-id="b8380-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="b8380-148">SQL Data Warehouse introduce una definizione semplificata delle partizioni, leggermente diversa da SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b8380-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="b8380-149">Le funzioni e gli schemi di partizionamento non vengono usati in SQL Data Warehouse come in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b8380-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="b8380-150">Invece, è sufficiente toodo è identificare i punti di limite di colonna e hello partizionati.</span><span class="sxs-lookup"><span data-stu-id="b8380-150">Instead, all you need toodo is identify partitioned column and hello boundary points.</span></span>  <span data-ttu-id="b8380-151">Sintassi di hello di partizionamento può essere leggermente diversa da SQL Server, i concetti di base hello sono hello stesso.</span><span class="sxs-lookup"><span data-stu-id="b8380-151">While hello syntax of partitioning may be slightly different from SQL Server, hello basic concepts are hello same.</span></span>  <span data-ttu-id="b8380-152">SQL Server e SQL Data Warehouse supportano una colonna di partizione per tabella, che può essere il partizionamento con intervallo.</span><span class="sxs-lookup"><span data-stu-id="b8380-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="b8380-153">toolearn più informazioni sul partizionamento, vedere [tabelle e indici partizionati][Partitioned Tables and Indexes].</span><span class="sxs-lookup"><span data-stu-id="b8380-153">toolearn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="b8380-154">Hello di sotto di esempio di un Data Warehouse di SQL partizionato [CREATE TABLE] [ CREATE TABLE] istruzione, le partizioni nella tabella FactInternetSales hello nella colonna OrderDateKey hello:</span><span class="sxs-lookup"><span data-stu-id="b8380-154">hello below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions hello FactInternetSales table on hello OrderDateKey column:</span></span>

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

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="b8380-155">Migrazione del partizionamento da SQL Server</span><span class="sxs-lookup"><span data-stu-id="b8380-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="b8380-156">definizioni tooSQL Data Warehouse di partizione semplicemente toomigrate SQL Server:</span><span class="sxs-lookup"><span data-stu-id="b8380-156">toomigrate SQL Server partition definitions tooSQL Data Warehouse simply:</span></span>

* <span data-ttu-id="b8380-157">Eliminare il Server SQL hello [lo schema di partizione][partition scheme].</span><span class="sxs-lookup"><span data-stu-id="b8380-157">Eliminate hello SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="b8380-158">Aggiungere hello [funzione di partizione] [ partition function] tooyour definizione creazione tabella.</span><span class="sxs-lookup"><span data-stu-id="b8380-158">Add hello [partition function][partition function] definition tooyour CREATE TABLE.</span></span>

<span data-ttu-id="b8380-159">Se si esegue la migrazione di una tabella partizionata da un hello di istanza di SQL Server di sotto di SQL consentono numero hello toointerrogate di righe in ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="b8380-159">If you are migrating a partitioned table from a SQL Server instance hello below SQL can help you toointerrogate hello number of rows that are in each partition.</span></span>  <span data-ttu-id="b8380-160">Tenere presente che se hello stessa granularità di partizionamento viene utilizzata in SQL Data Warehouse, il numero di hello di righe per partizione comporterà la riduzione di un fattore di 60.</span><span class="sxs-lookup"><span data-stu-id="b8380-160">Keep in mind that if hello same partitioning granularity is used on SQL Data Warehouse, hello number of rows per partition will decrease by a factor of 60.</span></span>  

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

## <a name="workload-management"></a><span data-ttu-id="b8380-161">Gestione del carico di lavoro</span><span class="sxs-lookup"><span data-stu-id="b8380-161">Workload management</span></span>
<span data-ttu-id="b8380-162">È un toofactor di considerazione finale nella decisione di partizione di tabella toohello [del carico di lavoro][workload management].</span><span class="sxs-lookup"><span data-stu-id="b8380-162">One final piece consideration toofactor in toohello table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="b8380-163">Gestione del carico di lavoro in SQL Data Warehouse è principalmente la gestione di hello di memoria e concorrenza.</span><span class="sxs-lookup"><span data-stu-id="b8380-163">Workload management in SQL Data Warehouse is primarily hello management of memory and concurrency.</span></span>  <span data-ttu-id="b8380-164">In hello SQL Data Warehouse memoria massima allocata tooeach distribuzione durante l'esecuzione di query è classi di risorse gestite.</span><span class="sxs-lookup"><span data-stu-id="b8380-164">In SQL Data Warehouse hello maximum memory allocated tooeach distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="b8380-165">In teoria le partizioni verranno ridimensionate in considerazione altri fattori quali i requisiti di memoria hello della compilazione degli indici columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="b8380-165">Ideally your partitions will be sized in consideration of other factors like hello memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="b8380-166">Gli indici columnstore cluster traggono importanti vantaggi quando la memoria allocata è maggiore.</span><span class="sxs-lookup"><span data-stu-id="b8380-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="b8380-167">Pertanto, si desidererà tooensure che ricompila un indice di partizione non richieda ulteriori di memoria.</span><span class="sxs-lookup"><span data-stu-id="b8380-167">Therefore, you will want tooensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="b8380-168">Aumento hello quantità di memoria disponibile tooyour query può essere ottenuto passaggio dal ruolo predefinito di hello, smallrc, tooone di hello altri ruoli, ad esempio largerc.</span><span class="sxs-lookup"><span data-stu-id="b8380-168">Increasing hello amount of memory available tooyour query can be achieved by switching from hello default role, smallrc, tooone of hello other roles such as largerc.</span></span>

<span data-ttu-id="b8380-169">Eseguendo una query su viste a gestione dinamica hello resource governor sono disponibili informazioni sull'allocazione di hello di memoria per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b8380-169">Information on hello allocation of memory per distribution is available by querying hello resource governor dynamic management views.</span></span> <span data-ttu-id="b8380-170">In realtà la concessione di memoria sarà minore di nelle figure hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="b8380-170">In reality your memory grant will be less than hello figures below.</span></span> <span data-ttu-id="b8380-171">Fornisce tuttavia un livello di indicazioni che è possibile usare durante il dimensionamento delle partizioni per le operazioni di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="b8380-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="b8380-172">Provare a tooavoid partizioni oltre hello concessione di memoria fornito dalla classe di risorse molto grande hello di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b8380-172">Try tooavoid sizing your partitions beyond hello memory grant provided by hello extra large resource class.</span></span> <span data-ttu-id="b8380-173">Se le partizioni di crescere oltre questo valore si corre il rischio di hello pressione della memoria che a sua volta comporta la compressione ottimale tooless.</span><span class="sxs-lookup"><span data-stu-id="b8380-173">If your partitions grow beyond this figure you run hello risk of memory pressure which in turn leads tooless optimal compression.</span></span>

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

## <a name="partition-switching"></a><span data-ttu-id="b8380-174">Cambio di partizione</span><span class="sxs-lookup"><span data-stu-id="b8380-174">Partition switching</span></span>
<span data-ttu-id="b8380-175">SQL Data Warehouse supporta la suddivisione, l'unione e il cambio di partizioni.</span><span class="sxs-lookup"><span data-stu-id="b8380-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="b8380-176">Ognuna di queste funzioni è excuted utilizzando hello [ALTER TABLE] [ ALTER TABLE] istruzione.</span><span class="sxs-lookup"><span data-stu-id="b8380-176">Each of these functions is excuted using hello [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="b8380-177">partizioni tooswitch tra due tabelle, che è necessario assicurarsi che le partizioni hello allineate sui loro rispettivi limiti e che le definizioni di tabella hello corrispondano.</span><span class="sxs-lookup"><span data-stu-id="b8380-177">tooswitch partitions between two tables you must ensure that hello partitions align on their respective boundaries and that hello table definitions match.</span></span> <span data-ttu-id="b8380-178">Come i vincoli check non sono disponibili intervallo hello tooenforce di valori in una tabella di origine di tabella hello deve contenere hello stessi limiti di partizione come tabella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="b8380-178">As check constraints are not available tooenforce hello range of values in a table hello source table must contain hello same partition boundaries as hello target table.</span></span> <span data-ttu-id="b8380-179">In caso non hello, quindi il cambio di partizione hello avrà esito negativo non verranno quindi sincronizzati i metadati della partizione hello.</span><span class="sxs-lookup"><span data-stu-id="b8380-179">If this is not hello case, then hello partition switch will fail as hello partition metadata will not be synchronized.</span></span>

### <a name="how-toosplit-a-partition-that-contains-data"></a><span data-ttu-id="b8380-180">Come toosplit una partizione contenente dati</span><span class="sxs-lookup"><span data-stu-id="b8380-180">How toosplit a partition that contains data</span></span>
<span data-ttu-id="b8380-181">più efficiente metodo toosplit una partizione che contiene già dati Hello è toouse un `CTAS` istruzione.</span><span class="sxs-lookup"><span data-stu-id="b8380-181">hello most efficient method toosplit a partition that already contains data is toouse a `CTAS` statement.</span></span> <span data-ttu-id="b8380-182">Se la tabella partizionata hello è un indice columnstore cluster quindi hello tabella partizione deve essere vuota prima che possa essere suddiviso.</span><span class="sxs-lookup"><span data-stu-id="b8380-182">If hello partitioned table is a clustered columnstore then hello table partition must be empty before it can be split.</span></span>

<span data-ttu-id="b8380-183">Di seguito è riportato un esempio di tabella columnstore contenente una riga in ogni partizione:</span><span class="sxs-lookup"><span data-stu-id="b8380-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

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
> <span data-ttu-id="b8380-184">Creazione dell'oggetto statistic hello è di assicurare che i metadati di tabella sono più accurato.</span><span class="sxs-lookup"><span data-stu-id="b8380-184">By Creating hello statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="b8380-185">Se si omette la creazione di statistiche, SQL Data Warehouse userà i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="b8380-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="b8380-186">Per altre informazioni, vedere l'articolo relativo alla gestione delle [statistiche][statistics].</span><span class="sxs-lookup"><span data-stu-id="b8380-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="b8380-187">È quindi possibile eseguire una query per il numero di riga hello utilizzando hello `sys.partitions` vista del catalogo:</span><span class="sxs-lookup"><span data-stu-id="b8380-187">We can then query for hello row count using hello `sys.partitions` catalog view:</span></span>

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

<span data-ttu-id="b8380-188">Se si tenta di toosplit questa tabella, si otterrà un errore:</span><span class="sxs-lookup"><span data-stu-id="b8380-188">If we try toosplit this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="b8380-189">Msg 35346, livello 15, stato 1, riga 44 divisa clausola dell'istruzione ALTER PARTITION non riuscita perché la partizione hello non è vuota.</span><span class="sxs-lookup"><span data-stu-id="b8380-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because hello partition is not empty.</span></span>  <span data-ttu-id="b8380-190">Solo partizioni vuote possono essere suddivise presenza di un indice columnstore sulla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="b8380-190">Only empty partitions can be split in when a columnstore index exists on hello table.</span></span> <span data-ttu-id="b8380-191">Provare a disabilitare l'indice columnstore hello prima di eseguire l'istruzione ALTER PARTITION hello, quindi ricompilare l'indice columnstore hello al termine dell'istruzione ALTER PARTITION.</span><span class="sxs-lookup"><span data-stu-id="b8380-191">Consider disabling hello columnstore index before issuing hello ALTER PARTITION statement, then rebuilding hello columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="b8380-192">Tuttavia, è possibile utilizzare `CTAS` toocreate un nuovo toohold tabella dati.</span><span class="sxs-lookup"><span data-stu-id="b8380-192">However, we can use `CTAS` toocreate a new table toohold our data.</span></span>

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

<span data-ttu-id="b8380-193">Come vengono allineati dei limiti delle partizioni hello è consentito un commutatore.</span><span class="sxs-lookup"><span data-stu-id="b8380-193">As hello partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="b8380-194">Tabella di origine hello questo lascerà con una partizione vuota che è possibile successivamente divisa.</span><span class="sxs-lookup"><span data-stu-id="b8380-194">This will leave hello source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="b8380-195">Tutto ciò che viene lasciato toodo è tooalign toohello i dati di partizione nuovi limiti utilizzando `CTAS` e passare i dati nella tabella principale toohello</span><span class="sxs-lookup"><span data-stu-id="b8380-195">All that is left toodo is tooalign our data toohello new partition boundaries using `CTAS` and switch our data back in toohello main table</span></span>

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

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

<span data-ttu-id="b8380-196">Dopo aver completato lo spostamento di hello dei dati hello è statistiche buona toorefresh hello in tooensure tabella di destinazione hello che indichino nuova distribuzione di hello dei dati di hello in partizioni i rispettivi:</span><span class="sxs-lookup"><span data-stu-id="b8380-196">Once you have completed hello movement of hello data it is a good idea toorefresh hello statistics on hello target table tooensure they accurately reflect hello new distribution of hello data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="b8380-197">Controllo del codice sorgente del partizionamento della tabella</span><span class="sxs-lookup"><span data-stu-id="b8380-197">Table partitioning source control</span></span>
<span data-ttu-id="b8380-198">tooavoid la definizione della tabella da **rusting** nel sistema di controllo del codice sorgente è hello tooconsider approccio:</span><span class="sxs-lookup"><span data-stu-id="b8380-198">tooavoid your table definition from **rusting** in your source control system you may want tooconsider hello following approach:</span></span>

1. <span data-ttu-id="b8380-199">Creare la tabella hello come una tabella partizionata, ma senza valori di partizione</span><span class="sxs-lookup"><span data-stu-id="b8380-199">Create hello table as a partitioned table but with no partition values</span></span>

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

1. <span data-ttu-id="b8380-200">`SPLIT`tabella Hello come parte del processo di distribuzione hello:</span><span class="sxs-lookup"><span data-stu-id="b8380-200">`SPLIT` hello table as part of hello deployment process:</span></span>

```sql
-- Create a table containing hello partition boundaries

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

-- Iterate over hello partition boundaries and split hello table

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

<span data-ttu-id="b8380-201">Con questo hello approccio rimane statico codice nel controllo del codice sorgente e hello partizionamento sono consentiti limiti toobe dinamico; evoluzione con warehouse hello nel tempo.</span><span class="sxs-lookup"><span data-stu-id="b8380-201">With this approach hello code in source control remains static and hello partitioning boundary values are allowed toobe dynamic; evolving with hello warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8380-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8380-202">Next steps</span></span>
<span data-ttu-id="b8380-203">toolearn, vedere gli articoli di hello in [Cenni preliminari su tabella][Overview], [tipi di dati tabella][Data Types], [la distribuzione di una tabella] [ Distribute], [L'indicizzazione di una tabella][Index], [gestione delle statistiche sulla tabella] [ Statistics] e [ Tabelle temporanee][Temporary].</span><span class="sxs-lookup"><span data-stu-id="b8380-203">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="b8380-204">Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="b8380-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
