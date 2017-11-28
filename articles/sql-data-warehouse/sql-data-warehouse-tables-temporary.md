---
title: aaaTemporary nelle tabelle SQL Data Warehouse | Documenti Microsoft
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
ms.openlocfilehash: 2e8b122eb6d71d5bc0a99ce8a2ecab5dbe2d1b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="2f049-103">Tabelle temporanee in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2f049-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2f049-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="2f049-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="2f049-105">[Tipi di dati][Data Types]</span><span class="sxs-lookup"><span data-stu-id="2f049-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="2f049-106">[Distribuzione][Distribute]</span><span class="sxs-lookup"><span data-stu-id="2f049-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="2f049-107">[Indice][Index]</span><span class="sxs-lookup"><span data-stu-id="2f049-107">[Index][Index]</span></span>
> * <span data-ttu-id="2f049-108">[Partizione][Partition]</span><span class="sxs-lookup"><span data-stu-id="2f049-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="2f049-109">[Statistiche][Statistics]</span><span class="sxs-lookup"><span data-stu-id="2f049-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="2f049-110">[Temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="2f049-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="2f049-111">Tabelle temporanee sono molto utili durante l'elaborazione dati, soprattutto durante la trasformazione in cui i risultati intermedi hello sono temporanei.</span><span class="sxs-lookup"><span data-stu-id="2f049-111">Temporary tables are very useful when processing data - especially during transformation where hello intermediate results are transient.</span></span> <span data-ttu-id="2f049-112">In SQL Data Warehouse le tabelle temporanee esistono a livello di sessione hello.</span><span class="sxs-lookup"><span data-stu-id="2f049-112">In SQL Data Warehouse temporary tables exist at hello session level.</span></span>  <span data-ttu-id="2f049-113">Sono solo toohello visibile sessione in cui sono stati creati e vengono eliminati automaticamente quando si disconnette tale sessione.</span><span class="sxs-lookup"><span data-stu-id="2f049-113">They are only visible toohello session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="2f049-114">Tabelle temporanee offrono un miglioramento delle prestazioni in quanto i relativi risultati vengono scritti toolocal anziché come archiviazione remota.</span><span class="sxs-lookup"><span data-stu-id="2f049-114">Temporary tables offer a performance benefit because their results are written toolocal rather than remote storage.</span></span>  <span data-ttu-id="2f049-115">Tabelle temporanee sono leggermente diverse in Azure SQL Data Warehouse di Database SQL di Azure sono accessibili da un punto qualsiasi all'interno di sessione hello, inclusi all'interno e all'esterno di una stored procedure.</span><span class="sxs-lookup"><span data-stu-id="2f049-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside hello session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="2f049-116">In questo articolo contiene informazioni essenziali per l'utilizzo di tabelle temporanee ed evidenzia i principi di hello delle tabelle temporanee livello di sessione.</span><span class="sxs-lookup"><span data-stu-id="2f049-116">This article contains essential guidance for using temporary tables and highlights hello principles of session level temporary tables.</span></span> <span data-ttu-id="2f049-117">Utilizzando le informazioni di hello in questo articolo consente di modularizzare codice, migliorando sia riusabilità e facilità di manutenzione del codice.</span><span class="sxs-lookup"><span data-stu-id="2f049-117">Using hello information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="2f049-118">Creazione di una tabella temporanea</span><span class="sxs-lookup"><span data-stu-id="2f049-118">Create a temporary table</span></span>
<span data-ttu-id="2f049-119">Le tabelle temporanee vengono create aggiungendo semplicemente un prefisso al nome di una tabella con `#`.</span><span class="sxs-lookup"><span data-stu-id="2f049-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="2f049-120">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2f049-120">For example:</span></span>

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

<span data-ttu-id="2f049-121">Tabelle temporanee possono anche essere create con un `CTAS` utilizzando esattamente hello stesso approccio:</span><span class="sxs-lookup"><span data-stu-id="2f049-121">Temporary tables can also be created with a `CTAS` using exactly hello same approach:</span></span>

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
> <span data-ttu-id="2f049-122">`CTAS`è un comando molto potente e hello è aggiunto il vantaggio di essere molto efficiente nell'utilizzo di spazio log delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="2f049-122">`CTAS` is a very powerful command and has hello added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="2f049-123">Eliminazione delle tabelle temporanee</span><span class="sxs-lookup"><span data-stu-id="2f049-123">Dropping temporary tables</span></span>
<span data-ttu-id="2f049-124">Quando viene creata una nuova sessione, non deve esistere alcuna tabella temporanea.</span><span class="sxs-lookup"><span data-stu-id="2f049-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="2f049-125">Tuttavia, se si chiama hello stessa stored procedure, che crea una password temporanea con hello stesso nome, tooensure che il `CREATE TABLE` istruzioni hanno esito positivo un semplice controllo pre-esistenza con un `DROP` può essere utilizzato come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2f049-125">However, if you are calling hello same stored procedure, which creates a temporary with hello same name, tooensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in hello below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="2f049-126">Per la codifica di coerenza, è una buona pratica toouse questo modello per le tabelle e le tabelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="2f049-126">For coding consistency, it is a good practice toouse this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="2f049-127">È anche una buona idea toouse `DROP TABLE` tooremove tabelle temporanee quando è stato completato nel codice.</span><span class="sxs-lookup"><span data-stu-id="2f049-127">It is also a good idea toouse `DROP TABLE` tooremove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="2f049-128">In fase di sviluppo di stored procedure è piuttosto comune toosee hello comandi drop collegati tra loro alla fine hello tooensure una procedura che questi oggetti vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="2f049-128">In stored procedure development it is quite common toosee hello drop commands bundled together at hello end of a procedure tooensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="2f049-129">Modularizzazione del codice</span><span class="sxs-lookup"><span data-stu-id="2f049-129">Modularizing code</span></span>
<span data-ttu-id="2f049-130">Poiché le tabelle temporanee possono verificarsi in qualsiasi punto in una sessione utente, può essere sfruttata toohelp si modularizzare il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f049-130">Since temporary tables can be seen anywhere in a user session, this can be exploited toohelp you modularize your application code.</span></span>  <span data-ttu-id="2f049-131">Ad esempio, hello stored procedura riportata di seguito riunisce hello consigliata di sopra del toogenerate DDL che aggiornerà tutte le statistiche nel database di hello in base al nome delle statistiche.</span><span class="sxs-lookup"><span data-stu-id="2f049-131">For example, hello stored procedure below brings together hello recommended practices from above toogenerate DDL which will update all statistics in hello database by statistic name.</span></span>

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

<span data-ttu-id="2f049-132">In questa fase hello sola azione che si è verificato è creazione hello di una stored procedure che verrà generato semplicemente una tabella temporanea, #stats_ddl, con le istruzioni DDL.</span><span class="sxs-lookup"><span data-stu-id="2f049-132">At this stage hello only action that has occurred is hello creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="2f049-133">Questa stored procedure eliminerà #stats_ddl se esiste già tooensure che non avrà esito negativo se eseguita più di una volta all'interno di una sessione.</span><span class="sxs-lookup"><span data-stu-id="2f049-133">This stored procedure will drop #stats_ddl if it already exists tooensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="2f049-134">Tuttavia, poiché non esiste alcun `DROP TABLE` al fine di hello di hello stored procedure, al termine hello stored procedure, verrà eliminato tabella hello creato in modo che possa essere letto all'esterno di procedure hello archiviato.</span><span class="sxs-lookup"><span data-stu-id="2f049-134">However, since there is no `DROP TABLE` at hello end of hello stored procedure, when hello stored procedure completes, it will leave hello created table so that it can be read outside of hello stored procedure.</span></span>  <span data-ttu-id="2f049-135">In SQL Data Warehouse, a differenza di altri database di SQL Server, è possibile toouse tabella temporanea di hello all'esterno di procedure hello che li ha creati.</span><span class="sxs-lookup"><span data-stu-id="2f049-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible toouse hello temporary table outside of hello procedure that created it.</span></span>  <span data-ttu-id="2f049-136">Tabelle temporanee di SQL Data Warehouse possono essere usate **ovunque** all'interno di sessione hello.</span><span class="sxs-lookup"><span data-stu-id="2f049-136">SQL Data Warehouse temporary tables can be used **anywhere** inside hello session.</span></span> <span data-ttu-id="2f049-137">Questo può causare codice modulare e gestibile di toomore come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2f049-137">This can lead toomore modular and manageable code as in hello below example:</span></span>

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

## <a name="temporary-table-limitations"></a><span data-ttu-id="2f049-138">Limitazioni della tabella temporanea</span><span class="sxs-lookup"><span data-stu-id="2f049-138">Temporary table limitations</span></span>
<span data-ttu-id="2f049-139">SQL Data Warehouse impone un paio di limitazioni quando si implementano tabelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="2f049-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="2f049-140">Attualmente sono supportate solo le tabelle temporanee nell'ambito della sessione.</span><span class="sxs-lookup"><span data-stu-id="2f049-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="2f049-141">Le tabelle temporanee globali non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="2f049-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="2f049-142">Inoltre, non è possibile creare visualizzazioni nelle tabelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="2f049-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f049-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f049-143">Next steps</span></span>
<span data-ttu-id="2f049-144">toolearn, vedere gli articoli di hello in [Cenni preliminari su tabella][Overview], [tipi di dati tabella][Data Types], [la distribuzione di una tabella] [ Distribute], [L'indicizzazione di una tabella][Index], [il partizionamento di una tabella] [ Partition] e [ Gestione delle statistiche sulla tabella][Statistics].</span><span class="sxs-lookup"><span data-stu-id="2f049-144">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="2f049-145">Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="2f049-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
