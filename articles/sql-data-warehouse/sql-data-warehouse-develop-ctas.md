---
title: Create Table As Select (CTAS) in SQL Data Warehouse | Microsoft Docs
description: "Suggerimenti per la codifica con l’istruzione create table as select (CTAS) in SQL Data Warehouse di Azure per lo sviluppo di soluzioni."
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
ms.openlocfilehash: cb08313726e8135feaa9b413937c2197ea397f4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="eef7f-103">Create Table As Select (CTAS) in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="eef7f-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="eef7f-104">Create Table As Select o `CTAS` è una delle funzionalità più importanti disponibili in T-SQL.</span><span class="sxs-lookup"><span data-stu-id="eef7f-104">Create table as select or `CTAS` is one of the most important T-SQL features available.</span></span> <span data-ttu-id="eef7f-105">È un'operazione completamente parallelizzata che crea una nuova tabella basata sull'output di un'istruzione SELECT.</span><span class="sxs-lookup"><span data-stu-id="eef7f-105">It is a fully parallelized operation that creates a new table based on the output of a SELECT statement.</span></span> <span data-ttu-id="eef7f-106">`CTAS` è il modo più semplice e veloce di creare la copia di una tabella.</span><span class="sxs-lookup"><span data-stu-id="eef7f-106">`CTAS` is the simplest and fastest way to create a copy of a table.</span></span> <span data-ttu-id="eef7f-107">Questo documento offre esempi e procedure consigliate per `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="eef7f-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="eef7f-108">SELECT..INTO e CTAS</span><span class="sxs-lookup"><span data-stu-id="eef7f-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="eef7f-109">È possibile considerare `CTAS` come una versione più potente di `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="eef7f-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="eef7f-110">Di seguito è riportato un esempio di un'istruzione semplice `SELECT..INTO`:</span><span class="sxs-lookup"><span data-stu-id="eef7f-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="eef7f-111">Nell'esempio precedente `[dbo].[FactInternetSales_new]` viene creata come una tabella ROUND_ROBIN distribuita con un'istruzione CLUSTERED COLUMNSTORE INDEX in quanto questi sono i valori predefiniti delle tabelle in SQL Data Warehouse di Azure.</span><span class="sxs-lookup"><span data-stu-id="eef7f-111">In the example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are the table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="eef7f-112">Tuttavia `SELECT..INTO` non consente di modificare il metodo di distribuzione o il tipo di indice come parte dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="eef7f-112">`SELECT..INTO` however does not allow you to change either the distribution method or the index type as part of the operation.</span></span> <span data-ttu-id="eef7f-113">Qui è dove si posiziona `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="eef7f-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="eef7f-114">Convertire l'istruzione precedente in `CTAS` è semplice:</span><span class="sxs-lookup"><span data-stu-id="eef7f-114">To convert the above to `CTAS` is quite straight-forward:</span></span>

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

<span data-ttu-id="eef7f-115">Con `CTAS` è possibile modificare sia la distribuzione dei dati che il tipo della tabella.</span><span class="sxs-lookup"><span data-stu-id="eef7f-115">With `CTAS` you are able to change both the distribution of the table data as well as the table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="eef7f-116">Se si intende solo modificare l'indice nell'operazione `CTAS` e la tabella di origine è con distribuzione hash, è possibile che l'operazione `CTAS` possa essere eseguita in modo ottimale se si mantiene la stessa distribuzione di colonne e tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="eef7f-116">If you are only trying to change the index in your `CTAS` operation and the source table is hash distributed then your `CTAS` operation will perform best if you maintain the same distribution column and data type.</span></span> <span data-ttu-id="eef7f-117">In questo modo si eviteranno spostamenti incrociati di distribuzione di dati durante le operazioni con migliori risultati.</span><span class="sxs-lookup"><span data-stu-id="eef7f-117">This will avoid cross distribution data movement during the operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-to-copy-a-table"></a><span data-ttu-id="eef7f-118">Uso di CTAS per copiare una tabella</span><span class="sxs-lookup"><span data-stu-id="eef7f-118">Using CTAS to copy a table</span></span>
<span data-ttu-id="eef7f-119">Probabilmente uno degli usi più comuni di `CTAS` consiste nel creare una copia di una tabella in modo da poter modificare il DDL.</span><span class="sxs-lookup"><span data-stu-id="eef7f-119">Perhaps one of the most common uses of `CTAS` is creating a copy of a table so that you can change the DDL.</span></span> <span data-ttu-id="eef7f-120">Se ad esempio la tabella è stata originariamente creata come `ROUND_ROBIN` e ora si vuole modificarla in una tabella distribuita su una colonna, `CTAS` rappresenta il metodo di modifica della colonna di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="eef7f-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it to a table distributed on a column, `CTAS` is how you would change the distribution column.</span></span> <span data-ttu-id="eef7f-121">`CTAS` anche per modificare il partizionamento, l'indicizzazione o i tipi di colonna.</span><span class="sxs-lookup"><span data-stu-id="eef7f-121">`CTAS` can also be used to change partitioning, indexing, or column types.</span></span>

<span data-ttu-id="eef7f-122">Si supponga che questa tabella sia stata creata usando il tipo di distribuzione predefinito di `ROUND_ROBIN` distribuito, in quanto non è stata specificata alcuna colonna di distribuzione in `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="eef7f-122">Let's say you created this table using the default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in the `CREATE TABLE`.</span></span>

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

<span data-ttu-id="eef7f-123">Ora si desidera creare una nuova copia di questa tabella con un indice cluster columnstore, in modo da poter sfruttare le prestazioni delle tabelle cluster columnstore.</span><span class="sxs-lookup"><span data-stu-id="eef7f-123">Now you want to create a new copy of this table with a Clustered Columnstore Index so that you can take advantage of the performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="eef7f-124">Si desidera anche distribuire la tabella in ProductKey, poiché si prevedono join per la colonna e si desidera evitare lo spostamento dei dati durante i join in ProductKey.</span><span class="sxs-lookup"><span data-stu-id="eef7f-124">You also want to distribute this table on ProductKey since you are anticipating joins on this column and want to avoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="eef7f-125">Infine, si desidera aggiungere il partizionamento in OrderDateKey in modo da poter eliminare rapidamente i vecchi dati eliminando le vecchie partizioni.</span><span class="sxs-lookup"><span data-stu-id="eef7f-125">Lastly you also want to add partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="eef7f-126">Di seguito è riportata l'istruzione CTAS per copiare la vecchia tabella in una nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="eef7f-126">Here is the CTAS statement which would copy your old table into a new table.</span></span>

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

<span data-ttu-id="eef7f-127">È infine possibile rinominare le tabelle in modo da scambiare la nuova tabella ed eliminare quella precedente.</span><span class="sxs-lookup"><span data-stu-id="eef7f-127">Finally you can rename your tables to swap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="eef7f-128">SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.</span><span class="sxs-lookup"><span data-stu-id="eef7f-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="eef7f-129">Per ottenere le migliori prestazioni dalle query, è importante creare statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento o dopo eventuali modifiche sostanziali dei dati.</span><span class="sxs-lookup"><span data-stu-id="eef7f-129">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="eef7f-130">Per una spiegazione dettagliata delle statistiche, vedere l'argomento [Statistiche][Statistics] nel gruppo di argomenti sullo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="eef7f-130">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-to-work-around-unsupported-features"></a><span data-ttu-id="eef7f-131">Uso di CTAS per ovviare a funzionalità non supportate</span><span class="sxs-lookup"><span data-stu-id="eef7f-131">Using CTAS to work around unsupported features</span></span>
<span data-ttu-id="eef7f-132">`CTAS` per ovviare a problemi derivanti da alcune funzionalità non supportate elencate di seguito.</span><span class="sxs-lookup"><span data-stu-id="eef7f-132">`CTAS` can also be used to work around a number of the unsupported features listed below.</span></span> <span data-ttu-id="eef7f-133">Questo può spesso rivelarsi una situazione favorevole in quando non solo il codice sarà conforme, ma l’esecuzione sarà più veloce in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="eef7f-133">This can often prove to be a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="eef7f-134">Si tratta del risultato della progettazione completamente parallelizzata.</span><span class="sxs-lookup"><span data-stu-id="eef7f-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="eef7f-135">Gli scenari che è possibile trattare con CTAS includono:</span><span class="sxs-lookup"><span data-stu-id="eef7f-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="eef7f-136">ANSI JOINS su UPDATE</span><span class="sxs-lookup"><span data-stu-id="eef7f-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="eef7f-137">ANSI JOINs su DELETE</span><span class="sxs-lookup"><span data-stu-id="eef7f-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="eef7f-138">Istruzione MERGE</span><span class="sxs-lookup"><span data-stu-id="eef7f-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="eef7f-139">Provare a considerare "prima CTAS".</span><span class="sxs-lookup"><span data-stu-id="eef7f-139">Try to think "CTAS first".</span></span> <span data-ttu-id="eef7f-140">Se si ritiene che sia possibile risolvere un problema con `CTAS` , questo approccio in genere si rivela la scelta migliore, anche se è necessario scrivere più dati.</span><span class="sxs-lookup"><span data-stu-id="eef7f-140">If you think you can solve a problem using `CTAS` then that is generally the best way to approach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="eef7f-141">Sostituzione di join ANSI per le istruzioni update</span><span class="sxs-lookup"><span data-stu-id="eef7f-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="eef7f-142">È possibile che si dispone di un aggiornamento complesso che unisce in join più di due tabelle utilizzando la sintassi di join ANSI per eseguire un’istruzione UPDATE o DELETE.</span><span class="sxs-lookup"><span data-stu-id="eef7f-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax to perform the UPDATE or DELETE.</span></span>

<span data-ttu-id="eef7f-143">Si immagini di dover aggiornare questa tabella:</span><span class="sxs-lookup"><span data-stu-id="eef7f-143">Imagine you had to update this table:</span></span>

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

<span data-ttu-id="eef7f-144">La query originale potrebbe essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="eef7f-144">The original query might have looked something like this:</span></span>

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

<span data-ttu-id="eef7f-145">Poiché SQL Data Warehouse non supporta i join ANSI nella clausola `FROM` di un'istruzione `UPDATE`, non è possibile copiare questo codice senza modificarlo leggermente.</span><span class="sxs-lookup"><span data-stu-id="eef7f-145">Since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="eef7f-146">È possibile combinare `CTAS` con un join implicito per sostituire questo codice:</span><span class="sxs-lookup"><span data-stu-id="eef7f-146">You can use a combination of a `CTAS` and an implicit join to replace this code:</span></span>

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

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="eef7f-147">Sostituzione di join ANSI per le istruzioni delete</span><span class="sxs-lookup"><span data-stu-id="eef7f-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="eef7f-148">Talvolta l'uso di `CTAS`si rivela l'approccio migliore per l'eliminazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="eef7f-148">Sometimes the best approach for deleting data is to use `CTAS`.</span></span> <span data-ttu-id="eef7f-149">Invece di eliminare i dati, si selezionano semplicemente i dati da mantenere.</span><span class="sxs-lookup"><span data-stu-id="eef7f-149">Rather than deleting the data simply select the data you want to keep.</span></span> <span data-ttu-id="eef7f-150">Ciò vale soprattutto per le istruzioni `DELETE` che usano la sintassi di join ANSI, in quanto SQL Data Warehouse non supporta i join ANSI nella clausola `FROM` di un'istruzione `DELETE`.</span><span class="sxs-lookup"><span data-stu-id="eef7f-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="eef7f-151">Un esempio di istruzione DELETE convertita è disponibile di seguito:</span><span class="sxs-lookup"><span data-stu-id="eef7f-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="eef7f-152">Sostituzione delle istruzioni merge</span><span class="sxs-lookup"><span data-stu-id="eef7f-152">Replace merge statements</span></span>
<span data-ttu-id="eef7f-153">Le istruzioni merge possono essere sostituite, almeno in parte, usando `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="eef7f-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="eef7f-154">È possibile consolidare `INSERT` e `UPDATE` in un'unica istruzione.</span><span class="sxs-lookup"><span data-stu-id="eef7f-154">You can consolidate the `INSERT` and the `UPDATE` into a single statement.</span></span> <span data-ttu-id="eef7f-155">Tutti i record eliminati dovevano essere chiusi in una seconda istruzione.</span><span class="sxs-lookup"><span data-stu-id="eef7f-155">Any deleted records would need to be closed off in a second statement.</span></span>

<span data-ttu-id="eef7f-156">Un esempio di `UPSERT` è riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="eef7f-156">An example of an `UPSERT` is available below:</span></span>

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

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="eef7f-157">Raccomandazione CTAS: dichiarare in modo esplicito il tipo di dati e il supporto di valori null di output</span><span class="sxs-lookup"><span data-stu-id="eef7f-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="eef7f-158">Durante la migrazione del codice, è possibile imbattersi in questo tipo di modello di codifica:</span><span class="sxs-lookup"><span data-stu-id="eef7f-158">When migrating code you might find you run across this type of coding pattern:</span></span>

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

<span data-ttu-id="eef7f-159">Istintivamente si potrebbe pensare che è necessario eseguire la migrazione di questo codice a CTAS e sarebbe un’operazione corretta.</span><span class="sxs-lookup"><span data-stu-id="eef7f-159">Instinctively you might think you should migrate this code to a CTAS and you would be correct.</span></span> <span data-ttu-id="eef7f-160">Tuttavia, esiste un problema nascosto.</span><span class="sxs-lookup"><span data-stu-id="eef7f-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="eef7f-161">Il codice seguente NON produce lo stesso risultato:</span><span class="sxs-lookup"><span data-stu-id="eef7f-161">The following code does NOT yield the same result:</span></span>

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

<span data-ttu-id="eef7f-162">Si noti che la colonna "result" porta avanti i valori del tipo di dati e del supporto di valori null dell'espressione.</span><span class="sxs-lookup"><span data-stu-id="eef7f-162">Notice that the column "result" carries forward the data type and nullability values of the expression.</span></span> <span data-ttu-id="eef7f-163">Ciò può causare lievi variazioni nei valori, se non si presta attenzione.</span><span class="sxs-lookup"><span data-stu-id="eef7f-163">This can lead to subtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="eef7f-164">Provare a eseguire il seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="eef7f-164">Try the following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="eef7f-165">Il valore archiviato per il risultato è diverso.</span><span class="sxs-lookup"><span data-stu-id="eef7f-165">The value stored for result is different.</span></span> <span data-ttu-id="eef7f-166">Poiché il valore persistente della colonna result viene utilizzato in altre espressioni, l'errore diventa ancora più significativo.</span><span class="sxs-lookup"><span data-stu-id="eef7f-166">As the persisted value in the result column is used in other expressions the error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="eef7f-167">Ciò è particolarmente importante per le migrazioni di dati.</span><span class="sxs-lookup"><span data-stu-id="eef7f-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="eef7f-168">Anche se la seconda query è senza dubbio più accurata, esiste un problema.</span><span class="sxs-lookup"><span data-stu-id="eef7f-168">Even though the second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="eef7f-169">I dati sono diversi rispetto al sistema di origine e ciò comporta problemi di integrità della migrazione.</span><span class="sxs-lookup"><span data-stu-id="eef7f-169">The data would be different compared to the source system and that leads to questions of integrity in the migration.</span></span> <span data-ttu-id="eef7f-170">Questo è uno dei rari casi in cui la risposta "errata" è effettivamente quella corretta.</span><span class="sxs-lookup"><span data-stu-id="eef7f-170">This is one of those rare cases where the "wrong" answer is actually the right one!</span></span>

<span data-ttu-id="eef7f-171">Il motivo per cui esiste questa differenza tra i due risultati è costituito dal cast implicito del tipo.</span><span class="sxs-lookup"><span data-stu-id="eef7f-171">The reason we see this disparity between the two results is down to implicit type casting.</span></span> <span data-ttu-id="eef7f-172">Nel primo esempio la tabella specifica la definizione di colonna.</span><span class="sxs-lookup"><span data-stu-id="eef7f-172">In the first example the table defines the column definition.</span></span> <span data-ttu-id="eef7f-173">Quando la riga viene inserita si verifica una conversione implicita del tipo.</span><span class="sxs-lookup"><span data-stu-id="eef7f-173">When the row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="eef7f-174">Nel secondo esempio non esiste alcuna conversione implicita del tipo poiché l'espressione definisce il tipo di dati della colonna.</span><span class="sxs-lookup"><span data-stu-id="eef7f-174">In the second example there is no implicit type conversion as the expression defines data type of the column.</span></span> <span data-ttu-id="eef7f-175">Si noti inoltre che la colonna nel secondo esempio è stata definita come una colonna che ammette valori null, mentre nel primo esempio non lo è.</span><span class="sxs-lookup"><span data-stu-id="eef7f-175">Notice also that the column in the second example has been defined as a NULLable column whereas in the first example it has not.</span></span> <span data-ttu-id="eef7f-176">Quando la tabella è stata creata nel primo esempio, il supporto di valori null della colonna è stato definito in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="eef7f-176">When the table was created in the first example column nullability was explicitly defined.</span></span> <span data-ttu-id="eef7f-177">Nel secondo esempio, è stato affidato all'espressione che per impostazione predefinita comporterebbe una definizione NULL.</span><span class="sxs-lookup"><span data-stu-id="eef7f-177">In the second example it was just left to the expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="eef7f-178">Per risolvere questi problemi è necessario impostare esplicitamente la conversione del tipo e il supporto di valori Null nella parte `SELECT` dell'istruzione `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="eef7f-178">To resolve these issues you must explicitly set the type conversion and nullability in the `SELECT` portion of the `CTAS` statement.</span></span> <span data-ttu-id="eef7f-179">Non è possibile impostare queste proprietà nella parte relativa alla creazione della tabella.</span><span class="sxs-lookup"><span data-stu-id="eef7f-179">You cannot set these properties in the create table part.</span></span>

<span data-ttu-id="eef7f-180">Il seguente esempio illustra come correggere il codice:</span><span class="sxs-lookup"><span data-stu-id="eef7f-180">The example below demonstrates how to fix the code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="eef7f-181">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="eef7f-181">Note the following:</span></span>

* <span data-ttu-id="eef7f-182">Era possibile usare CAST o CONVERT</span><span class="sxs-lookup"><span data-stu-id="eef7f-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="eef7f-183">ISNULL viene usato per forzare NULLability e non COALESCE</span><span class="sxs-lookup"><span data-stu-id="eef7f-183">ISNULL is used to force NULLability not COALESCE</span></span>
* <span data-ttu-id="eef7f-184">ISNULL è la funzione più esterna</span><span class="sxs-lookup"><span data-stu-id="eef7f-184">ISNULL is the outermost function</span></span>
* <span data-ttu-id="eef7f-185">La seconda parte di ISNULL è una costante, ad esempio 0</span><span class="sxs-lookup"><span data-stu-id="eef7f-185">The second part of the ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="eef7f-186">Per impostare correttamente il supporto di valori Null è fondamentale usare `ISNULL` e non `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="eef7f-186">For the nullability to be correctly set it is vital to use `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="eef7f-187">`COALESCE` non è una funzione deterministica e pertanto il risultato dell'espressione sarà sempre NULLable.</span><span class="sxs-lookup"><span data-stu-id="eef7f-187">`COALESCE` is not a deterministic function and so the result of the expression will always be NULLable.</span></span> <span data-ttu-id="eef7f-188">`ISNULL` è diverso.</span><span class="sxs-lookup"><span data-stu-id="eef7f-188">`ISNULL` is different.</span></span> <span data-ttu-id="eef7f-189">È deterministico.</span><span class="sxs-lookup"><span data-stu-id="eef7f-189">It is deterministic.</span></span> <span data-ttu-id="eef7f-190">Pertanto quando la seconda parte della funzione `ISNULL` è una costante o un valore letterale, il valore risultante sarà NOT NULL.</span><span class="sxs-lookup"><span data-stu-id="eef7f-190">Therefore when the second part of the `ISNULL` function is a constant or a literal then the resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="eef7f-191">Questo suggerimento non è utile solo per garantire l'integrità dei calcoli.</span><span class="sxs-lookup"><span data-stu-id="eef7f-191">This tip is not just useful for ensuring the integrity of your calculations.</span></span> <span data-ttu-id="eef7f-192">È importante anche per il cambio di partizione della tabella.</span><span class="sxs-lookup"><span data-stu-id="eef7f-192">It is also important for table partition switching.</span></span> <span data-ttu-id="eef7f-193">Si supponga di disporre di questa tabella definita come dato di fatto:</span><span class="sxs-lookup"><span data-stu-id="eef7f-193">Imagine you have this table defined as your fact:</span></span>

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

<span data-ttu-id="eef7f-194">Tuttavia, il campo del valore è un'espressione calcolata che non fa parte dei dati di origine.</span><span class="sxs-lookup"><span data-stu-id="eef7f-194">However, the value field is a calculated expression it is not part of the source data.</span></span>

<span data-ttu-id="eef7f-195">Per creare il set di dati partizionati è possibile eseguire questa operazione:</span><span class="sxs-lookup"><span data-stu-id="eef7f-195">To create your partitioned dataset you might want to do this:</span></span>

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

<span data-ttu-id="eef7f-196">La query verrebbe eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="eef7f-196">The query would run perfectly fine.</span></span> <span data-ttu-id="eef7f-197">Il problema sorge quando si tenta di eseguire il cambio di partizione.</span><span class="sxs-lookup"><span data-stu-id="eef7f-197">The problem comes when you try to perform the partition switch.</span></span> <span data-ttu-id="eef7f-198">Le definizioni di tabella non corrispondono.</span><span class="sxs-lookup"><span data-stu-id="eef7f-198">The table definitions do not match.</span></span> <span data-ttu-id="eef7f-199">Per far corrispondere le definizioni di tabella è necessario modificare CTAS.</span><span class="sxs-lookup"><span data-stu-id="eef7f-199">To make the table definitions match the CTAS needs to be modified.</span></span>

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

<span data-ttu-id="eef7f-200">Pertanto è possibile vedere che la coerenza del tipo e le proprietà di gestione del supporto di valori null in CTAS è un’ottima procedura tecnica consigliata.</span><span class="sxs-lookup"><span data-stu-id="eef7f-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="eef7f-201">Consente di mantenere l'integrità dei calcoli e assicura inoltre che il cambio di partizione sia possibile.</span><span class="sxs-lookup"><span data-stu-id="eef7f-201">It helps to maintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="eef7f-202">Fare riferimento a MSDN per ulteriori informazioni sull'utilizzo di [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="eef7f-202">Please refer to MSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="eef7f-203">È una delle istruzioni più importanti di SQL Data Warehouse di Azure.</span><span class="sxs-lookup"><span data-stu-id="eef7f-203">It is one of the most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="eef7f-204">Assicurarsi di averla compresa completamente.</span><span class="sxs-lookup"><span data-stu-id="eef7f-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eef7f-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eef7f-205">Next steps</span></span>
<span data-ttu-id="eef7f-206">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="eef7f-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
