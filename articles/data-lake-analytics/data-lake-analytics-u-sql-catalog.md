---
title: Introduzione a catalogo hello U-SQL | Documenti Microsoft
description: Informazioni su come toouse hello U-SQL catalogo dati e codice tooshare.
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
ms.openlocfilehash: 559bb7a3879031eb290a3e82946d7bf42ac9f553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-u-sql-catalog"></a><span data-ttu-id="c6252-103">Introduzione a hello catalogo U-SQL</span><span class="sxs-lookup"><span data-stu-id="c6252-103">Get started with hello U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="c6252-104">Creare una funzione con valori di tabella (TVF)</span><span class="sxs-lookup"><span data-stu-id="c6252-104">Create a TVF</span></span>

<span data-ttu-id="c6252-105">In script U-SQL hello precedente si ripetuti utilizzo hello di estrazione tooread da hello stesso file di origine.</span><span class="sxs-lookup"><span data-stu-id="c6252-105">In hello previous U-SQL script, you repeated hello use of EXTRACT tooread from hello same source file.</span></span> <span data-ttu-id="c6252-106">Con U-SQL con valori di tabella funzione hello (TVF), è possibile incapsulare dati hello per il riutilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="c6252-106">With hello U-SQL table-valued function (TVF), you can encapsulate hello data for future reuse.</span></span>  

<span data-ttu-id="c6252-107">Hello script seguente viene creata una TVF chiamato `Searchlog()` nel database predefinito hello e nello schema:</span><span class="sxs-lookup"><span data-stu-id="c6252-107">hello following script creates a TVF called `Searchlog()` in hello default database and schema:</span></span>

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

<span data-ttu-id="c6252-108">Hello lo script seguente viene illustrato come toouse hello TVF che è stata definita nello script precedente hello:</span><span class="sxs-lookup"><span data-stu-id="c6252-108">hello following script shows you how toouse hello TVF that was defined in hello previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="c6252-109">Creare viste</span><span class="sxs-lookup"><span data-stu-id="c6252-109">Create views</span></span>

<span data-ttu-id="c6252-110">Se si dispone di una singola espressione di query, anziché un TVF è possibile utilizzare un tooencapsulate vista U-SQL dell'espressione.</span><span class="sxs-lookup"><span data-stu-id="c6252-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW tooencapsulate that expression.</span></span>

<span data-ttu-id="c6252-111">lo script seguente Hello crea una vista denominata `SearchlogView` nel database predefinito hello e nello schema:</span><span class="sxs-lookup"><span data-stu-id="c6252-111">hello following script creates a view called `SearchlogView` in hello default database and schema:</span></span>

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

<span data-ttu-id="c6252-112">lo script seguente Hello di seguito viene illustrato l'utilizzo di hello della vista hello definito:</span><span class="sxs-lookup"><span data-stu-id="c6252-112">hello following script demonstrates hello use of hello defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="c6252-113">Creare tabelle</span><span class="sxs-lookup"><span data-stu-id="c6252-113">Create tables</span></span>
<span data-ttu-id="c6252-114">Come con le tabelle di database relazionale, con U-SQL è possibile creare una tabella con uno schema predefinito o creare una tabella che deriva hello da query hello che popola la tabella hello (noto anche come CREATE TABLE AS SELECT o un'istruzione CTAS).</span><span class="sxs-lookup"><span data-stu-id="c6252-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers hello schema from hello query that populates hello table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="c6252-115">Creare un database e due tabelle utilizzando hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="c6252-115">Create a database and two tables by using hello following script:</span></span>

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

## <a name="query-tables"></a><span data-ttu-id="c6252-116">Eseguire query su tabelle</span><span class="sxs-lookup"><span data-stu-id="c6252-116">Query tables</span></span>
<span data-ttu-id="c6252-117">È possibile eseguire query di tabelle, ad esempio quelli creati nello script precedente hello in hello allo stesso modo di eseguire la query dei file di dati hello.</span><span class="sxs-lookup"><span data-stu-id="c6252-117">You can query tables, such as those created in hello previous script, in hello same way that you query hello data files.</span></span> <span data-ttu-id="c6252-118">Anziché creare un set di righe tramite l'estrazione, è ora possibile fare riferimento toohello nome della tabella.</span><span class="sxs-lookup"><span data-stu-id="c6252-118">Instead of creating a rowset by using EXTRACT, you now can refer toohello table name.</span></span>

<span data-ttu-id="c6252-119">tooread dalle tabelle di hello, modificare uno script di trasformazione hello utilizzata in precedenza:</span><span class="sxs-lookup"><span data-stu-id="c6252-119">tooread from hello tables, modify hello transform script that you used previously:</span></span>

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
    too"/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="c6252-120">Attualmente, non è possibile eseguire un'istruzione SELECT in una tabella in hello hello uno stesso script in cui è stato creato tabella hello.</span><span class="sxs-lookup"><span data-stu-id="c6252-120">Currently, you cannot run a SELECT on a table in hello same script as hello one where you created hello table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6252-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6252-121">Next Steps</span></span>
* [<span data-ttu-id="c6252-122">Panoramica di Analisi Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="c6252-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="c6252-123">Sviluppare script U-SQL con Data Lake Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6252-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="c6252-124">Monitorare e risolvere i problemi dei processi di Azure Data Lake Analytics tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c6252-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
