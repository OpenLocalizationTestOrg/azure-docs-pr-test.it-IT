---
title: Introduzione al linguaggio U-SQL | Microsoft Docs
description: Informazioni sulle basi del linguaggio U-SQL.
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
ms.openlocfilehash: 38c4e1b9bd24ef0b8a81f6154620f3f98d3b5ac1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="1f220-103">Introduzione a U-SQL</span><span class="sxs-lookup"><span data-stu-id="1f220-103">Get started with U-SQL</span></span>
<span data-ttu-id="1f220-104">U-SQL è un linguaggio che combina SQL dichiarativo con C# imperativo per consentire di elaborare da su qualsiasi scala.</span><span class="sxs-lookup"><span data-stu-id="1f220-104">U-SQL is a language that combines declarative SQL with imperative C# to let you process data at any scale.</span></span> <span data-ttu-id="1f220-105">Le funzionalità di query scalabili e distribuite offerte da U-SQL consentono di analizzare con efficienza i dati presenti in archivi relazionali, ad esempio il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="1f220-105">Through the scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="1f220-106">Con U-SQL è possibile elaborare i dati non strutturati applicando schemi in lettura e inserendo logiche personalizzate e funzioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="1f220-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="1f220-107">Inoltre, U-SQL include estendibilità che consente un controllo specifico delle modalità di esecuzione su vasta scala.</span><span class="sxs-lookup"><span data-stu-id="1f220-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how to execute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="1f220-108">Risorse di formazione</span><span class="sxs-lookup"><span data-stu-id="1f220-108">Learning resources</span></span>

* <span data-ttu-id="1f220-109">L'[esercitazione su U-SQL](http://aka.ms/usqltutorial) fornisce una procedura dettagliata guidata per la maggior parte del linguaggio U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1f220-109">The [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of the U-SQL language.</span></span> <span data-ttu-id="1f220-110">Si consiglia la lettura di questo documento a tutti gli sviluppatori che vogliono apprendere il linguaggio U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1f220-110">This document is recommended reading for all developers wanting to learn U-SQL.</span></span>
* <span data-ttu-id="1f220-111">Per informazioni dettagliate sulla **sintassi del linguaggio U-SQL**, vedere le [Informazioni di riferimento sul linguaggio U-SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="1f220-111">For detailed information about the **U-SQL language syntax**, see the [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="1f220-112">Per informazioni sulla **filosofia di progettazione alla base di U-SQL**, vedere il post sul blog di Visual Studio [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/) (Introduzione a U-SQL: un linguaggio che facilita l'elaborazione dei Big Data).</span><span class="sxs-lookup"><span data-stu-id="1f220-112">To understand the **U-SQL design philosophy**, see the Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f220-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1f220-113">Prerequisites</span></span>

<span data-ttu-id="1f220-114">Prima di analizzare gli esempi in U-SQL di questo documento, leggere e completare l'[Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1f220-114">Before you go through the U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="1f220-115">Questa esercitazione illustra la meccanica dell'uso di U-SQL con Strumenti Azure Data Lake per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1f220-115">That tutorial explains the mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="1f220-116">Il primo script U-SQL</span><span class="sxs-lookup"><span data-stu-id="1f220-116">Your first U-SQL script</span></span>

<span data-ttu-id="1f220-117">Lo script U-SQL seguente è semplice e ci consente di esplorare molti aspetti del linguaggio U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1f220-117">The following U-SQL script is simple and lets us explore many aspects the U-SQL language.</span></span>

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
    TO "/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="1f220-118">Lo script non è stato sottoposto a molte procedure di trasformazione.</span><span class="sxs-lookup"><span data-stu-id="1f220-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="1f220-119">Legge i dati dal file di origine denominato `SearchLog.tsv`, li schematizza e scrive il set di righe in un file denominato SearchLog-first-u-sql.csv.</span><span class="sxs-lookup"><span data-stu-id="1f220-119">It reads from the source file called `SearchLog.tsv`, schematizes it, and writes the rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="1f220-120">Osservare il punto interrogativo accanto al tipo di dati del campo `Duration`.</span><span class="sxs-lookup"><span data-stu-id="1f220-120">Notice the question mark next to the data type in the `Duration` field.</span></span> <span data-ttu-id="1f220-121">Significa che il campo `Duration` può avere anche un valore null.</span><span class="sxs-lookup"><span data-stu-id="1f220-121">It means that the `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="1f220-122">Concetti chiave</span><span class="sxs-lookup"><span data-stu-id="1f220-122">Key concepts</span></span>
* <span data-ttu-id="1f220-123">**Variabili del set di righe**: ad ogni espressione di query che produce un set di righe può essere assegnata una variabile.</span><span class="sxs-lookup"><span data-stu-id="1f220-123">**Rowset variables**: Each query expression that produces a rowset can be assigned to a variable.</span></span> <span data-ttu-id="1f220-124">U-SQL segue il modello di denominazione delle variabili T-SQ, ad esempio `@searchlog`, nello script.</span><span class="sxs-lookup"><span data-stu-id="1f220-124">U-SQL follows the T-SQL variable naming pattern (`@searchlog`, for example) in the script.</span></span>
* <span data-ttu-id="1f220-125">La parola chiave **EXTRACT** legge i dati di un file e definisce lo schema sulla lettura.</span><span class="sxs-lookup"><span data-stu-id="1f220-125">The **EXTRACT** keyword reads data from a file and defines the schema on read.</span></span> <span data-ttu-id="1f220-126">`Extractors.Tsv` è un estrattore di U-SQL integrato per i valori separati da tabulazioni.</span><span class="sxs-lookup"><span data-stu-id="1f220-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="1f220-127">È possibile sviluppare estrattori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="1f220-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="1f220-128">**OUTPUT** scrive i dati da un set di righe a un file.</span><span class="sxs-lookup"><span data-stu-id="1f220-128">The **OUTPUT** writes data from a rowset to a file.</span></span> <span data-ttu-id="1f220-129">`Outputters.Csv()` è un outputter di U-SQL integrato per creare un file con valori separati da virgole.</span><span class="sxs-lookup"><span data-stu-id="1f220-129">`Outputters.Csv()` is a built-in U-SQL outputter to create a comma-separated-value file.</span></span> <span data-ttu-id="1f220-130">È possibile sviluppare anche outputter personalizzati.</span><span class="sxs-lookup"><span data-stu-id="1f220-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="1f220-131">Percorsi di file</span><span class="sxs-lookup"><span data-stu-id="1f220-131">File paths</span></span>

<span data-ttu-id="1f220-132">Le istruzioni EXTRACT e OUTPUT usano percorsi di file.</span><span class="sxs-lookup"><span data-stu-id="1f220-132">The EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="1f220-133">I percorsi di file possono essere assoluti o relativi:</span><span class="sxs-lookup"><span data-stu-id="1f220-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="1f220-134">Il seguente percorso di file assoluto fa riferimento a un file in un Data Lake Store denominato `mystore`:</span><span class="sxs-lookup"><span data-stu-id="1f220-134">This following absolute file path refers to a file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="1f220-135">Il seguente percorso di file inizia con `"/"`.</span><span class="sxs-lookup"><span data-stu-id="1f220-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="1f220-136">Fa riferimento a un file nell'account di Data Lake Store predefinito:</span><span class="sxs-lookup"><span data-stu-id="1f220-136">It refers to a file in the default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="1f220-137">Usare variabili scalari</span><span class="sxs-lookup"><span data-stu-id="1f220-137">Use scalar variables</span></span>

<span data-ttu-id="1f220-138">Per gestire più facilmente lo script, è possibile usare anche variabili scalari.</span><span class="sxs-lookup"><span data-stu-id="1f220-138">You can use scalar variables as well to make your script maintenance easier.</span></span> <span data-ttu-id="1f220-139">Lo script U-SQL precedente può essere anche scritto come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="1f220-139">The previous U-SQL script can also be written as:</span></span>

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
        TO @out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="1f220-140">Trasformare set di righe</span><span class="sxs-lookup"><span data-stu-id="1f220-140">Transform rowsets</span></span>

<span data-ttu-id="1f220-141">Usare l'istruzione **SELECT** per trasformare set di righe:</span><span class="sxs-lookup"><span data-stu-id="1f220-141">Use **SELECT** to transform rowsets:</span></span>

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
        TO "/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="1f220-142">La clausola WHERE usa un'[espressione booleana C#](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f220-142">The WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="1f220-143">È possibile usare il linguaggio di espressione C# per creare espressioni e funzioni personali.</span><span class="sxs-lookup"><span data-stu-id="1f220-143">You can use the C# expression language to do your own expressions and functions.</span></span> <span data-ttu-id="1f220-144">È anche possibile combinarle con congiunzioni (AND) e disgiunzioni (OR) logiche per eseguire operazioni di filtro più complesse.</span><span class="sxs-lookup"><span data-stu-id="1f220-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="1f220-145">Lo script seguente usa il metodo DateTime.Parse() e una congiunzione.</span><span class="sxs-lookup"><span data-stu-id="1f220-145">The following script uses the DateTime.Parse() method and a conjunction.</span></span>

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
        TO "/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="1f220-146">La seconda query fa riferimento al risultato del primo set di righe e il risultato è pertanto una composizione dei due filtri.</span><span class="sxs-lookup"><span data-stu-id="1f220-146">The second query is operating on the result of the first rowset, which creates a composite of the two filters.</span></span> <span data-ttu-id="1f220-147">È anche possibile riusare un nome di variabile poiché i nomi vengono definiti nell'ambito lessicale.</span><span class="sxs-lookup"><span data-stu-id="1f220-147">You can also reuse a variable name, and the names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="1f220-148">Aggregare set di righe</span><span class="sxs-lookup"><span data-stu-id="1f220-148">Aggregate rowsets</span></span>
<span data-ttu-id="1f220-149">U-SQL consente di usare le istruzioni familiari ORDER BY e GROUP BY, nonché le aggregazioni.</span><span class="sxs-lookup"><span data-stu-id="1f220-149">U-SQL gives you the familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="1f220-150">La query seguente trova la durata totale per area e mostra quindi le prime cinque durate, elencate in ordine.</span><span class="sxs-lookup"><span data-stu-id="1f220-150">The following query finds the total duration per region, and then displays the top five durations in order.</span></span>

<span data-ttu-id="1f220-151">I set di righe U-SQL non mantengono l'ordine per la query successiva.</span><span class="sxs-lookup"><span data-stu-id="1f220-151">U-SQL rowsets do not preserve their order for the next query.</span></span> <span data-ttu-id="1f220-152">Per ordinare un output, pertanto, è necessario aggiungere ORDER BY all'istruzione OUTPUT:</span><span class="sxs-lookup"><span data-stu-id="1f220-152">Thus, to order an output, you need to add ORDER BY to the OUTPUT statement:</span></span>

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
        TO @out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        TO @out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="1f220-153">La clausola U-SQL ORDER BY richiede l'uso della clausola FETCH in un'espressione SELECT.</span><span class="sxs-lookup"><span data-stu-id="1f220-153">The U-SQL ORDER BY clause requires using the FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="1f220-154">È possibile usare la clausola U-SQL HAVING per limitare l'output ai gruppi che soddisfano la condizione HAVING:</span><span class="sxs-lookup"><span data-stu-id="1f220-154">The U-SQL HAVING clause can be used to restrict the output to groups that satisfy the HAVING condition:</span></span>

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
        TO "/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="1f220-155">Per gli scenari avanzati di aggregazione, vedere la documentazione di riferimento U-SQL per le [funzioni di aggregazione, analisi e riferimento](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="1f220-155">For advanced aggregation scenarios, see the The U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f220-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1f220-156">Next steps</span></span>
* [<span data-ttu-id="1f220-157">Panoramica di Analisi Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1f220-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="1f220-158">Sviluppare script U-SQL con Data Lake Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f220-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
