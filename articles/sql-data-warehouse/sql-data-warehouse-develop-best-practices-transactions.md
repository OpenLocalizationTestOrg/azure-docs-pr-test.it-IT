---
title: le transazioni aaaOptimizing per SQL Data Warehouse | Documenti Microsoft
description: Indicazioni sulle procedure consigliate per la scrittura di aggiornamenti di transazioni efficienti in Azure SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a>Ottimizzazione delle transazioni per SQL Data Warehouse
Questo articolo spiega come toooptimize hello prestazioni del codice transazionale riducendo i rischi per i ripristini lungo.

## <a name="transactions-and-logging"></a>Transazioni e registrazione
Le transazioni sono un componente importante in un motore di database relazionale. SQL Data Warehouse usa le transazioni durante la modifica dei dati. Queste operazioni possono essere esplicite o implicite. Le istruzioni singole `INSERT`, `UPDATE` e `DELETE` sono esempi di transazioni implicite. Le transazioni esplicite sono scritti in modo esplicito da uno sviluppatore utilizzando `BEGIN TRAN`, `COMMIT TRAN` o `ROLLBACK TRAN` e vengono in genere usate quando le istruzioni di modifica più necessario toobe collegati in un'unica unità atomica. 

Azure SQL Data Warehouse viene eseguito il commit del database toohello modifiche utilizzando i log delle transazioni. Ogni distribuzione ha un proprio log delle transazioni. Le scritture del log delle transazioni avvengono in modo automatico e non è richiesta alcuna configurazione. Tuttavia, durante questo processo garantisce la scrittura di hello introdurre un sovraccarico nel sistema hello. È possibile ridurre al minimo tale impatto scrivendo codice efficiente a livello transazionale. Il codice efficiente a livello transazionale rientra in due categorie generali.

* Sfruttare costrutti di registrazione minima, dove possibile.
* Elaborazione di dati con la forma singolare tooavoid con ambito batch transazioni a esecuzione prolungata
* Adottare una modello per la partizione specificata tooa di grandi dimensioni modifiche del cambio di partizione

## <a name="minimal-vs-full-logging"></a>Confronto tra registrazione minima e registrazione completa
A differenza delle operazioni con registrazione completa, che utilizzano traccia tookeep di hello transaction log di ogni modifica della riga, operazioni con registrazione minima tenere traccia delle allocazioni di extent e solo le modifiche dei metadati. Di conseguenza, la registrazione minima implica la registrazione solo informazioni hello sono obbligatorio toorollback hello di transazione nell'evento hello di un errore o di una richiesta esplicita (`ROLLBACK TRAN`). Come molto meno informazioni vengono rilevate nel log delle transazioni hello, un'operazione con registrazione minima offre prestazioni migliori rispetto a un'operazione completamente registrata con dimensione simili. Inoltre, in quanto un minor numero di scritture log delle transazioni hello, una minore quantità di dati di log viene generata e pertanto i/o più efficiente.

limiti di sicurezza delle transazioni Hello si applicano solo operazioni toofully registrati.

> [!NOTE]
> le operazioni con registrazione minima possono partecipare alle transazioni esplicite. Come vengono rilevate tutte le modifiche in strutture di allocazione, è possibile tooroll back minima operazioni registrate. È importante registrato toounderstand che modifica hello è "minima" non è non registrato.
> 
> 

## <a name="minimally-logged-operations"></a>Operazioni con registrazione minima
Hello operazioni indicate di seguito sono in grado di corso la registrazione minima:

* CREATE TABLE AS SELECT ([CTAS][CTAS])
* INSERT..SELECT
* CREATE INDEX
* ALTER INDEX REBUILD
* DROP INDEX
* TRUNCATE TABLE
* DROP TABLE
* ALTER TABLE SWITCH PARTITION

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> Operazioni di spostamento dei dati interni (ad esempio `BROADCAST` e `SHUFFLE`) non sono interessati da limite di sicurezza delle transazioni hello.
> 
> 

## <a name="minimal-logging-with-bulk-load"></a>Registrazione minima con caricamento bulk
`CTAS` e `INSERT...SELECT` sono entrambe operazioni di caricamento bulk. Tuttavia, entrambi sono influenzate dalla definizione di tabella di destinazione hello e dipendono da uno scenario di carico hello. La tabella riportata di seguito indica la registrazione completa o minima delle operazioni bulk elencate:  

| Indice primario | Scenario di caricamento | Modalità di registrazione |
| --- | --- | --- |
| Heap |Qualsiasi |**Minima** |
| Indice cluster |Tabella di destinazione vuota |**Minima** |
| Indice cluster |Le righe caricate non si sovrappongono alle pagine esistenti nella destinazione |**Minima** |
| Indice cluster |Le righe caricate si sovrappongono alle pagine esistenti nella destinazione |Completa |
| Indice columnstore cluster |Dimensioni batch >= 102.400 per ogni distribuzione allineata alle partizioni |**Minima** |
| Indice columnstore cluster |Dimensioni batch < 102.400 per ogni distribuzione allineata alle partizioni |Completa |

Vale la pena notare che eventuali scritture gli indici secondari o non cluster tooupdate sarà sempre completamente operazioni registrate.

> [!IMPORTANT]
> SQL Data Warehouse ha 60 distribuzioni. Di conseguenza, presupponendo che tutte le righe sono distribuite uniformemente e di destinazione in una singola partizione, il batch sarà necessario righe toocontain 6,144,000 o toobe maggiore minima registrate durante la scrittura tooa indice Columnstore cluster. Se viene partizionata hello e righe hello inserite span dei limiti delle partizioni, è necessario 6,144,000 righe al limite della partizione presupponendo che anche la distribuzione dei dati. Ogni partizione in ogni distribuzione deve superare in modo indipendente soglia di righe per hello insert toobe registrazione minima in distribuzione hello 102.400 hello.
> 
> 

Il caricamento di dati in una tabella non vuota con un indice cluster può spesso contenere una combinazione di righe con registrazione completa e con registrazione minima. Un indice cluster è un albero B (bilanciato) di pagine. Se la pagina hello scritti tooalready contiene le righe da un'altra transazione, quindi tali operazioni di scrittura verrà registrate completamente. Tuttavia, se la pagina hello è vuota quindi pagina toothat di scrittura hello verrà minima registrato.

## <a name="optimizing-deletes"></a>Ottimizzazione delle eliminazioni
`DELETE` è un'operazione con registrazione completa.  Se è necessario toodelete una grande quantità di dati in una tabella o una partizione, è spesso opportuno troppo`SELECT` dati hello desiderato tookeep, che può essere eseguito come un'operazione con registrazione minima.  tooaccomplish, creare una nuova tabella con [un'istruzione CTAS][CTAS].  Una volta creata, utilizzare [RINOMINARE] [ RENAME] tooswap la tabella precedente con la tabella hello appena creato.

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a>Ottimizzazione degli aggiornamenti
`UPDATE` è un'operazione con registrazione completa.  Se è necessario tooupdate un numero elevato di righe in una tabella o una partizione può essere spesso molto più efficiente toouse un'operazione con registrazione minima, ad esempio [un'istruzione CTAS] [ CTAS] toodo in modo.

In hello esempio riportato di seguito un aggiornamento di tabelle complete è stato convertito tooa `CTAS` in modo che sia possibile la registrazione minima.

In questo caso aggiungiamo posteriori vendite toohello importo dello sconto nella tabella hello:

```sql
--Step 01. Create a new table containing hello "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> Per creare nuovamente tabelle di grandi dimensioni è possibile sfruttare le funzionalità di gestione del carico di lavoro di SQL Data Warehouse. Per ulteriori informazioni, vedere toohello sezione relativa alla gestione del carico di lavoro in hello [concorrenza] [ concurrency] articolo.
> 
> 

## <a name="optimizing-with-partition-switching"></a>Ottimizzazione con cambio della partizione
In caso di modifiche su larga scala in una [partizione di tabella][table partition] può risultare molto utile adottare un modello di cambio di partizione. Se hello la modifica dei dati è significativa e intervalli di più partizioni, quindi scorrere semplicemente partizioni hello raggiunge hello stesso risultato.

di seguito sono riportati i passaggi di Hello tooperform un cambio di partizione:

1. Creare una partizione di disattivazione vuota.
2. Eseguire l'aggiornamento"hello" come una istruzione CTAS
3. Hello esistente dati toohello la tabella di disattivazione
4. Passare a nuovi dati hello
5. Pulizia dei dati hello

Tuttavia, toohelp identificare hello tooswitch di partizioni è necessario innanzitutto toobuild una routine di supporto, ad esempio hello uno riportato di seguito. 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

Questa procedura consente di ottimizzare riutilizzo del codice e mantiene esempio più compatto del cambio di partizione hello.

Hello di codice riportato di seguito cinque passaggi hello indicato in precedenza tooachieve una routine di cambio della partizione completa.

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a>Riduzione della registrazione con batch di piccole dimensioni
Per le operazioni di modifica di dati di grandi dimensioni, può avere senso toodivide hello operazione in unità di hello tooscope blocchi o i batch di lavoro.

Di seguito viene fornito un esempio funzionante. dimensioni del batch Hello sono stata impostata una semplice numero tecnica di hello toohighlight tooa. In realtà la dimensione del batch hello sarebbe notevolmente maggiore. 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a>Linee guida per la sospensione e il ridimensionamento
Azure SQL Data Warehouse permette di sospendere, riprendere e ridimensionare il data warehouse su richiesta. Quando si sospende o ridimensionare il Data Warehouse di SQL è importante toounderstand che qualsiasi pertanto le transazioni vengono terminate immediatamente. causa toobe eventuali transazioni aperte a rollback. Se il carico di lavoro ha rilasciato una lunga esecuzione e la modifica di dati incompleti precedente toohello sospensione o dell'operazione di ridimensionamento, quindi questo lavoro sarà necessario toobe annullata. Questo potrebbe influire sulle hello tempo toopause o ridimensionare il database di Azure SQL Data Warehouse. 

> [!IMPORTANT]
> `UPDATE` e `DELETE` sono operazioni con registrazione completa e qualsiasi operazione di annullamento o ripristino può richiedere molto più tempo rispetto alle operazioni con registrazione minima equivalenti. 
> 
> 

scenario migliore Hello è toolet in fase di trasferimento dati Modifica transazioni completo precedente toopausing o ridimensionamento SQL Data Warehouse. Tuttavia, questo potrebbe non essere sempre possibile. rischio hello toomitigate di un rollback lungo considerare una delle seguenti opzioni hello:

* Riscrivere le operazioni a esecuzione prolungata con [CTAS][CTAS]
* Suddividere operazione hello in blocchi. opera su un subset di righe hello

## <a name="next-steps"></a>Passaggi successivi
Vedere [transazioni in SQL Data Warehouse] [ Transactions in SQL Data Warehouse] toolearn informazioni sui livelli di isolamento e i limiti transazionali.  Per una panoramica delle altre procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

