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
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="61017-103">Create Table As Select (CTAS) in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="61017-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="61017-104">Creare una tabella come selezione o `CTAS` è uno dei hello più importanti funzionalità di T-SQL disponibili.</span><span class="sxs-lookup"><span data-stu-id="61017-104">Create table as select or `CTAS` is one of hello most important T-SQL features available.</span></span> <span data-ttu-id="61017-105">È un'operazione completamente parallelizzata che crea una nuova tabella basata sull'output di hello di un'istruzione SELECT.</span><span class="sxs-lookup"><span data-stu-id="61017-105">It is a fully parallelized operation that creates a new table based on hello output of a SELECT statement.</span></span> <span data-ttu-id="61017-106">`CTAS`è hello più semplice e veloce toocreate una copia di una tabella.</span><span class="sxs-lookup"><span data-stu-id="61017-106">`CTAS` is hello simplest and fastest way toocreate a copy of a table.</span></span> <span data-ttu-id="61017-107">Questo documento offre esempi e procedure consigliate per `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="61017-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="61017-108">SELECT..INTO e CTAS</span><span class="sxs-lookup"><span data-stu-id="61017-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="61017-109">È possibile considerare `CTAS` come una versione più potente di `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="61017-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="61017-110">Di seguito è riportato un esempio di un'istruzione semplice `SELECT..INTO`:</span><span class="sxs-lookup"><span data-stu-id="61017-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="61017-111">Nell'esempio hello sopra `[dbo].[FactInternetSales_new]` verrebbe creato come tabella di distribuita ROUND_ROBIN con un indice COLUMNSTORE cluster su di esso, poiché si tratta di valori predefiniti di tabella hello in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="61017-111">In hello example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are hello table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="61017-112">`SELECT..INTO`tuttavia non consente l'indice di metodo o hello distribuzione hello digitare come parte dell'operazione hello toochange.</span><span class="sxs-lookup"><span data-stu-id="61017-112">`SELECT..INTO` however does not allow you toochange either hello distribution method or hello index type as part of hello operation.</span></span> <span data-ttu-id="61017-113">Qui è dove si posiziona `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="61017-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="61017-114">tooconvert hello sopra troppo`CTAS` è piuttosto semplice:</span><span class="sxs-lookup"><span data-stu-id="61017-114">tooconvert hello above too`CTAS` is quite straight-forward:</span></span>

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

<span data-ttu-id="61017-115">Con `CTAS` si è in grado di toochange entrambi hello distribuzione dei dati della tabella hello, nonché il tipo di tabella hello.</span><span class="sxs-lookup"><span data-stu-id="61017-115">With `CTAS` you are able toochange both hello distribution of hello table data as well as hello table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="61017-116">Se si sta solo tentando indice hello toochange il `CTAS` operazione e hello tabella di origine è hash distribuita è possibile che il `CTAS` eseguirà l'operazione migliore se è necessario mantenere hello stesso tipo di dati e di colonna di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="61017-116">If you are only trying toochange hello index in your `CTAS` operation and hello source table is hash distributed then your `CTAS` operation will perform best if you maintain hello same distribution column and data type.</span></span> <span data-ttu-id="61017-117">Questo modo si evita tra lo spostamento dei dati di distribuzione durante l'operazione di hello che risulta più efficiente.</span><span class="sxs-lookup"><span data-stu-id="61017-117">This will avoid cross distribution data movement during hello operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-toocopy-a-table"></a><span data-ttu-id="61017-118">Utilizzando un'istruzione CTAS toocopy una tabella</span><span class="sxs-lookup"><span data-stu-id="61017-118">Using CTAS toocopy a table</span></span>
<span data-ttu-id="61017-119">Forse una delle più comuni di hello utilizzi di `CTAS` sta creando una copia di una tabella in modo che sia possibile modificare hello DDL.</span><span class="sxs-lookup"><span data-stu-id="61017-119">Perhaps one of hello most common uses of `CTAS` is creating a copy of a table so that you can change hello DDL.</span></span> <span data-ttu-id="61017-120">Se ad esempio originariamente creata la tabella come `ROUND_ROBIN` e ora si desidera modificarlo tooa tabella distribuiti in una colonna, `CTAS` è come sarebbe stato necessario modificare la colonna di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="61017-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it tooa table distributed on a column, `CTAS` is how you would change hello distribution column.</span></span> <span data-ttu-id="61017-121">`CTAS`può anche essere toochange utilizzati tipi di partizionamento, l'indicizzazione o di colonna.</span><span class="sxs-lookup"><span data-stu-id="61017-121">`CTAS` can also be used toochange partitioning, indexing, or column types.</span></span>

<span data-ttu-id="61017-122">Si supponga che per creare questa tabella con tipo di distribuzione predefinito di hello `ROUND_ROBIN` distribuita poiché è stata specificata alcuna colonna di distribuzione in hello `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="61017-122">Let's say you created this table using hello default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in hello `CREATE TABLE`.</span></span>

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

<span data-ttu-id="61017-123">Si desidera ora toocreate una nuova copia di questa tabella con un indice Columnstore cluster in modo che è possibile sfruttare le prestazioni di hello delle tabelle Columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="61017-123">Now you want toocreate a new copy of this table with a Clustered Columnstore Index so that you can take advantage of hello performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="61017-124">È anche opportuno toodistribute la tabella nella ProductKey poiché si sono prevedendo join su questa colonna e si desidera tooavoid lo spostamento di dati durante l'unione in ProductKey join.</span><span class="sxs-lookup"><span data-stu-id="61017-124">You also want toodistribute this table on ProductKey since you are anticipating joins on this column and want tooavoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="61017-125">Infine è tooadd partizionamento in OrderDateKey in modo che è possibile eliminare rapidamente dati precedenti l'eliminazione di partizioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="61017-125">Lastly you also want tooadd partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="61017-126">Ecco l'istruzione un'istruzione CTAS hello copiava la vecchia tabella in una nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="61017-126">Here is hello CTAS statement which would copy your old table into a new table.</span></span>

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

<span data-ttu-id="61017-127">Infine è possibile rinominare le tabelle tooswap nella nuova tabella e quindi eliminare la tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="61017-127">Finally you can rename your tables tooswap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="61017-128">SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.</span><span class="sxs-lookup"><span data-stu-id="61017-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="61017-129">Ordine tooget hello prestazioni migliori dalle query, è importante creare statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento hello o si verificano modifiche sostanziali in dati hello.</span><span class="sxs-lookup"><span data-stu-id="61017-129">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="61017-130">Per una spiegazione dettagliata delle statistiche, vedere hello [statistiche] [ Statistics] argomento nel gruppo di sviluppare hello degli argomenti.</span><span class="sxs-lookup"><span data-stu-id="61017-130">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a><span data-ttu-id="61017-131">Utilizzando un'istruzione CTAS toowork intorno a funzionalità non supportate</span><span class="sxs-lookup"><span data-stu-id="61017-131">Using CTAS toowork around unsupported features</span></span>
<span data-ttu-id="61017-132">`CTAS`può inoltre essere utilizzati toowork intorno a un numero di funzionalità non supportata hello elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="61017-132">`CTAS` can also be used toowork around a number of hello unsupported features listed below.</span></span> <span data-ttu-id="61017-133">Questo può spesso risultare toobe una situazione win/win come non solo il codice sarà conforme, ma verranno spesso eseguite più velocemente in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="61017-133">This can often prove toobe a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="61017-134">Si tratta del risultato della progettazione completamente parallelizzata.</span><span class="sxs-lookup"><span data-stu-id="61017-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="61017-135">Gli scenari che è possibile trattare con CTAS includono:</span><span class="sxs-lookup"><span data-stu-id="61017-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="61017-136">ANSI JOINS su UPDATE</span><span class="sxs-lookup"><span data-stu-id="61017-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="61017-137">ANSI JOINs su DELETE</span><span class="sxs-lookup"><span data-stu-id="61017-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="61017-138">Istruzione MERGE</span><span class="sxs-lookup"><span data-stu-id="61017-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="61017-139">Provare a toothink "un'istruzione CTAS prima".</span><span class="sxs-lookup"><span data-stu-id="61017-139">Try toothink "CTAS first".</span></span> <span data-ttu-id="61017-140">Se si ritiene che sia possibile risolvere un problema di mediante `CTAS` che è in genere tooapproach modo migliore di hello, anche se si siano scrivendo più dati, di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="61017-140">If you think you can solve a problem using `CTAS` then that is generally hello best way tooapproach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="61017-141">Sostituzione di join ANSI per le istruzioni update</span><span class="sxs-lookup"><span data-stu-id="61017-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="61017-142">È possibile che si dispone di un aggiornamento complesso che unisce in join più di due tabelle utilizzando hello tooperform sintassi join ANSI UPDATE o DELETE.</span><span class="sxs-lookup"><span data-stu-id="61017-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax tooperform hello UPDATE or DELETE.</span></span>

<span data-ttu-id="61017-143">Si supponga che era tooupdate questa tabella:</span><span class="sxs-lookup"><span data-stu-id="61017-143">Imagine you had tooupdate this table:</span></span>

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

<span data-ttu-id="61017-144">la query originale Hello potrebbe siano presenti simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="61017-144">hello original query might have looked something like this:</span></span>

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

<span data-ttu-id="61017-145">Poiché SQL Data Warehouse non supporta ANSI unisce in hello `FROM` clausola di un `UPDATE` istruzione, non è possibile copiare questo codice su senza modificarla leggermente.</span><span class="sxs-lookup"><span data-stu-id="61017-145">Since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="61017-146">È possibile utilizzare una combinazione di un `CTAS` e implicita join tooreplace questo codice:</span><span class="sxs-lookup"><span data-stu-id="61017-146">You can use a combination of a `CTAS` and an implicit join tooreplace this code:</span></span>

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

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="61017-147">Sostituzione di join ANSI per le istruzioni delete</span><span class="sxs-lookup"><span data-stu-id="61017-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="61017-148">In alcuni casi hello migliore approccio per l'eliminazione dei dati è toouse `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="61017-148">Sometimes hello best approach for deleting data is toouse `CTAS`.</span></span> <span data-ttu-id="61017-149">Anziché di eliminazione dei dati di hello semplicemente selezionare hello dati tookeep.</span><span class="sxs-lookup"><span data-stu-id="61017-149">Rather than deleting hello data simply select hello data you want tookeep.</span></span> <span data-ttu-id="61017-150">Questo particolarmente vero per `DELETE` le istruzioni che utilizzano ansi join di sintassi perché SQL Data Warehouse non supporta i join ANSI in hello `FROM` clausola di un `DELETE` istruzione.</span><span class="sxs-lookup"><span data-stu-id="61017-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="61017-151">Un esempio di istruzione DELETE convertita è disponibile di seguito:</span><span class="sxs-lookup"><span data-stu-id="61017-151">An example of a converted DELETE statement is available below:</span></span>

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

## <a name="replace-merge-statements"></a><span data-ttu-id="61017-152">Sostituzione delle istruzioni merge</span><span class="sxs-lookup"><span data-stu-id="61017-152">Replace merge statements</span></span>
<span data-ttu-id="61017-153">Le istruzioni merge possono essere sostituite, almeno in parte, usando `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="61017-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="61017-154">È possibile consolidare hello `INSERT` hello e `UPDATE` in una singola istruzione.</span><span class="sxs-lookup"><span data-stu-id="61017-154">You can consolidate hello `INSERT` and hello `UPDATE` into a single statement.</span></span> <span data-ttu-id="61017-155">Qualsiasi record eliminato sarebbe necessario toobe chiuso in una seconda istruzione.</span><span class="sxs-lookup"><span data-stu-id="61017-155">Any deleted records would need toobe closed off in a second statement.</span></span>

<span data-ttu-id="61017-156">Un esempio di `UPSERT` è riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="61017-156">An example of an `UPSERT` is available below:</span></span>

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

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="61017-157">Raccomandazione CTAS: dichiarare in modo esplicito il tipo di dati e il supporto di valori null di output</span><span class="sxs-lookup"><span data-stu-id="61017-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="61017-158">Durante la migrazione del codice, è possibile imbattersi in questo tipo di modello di codifica:</span><span class="sxs-lookup"><span data-stu-id="61017-158">When migrating code you might find you run across this type of coding pattern:</span></span>

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

<span data-ttu-id="61017-159">Si pensi istintivamente è necessario eseguire la migrazione di questo tooa codice un'istruzione CTAS e sarebbe corretta.</span><span class="sxs-lookup"><span data-stu-id="61017-159">Instinctively you might think you should migrate this code tooa CTAS and you would be correct.</span></span> <span data-ttu-id="61017-160">Tuttavia, esiste un problema nascosto.</span><span class="sxs-lookup"><span data-stu-id="61017-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="61017-161">Hello codice riportato di seguito non produce hello stesso risultato:</span><span class="sxs-lookup"><span data-stu-id="61017-161">hello following code does NOT yield hello same result:</span></span>

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

<span data-ttu-id="61017-162">Si noti che il risultato"hello colonne" estende valori hello dati tipo e il supporto di valori null dell'espressione hello.</span><span class="sxs-lookup"><span data-stu-id="61017-162">Notice that hello column "result" carries forward hello data type and nullability values of hello expression.</span></span> <span data-ttu-id="61017-163">Se non si è attenzione, questo può causare toosubtle variazioni nei valori.</span><span class="sxs-lookup"><span data-stu-id="61017-163">This can lead toosubtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="61017-164">Provare seguenti hello ad esempio:</span><span class="sxs-lookup"><span data-stu-id="61017-164">Try hello following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="61017-165">il valore di Hello archiviato per il risultato è diverso.</span><span class="sxs-lookup"><span data-stu-id="61017-165">hello value stored for result is different.</span></span> <span data-ttu-id="61017-166">Errore hello espressioni hello persistente valore nella colonna di risultati hello viene utilizzato in altre diventa ancora più significativo.</span><span class="sxs-lookup"><span data-stu-id="61017-166">As hello persisted value in hello result column is used in other expressions hello error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="61017-167">Ciò è particolarmente importante per le migrazioni di dati.</span><span class="sxs-lookup"><span data-stu-id="61017-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="61017-168">Anche se probabilmente più accurate query secondo hello è un problema.</span><span class="sxs-lookup"><span data-stu-id="61017-168">Even though hello second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="61017-169">dati Hello sarebbe toohello confrontati diverso sistema di origine e tooquestions dell'integrità che comporta la migrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="61017-169">hello data would be different compared toohello source system and that leads tooquestions of integrity in hello migration.</span></span> <span data-ttu-id="61017-170">Questo è uno dei rari casi in cui destra di hello effettivamente una risposta "corretto" hello!</span><span class="sxs-lookup"><span data-stu-id="61017-170">This is one of those rare cases where hello "wrong" answer is actually hello right one!</span></span>

<span data-ttu-id="61017-171">Hello motivo, è possibile notare questo disparità tra i risultati di due hello è inattivo tooimplicit cast di tipo.</span><span class="sxs-lookup"><span data-stu-id="61017-171">hello reason we see this disparity between hello two results is down tooimplicit type casting.</span></span> <span data-ttu-id="61017-172">Prima tabella di esempio hello hello definisce la definizione di colonna hello.</span><span class="sxs-lookup"><span data-stu-id="61017-172">In hello first example hello table defines hello column definition.</span></span> <span data-ttu-id="61017-173">Quando viene inserita la riga hello si verifica una conversione implicita del tipo.</span><span class="sxs-lookup"><span data-stu-id="61017-173">When hello row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="61017-174">Nel secondo esempio hello non è alcuna conversione implicita del tipo come espressione hello definisce il tipo di dati della colonna hello.</span><span class="sxs-lookup"><span data-stu-id="61017-174">In hello second example there is no implicit type conversion as hello expression defines data type of hello column.</span></span> <span data-ttu-id="61017-175">Si noti che la colonna nel secondo esempio hello hello è stata definita come una colonna che ammette valori null mentre nel primo esempio hello non sia.</span><span class="sxs-lookup"><span data-stu-id="61017-175">Notice also that hello column in hello second example has been defined as a NULLable column whereas in hello first example it has not.</span></span> <span data-ttu-id="61017-176">Creazione tabella hello in hello primo esempio colonna ammissione di valori null è stata definita in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="61017-176">When hello table was created in hello first example column nullability was explicitly defined.</span></span> <span data-ttu-id="61017-177">Nel secondo esempio hello è stato appena uscito toohello espressione e per impostazione predefinita questo porterebbe a una definizione di NULL.</span><span class="sxs-lookup"><span data-stu-id="61017-177">In hello second example it was just left toohello expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="61017-178">tooresolve questi problemi, è necessario impostare esplicitamente la conversione di tipo hello e supporto di valori null in hello `SELECT` parte hello `CTAS` istruzione.</span><span class="sxs-lookup"><span data-stu-id="61017-178">tooresolve these issues you must explicitly set hello type conversion and nullability in hello `SELECT` portion of hello `CTAS` statement.</span></span> <span data-ttu-id="61017-179">Non è possibile impostare queste proprietà in hello creare parte di tabella.</span><span class="sxs-lookup"><span data-stu-id="61017-179">You cannot set these properties in hello create table part.</span></span>

<span data-ttu-id="61017-180">Hello riportato di seguito come toofix hello codice:</span><span class="sxs-lookup"><span data-stu-id="61017-180">hello example below demonstrates how toofix hello code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="61017-181">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="61017-181">Note hello following:</span></span>

* <span data-ttu-id="61017-182">Era possibile usare CAST o CONVERT</span><span class="sxs-lookup"><span data-stu-id="61017-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="61017-183">ISNULL viene utilizzato tooforce ammissione di valori null non COALESCE</span><span class="sxs-lookup"><span data-stu-id="61017-183">ISNULL is used tooforce NULLability not COALESCE</span></span>
* <span data-ttu-id="61017-184">ISNULL è più esterno della funzione hello</span><span class="sxs-lookup"><span data-stu-id="61017-184">ISNULL is hello outermost function</span></span>
* <span data-ttu-id="61017-185">Hello seconda parte hello ISNULL è una costante, ovvero 0</span><span class="sxs-lookup"><span data-stu-id="61017-185">hello second part of hello ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="61017-186">Per hello ammissione di valori null toobe impostato correttamente è essenziale toouse `ISNULL` e non `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="61017-186">For hello nullability toobe correctly set it is vital toouse `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="61017-187">`COALESCE`non è una funzione deterministica e pertanto il risultato di hello di hello espressione sarà sempre ammette valori null.</span><span class="sxs-lookup"><span data-stu-id="61017-187">`COALESCE` is not a deterministic function and so hello result of hello expression will always be NULLable.</span></span> <span data-ttu-id="61017-188">`ISNULL` è diverso.</span><span class="sxs-lookup"><span data-stu-id="61017-188">`ISNULL` is different.</span></span> <span data-ttu-id="61017-189">È deterministico.</span><span class="sxs-lookup"><span data-stu-id="61017-189">It is deterministic.</span></span> <span data-ttu-id="61017-190">Pertanto quando hello seconda parte di hello `ISNULL` funzione è una costante o un valore letterale, valore risultante di hello sarà non NULL.</span><span class="sxs-lookup"><span data-stu-id="61017-190">Therefore when hello second part of hello `ISNULL` function is a constant or a literal then hello resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="61017-191">Questo suggerimento non è utile solo per garantire l'integrità di hello dei calcoli.</span><span class="sxs-lookup"><span data-stu-id="61017-191">This tip is not just useful for ensuring hello integrity of your calculations.</span></span> <span data-ttu-id="61017-192">È importante anche per il cambio di partizione della tabella.</span><span class="sxs-lookup"><span data-stu-id="61017-192">It is also important for table partition switching.</span></span> <span data-ttu-id="61017-193">Si supponga di disporre di questa tabella definita come dato di fatto:</span><span class="sxs-lookup"><span data-stu-id="61017-193">Imagine you have this table defined as your fact:</span></span>

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

<span data-ttu-id="61017-194">Campo del valore hello invece un'espressione calcolata non è parte di dati di origine hello.</span><span class="sxs-lookup"><span data-stu-id="61017-194">However, hello value field is a calculated expression it is not part of hello source data.</span></span>

<span data-ttu-id="61017-195">toocreate il set di dati partizionati è toodo questo:</span><span class="sxs-lookup"><span data-stu-id="61017-195">toocreate your partitioned dataset you might want toodo this:</span></span>

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

<span data-ttu-id="61017-196">Hello verrebbe eseguita ottimale.</span><span class="sxs-lookup"><span data-stu-id="61017-196">hello query would run perfectly fine.</span></span> <span data-ttu-id="61017-197">problema di Hello viene fornito quando si tenta di cambio di partizione tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="61017-197">hello problem comes when you try tooperform hello partition switch.</span></span> <span data-ttu-id="61017-198">le definizioni di tabella Hello non corrispondono.</span><span class="sxs-lookup"><span data-stu-id="61017-198">hello table definitions do not match.</span></span> <span data-ttu-id="61017-199">le definizioni di tabella hello toomake corrispondano hello che un'istruzione CTAS deve toobe modificato.</span><span class="sxs-lookup"><span data-stu-id="61017-199">toomake hello table definitions match hello CTAS needs toobe modified.</span></span>

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

<span data-ttu-id="61017-200">Pertanto è possibile vedere che la coerenza del tipo e le proprietà di gestione del supporto di valori null in CTAS è un’ottima procedura tecnica consigliata.</span><span class="sxs-lookup"><span data-stu-id="61017-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="61017-201">Consente di integrità toomaintain nei calcoli e assicura anche che sia possibile cambio della partizione.</span><span class="sxs-lookup"><span data-stu-id="61017-201">It helps toomaintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="61017-202">Per ulteriori informazioni sull'utilizzo, vedere tooMSDN [un'istruzione CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="61017-202">Please refer tooMSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="61017-203">È uno dei più importanti istruzioni di hello in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="61017-203">It is one of hello most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="61017-204">Assicurarsi di averla compresa completamente.</span><span class="sxs-lookup"><span data-stu-id="61017-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61017-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61017-205">Next steps</span></span>
<span data-ttu-id="61017-206">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="61017-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
