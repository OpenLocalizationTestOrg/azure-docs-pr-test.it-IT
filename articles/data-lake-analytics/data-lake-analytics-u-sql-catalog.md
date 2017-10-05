---
title: Introduzione al catalogo di U-SQL | Microsoft Docs
description: Informazioni su come usare il catalogo di U-SQL per condividere codice e dati.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: edmaca
ms.openlocfilehash: 08364c6c7bea53807844e3b1cc327dc3742e0487
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-u-sql-catalog"></a><span data-ttu-id="490ba-103">Introduzione al catalogo di U-SQL</span><span class="sxs-lookup"><span data-stu-id="490ba-103">Get started with the U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="490ba-104">Creare una funzione con valori di tabella (TVF)</span><span class="sxs-lookup"><span data-stu-id="490ba-104">Create a TVF</span></span>

<span data-ttu-id="490ba-105">Nel precedente script U-SQL, è stato usato più volte l'oggetto EXTRACT per leggere da uno stesso file di origine.</span><span class="sxs-lookup"><span data-stu-id="490ba-105">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span></span> <span data-ttu-id="490ba-106">La funzione con valori di tabella (TVF) U-SQL consente di incapsulare i dati per un riutilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="490ba-106">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span></span>  

<span data-ttu-id="490ba-107">Lo script seguente crea una funzione TVF denominata `Searchlog()` nel database e nello schema predefiniti:</span><span class="sxs-lookup"><span data-stu-id="490ba-107">The following script creates a TVF called `Searchlog()` in the default database and schema:</span></span>

```
DROP FUNCTION IF EXISTS Searchlog;

CREATE FUNCTION Searchlog()
RETURNS @searchlog TABLE
(
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
)
AS BEGIN
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
RETURN;
END;
```

<span data-ttu-id="490ba-108">Lo script seguente illustra come usare la funzione con valori di tabella definita nello script precedente:</span><span class="sxs-lookup"><span data-stu-id="490ba-108">The following script shows you how to use the TVF that was defined in the previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="490ba-109">Creare viste</span><span class="sxs-lookup"><span data-stu-id="490ba-109">Create views</span></span>

<span data-ttu-id="490ba-110">Se si ha una sola espressione di query, anziché una funzione TVF è possibile usare una VISTA U-SQL per incapsulare l'espressione.</span><span class="sxs-lookup"><span data-stu-id="490ba-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW to encapsulate that expression.</span></span>

<span data-ttu-id="490ba-111">Lo script seguente crea una vista denominata `SearchlogView` nel database e nello schema predefiniti:</span><span class="sxs-lookup"><span data-stu-id="490ba-111">The following script creates a view called `SearchlogView` in the default database and schema:</span></span>

```
DROP VIEW IF EXISTS SearchlogView;

CREATE VIEW SearchlogView AS  
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
```

<span data-ttu-id="490ba-112">Lo script seguente illustra l'uso della vista definita:</span><span class="sxs-lookup"><span data-stu-id="490ba-112">The following script demonstrates the use of the defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="490ba-113">Creare tabelle</span><span class="sxs-lookup"><span data-stu-id="490ba-113">Create tables</span></span>
<span data-ttu-id="490ba-114">Analogamente a una tabella di database relazionale, U-SQL consente di creare una tabella con uno schema predefinito oppure di creare una tabella e dedurre lo schema dalla query che popola la tabella (nota anche come istruzione CREATE TABLE AS SELECT o CTAS).</span><span class="sxs-lookup"><span data-stu-id="490ba-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="490ba-115">Lo script seguente crea un database e due tabelle:</span><span class="sxs-lookup"><span data-stu-id="490ba-115">Create a database and two tables by using the following script:</span></span>

```
DROP DATABASE IF EXISTS SearchLogDb;
CREATE DATABASE SearchLogDb;
USE DATABASE SearchLogDb;

DROP TABLE IF EXISTS SearchLog1;
DROP TABLE IF EXISTS SearchLog2;

CREATE TABLE SearchLog1 (
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string,

            INDEX sl_idx CLUSTERED (UserId ASC)
                DISTRIBUTED BY HASH (UserId)
);

INSERT INTO SearchLog1 SELECT * FROM master.dbo.Searchlog() AS s;

CREATE TABLE SearchLog2(
    INDEX sl_idx CLUSTERED (UserId ASC)
            DISTRIBUTED BY HASH (UserId)
) AS SELECT * FROM master.dbo.Searchlog() AS S; // You can use EXTRACT or SELECT here
```

## <a name="query-tables"></a><span data-ttu-id="490ba-116">Eseguire query su tabelle</span><span class="sxs-lookup"><span data-stu-id="490ba-116">Query tables</span></span>
<span data-ttu-id="490ba-117">È possibile eseguire una query su una tabella, come quelle create nello script precedente, nello stesso modo in cui si esegue su un file di dati.</span><span class="sxs-lookup"><span data-stu-id="490ba-117">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span></span> <span data-ttu-id="490ba-118">Anziché creare un set di righe usando l'istruzione EXTRACT, è possibile ora fare riferimento al nome della tabella.</span><span class="sxs-lookup"><span data-stu-id="490ba-118">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span></span>

<span data-ttu-id="490ba-119">Modificare lo script di trasformazione usato in precedenza in modo da leggere i dati direttamente dalle tabelle:</span><span class="sxs-lookup"><span data-stu-id="490ba-119">To read from the tables, modify the transform script that you used previously:</span></span>

```
@rs1 =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchLogDb.dbo.SearchLog2
GROUP BY Region;

@res =
    SELECT *
    FROM @rs1
    ORDER BY TotalDuration DESC
    FETCH 5 ROWS;

OUTPUT @res
    TO "/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="490ba-120">Non è attualmente possibile eseguire un'istruzione SELECT in una tabella presente nello stesso script in cui è stata creata la tabella.</span><span class="sxs-lookup"><span data-stu-id="490ba-120">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="490ba-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="490ba-121">Next Steps</span></span>
* [<span data-ttu-id="490ba-122">Panoramica di Analisi Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="490ba-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="490ba-123">Sviluppare script U-SQL con Data Lake Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="490ba-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="490ba-124">Monitorare e risolvere i problemi dei processi di Azure Data Lake Analytics tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="490ba-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
