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
# <a name="get-started-with-u-sql"></a><span data-ttu-id="ff739-103">Introduzione a U-SQL</span><span class="sxs-lookup"><span data-stu-id="ff739-103">Get started with U-SQL</span></span>
<span data-ttu-id="ff739-104">U-SQL è un linguaggio che combina SQL dichiarativa con imperativo c# toolet si elaborano i dati su qualsiasi scala.</span><span class="sxs-lookup"><span data-stu-id="ff739-104">U-SQL is a language that combines declarative SQL with imperative C# toolet you process data at any scale.</span></span> <span data-ttu-id="ff739-105">Tramite hello scalabile, query distribuite funzionalità di U-SQL, è possibile analizzare in modo efficiente i dati in archivi relazionali, ad esempio Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff739-105">Through hello scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="ff739-106">Con U-SQL è possibile elaborare i dati non strutturati applicando schemi in lettura e inserendo logiche personalizzate e funzioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="ff739-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="ff739-107">Inoltre, U-SQL include esempi di estensibilità che fornisce un controllo accurato sul modo in tooexecute su larga scala.</span><span class="sxs-lookup"><span data-stu-id="ff739-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how tooexecute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="ff739-108">Risorse di formazione</span><span class="sxs-lookup"><span data-stu-id="ff739-108">Learning resources</span></span>

* <span data-ttu-id="ff739-109">Hello [U-SQL esercitazione](http://aka.ms/usqltutorial) fornisce una procedura guidata della maggior parte del linguaggio hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ff739-109">hello [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of hello U-SQL language.</span></span> <span data-ttu-id="ff739-110">Questo documento è consigliabile leggere per tutti gli sviluppatori che desiderano toolearn U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ff739-110">This document is recommended reading for all developers wanting toolearn U-SQL.</span></span>
* <span data-ttu-id="ff739-111">Per informazioni dettagliate su hello **sintassi del linguaggio U-SQL**, vedere hello [riferimenti al linguaggio U-SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="ff739-111">For detailed information about hello **U-SQL language syntax**, see hello [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="ff739-112">hello toounderstand **filosofia di progettazione U-SQL**, vedere post sul blog di Visual Studio hello [introduzione U-SQL: un linguaggio che semplifica Big l'elaborazione dati](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="ff739-112">toounderstand hello **U-SQL design philosophy**, see hello Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff739-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ff739-113">Prerequisites</span></span>

<span data-ttu-id="ff739-114">Prima di passare a esempi di hello U-SQL in questo documento, leggere e completare [esercitazione: script U-SQL sviluppare utilizzando Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ff739-114">Before you go through hello U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="ff739-115">Tale esercitazione vengono illustrati i meccanismi di hello dell'utilizzo di U-SQL con Azure Data Lake Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ff739-115">That tutorial explains hello mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="ff739-116">Il primo script U-SQL</span><span class="sxs-lookup"><span data-stu-id="ff739-116">Your first U-SQL script</span></span>

<span data-ttu-id="ff739-117">lo script U-SQL seguente Hello è semplice e consente di esplorare language di hello U-SQL molti aspetti.</span><span class="sxs-lookup"><span data-stu-id="ff739-117">hello following U-SQL script is simple and lets us explore many aspects hello U-SQL language.</span></span>

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

<span data-ttu-id="ff739-118">Lo script non è stato sottoposto a molte procedure di trasformazione.</span><span class="sxs-lookup"><span data-stu-id="ff739-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="ff739-119">La lettura da file di origine hello chiamato `SearchLog.tsv`, schematizes e set di righe hello vengono scritte in un file denominato SearchLog-primo-u-sql.csv.</span><span class="sxs-lookup"><span data-stu-id="ff739-119">It reads from hello source file called `SearchLog.tsv`, schematizes it, and writes hello rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="ff739-120">Si noti hello punto interrogativo toohello tipo di dati successivo in hello `Duration` campo.</span><span class="sxs-lookup"><span data-stu-id="ff739-120">Notice hello question mark next toohello data type in hello `Duration` field.</span></span> <span data-ttu-id="ff739-121">Ciò significa che hello `Duration` campo può essere null.</span><span class="sxs-lookup"><span data-stu-id="ff739-121">It means that hello `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="ff739-122">Concetti chiave</span><span class="sxs-lookup"><span data-stu-id="ff739-122">Key concepts</span></span>
* <span data-ttu-id="ff739-123">**Le variabili di set di righe**: ogni espressione di query che produce un set di righe può essere assegnati tooa variabile.</span><span class="sxs-lookup"><span data-stu-id="ff739-123">**Rowset variables**: Each query expression that produces a rowset can be assigned tooa variable.</span></span> <span data-ttu-id="ff739-124">U-SQL segua il modello di denominazione variabile di hello T-SQL (`@searchlog`, ad esempio) nello script hello.</span><span class="sxs-lookup"><span data-stu-id="ff739-124">U-SQL follows hello T-SQL variable naming pattern (`@searchlog`, for example) in hello script.</span></span>
* <span data-ttu-id="ff739-125">Hello **estrarre** (parola chiave) legge i dati da un file e definisce schema hello in lettura.</span><span class="sxs-lookup"><span data-stu-id="ff739-125">hello **EXTRACT** keyword reads data from a file and defines hello schema on read.</span></span> <span data-ttu-id="ff739-126">`Extractors.Tsv` è un estrattore di U-SQL integrato per i valori separati da tabulazioni.</span><span class="sxs-lookup"><span data-stu-id="ff739-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="ff739-127">È possibile sviluppare estrattori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="ff739-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="ff739-128">Hello **OUTPUT** scrive i dati da un file tooa set di righe.</span><span class="sxs-lookup"><span data-stu-id="ff739-128">hello **OUTPUT** writes data from a rowset tooa file.</span></span> <span data-ttu-id="ff739-129">`Outputters.Csv()`è un toocreate di outputter U-SQL incorporato un file con valori separati da virgole.</span><span class="sxs-lookup"><span data-stu-id="ff739-129">`Outputters.Csv()` is a built-in U-SQL outputter toocreate a comma-separated-value file.</span></span> <span data-ttu-id="ff739-130">È possibile sviluppare anche outputter personalizzati.</span><span class="sxs-lookup"><span data-stu-id="ff739-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="ff739-131">Percorsi di file</span><span class="sxs-lookup"><span data-stu-id="ff739-131">File paths</span></span>

<span data-ttu-id="ff739-132">Hello estrazione e le istruzioni di OUTPUT è possibile usare i percorsi di file.</span><span class="sxs-lookup"><span data-stu-id="ff739-132">hello EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="ff739-133">I percorsi di file possono essere assoluti o relativi:</span><span class="sxs-lookup"><span data-stu-id="ff739-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="ff739-134">Questo percorso file assoluto seguente fa riferimento a file tooa in un archivio Data Lake denominato `mystore`:</span><span class="sxs-lookup"><span data-stu-id="ff739-134">This following absolute file path refers tooa file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="ff739-135">Il seguente percorso di file inizia con `"/"`.</span><span class="sxs-lookup"><span data-stu-id="ff739-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="ff739-136">Fa riferimento il file tooa nell'account archivio Data Lake di hello predefinito:</span><span class="sxs-lookup"><span data-stu-id="ff739-136">It refers tooa file in hello default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="ff739-137">Usare variabili scalari</span><span class="sxs-lookup"><span data-stu-id="ff739-137">Use scalar variables</span></span>

<span data-ttu-id="ff739-138">È possibile utilizzare variabili scalari come toomake e di manutenzione di uno script semplice.</span><span class="sxs-lookup"><span data-stu-id="ff739-138">You can use scalar variables as well toomake your script maintenance easier.</span></span> <span data-ttu-id="ff739-139">script U-SQL precedente Hello possono anche essere scritti come:</span><span class="sxs-lookup"><span data-stu-id="ff739-139">hello previous U-SQL script can also be written as:</span></span>

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

## <a name="transform-rowsets"></a><span data-ttu-id="ff739-140">Trasformare set di righe</span><span class="sxs-lookup"><span data-stu-id="ff739-140">Transform rowsets</span></span>

<span data-ttu-id="ff739-141">Utilizzare **selezionare** tootransform set di righe:</span><span class="sxs-lookup"><span data-stu-id="ff739-141">Use **SELECT** tootransform rowsets:</span></span>

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

<span data-ttu-id="ff739-142">Hello clausola WHERE viene utilizzata una [espressione c# booleana](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff739-142">hello WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="ff739-143">È possibile utilizzare language hello c# espressione toodo proprie espressioni e funzioni.</span><span class="sxs-lookup"><span data-stu-id="ff739-143">You can use hello C# expression language toodo your own expressions and functions.</span></span> <span data-ttu-id="ff739-144">È anche possibile combinarle con congiunzioni (AND) e disgiunzioni (OR) logiche per eseguire operazioni di filtro più complesse.</span><span class="sxs-lookup"><span data-stu-id="ff739-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="ff739-145">Hello lo script seguente usa il metodo DateTime.Parse() hello e un insieme.</span><span class="sxs-lookup"><span data-stu-id="ff739-145">hello following script uses hello DateTime.Parse() method and a conjunction.</span></span>

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
 ><span data-ttu-id="ff739-146">seconda query Hello funziona sul risultato di hello di hello primo set di righe, che viene creata una composizione di hello due filtri.</span><span class="sxs-lookup"><span data-stu-id="ff739-146">hello second query is operating on hello result of hello first rowset, which creates a composite of hello two filters.</span></span> <span data-ttu-id="ff739-147">È inoltre possibile riutilizzare un nome di variabile e i nomi di hello nell'ambito lessicale.</span><span class="sxs-lookup"><span data-stu-id="ff739-147">You can also reuse a variable name, and hello names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="ff739-148">Aggregare set di righe</span><span class="sxs-lookup"><span data-stu-id="ff739-148">Aggregate rowsets</span></span>
<span data-ttu-id="ff739-149">Consente di U-SQL hello familiarità ORDER BY, GROUP BY e le aggregazioni.</span><span class="sxs-lookup"><span data-stu-id="ff739-149">U-SQL gives you hello familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="ff739-150">Hello nella query seguente trova durata totale hello per area e quindi Visualizza la durata di cinque top hello in ordine.</span><span class="sxs-lookup"><span data-stu-id="ff739-150">hello following query finds hello total duration per region, and then displays hello top five durations in order.</span></span>

<span data-ttu-id="ff739-151">U-SQL set di righe non mantenere l'ordine per la query successiva hello.</span><span class="sxs-lookup"><span data-stu-id="ff739-151">U-SQL rowsets do not preserve their order for hello next query.</span></span> <span data-ttu-id="ff739-152">Di conseguenza, tooorder un output, è necessario tooadd istruzione ORDER BY toohello OUTPUT:</span><span class="sxs-lookup"><span data-stu-id="ff739-152">Thus, tooorder an output, you need tooadd ORDER BY toohello OUTPUT statement:</span></span>

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

<span data-ttu-id="ff739-153">Hello U-SQL clausole ORDER BY richiede l'utilizzo di clausola FETCH hello in un'espressione SELECT.</span><span class="sxs-lookup"><span data-stu-id="ff739-153">hello U-SQL ORDER BY clause requires using hello FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="ff739-154">clausola U-SQL con Hello può essere utilizzato toorestrict hello output toogroups che soddisfano condizioni HAVING hello:</span><span class="sxs-lookup"><span data-stu-id="ff739-154">hello U-SQL HAVING clause can be used toorestrict hello output toogroups that satisfy hello HAVING condition:</span></span>

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

<span data-ttu-id="ff739-155">Per scenari di aggregazione avanzate, vedere la documentazione di riferimento di hello hello U-SQL per [aggregare, analitico e fanno riferimento a funzioni](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="ff739-155">For advanced aggregation scenarios, see hello hello U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff739-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ff739-156">Next steps</span></span>
* [<span data-ttu-id="ff739-157">Panoramica di Analisi Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ff739-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="ff739-158">Sviluppare script U-SQL con Data Lake Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ff739-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
