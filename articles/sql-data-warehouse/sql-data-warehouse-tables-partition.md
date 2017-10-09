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
# <a name="partitioning-tables-in-sql-data-warehouse"></a>Tabelle di partizionamento in SQL Data Warehouse
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

Il partizionamento è supportato in tutti i tipi di tabella di SQL Data Warehouse, tra cui columnstore cluster, indice cluster e heap.  Il partizionamento è supportato anche in tutti i tipi di distribuzione, sia hash che round robin.  Partizionamento consente toodivide i dati in gruppi più piccoli dei dati e nella maggior parte dei casi, il partizionamento viene effettuati su una colonna di date.

## <a name="benefits-of-partitioning"></a>Vantaggi del partizionamento
Il partizionamento può recare vantaggio alle prestazioni di query e di conservazione dei dati.  Se si avvantaggia entrambi o solo uno è dipendono dalla modalità di caricamento di dati e se hello stessa colonna può essere utilizzata per entrambi gli scopi, poiché il partizionamento può essere eseguito solo in una colonna.

### <a name="benefits-tooloads"></a>Vantaggi tooloads
Il vantaggio principale Hello di partizionamento in SQL Data Warehouse è migliorare hello efficienza e prestazioni di caricamento dati da utilizzare dell'eliminazione di una partizione, passaggio e unione.  Nella maggior parte dei casi i dati sono partizionati in una data colonna che è strettamente legata sequenza toohello quali dati hello sono caricato toohello database.  Uno dei principali vantaggi di hello dell'utilizzo di partizioni toomaintain dati hello prevenzione di registrazione delle transazioni.  Mentre semplicemente l'inserimento, aggiornamento o eliminazione di dati può essere l'approccio più semplice di hello, con una piccola pensiero e impegno, tramite il partizionamento durante il processo di caricamento può migliorare notevolmente le prestazioni.

Cambio della partizione, è possibile rimuovere tooquickly usato o sostituire una sezione di una tabella.  Ad esempio, una tabella dei fatti vendite potrebbe contenere solo i dati per hello ultimi 36 mesi.  Alla fine di hello di ogni mese, hello mese meno recente dei dati di vendita viene eliminato dalla tabella hello.  È stato possibile eliminare i dati utilizzando una data di hello toodelete istruzione delete per hello mese meno recente.  Tuttavia, l'eliminazione di una grande quantità di dati riga per riga con un'istruzione delete può richiedere molto tempo, nonché creare rischio hello di transazioni di grandi dimensioni può richiedere un toorollback molto tempo se si verificano problemi.  Un approccio più appropriato è toosimply partizione meno recente hello rilascio dei dati.  In cui le singole righe hello di eliminazione potrebbe richiedere ore, l'eliminazione di un'intera partizione potrebbe richiedere secondi.

### <a name="benefits-tooqueries"></a>Vantaggi tooqueries
Partizionamento può essere anche usato tooimprove le prestazioni delle query.  Se una query che applica un filtro in una colonna di partizionamento, si può limitare hello tooonly di analisi hello qualificazione di partizioni che possono essere un subset molto più piccolo di dati di hello, evitando un'analisi completa della tabella.  Con l'introduzione di hello degli indici columnstore cluster, prestazioni hello come predicato di eliminazione sono meno utile, ma in alcuni casi può essere tooqueries un vantaggio.  Ad esempio, se nella tabella dei fatti di vendita hello è suddiviso in mesi 36 mediante il campo di data di vendita hello, quindi query per filtrare nella data di vendita hello possibile ignorare la ricerca in partizioni che non corrispondono a filtro hello.

## <a name="partition-sizing-guidance"></a>Indicazioni sul dimensionamento delle partizioni
Durante il partizionamento possono essere utilizzato tooimprove prestazioni alcuni scenari, la creazione di una tabella con **troppi** partizioni possono influire negativamente sulle prestazioni in alcune circostanze.  Questi problemi valgono soprattutto per le tabelle columnstore cluster.  Per il partizionamento toobe utile, è importante toounderstand quando toouse partizionamento e hello il numero di partizioni toocreate.  Vi è alcuna regola disco rigido veloce come toohow molte partizioni sono troppi, dipende dai dati e il numero di partizioni si sta caricando toosimultaneously.  Ma come una regola empirica generale, considerare l'aggiunta di 10s too100s di partizioni, non 1000s.

Durante la creazione di partizionamento in **columnstore cluster** tabelle, è importante tooconsider quante righe verranno inserite in ogni partizione.  Per ottenere risultati ottimali in termini di compressione e prestazioni delle tabelle columnstore cluster, è necessario almeno 1 milione di righe per distribuzione e partizione.  Prima della creazione delle partizioni, SQL Data Warehouse divide già ogni tabella in 60 database distribuiti.  Qualsiasi tabella aggiunta tooa partizionamento è inoltre distribuzioni toohello create background hello.  Utilizzo di questo esempio, se nella tabella dei fatti di vendita hello contenuto 36 partizioni mensili e dato che SQL Data Warehouse è 60 distribuzioni, quindi hello dei fatti di vendita nella tabella deve contenere 60 milioni di righe al mese o 2.1 miliardi di righe quando vengono popolati tutti i mesi.  Se una tabella contiene molto meno righe rispetto al hello consigliato numero minimo di righe per partizione, utilizzare un minor numero di partizioni in ordine toomake aumento hello numerose righe per partizione.  Vedere anche hello [indicizzazione] [ Index] articolo che include le query che possono essere eseguite in qualità di hello tooassess SQL Data Warehouse di indici columnstore cluster.

## <a name="syntax-difference-from-sql-server"></a>Differenze di sintassi rispetto a SQL Server
SQL Data Warehouse introduce una definizione semplificata delle partizioni, leggermente diversa da SQL Server.  Le funzioni e gli schemi di partizionamento non vengono usati in SQL Data Warehouse come in SQL Server.  Invece, è sufficiente toodo è identificare i punti di limite di colonna e hello partizionati.  Sintassi di hello di partizionamento può essere leggermente diversa da SQL Server, i concetti di base hello sono hello stesso.  SQL Server e SQL Data Warehouse supportano una colonna di partizione per tabella, che può essere il partizionamento con intervallo.  toolearn più informazioni sul partizionamento, vedere [tabelle e indici partizionati][Partitioned Tables and Indexes].

Hello di sotto di esempio di un Data Warehouse di SQL partizionato [CREATE TABLE] [ CREATE TABLE] istruzione, le partizioni nella tabella FactInternetSales hello nella colonna OrderDateKey hello:

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

## <a name="migrating-partitioning-from-sql-server"></a>Migrazione del partizionamento da SQL Server
definizioni tooSQL Data Warehouse di partizione semplicemente toomigrate SQL Server:

* Eliminare il Server SQL hello [lo schema di partizione][partition scheme].
* Aggiungere hello [funzione di partizione] [ partition function] tooyour definizione creazione tabella.

Se si esegue la migrazione di una tabella partizionata da un hello di istanza di SQL Server di sotto di SQL consentono numero hello toointerrogate di righe in ogni partizione.  Tenere presente che se hello stessa granularità di partizionamento viene utilizzata in SQL Data Warehouse, il numero di hello di righe per partizione comporterà la riduzione di un fattore di 60.  

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

## <a name="workload-management"></a>Gestione del carico di lavoro
È un toofactor di considerazione finale nella decisione di partizione di tabella toohello [del carico di lavoro][workload management].  Gestione del carico di lavoro in SQL Data Warehouse è principalmente la gestione di hello di memoria e concorrenza.  In hello SQL Data Warehouse memoria massima allocata tooeach distribuzione durante l'esecuzione di query è classi di risorse gestite.  In teoria le partizioni verranno ridimensionate in considerazione altri fattori quali i requisiti di memoria hello della compilazione degli indici columnstore cluster.  Gli indici columnstore cluster traggono importanti vantaggi quando la memoria allocata è maggiore.  Pertanto, si desidererà tooensure che ricompila un indice di partizione non richieda ulteriori di memoria. Aumento hello quantità di memoria disponibile tooyour query può essere ottenuto passaggio dal ruolo predefinito di hello, smallrc, tooone di hello altri ruoli, ad esempio largerc.

Eseguendo una query su viste a gestione dinamica hello resource governor sono disponibili informazioni sull'allocazione di hello di memoria per ogni distribuzione. In realtà la concessione di memoria sarà minore di nelle figure hello seguenti. Fornisce tuttavia un livello di indicazioni che è possibile usare durante il dimensionamento delle partizioni per le operazioni di gestione dati.  Provare a tooavoid partizioni oltre hello concessione di memoria fornito dalla classe di risorse molto grande hello di ridimensionamento. Se le partizioni di crescere oltre questo valore si corre il rischio di hello pressione della memoria che a sua volta comporta la compressione ottimale tooless.

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

## <a name="partition-switching"></a>Cambio di partizione
SQL Data Warehouse supporta la suddivisione, l'unione e il cambio di partizioni. Ognuna di queste funzioni è excuted utilizzando hello [ALTER TABLE] [ ALTER TABLE] istruzione.

partizioni tooswitch tra due tabelle, che è necessario assicurarsi che le partizioni hello allineate sui loro rispettivi limiti e che le definizioni di tabella hello corrispondano. Come i vincoli check non sono disponibili intervallo hello tooenforce di valori in una tabella di origine di tabella hello deve contenere hello stessi limiti di partizione come tabella di destinazione hello. In caso non hello, quindi il cambio di partizione hello avrà esito negativo non verranno quindi sincronizzati i metadati della partizione hello.

### <a name="how-toosplit-a-partition-that-contains-data"></a>Come toosplit una partizione contenente dati
più efficiente metodo toosplit una partizione che contiene già dati Hello è toouse un `CTAS` istruzione. Se la tabella partizionata hello è un indice columnstore cluster quindi hello tabella partizione deve essere vuota prima che possa essere suddiviso.

Di seguito è riportato un esempio di tabella columnstore contenente una riga in ogni partizione:

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
> Creazione dell'oggetto statistic hello è di assicurare che i metadati di tabella sono più accurato. Se si omette la creazione di statistiche, SQL Data Warehouse userà i valori predefiniti. Per altre informazioni, vedere l'articolo relativo alla gestione delle [statistiche][statistics].
> 
> 

È quindi possibile eseguire una query per il numero di riga hello utilizzando hello `sys.partitions` vista del catalogo:

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

Se si tenta di toosplit questa tabella, si otterrà un errore:

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Msg 35346, livello 15, stato 1, riga 44 divisa clausola dell'istruzione ALTER PARTITION non riuscita perché la partizione hello non è vuota.  Solo partizioni vuote possono essere suddivise presenza di un indice columnstore sulla tabella hello. Provare a disabilitare l'indice columnstore hello prima di eseguire l'istruzione ALTER PARTITION hello, quindi ricompilare l'indice columnstore hello al termine dell'istruzione ALTER PARTITION.

Tuttavia, è possibile utilizzare `CTAS` toocreate un nuovo toohold tabella dati.

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

Come vengono allineati dei limiti delle partizioni hello è consentito un commutatore. Tabella di origine hello questo lascerà con una partizione vuota che è possibile successivamente divisa.

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Tutto ciò che viene lasciato toodo è tooalign toohello i dati di partizione nuovi limiti utilizzando `CTAS` e passare i dati nella tabella principale toohello

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

Dopo aver completato lo spostamento di hello dei dati hello è statistiche buona toorefresh hello in tooensure tabella di destinazione hello che indichino nuova distribuzione di hello dei dati di hello in partizioni i rispettivi:

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a>Controllo del codice sorgente del partizionamento della tabella
tooavoid la definizione della tabella da **rusting** nel sistema di controllo del codice sorgente è hello tooconsider approccio:

1. Creare la tabella hello come una tabella partizionata, ma senza valori di partizione

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

1. `SPLIT`tabella Hello come parte del processo di distribuzione hello:

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

Con questo hello approccio rimane statico codice nel controllo del codice sorgente e hello partizionamento sono consentiti limiti toobe dinamico; evoluzione con warehouse hello nel tempo.

## <a name="next-steps"></a>Passaggi successivi
toolearn, vedere gli articoli di hello in [Cenni preliminari su tabella][Overview], [tipi di dati tabella][Data Types], [la distribuzione di una tabella] [ Distribute], [L'indicizzazione di una tabella][Index], [gestione delle statistiche sulla tabella] [ Statistics] e [ Tabelle temporanee][Temporary].  Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].

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
