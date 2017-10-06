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
# <a name="get-started-with-hello-u-sql-catalog"></a>Introduzione a hello catalogo U-SQL

## <a name="create-a-tvf"></a>Creare una funzione con valori di tabella (TVF)

In script U-SQL hello precedente si ripetuti utilizzo hello di estrazione tooread da hello stesso file di origine. Con U-SQL con valori di tabella funzione hello (TVF), è possibile incapsulare dati hello per il riutilizzo futuro.  

Hello script seguente viene creata una TVF chiamato `Searchlog()` nel database predefinito hello e nello schema:

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

Hello lo script seguente viene illustrato come toouse hello TVF che è stata definita nello script precedente hello:

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

## <a name="create-views"></a>Creare viste

Se si dispone di una singola espressione di query, anziché un TVF è possibile utilizzare un tooencapsulate vista U-SQL dell'espressione.

lo script seguente Hello crea una vista denominata `SearchlogView` nel database predefinito hello e nello schema:

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

lo script seguente Hello di seguito viene illustrato l'utilizzo di hello della vista hello definito:

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

## <a name="create-tables"></a>Creare tabelle
Come con le tabelle di database relazionale, con U-SQL è possibile creare una tabella con uno schema predefinito o creare una tabella che deriva hello da query hello che popola la tabella hello (noto anche come CREATE TABLE AS SELECT o un'istruzione CTAS).

Creare un database e due tabelle utilizzando hello lo script seguente:

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

## <a name="query-tables"></a>Eseguire query su tabelle
È possibile eseguire query di tabelle, ad esempio quelli creati nello script precedente hello in hello allo stesso modo di eseguire la query dei file di dati hello. Anziché creare un set di righe tramite l'estrazione, è ora possibile fare riferimento toohello nome della tabella.

tooread dalle tabelle di hello, modificare uno script di trasformazione hello utilizzata in precedenza:

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
 >Attualmente, non è possibile eseguire un'istruzione SELECT in una tabella in hello hello uno stesso script in cui è stato creato tabella hello.

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica di Analisi Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Sviluppare script U-SQL con Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Monitorare e risolvere i problemi dei processi di Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
