---
title: Tabelle temporanee in SQL Data Warehouse | Documentazione Microsoft
description: Introduzione alle tabelle temporanee di SQL Data Warehouse di Azure.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 9b1119eb-7f54-46d0-ad74-19c85a2a555a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: fd8c31a727dae3b011aa8294a81f005bad72a278
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="b5ddf-103">Tabelle temporanee in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b5ddf-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="b5ddf-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="b5ddf-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="b5ddf-105">[Tipi di dati][Data Types]</span><span class="sxs-lookup"><span data-stu-id="b5ddf-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="b5ddf-106">[Distribuzione][Distribute]</span><span class="sxs-lookup"><span data-stu-id="b5ddf-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="b5ddf-107">[Indice][Index]</span><span class="sxs-lookup"><span data-stu-id="b5ddf-107">[Index][Index]</span></span>
> * <span data-ttu-id="b5ddf-108">[Partizione][Partition]</span><span class="sxs-lookup"><span data-stu-id="b5ddf-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="b5ddf-109">[Statistiche][Statistics]</span><span class="sxs-lookup"><span data-stu-id="b5ddf-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="b5ddf-110">[Temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="b5ddf-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="b5ddf-111">Le tabelle temporanee sono molto utili durante l'elaborazione dati, soprattutto durante la trasformazione in cui i risultati intermedi sono temporanei.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-111">Temporary tables are very useful when processing data - especially during transformation where the intermediate results are transient.</span></span> <span data-ttu-id="b5ddf-112">In SQL Data Warehouse le tabelle temporanee esistono a livello di sessione.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-112">In SQL Data Warehouse temporary tables exist at the session level.</span></span>  <span data-ttu-id="b5ddf-113">Sono visibili solo per la sessione in cui sono stati creati e vengono eliminati automaticamente quando si disconnette tale sessione.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-113">They are only visible to the session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="b5ddf-114">Le tabelle temporanee offrono un miglioramento delle prestazioni, perché i loro risultati vengono scritti in locale anziché nell'archiviazione remota.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-114">Temporary tables offer a performance benefit because their results are written to local rather than remote storage.</span></span>  <span data-ttu-id="b5ddf-115">Le tabelle temporanee sono leggermente diverse in SQL Data Warehouse di Azure rispetto al database SQL di Azure, poiché è possibile accedervi da un punto qualsiasi della sessione, sia dall'interno che dall'esterno di una stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside the session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="b5ddf-116">Questo articolo contiene le linee guida fondamentali per l'uso delle tabelle temporanee ed evidenzia i principi delle tabelle temporanee a livello di sessione.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-116">This article contains essential guidance for using temporary tables and highlights the principles of session level temporary tables.</span></span> <span data-ttu-id="b5ddf-117">Usando le informazioni in questo articolo è possibile modularizzare il codice, aumentando le possibilità di riutilizzo e la facilità di manutenzione del codice.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-117">Using the information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="b5ddf-118">Creazione di una tabella temporanea</span><span class="sxs-lookup"><span data-stu-id="b5ddf-118">Create a temporary table</span></span>
<span data-ttu-id="b5ddf-119">Le tabelle temporanee vengono create aggiungendo semplicemente un prefisso al nome di una tabella con `#`.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="b5ddf-120">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b5ddf-120">For example:</span></span>

```sql
CREATE TABLE #stats_ddl
(
    [schema_name]        NVARCHAR(128) NOT NULL
,    [table_name]            NVARCHAR(128) NOT NULL
,    [stats_name]            NVARCHAR(128) NOT NULL
,    [stats_is_filtered]     BIT           NOT NULL
,    [seq_nmbr]              BIGINT        NOT NULL
,    [two_part_name]         NVARCHAR(260) NOT NULL
,    [three_part_name]       NVARCHAR(400) NOT NULL
)
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
```

<span data-ttu-id="b5ddf-121">Le tabelle temporanee possono essere create anche con `CTAS` adottando esattamente lo stesso approccio:</span><span class="sxs-lookup"><span data-stu-id="b5ddf-121">Temporary tables can also be created with a `CTAS` using exactly the same approach:</span></span>

```sql
CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
``` 

> [!NOTE]
> <span data-ttu-id="b5ddf-122">`CTAS` è un comando molto efficace e offre l'ulteriore vantaggio di essere molto efficiente nell'uso dello spazio dei log delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-122">`CTAS` is a very powerful command and has the added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="b5ddf-123">Eliminazione delle tabelle temporanee</span><span class="sxs-lookup"><span data-stu-id="b5ddf-123">Dropping temporary tables</span></span>
<span data-ttu-id="b5ddf-124">Quando viene creata una nuova sessione, non deve esistere alcuna tabella temporanea.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="b5ddf-125">Tuttavia, se si richiama la stessa stored procedure che crea una variabile temporanea con lo stesso nome, per garantire che le istruzioni `CREATE TABLE` abbiano esito positivo è possibile eseguire un controllo di pre-esistenza con `DROP`, come nel seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="b5ddf-125">However, if you are calling the same stored procedure, which creates a temporary with the same name, to ensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in the below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="b5ddf-126">Una procedura consigliata per la coerenza della codifica è usare questo modello per le tabelle e le tabelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-126">For coding consistency, it is a good practice to use this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="b5ddf-127">È inoltre consigliabile usare `DROP TABLE` per rimuovere le tabelle temporanee quando non sono più necessarie.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-127">It is also a good idea to use `DROP TABLE` to remove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="b5ddf-128">Nello sviluppo delle stored procedure è abbastanza comune visualizzare i comandi di eliminazione raggruppati in bundle alla fine di una procedura per garantire che questi oggetti vengano puliti.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-128">In stored procedure development it is quite common to see the drop commands bundled together at the end of a procedure to ensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="b5ddf-129">Modularizzazione del codice</span><span class="sxs-lookup"><span data-stu-id="b5ddf-129">Modularizing code</span></span>
<span data-ttu-id="b5ddf-130">Dal momento che le tabelle temporanee sono visibili in qualsiasi punto di una sessione utente, questo può essere sfruttato per modularizzare il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-130">Since temporary tables can be seen anywhere in a user session, this can be exploited to help you modularize your application code.</span></span>  <span data-ttu-id="b5ddf-131">Ad esempio, la stored procedure seguente riunisce le procedure consigliate riportate sopra per generare un DDL che aggiorna tutte le statistiche nel database in base al nome della statistica.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-131">For example, the stored procedure below brings together the recommended practices from above to generate DDL which will update all statistics in the database by statistic name.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_update_stats]
(   @update_type    tinyint -- 1 default 2 fullscan 3 sample 4 resample
    ,@sample_pct     tinyint
)
AS

IF @update_type NOT IN (1,2,3,4)
BEGIN;
    THROW 151000,'Invalid value for @update_type parameter. Valid range 1 (default), 2 (fullscan), 3 (sample) or 4 (resample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END

CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
GO
```

<span data-ttu-id="b5ddf-132">In questa fase l'unica azione che si è verificata è la creazione di una stored procedure che genererà semplicemente una tabella temporanea, #stats_ddl, con le istruzioni DDL.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-132">At this stage the only action that has occurred is the creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="b5ddf-133">Questa stored procedure eliminerà #stats_ddl se esiste già per garantire che non avrà esito negativo se eseguita più volte all'interno di una sessione.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-133">This stored procedure will drop #stats_ddl if it already exists to ensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="b5ddf-134">Tuttavia, poiché non esiste `DROP TABLE` alla fine della stored procedure, al termine della stored procedure, la tabella creata verrà conservata in modo che possa essere letta all'esterno della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-134">However, since there is no `DROP TABLE` at the end of the stored procedure, when the stored procedure completes, it will leave the created table so that it can be read outside of the stored procedure.</span></span>  <span data-ttu-id="b5ddf-135">A differenza che negli altri server di database SQL, in SQL Data Warehouse è possibile usare la tabella temporanea all'esterno della procedura che l'ha creata.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible to use the temporary table outside of the procedure that created it.</span></span>  <span data-ttu-id="b5ddf-136">Le tabelle temporanee di SQL Data Warehouse possono essere usate **ovunque** all'interno della sessione.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-136">SQL Data Warehouse temporary tables can be used **anywhere** inside the session.</span></span> <span data-ttu-id="b5ddf-137">In questo modo è possibile ottenere codice più modulare e gestibile come nel seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="b5ddf-137">This can lead to more modular and manageable code as in the below example:</span></span>

```sql
EXEC [dbo].[prc_sqldw_update_stats] @update_type = 1, @sample_pct = NULL;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''

WHILE @i <= @t
BEGIN
    SET @s=(SELECT update_stats_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

## <a name="temporary-table-limitations"></a><span data-ttu-id="b5ddf-138">Limitazioni della tabella temporanea</span><span class="sxs-lookup"><span data-stu-id="b5ddf-138">Temporary table limitations</span></span>
<span data-ttu-id="b5ddf-139">SQL Data Warehouse impone un paio di limitazioni quando si implementano tabelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="b5ddf-140">Attualmente sono supportate solo le tabelle temporanee nell'ambito della sessione.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="b5ddf-141">Le tabelle temporanee globali non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="b5ddf-142">Inoltre, non è possibile creare visualizzazioni nelle tabelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="b5ddf-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5ddf-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b5ddf-143">Next steps</span></span>
<span data-ttu-id="b5ddf-144">Per altre informazioni, vedere gli articoli [Panoramica delle tabelle][Overview], [Tipi di dati per le tabelle][Data Types], [Distribuzione di una tabella][Distribute], [Indicizzazione di una tabella][Index], [Partizionamento di una tabella][Partition] [Gestione delle statistiche nelle tabelle][Statistics].</span><span class="sxs-lookup"><span data-stu-id="b5ddf-144">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="b5ddf-145">Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="b5ddf-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

<!--MSDN references-->

<!--Other Web references-->
