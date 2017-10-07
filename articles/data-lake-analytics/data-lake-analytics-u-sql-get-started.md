---
title: Introduzione al linguaggio U-SQL | Microsoft Docs
description: Nozioni di base hello di hello linguaggio U-SQL.
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
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a>Introduzione a U-SQL
U-SQL è un linguaggio che combina SQL dichiarativa con imperativo c# toolet si elaborano i dati su qualsiasi scala. Tramite hello scalabile, query distribuite funzionalità di U-SQL, è possibile analizzare in modo efficiente i dati in archivi relazionali, ad esempio Database SQL di Azure. Con U-SQL è possibile elaborare i dati non strutturati applicando schemi in lettura e inserendo logiche personalizzate e funzioni definite dall'utente. Inoltre, U-SQL include esempi di estensibilità che fornisce un controllo accurato sul modo in tooexecute su larga scala. 

## <a name="learning-resources"></a>Risorse di formazione

* Hello [U-SQL esercitazione](http://aka.ms/usqltutorial) fornisce una procedura guidata della maggior parte del linguaggio hello U-SQL. Questo documento è consigliabile leggere per tutti gli sviluppatori che desiderano toolearn U-SQL.
* Per informazioni dettagliate su hello **sintassi del linguaggio U-SQL**, vedere hello [riferimenti al linguaggio U-SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).
* hello toounderstand **filosofia di progettazione U-SQL**, vedere post sul blog di Visual Studio hello [introduzione U-SQL: un linguaggio che semplifica Big l'elaborazione dati](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

## <a name="prerequisites"></a>Prerequisiti

Prima di passare a esempi di hello U-SQL in questo documento, leggere e completare [esercitazione: script U-SQL sviluppare utilizzando Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Tale esercitazione vengono illustrati i meccanismi di hello dell'utilizzo di U-SQL con Azure Data Lake Tools per Visual Studio.

## <a name="your-first-u-sql-script"></a>Il primo script U-SQL

lo script U-SQL seguente Hello è semplice e consente di esplorare language di hello U-SQL molti aspetti.

```
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

OUTPUT @searchlog   
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

Lo script non è stato sottoposto a molte procedure di trasformazione. La lettura da file di origine hello chiamato `SearchLog.tsv`, schematizes e set di righe hello vengono scritte in un file denominato SearchLog-primo-u-sql.csv.

Si noti hello punto interrogativo toohello tipo di dati successivo in hello `Duration` campo. Ciò significa che hello `Duration` campo può essere null.

### <a name="key-concepts"></a>Concetti chiave
* **Le variabili di set di righe**: ogni espressione di query che produce un set di righe può essere assegnati tooa variabile. U-SQL segua il modello di denominazione variabile di hello T-SQL (`@searchlog`, ad esempio) nello script hello.
* Hello **estrarre** (parola chiave) legge i dati da un file e definisce schema hello in lettura. `Extractors.Tsv` è un estrattore di U-SQL integrato per i valori separati da tabulazioni. È possibile sviluppare estrattori personalizzati.
* Hello **OUTPUT** scrive i dati da un file tooa set di righe. `Outputters.Csv()`è un toocreate di outputter U-SQL incorporato un file con valori separati da virgole. È possibile sviluppare anche outputter personalizzati.

### <a name="file-paths"></a>Percorsi di file

Hello estrazione e le istruzioni di OUTPUT è possibile usare i percorsi di file. I percorsi di file possono essere assoluti o relativi:

Questo percorso file assoluto seguente fa riferimento a file tooa in un archivio Data Lake denominato `mystore`:

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

Il seguente percorso di file inizia con `"/"`. Fa riferimento il file tooa nell'account archivio Data Lake di hello predefinito:

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a>Usare variabili scalari

È possibile utilizzare variabili scalari come toomake e di manutenzione di uno script semplice. script U-SQL precedente Hello possono anche essere scritti come:

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a>Trasformare set di righe

Utilizzare **selezionare** tootransform set di righe:

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

Hello clausola WHERE viene utilizzata una [espressione c# booleana](https://msdn.microsoft.com/library/6a71f45d.aspx). È possibile utilizzare language hello c# espressione toodo proprie espressioni e funzioni. È anche possibile combinarle con congiunzioni (AND) e disgiunzioni (OR) logiche per eseguire operazioni di filtro più complesse.

Hello lo script seguente usa il metodo DateTime.Parse() hello e un insieme.

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 >seconda query Hello funziona sul risultato di hello di hello primo set di righe, che viene creata una composizione di hello due filtri. È inoltre possibile riutilizzare un nome di variabile e i nomi di hello nell'ambito lessicale.

## <a name="aggregate-rowsets"></a>Aggregare set di righe
Consente di U-SQL hello familiarità ORDER BY, GROUP BY e le aggregazioni.

Hello nella query seguente trova durata totale hello per area e quindi Visualizza la durata di cinque top hello in ordine.

U-SQL set di righe non mantenere l'ordine per la query successiva hello. Di conseguenza, tooorder un output, è necessario tooadd istruzione ORDER BY toohello OUTPUT:

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

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

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

Hello U-SQL clausole ORDER BY richiede l'utilizzo di clausola FETCH hello in un'espressione SELECT.

clausola U-SQL con Hello può essere utilizzato toorestrict hello output toogroups che soddisfano condizioni HAVING hello:

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

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

Per scenari di aggregazione avanzate, vedere la documentazione di riferimento di hello hello U-SQL per [aggregare, analitico e fanno riferimento a funzioni](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica di Analisi Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Sviluppare script U-SQL con Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
