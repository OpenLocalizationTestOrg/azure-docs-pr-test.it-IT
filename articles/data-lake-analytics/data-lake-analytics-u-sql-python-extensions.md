---
title: Consente di generare script U-SQL aaaExtend con Python in Azure Data Lake Analitica | Documenti Microsoft
description: Informazioni su come codice toorun Python script U-SQL
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="f38c5-103">Esercitazione: Introduzione all'estensione di U-SQL con Python</span><span class="sxs-lookup"><span data-stu-id="f38c5-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="f38c5-104">Le estensioni di Python per U-SQL consentono agli sviluppatori tooperform massiva l'esecuzione parallela di codice Python.</span><span class="sxs-lookup"><span data-stu-id="f38c5-104">Python Extensions for U-SQL enable developers tooperform massively parallel execution of Python code.</span></span> <span data-ttu-id="f38c5-105">Hello di esempio seguente illustra i passaggi di base hello:</span><span class="sxs-lookup"><span data-stu-id="f38c5-105">hello following example illustrates hello basic steps:</span></span>

* <span data-ttu-id="f38c5-106">Hello utilizzare `REFERENCE ASSEMBLY` istruzione tooenable Python estensioni hello Script U-SQL</span><span class="sxs-lookup"><span data-stu-id="f38c5-106">Use hello `REFERENCE ASSEMBLY` statement tooenable Python extensions for hello U-SQL Script</span></span>
* <span data-ttu-id="f38c5-107">Utilizzo di hello `REDUCE` hello toopartition operazione dati su una chiave di input</span><span class="sxs-lookup"><span data-stu-id="f38c5-107">Using hello `REDUCE` operation toopartition hello input data on a key</span></span>
* <span data-ttu-id="f38c5-108">le estensioni di Python per U-SQL Hello includono un riduttore incorporato (`Extension.Python.Reducer`) che esegue codice Python in ogni riduttore toohello vertice assegnato</span><span class="sxs-lookup"><span data-stu-id="f38c5-108">hello Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned toohello reducer</span></span>
* <span data-ttu-id="f38c5-109">Hello script U-SQL contiene codice Python incorporato hello che dispone di una funzione denominata `usqlml_main` che accetta un pandas frame di dati come input e restituisce un pandas frame di dati come output.</span><span class="sxs-lookup"><span data-stu-id="f38c5-109">hello U-SQL script contains hello embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="f38c5-110">Come Python si integra con U-SQL</span><span class="sxs-lookup"><span data-stu-id="f38c5-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="f38c5-111">Tipi di dati</span><span class="sxs-lookup"><span data-stu-id="f38c5-111">Datatypes</span></span>

* <span data-ttu-id="f38c5-112">Le colonne stringa e numeriche di U-SQL vengono convertite come sono tra Pandas e U-SQL</span><span class="sxs-lookup"><span data-stu-id="f38c5-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="f38c5-113">I valori null U-SQL vengono convertiti tooand da Pandas `NA` valori</span><span class="sxs-lookup"><span data-stu-id="f38c5-113">U-SQL Nulls are converted tooand from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="f38c5-114">Schemi</span><span class="sxs-lookup"><span data-stu-id="f38c5-114">Schemas</span></span>

* <span data-ttu-id="f38c5-115">I vettori indice di Pandas non sono supportati in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f38c5-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="f38c5-116">Tutti i frame di dati di input nella funzione di Python hello hanno sempre un indice numerico a 64 bit compreso tra 0 e il numero di hello di righe meno 1.</span><span class="sxs-lookup"><span data-stu-id="f38c5-116">All input data frames in hello Python function always have a 64-bit numerical index from 0 through hello number of rows minus 1.</span></span> 
* <span data-ttu-id="f38c5-117">I set di dati di U-SQL non possono avere nomi di colonna duplicati.</span><span class="sxs-lookup"><span data-stu-id="f38c5-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="f38c5-118">Nomi di colonna dei set di dati di U-SQL che non sono stringhe.</span><span class="sxs-lookup"><span data-stu-id="f38c5-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="f38c5-119">Versioni di Python</span><span class="sxs-lookup"><span data-stu-id="f38c5-119">Python Versions</span></span>
<span data-ttu-id="f38c5-120">È supportato solo Python 3.5.1 (compilato per Windows).</span><span class="sxs-lookup"><span data-stu-id="f38c5-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="f38c5-121">Moduli standard di Python</span><span class="sxs-lookup"><span data-stu-id="f38c5-121">Standard Python modules</span></span>
<span data-ttu-id="f38c5-122">Tutti i moduli Python standard hello sono inclusi.</span><span class="sxs-lookup"><span data-stu-id="f38c5-122">All hello standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="f38c5-123">Altri moduli di Python</span><span class="sxs-lookup"><span data-stu-id="f38c5-123">Additional Python modules</span></span>
<span data-ttu-id="f38c5-124">Oltre alle librerie standard di Python di hello, sono incluse varie librerie python comunemente usate:</span><span class="sxs-lookup"><span data-stu-id="f38c5-124">Besides hello standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="f38c5-125">Messaggi di eccezione</span><span class="sxs-lookup"><span data-stu-id="f38c5-125">Exception Messages</span></span>
<span data-ttu-id="f38c5-126">Attualmente un'eccezione nel codice Python viene visualizzata come errore di vertice generico.</span><span class="sxs-lookup"><span data-stu-id="f38c5-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="f38c5-127">I messaggi di errore di hello processo U-SQL verranno visualizzati hello future, messaggio di eccezione hello Python.</span><span class="sxs-lookup"><span data-stu-id="f38c5-127">In hello future, hello U-SQL Job error messages will display hello Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="f38c5-128">Limitazioni delle dimensioni di input e output</span><span class="sxs-lookup"><span data-stu-id="f38c5-128">Input and Output size limitations</span></span>
<span data-ttu-id="f38c5-129">Ogni vertice ha una quantità limitata di memoria assegnata tooit.</span><span class="sxs-lookup"><span data-stu-id="f38c5-129">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="f38c5-130">che attualmente corrisponde a 6 GB per AU.</span><span class="sxs-lookup"><span data-stu-id="f38c5-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="f38c5-131">Poiché hello frame di dati di input e output devono essere presenti in memoria nel codice Python hello, dimensione totale di hello per hello input e output non può superare 6 GB.</span><span class="sxs-lookup"><span data-stu-id="f38c5-131">Because hello input and output DataFrames must exist in memory in hello Python code, hello total size for hello input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="f38c5-132">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f38c5-132">See also</span></span>
* [<span data-ttu-id="f38c5-133">Panoramica di Analisi Data Lake di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f38c5-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="f38c5-134">Sviluppare script U-SQL mediante Strumenti di Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f38c5-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="f38c5-135">Uso delle funzioni finestra di U-SQL per i processi di Analisi Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="f38c5-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

