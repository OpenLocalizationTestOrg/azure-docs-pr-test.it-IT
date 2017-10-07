---
title: aaaGroup dalle opzioni in SQL Data Warehouse | Documenti Microsoft
description: "Suggerimenti per l’implementazione delle opzioni group by in SQL Data Warehouse di Azure per lo sviluppo di soluzioni."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f95a1e43-768f-4b7b-8a10-8a0509d0c871
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: cc443c2af4e3ef2babd74d78aa6fb57bb3c1c7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="d905b-103">Opzioni Group by in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d905b-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="d905b-104">Hello [GROUP BY] [ GROUP BY] viene utilizzata la clausola set riepilogo tooaggregate dati tooa di righe.</span><span class="sxs-lookup"><span data-stu-id="d905b-104">hello [GROUP BY][GROUP BY] clause is used tooaggregate data tooa summary set of rows.</span></span> <span data-ttu-id="d905b-105">Include inoltre alcune opzioni che estendono la funzionalità che toobe necessità aggirato come non sono supportati direttamente da Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d905b-105">It also has a few options that extend it's functionality that need toobe worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="d905b-106">Queste opzioni sono</span><span class="sxs-lookup"><span data-stu-id="d905b-106">These options are</span></span>

* <span data-ttu-id="d905b-107">GROUP BY con ROLLUP</span><span class="sxs-lookup"><span data-stu-id="d905b-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="d905b-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="d905b-108">GROUPING SETS</span></span>
* <span data-ttu-id="d905b-109">GROUP BY con CUBE</span><span class="sxs-lookup"><span data-stu-id="d905b-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="d905b-110">Opzioni di rollup e raggruppamento di set</span><span class="sxs-lookup"><span data-stu-id="d905b-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="d905b-111">opzione più semplice Hello è toouse `UNION ALL` invece tooperform hello rollup anziché basarsi sul hello sintassi esplicita.</span><span class="sxs-lookup"><span data-stu-id="d905b-111">hello simplest option here is toouse `UNION ALL` instead tooperform hello rollup rather than relying on hello explicit syntax.</span></span> <span data-ttu-id="d905b-112">risultato Hello è esattamente hello stesso</span><span class="sxs-lookup"><span data-stu-id="d905b-112">hello result is exactly hello same</span></span>

<span data-ttu-id="d905b-113">Di seguito è riportato un esempio di un gruppo dall'istruzione tramite hello `ROLLUP` opzione:</span><span class="sxs-lookup"><span data-stu-id="d905b-113">Below is an example of a group by statement using hello `ROLLUP` option:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount)             AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t       ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY ROLLUP (
                        [SalesTerritoryCountry]
                ,       [SalesTerritoryRegion]
                )
;
```

<span data-ttu-id="d905b-114">Con i ROLLUP è stato richiesto hello seguendo le aggregazioni:</span><span class="sxs-lookup"><span data-stu-id="d905b-114">By using ROLLUP we have requested hello following aggregations:</span></span>

* <span data-ttu-id="d905b-115">Paese e area</span><span class="sxs-lookup"><span data-stu-id="d905b-115">Country and Region</span></span>
* <span data-ttu-id="d905b-116">Paese</span><span class="sxs-lookup"><span data-stu-id="d905b-116">Country</span></span>
* <span data-ttu-id="d905b-117">Grand Total</span><span class="sxs-lookup"><span data-stu-id="d905b-117">Grand Total</span></span>

<span data-ttu-id="d905b-118">tooreplace questo valore è necessario toouse `UNION ALL`; specificando le aggregazioni hello richieste in modo esplicito tooreturn hello stessi risultati:</span><span class="sxs-lookup"><span data-stu-id="d905b-118">tooreplace this you will need toouse `UNION ALL`; specifying hello aggregations required explicitly tooreturn hello same results:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
UNION ALL
SELECT [SalesTerritoryCountry]
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
UNION ALL
SELECT NULL
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey;
```

<span data-ttu-id="d905b-119">Per GROUPING SETS, è sufficiente toodo è adottare hello stesso principale, ma solo creare sezioni UNION ALL per hello livelli di aggregazione desideriamo toosee</span><span class="sxs-lookup"><span data-stu-id="d905b-119">For GROUPING SETS all we need toodo is adopt hello same principal but only create UNION ALL sections for hello aggregation levels we want toosee</span></span>

## <a name="cube-options"></a><span data-ttu-id="d905b-120">Opzioni Cube</span><span class="sxs-lookup"><span data-stu-id="d905b-120">Cube options</span></span>
<span data-ttu-id="d905b-121">È possibile toocreate un GROUP BY WITH CUBE approccio di hello UNION ALL.</span><span class="sxs-lookup"><span data-stu-id="d905b-121">It is possible toocreate a GROUP BY WITH CUBE using hello UNION ALL approach.</span></span> <span data-ttu-id="d905b-122">problema di Hello è che il codice hello può diventare rapidamente un'operazione complessa e difficile da gestire.</span><span class="sxs-lookup"><span data-stu-id="d905b-122">hello problem is that hello code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="d905b-123">toomitigate questo è possibile utilizzare questo più avanzate approccio.</span><span class="sxs-lookup"><span data-stu-id="d905b-123">toomitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="d905b-124">Consente di usare il precedente esempio di hello.</span><span class="sxs-lookup"><span data-stu-id="d905b-124">Let's use hello example above.</span></span>

<span data-ttu-id="d905b-125">primo passaggio Hello è hello toodefine 'cube' che definisce tutti i livelli di aggregazione che si desidera toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="d905b-125">hello first step is toodefine hello 'cube' that defines all hello levels of aggregation that we want toocreate.</span></span> <span data-ttu-id="d905b-126">È importante tootake nota di hello CROSS JOIN di tabelle derivate due hello.</span><span class="sxs-lookup"><span data-stu-id="d905b-126">It is important tootake note of hello CROSS JOIN of hello two derived tables.</span></span> <span data-ttu-id="d905b-127">Tutti i livelli di hello viene generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d905b-127">This generates all hello levels for us.</span></span> <span data-ttu-id="d905b-128">resto di Hello del codice hello è effettivamente presente per la formattazione.</span><span class="sxs-lookup"><span data-stu-id="d905b-128">hello rest of hello code is really there for formatting.</span></span>

```sql
CREATE TABLE #Cube
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
AS
WITH GrpCube AS
(SELECT    CAST(ISNULL(Country,'NULL')+','+ISNULL(Region,'NULL') AS NVARCHAR(50)) as 'Cols'
,          CAST(ISNULL(Country+',','')+ISNULL(Region,'') AS NVARCHAR(50))  as 'GroupBy'
,          ROW_NUMBER() OVER (ORDER BY Country) as 'Seq'
FROM       ( SELECT 'SalesTerritoryCountry' as Country
             UNION ALL
             SELECT NULL
           ) c
CROSS JOIN ( SELECT 'SalesTerritoryRegion' as Region
             UNION ALL
             SELECT NULL
           ) r
)
SELECT Cols
,      CASE WHEN SUBSTRING(GroupBy,LEN(GroupBy),1) = ','
            THEN SUBSTRING(GroupBy,1,LEN(GroupBy)-1)
            ELSE GroupBy
       END AS GroupBy  --Remove Trailing Comma
,Seq
FROM GrpCube;
```

<span data-ttu-id="d905b-129">risultati Hello di hello un'istruzione CTAS può essere illustrata di seguito:</span><span class="sxs-lookup"><span data-stu-id="d905b-129">hello results of hello CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="d905b-130">secondo passaggio Hello è toospecify che comporta un provvisorio toostore tabella di destinazione:</span><span class="sxs-lookup"><span data-stu-id="d905b-130">hello second step is toospecify a target table toostore interim results:</span></span>

```sql
DECLARE
 @SQL NVARCHAR(4000)
,@Columns NVARCHAR(4000)
,@GroupBy NVARCHAR(4000)
,@i INT = 1
,@nbr INT = 0
;
CREATE TABLE #Results
(
 [SalesTerritoryCountry] NVARCHAR(50)
,[SalesTerritoryRegion]  NVARCHAR(50)
,[TotalSalesAmount]      MONEY
)
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
;
```

<span data-ttu-id="d905b-131">terzo passaggio Hello è tooloop sul cubo di esecuzione hello aggregazione di colonne.</span><span class="sxs-lookup"><span data-stu-id="d905b-131">hello third step is tooloop over our cube of columns performing hello aggregation.</span></span> <span data-ttu-id="d905b-132">query Hello verrà eseguito una volta per ogni riga nella tabella temporanea hello #Cube e archiviare i risultati di hello nella tabella temporanea hello #Results</span><span class="sxs-lookup"><span data-stu-id="d905b-132">hello query will run once for every row in hello #Cube temporary table and store hello results in hello #Results temp table</span></span>

```sql
SET @nbr =(SELECT MAX(Seq) FROM #Cube);

WHILE @i<=@nbr
BEGIN
    SET @Columns = (SELECT Cols    FROM #Cube where seq = @i);
    SET @GroupBy = (SELECT GroupBy FROM #Cube where seq = @i);

    SET @SQL ='INSERT INTO #Results
              SELECT '+@Columns+'
              ,      SUM(SalesAmount) AS TotalSalesAmount
              FROM  dbo.factInternetSales s
              JOIN  dbo.DimSalesTerritory t  
              ON s.SalesTerritoryKey = t.SalesTerritoryKey
              '+CASE WHEN @GroupBy <>''
                     THEN 'GROUP BY '+@GroupBy ELSE '' END

    EXEC sp_executesql @SQL;
    SET @i +=1;
END
```

<span data-ttu-id="d905b-133">Infine è possibile restituire i risultati di hello semplicemente leggendo da una tabella temporanea hello #Results</span><span class="sxs-lookup"><span data-stu-id="d905b-133">Lastly we can return hello results by simply reading from hello #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="d905b-134">Suddivisione di codice hello in sezioni e generando un ciclo hello costrutto di codice diventa più gestibile e gestibile.</span><span class="sxs-lookup"><span data-stu-id="d905b-134">By breaking hello code up into sections and generating a looping construct hello code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d905b-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d905b-135">Next steps</span></span>
<span data-ttu-id="d905b-136">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="d905b-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
