---
title: Opzioni Group by in SQL Data Warehouse | Documentazione Microsoft
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
ms.openlocfilehash: da71cb834c13da5d0f5690f471efc6c696163f30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="64752-103">Opzioni Group by in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="64752-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="64752-104">La clausola [GROUP BY][GROUP BY] viene usata per aggregare i dati a un set di righe di riepilogo.</span><span class="sxs-lookup"><span data-stu-id="64752-104">The [GROUP BY][GROUP BY] clause is used to aggregate data to a summary set of rows.</span></span> <span data-ttu-id="64752-105">Include inoltre alcune opzioni che ne estendono la funzionalità che devono essere evitate in quanto non sono supportate direttamente SQL Data Warehouse di Azure.</span><span class="sxs-lookup"><span data-stu-id="64752-105">It also has a few options that extend it's functionality that need to be worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="64752-106">Queste opzioni sono</span><span class="sxs-lookup"><span data-stu-id="64752-106">These options are</span></span>

* <span data-ttu-id="64752-107">GROUP BY con ROLLUP</span><span class="sxs-lookup"><span data-stu-id="64752-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="64752-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="64752-108">GROUPING SETS</span></span>
* <span data-ttu-id="64752-109">GROUP BY con CUBE</span><span class="sxs-lookup"><span data-stu-id="64752-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="64752-110">Opzioni di rollup e raggruppamento di set</span><span class="sxs-lookup"><span data-stu-id="64752-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="64752-111">L'opzione più semplice consiste nell'utilizzare `UNION ALL` invece di eseguire il rollup anziché utilizzare la sintassi esplicita.</span><span class="sxs-lookup"><span data-stu-id="64752-111">The simplest option here is to use `UNION ALL` instead to perform the rollup rather than relying on the explicit syntax.</span></span> <span data-ttu-id="64752-112">Il risultato è esattamente lo stesso</span><span class="sxs-lookup"><span data-stu-id="64752-112">The result is exactly the same</span></span>

<span data-ttu-id="64752-113">Di seguito è riportato un esempio di istruzione group by utilizzando l’opzione `ROLLUP` :</span><span class="sxs-lookup"><span data-stu-id="64752-113">Below is an example of a group by statement using the `ROLLUP` option:</span></span>

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

<span data-ttu-id="64752-114">Usando ROLLUP sono state richieste le aggregazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="64752-114">By using ROLLUP we have requested the following aggregations:</span></span>

* <span data-ttu-id="64752-115">Paese e area</span><span class="sxs-lookup"><span data-stu-id="64752-115">Country and Region</span></span>
* <span data-ttu-id="64752-116">Paese</span><span class="sxs-lookup"><span data-stu-id="64752-116">Country</span></span>
* <span data-ttu-id="64752-117">Grand Total</span><span class="sxs-lookup"><span data-stu-id="64752-117">Grand Total</span></span>

<span data-ttu-id="64752-118">Per sostituire questo valore è necessario utilizzare `UNION ALL`; specificando le aggregazioni necessarie in modo esplicito per restituire gli stessi risultati:</span><span class="sxs-lookup"><span data-stu-id="64752-118">To replace this you will need to use `UNION ALL`; specifying the aggregations required explicitly to return the same results:</span></span>

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

<span data-ttu-id="64752-119">Per GROUPING SETS è necessario adottare la stessa entità e creare solo sezioni UNION ALL per i livelli di aggregazione che si desidera visualizzare.</span><span class="sxs-lookup"><span data-stu-id="64752-119">For GROUPING SETS all we need to do is adopt the same principal but only create UNION ALL sections for the aggregation levels we want to see</span></span>

## <a name="cube-options"></a><span data-ttu-id="64752-120">Opzioni Cube</span><span class="sxs-lookup"><span data-stu-id="64752-120">Cube options</span></span>
<span data-ttu-id="64752-121">È possibile creare un GROUP BY WITH CUBE utilizzando l'approccio UNION ALL.</span><span class="sxs-lookup"><span data-stu-id="64752-121">It is possible to create a GROUP BY WITH CUBE using the UNION ALL approach.</span></span> <span data-ttu-id="64752-122">Il problema è che il codice può risultare complesso e difficile da gestire.</span><span class="sxs-lookup"><span data-stu-id="64752-122">The problem is that the code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="64752-123">Per risolvere questo problema è possibile utilizzare questo approccio avanzato.</span><span class="sxs-lookup"><span data-stu-id="64752-123">To mitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="64752-124">Utilizzare l'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="64752-124">Let's use the example above.</span></span>

<span data-ttu-id="64752-125">Il primo passaggio consiste nel definire il cubo che definisce tutti i livelli di aggregazione che si desidera creare.</span><span class="sxs-lookup"><span data-stu-id="64752-125">The first step is to define the 'cube' that defines all the levels of aggregation that we want to create.</span></span> <span data-ttu-id="64752-126">È importante tenere conto del CROSS JOIN delle due tabelle derivate.</span><span class="sxs-lookup"><span data-stu-id="64752-126">It is important to take note of the CROSS JOIN of the two derived tables.</span></span> <span data-ttu-id="64752-127">In tal modo tutti i livelli vengono generati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="64752-127">This generates all the levels for us.</span></span> <span data-ttu-id="64752-128">Il resto del codice è disponibile per la formattazione.</span><span class="sxs-lookup"><span data-stu-id="64752-128">The rest of the code is really there for formatting.</span></span>

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

<span data-ttu-id="64752-129">Di seguito sono illustrati i risultati del CTAS:</span><span class="sxs-lookup"><span data-stu-id="64752-129">The results of the CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="64752-130">Il secondo passaggio consiste nel specificare una tabella di destinazione per archiviare i risultati temporanei:</span><span class="sxs-lookup"><span data-stu-id="64752-130">The second step is to specify a target table to store interim results:</span></span>

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

<span data-ttu-id="64752-131">Il terzo passaggio consiste nell’eseguire il ciclo del cubo delle colonne per eseguire l'aggregazione.</span><span class="sxs-lookup"><span data-stu-id="64752-131">The third step is to loop over our cube of columns performing the aggregation.</span></span> <span data-ttu-id="64752-132">La query verrà eseguita una volta per ogni riga nella tabella temporanea #Cube e i risultati verranno archiviati nella tabella temporanea #Results</span><span class="sxs-lookup"><span data-stu-id="64752-132">The query will run once for every row in the #Cube temporary table and store the results in the #Results temp table</span></span>

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

<span data-ttu-id="64752-133">Infine è possibile restituire i risultati semplicemente leggendo dalla tabella temporanea #Results</span><span class="sxs-lookup"><span data-stu-id="64752-133">Lastly we can return the results by simply reading from the #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="64752-134">Suddividendo il codice in sezioni e generando un costrutto di ciclo il codice diventa più gestibile e gestibile e sostenibile.</span><span class="sxs-lookup"><span data-stu-id="64752-134">By breaking the code up into sections and generating a looping construct the code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64752-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="64752-135">Next steps</span></span>
<span data-ttu-id="64752-136">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="64752-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
