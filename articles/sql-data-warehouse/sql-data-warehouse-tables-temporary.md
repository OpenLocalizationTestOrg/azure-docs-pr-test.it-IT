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
# <a name="temporary-tables-in-sql-data-warehouse"></a>Tabelle temporanee in SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Panoramica][Overview]
> * [Tipi di dati][Data Types]
> * [Distribuzione][Distribute]
> * [Indice][Index]
> * [Partizione][Partition]
> * [Statistiche][Statistics]
> * [Temporanee][Temporary]
> 
> 

Tabelle temporanee sono molto utili durante l'elaborazione dati, soprattutto durante la trasformazione in cui i risultati intermedi hello sono temporanei. In SQL Data Warehouse le tabelle temporanee esistono a livello di sessione hello.  Sono solo toohello visibile sessione in cui sono stati creati e vengono eliminati automaticamente quando si disconnette tale sessione.  Tabelle temporanee offrono un miglioramento delle prestazioni in quanto i relativi risultati vengono scritti toolocal anziché come archiviazione remota.  Tabelle temporanee sono leggermente diverse in Azure SQL Data Warehouse di Database SQL di Azure sono accessibili da un punto qualsiasi all'interno di sessione hello, inclusi all'interno e all'esterno di una stored procedure.

In questo articolo contiene informazioni essenziali per l'utilizzo di tabelle temporanee ed evidenzia i principi di hello delle tabelle temporanee livello di sessione. Utilizzando le informazioni di hello in questo articolo consente di modularizzare codice, migliorando sia riusabilità e facilità di manutenzione del codice.

## <a name="create-a-temporary-table"></a>Creazione di una tabella temporanea
Le tabelle temporanee vengono create aggiungendo semplicemente un prefisso al nome di una tabella con `#`.  ad esempio:

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

Tabelle temporanee possono anche essere create con un `CTAS` utilizzando esattamente hello stesso approccio:

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
> `CTAS`è un comando molto potente e hello è aggiunto il vantaggio di essere molto efficiente nell'utilizzo di spazio log delle transazioni. 
> 
> 

## <a name="dropping-temporary-tables"></a>Eliminazione delle tabelle temporanee
Quando viene creata una nuova sessione, non deve esistere alcuna tabella temporanea.  Tuttavia, se si chiama hello stessa stored procedure, che crea una password temporanea con hello stesso nome, tooensure che il `CREATE TABLE` istruzioni hanno esito positivo un semplice controllo pre-esistenza con un `DROP` può essere utilizzato come hello di esempio seguente:

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

Per la codifica di coerenza, è una buona pratica toouse questo modello per le tabelle e le tabelle temporanee.  È anche una buona idea toouse `DROP TABLE` tooremove tabelle temporanee quando è stato completato nel codice.  In fase di sviluppo di stored procedure è piuttosto comune toosee hello comandi drop collegati tra loro alla fine hello tooensure una procedura che questi oggetti vengono eliminati.

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a>Modularizzazione del codice
Poiché le tabelle temporanee possono verificarsi in qualsiasi punto in una sessione utente, può essere sfruttata toohelp si modularizzare il codice dell'applicazione.  Ad esempio, hello stored procedura riportata di seguito riunisce hello consigliata di sopra del toogenerate DDL che aggiornerà tutte le statistiche nel database di hello in base al nome delle statistiche.

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

In questa fase hello sola azione che si è verificato è creazione hello di una stored procedure che verrà generato semplicemente una tabella temporanea, #stats_ddl, con le istruzioni DDL.  Questa stored procedure eliminerà #stats_ddl se esiste già tooensure che non avrà esito negativo se eseguita più di una volta all'interno di una sessione.  Tuttavia, poiché non esiste alcun `DROP TABLE` al fine di hello di hello stored procedure, al termine hello stored procedure, verrà eliminato tabella hello creato in modo che possa essere letto all'esterno di procedure hello archiviato.  In SQL Data Warehouse, a differenza di altri database di SQL Server, è possibile toouse tabella temporanea di hello all'esterno di procedure hello che li ha creati.  Tabelle temporanee di SQL Data Warehouse possono essere usate **ovunque** all'interno di sessione hello. Questo può causare codice modulare e gestibile di toomore come hello di esempio seguente:

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

## <a name="temporary-table-limitations"></a>Limitazioni della tabella temporanea
SQL Data Warehouse impone un paio di limitazioni quando si implementano tabelle temporanee.  Attualmente sono supportate solo le tabelle temporanee nell'ambito della sessione.  Le tabelle temporanee globali non sono supportate.  Inoltre, non è possibile creare visualizzazioni nelle tabelle temporanee.

## <a name="next-steps"></a>Passaggi successivi
toolearn, vedere gli articoli di hello in [Cenni preliminari su tabella][Overview], [tipi di dati tabella][Data Types], [la distribuzione di una tabella] [ Distribute], [L'indicizzazione di una tabella][Index], [il partizionamento di una tabella] [ Partition] e [ Gestione delle statistiche sulla tabella][Statistics].  Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].

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
