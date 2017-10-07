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
# <a name="group-by-options-in-sql-data-warehouse"></a>Opzioni Group by in SQL Data Warehouse
Hello [GROUP BY] [ GROUP BY] viene utilizzata la clausola set riepilogo tooaggregate dati tooa di righe. Include inoltre alcune opzioni che estendono la funzionalità che toobe necessità aggirato come non sono supportati direttamente da Azure SQL Data Warehouse.

Queste opzioni sono

* GROUP BY con ROLLUP
* GROUPING SETS
* GROUP BY con CUBE

## <a name="rollup-and-grouping-sets-options"></a>Opzioni di rollup e raggruppamento di set
opzione più semplice Hello è toouse `UNION ALL` invece tooperform hello rollup anziché basarsi sul hello sintassi esplicita. risultato Hello è esattamente hello stesso

Di seguito è riportato un esempio di un gruppo dall'istruzione tramite hello `ROLLUP` opzione:

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

Con i ROLLUP è stato richiesto hello seguendo le aggregazioni:

* Paese e area
* Paese
* Grand Total

tooreplace questo valore è necessario toouse `UNION ALL`; specificando le aggregazioni hello richieste in modo esplicito tooreturn hello stessi risultati:

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

Per GROUPING SETS, è sufficiente toodo è adottare hello stesso principale, ma solo creare sezioni UNION ALL per hello livelli di aggregazione desideriamo toosee

## <a name="cube-options"></a>Opzioni Cube
È possibile toocreate un GROUP BY WITH CUBE approccio di hello UNION ALL. problema di Hello è che il codice hello può diventare rapidamente un'operazione complessa e difficile da gestire. toomitigate questo è possibile utilizzare questo più avanzate approccio.

Consente di usare il precedente esempio di hello.

primo passaggio Hello è hello toodefine 'cube' che definisce tutti i livelli di aggregazione che si desidera toocreate hello. È importante tootake nota di hello CROSS JOIN di tabelle derivate due hello. Tutti i livelli di hello viene generato automaticamente. resto di Hello del codice hello è effettivamente presente per la formattazione.

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

risultati Hello di hello un'istruzione CTAS può essere illustrata di seguito:

![][1]

secondo passaggio Hello è toospecify che comporta un provvisorio toostore tabella di destinazione:

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

terzo passaggio Hello è tooloop sul cubo di esecuzione hello aggregazione di colonne. query Hello verrà eseguito una volta per ogni riga nella tabella temporanea hello #Cube e archiviare i risultati di hello nella tabella temporanea hello #Results

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

Infine è possibile restituire i risultati di hello semplicemente leggendo da una tabella temporanea hello #Results

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

Suddivisione di codice hello in sezioni e generando un ciclo hello costrutto di codice diventa più gestibile e gestibile.

## <a name="next-steps"></a>Passaggi successivi
Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
