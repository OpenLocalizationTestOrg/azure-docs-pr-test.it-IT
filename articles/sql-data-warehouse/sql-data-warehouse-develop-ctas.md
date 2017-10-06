---
title: tabella aaaCreate come selezionare SQL Data Warehouse (un'istruzione CTAS) | Documenti Microsoft
description: Suggerimenti per la codifica con hello creare una tabella come selezionare l'istruzione (un'istruzione CTAS) in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: shigu;barbkess
ms.openlocfilehash: e381601a0a4d94e189d8f9115bf2e7593025410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a>Create Table As Select (CTAS) in SQL Data Warehouse
Creare una tabella come selezione o `CTAS` è uno dei hello più importanti funzionalità di T-SQL disponibili. È un'operazione completamente parallelizzata che crea una nuova tabella basata sull'output di hello di un'istruzione SELECT. `CTAS`è hello più semplice e veloce toocreate una copia di una tabella. Questo documento offre esempi e procedure consigliate per `CTAS`.

## <a name="selectinto-vs-ctas"></a>SELECT..INTO e CTAS
È possibile considerare `CTAS` come una versione più potente di `SELECT..INTO`.

Di seguito è riportato un esempio di un'istruzione semplice `SELECT..INTO`:

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

Nell'esempio hello sopra `[dbo].[FactInternetSales_new]` verrebbe creato come tabella di distribuita ROUND_ROBIN con un indice COLUMNSTORE cluster su di esso, poiché si tratta di valori predefiniti di tabella hello in Azure SQL Data Warehouse.

`SELECT..INTO`tuttavia non consente l'indice di metodo o hello distribuzione hello digitare come parte dell'operazione hello toochange. Qui è dove si posiziona `CTAS`.

tooconvert hello sopra troppo`CTAS` è piuttosto semplice:

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

Con `CTAS` si è in grado di toochange entrambi hello distribuzione dei dati della tabella hello, nonché il tipo di tabella hello. 

> [!NOTE]
> Se si sta solo tentando indice hello toochange il `CTAS` operazione e hello tabella di origine è hash distribuita è possibile che il `CTAS` eseguirà l'operazione migliore se è necessario mantenere hello stesso tipo di dati e di colonna di distribuzione. Questo modo si evita tra lo spostamento dei dati di distribuzione durante l'operazione di hello che risulta più efficiente.
> 
> 

## <a name="using-ctas-toocopy-a-table"></a>Utilizzando un'istruzione CTAS toocopy una tabella
Forse una delle più comuni di hello utilizzi di `CTAS` sta creando una copia di una tabella in modo che sia possibile modificare hello DDL. Se ad esempio originariamente creata la tabella come `ROUND_ROBIN` e ora si desidera modificarlo tooa tabella distribuiti in una colonna, `CTAS` è come sarebbe stato necessario modificare la colonna di distribuzione hello. `CTAS`può anche essere toochange utilizzati tipi di partizionamento, l'indicizzazione o di colonna.

Si supponga che per creare questa tabella con tipo di distribuzione predefinito di hello `ROUND_ROBIN` distribuita poiché è stata specificata alcuna colonna di distribuzione in hello `CREATE TABLE`.

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

Si desidera ora toocreate una nuova copia di questa tabella con un indice Columnstore cluster in modo che è possibile sfruttare le prestazioni di hello delle tabelle Columnstore cluster. È anche opportuno toodistribute la tabella nella ProductKey poiché si sono prevedendo join su questa colonna e si desidera tooavoid lo spostamento di dati durante l'unione in ProductKey join. Infine è tooadd partizionamento in OrderDateKey in modo che è possibile eliminare rapidamente dati precedenti l'eliminazione di partizioni precedenti. Ecco l'istruzione un'istruzione CTAS hello copiava la vecchia tabella in una nuova tabella.

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

Infine è possibile rinominare le tabelle tooswap nella nuova tabella e quindi eliminare la tabella precedente.

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.  Ordine tooget hello prestazioni migliori dalle query, è importante creare statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento hello o si verificano modifiche sostanziali in dati hello.  Per una spiegazione dettagliata delle statistiche, vedere hello [statistiche] [ Statistics] argomento nel gruppo di sviluppare hello degli argomenti.
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a>Utilizzando un'istruzione CTAS toowork intorno a funzionalità non supportate
`CTAS`può inoltre essere utilizzati toowork intorno a un numero di funzionalità non supportata hello elencati di seguito. Questo può spesso risultare toobe una situazione win/win come non solo il codice sarà conforme, ma verranno spesso eseguite più velocemente in SQL Data Warehouse. Si tratta del risultato della progettazione completamente parallelizzata. Gli scenari che è possibile trattare con CTAS includono:

* ANSI JOINS su UPDATE
* ANSI JOINs su DELETE
* Istruzione MERGE

> [!NOTE]
> Provare a toothink "un'istruzione CTAS prima". Se si ritiene che sia possibile risolvere un problema di mediante `CTAS` che è in genere tooapproach modo migliore di hello, anche se si siano scrivendo più dati, di conseguenza.
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a>Sostituzione di join ANSI per le istruzioni update
È possibile che si dispone di un aggiornamento complesso che unisce in join più di due tabelle utilizzando hello tooperform sintassi join ANSI UPDATE o DELETE.

Si supponga che era tooupdate questa tabella:

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

la query originale Hello potrebbe siano presenti simile al seguente:

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

Poiché SQL Data Warehouse non supporta ANSI unisce in hello `FROM` clausola di un `UPDATE` istruzione, non è possibile copiare questo codice su senza modificarla leggermente.

È possibile utilizzare una combinazione di un `CTAS` e implicita join tooreplace questo codice:

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join tooperform hello update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop hello interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a>Sostituzione di join ANSI per le istruzioni delete
In alcuni casi hello migliore approccio per l'eliminazione dei dati è toouse `CTAS`. Anziché di eliminazione dei dati di hello semplicemente selezionare hello dati tookeep. Questo particolarmente vero per `DELETE` le istruzioni che utilizzano ansi join di sintassi perché SQL Data Warehouse non supporta i join ANSI in hello `FROM` clausola di un `DELETE` istruzione.

Un esempio di istruzione DELETE convertita è disponibile di seguito:

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish tookeep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        tooDimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert tooDimProduct;
```

## <a name="replace-merge-statements"></a>Sostituzione delle istruzioni merge
Le istruzioni merge possono essere sostituite, almeno in parte, usando `CTAS`. È possibile consolidare hello `INSERT` hello e `UPDATE` in una singola istruzione. Qualsiasi record eliminato sarebbe necessario toobe chiuso in una seconda istruzione.

Un esempio di `UPSERT` è riportato di seguito:

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          too[DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  too[DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a>Raccomandazione CTAS: dichiarare in modo esplicito il tipo di dati e il supporto di valori null di output
Durante la migrazione del codice, è possibile imbattersi in questo tipo di modello di codifica:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

Si pensi istintivamente è necessario eseguire la migrazione di questo tooa codice un'istruzione CTAS e sarebbe corretta. Tuttavia, esiste un problema nascosto.

Hello codice riportato di seguito non produce hello stesso risultato:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

Si noti che il risultato"hello colonne" estende valori hello dati tipo e il supporto di valori null dell'espressione hello. Se non si è attenzione, questo può causare toosubtle variazioni nei valori.

Provare seguenti hello ad esempio:

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

il valore di Hello archiviato per il risultato è diverso. Errore hello espressioni hello persistente valore nella colonna di risultati hello viene utilizzato in altre diventa ancora più significativo.

![][1]

Ciò è particolarmente importante per le migrazioni di dati. Anche se probabilmente più accurate query secondo hello è un problema. dati Hello sarebbe toohello confrontati diverso sistema di origine e tooquestions dell'integrità che comporta la migrazione di hello. Questo è uno dei rari casi in cui destra di hello effettivamente una risposta "corretto" hello!

Hello motivo, è possibile notare questo disparità tra i risultati di due hello è inattivo tooimplicit cast di tipo. Prima tabella di esempio hello hello definisce la definizione di colonna hello. Quando viene inserita la riga hello si verifica una conversione implicita del tipo. Nel secondo esempio hello non è alcuna conversione implicita del tipo come espressione hello definisce il tipo di dati della colonna hello. Si noti che la colonna nel secondo esempio hello hello è stata definita come una colonna che ammette valori null mentre nel primo esempio hello non sia. Creazione tabella hello in hello primo esempio colonna ammissione di valori null è stata definita in modo esplicito. Nel secondo esempio hello è stato appena uscito toohello espressione e per impostazione predefinita questo porterebbe a una definizione di NULL.  

tooresolve questi problemi, è necessario impostare esplicitamente la conversione di tipo hello e supporto di valori null in hello `SELECT` parte hello `CTAS` istruzione. Non è possibile impostare queste proprietà in hello creare parte di tabella.

Hello riportato di seguito come toofix hello codice:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

Si noti hello segue:

* Era possibile usare CAST o CONVERT
* ISNULL viene utilizzato tooforce ammissione di valori null non COALESCE
* ISNULL è più esterno della funzione hello
* Hello seconda parte hello ISNULL è una costante, ovvero 0

> [!NOTE]
> Per hello ammissione di valori null toobe impostato correttamente è essenziale toouse `ISNULL` e non `COALESCE`. `COALESCE`non è una funzione deterministica e pertanto il risultato di hello di hello espressione sarà sempre ammette valori null. `ISNULL` è diverso. È deterministico. Pertanto quando hello seconda parte di hello `ISNULL` funzione è una costante o un valore letterale, valore risultante di hello sarà non NULL.
> 
> 

Questo suggerimento non è utile solo per garantire l'integrità di hello dei calcoli. È importante anche per il cambio di partizione della tabella. Si supponga di disporre di questa tabella definita come dato di fatto:

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

Campo del valore hello invece un'espressione calcolata non è parte di dati di origine hello.

toocreate il set di dati partizionati è toodo questo:

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

Hello verrebbe eseguita ottimale. problema di Hello viene fornito quando si tenta di cambio di partizione tooperform hello. le definizioni di tabella Hello non corrispondono. le definizioni di tabella hello toomake corrispondano hello che un'istruzione CTAS deve toobe modificato.

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

Pertanto è possibile vedere che la coerenza del tipo e le proprietà di gestione del supporto di valori null in CTAS è un’ottima procedura tecnica consigliata. Consente di integrità toomaintain nei calcoli e assicura anche che sia possibile cambio della partizione.

Per ulteriori informazioni sull'utilizzo, vedere tooMSDN [un'istruzione CTAS][CTAS]. È uno dei più importanti istruzioni di hello in Azure SQL Data Warehouse. Assicurarsi di averla compresa completamente.

## <a name="next-steps"></a>Passaggi successivi
Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
