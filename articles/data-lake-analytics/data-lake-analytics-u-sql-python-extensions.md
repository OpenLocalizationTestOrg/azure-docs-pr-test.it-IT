---
title: Estendere gli script U-SQL con Python in Azure Data Lake Analytics | Documentazione Microsoft
description: Informazioni su come eseguire il codice Python negli script U-SQL
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
ms.openlocfilehash: d18ef1f747aee2fa01cef9891432d0461031ee4c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="93fc3-103">Esercitazione: Introduzione all'estensione di U-SQL con Python</span><span class="sxs-lookup"><span data-stu-id="93fc3-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="93fc3-104">Le estensioni Python per U-SQL consentono agli sviluppatori di effettuare esecuzioni parallele elevate del codice Python.</span><span class="sxs-lookup"><span data-stu-id="93fc3-104">Python Extensions for U-SQL enable developers to perform massively parallel execution of Python code.</span></span> <span data-ttu-id="93fc3-105">L'esempio seguente illustra i passaggi di base:</span><span class="sxs-lookup"><span data-stu-id="93fc3-105">The following example illustrates the basic steps:</span></span>

* <span data-ttu-id="93fc3-106">Usare l'istruzione `REFERENCE ASSEMBLY` per abilitare le estensioni Python per lo script U-SQL</span><span class="sxs-lookup"><span data-stu-id="93fc3-106">Use the `REFERENCE ASSEMBLY` statement to enable Python extensions for the U-SQL Script</span></span>
* <span data-ttu-id="93fc3-107">Uso dell'operazione `REDUCE` per partizionare i dati di input in una chiave</span><span class="sxs-lookup"><span data-stu-id="93fc3-107">Using the `REDUCE` operation to partition the input data on a key</span></span>
* <span data-ttu-id="93fc3-108">Le estensioni Python per U-SQL includono un riduttore predefinito (`Extension.Python.Reducer`) che esegue il codice Python in ogni vertice assegnato al riduttore</span><span class="sxs-lookup"><span data-stu-id="93fc3-108">The Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned to the reducer</span></span>
* <span data-ttu-id="93fc3-109">Lo script U-SQL contiene il codice Python incorporato che include una funzione denominata `usqlml_main` che accetta un intervallo di dati Pandas come input e restituisce un intervallo di dati Pandas come output.</span><span class="sxs-lookup"><span data-stu-id="93fc3-109">The U-SQL script contains the embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

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
        TO "/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="93fc3-110">Come Python si integra con U-SQL</span><span class="sxs-lookup"><span data-stu-id="93fc3-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="93fc3-111">Tipi di dati</span><span class="sxs-lookup"><span data-stu-id="93fc3-111">Datatypes</span></span>

* <span data-ttu-id="93fc3-112">Le colonne stringa e numeriche di U-SQL vengono convertite come sono tra Pandas e U-SQL</span><span class="sxs-lookup"><span data-stu-id="93fc3-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="93fc3-113">I valori Null di U-SQL vengono convertiti in e da valori `NA` di Pandas</span><span class="sxs-lookup"><span data-stu-id="93fc3-113">U-SQL Nulls are converted to and from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="93fc3-114">Schemi</span><span class="sxs-lookup"><span data-stu-id="93fc3-114">Schemas</span></span>

* <span data-ttu-id="93fc3-115">I vettori indice di Pandas non sono supportati in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="93fc3-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="93fc3-116">Tutti i frame di dati di input della funzione Python hanno sempre un indice numerico a 64 bit compreso tra 0 e il numero di righe meno 1.</span><span class="sxs-lookup"><span data-stu-id="93fc3-116">All input data frames in the Python function always have a 64-bit numerical index from 0 through the number of rows minus 1.</span></span> 
* <span data-ttu-id="93fc3-117">I set di dati di U-SQL non possono avere nomi di colonna duplicati.</span><span class="sxs-lookup"><span data-stu-id="93fc3-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="93fc3-118">Nomi di colonna dei set di dati di U-SQL che non sono stringhe.</span><span class="sxs-lookup"><span data-stu-id="93fc3-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="93fc3-119">Versioni di Python</span><span class="sxs-lookup"><span data-stu-id="93fc3-119">Python Versions</span></span>
<span data-ttu-id="93fc3-120">È supportato solo Python 3.5.1 (compilato per Windows).</span><span class="sxs-lookup"><span data-stu-id="93fc3-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="93fc3-121">Moduli standard di Python</span><span class="sxs-lookup"><span data-stu-id="93fc3-121">Standard Python modules</span></span>
<span data-ttu-id="93fc3-122">Sono inclusi tutti i moduli di Python standard.</span><span class="sxs-lookup"><span data-stu-id="93fc3-122">All the standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="93fc3-123">Altri moduli di Python</span><span class="sxs-lookup"><span data-stu-id="93fc3-123">Additional Python modules</span></span>
<span data-ttu-id="93fc3-124">Oltre alle librerie di Python standard, sono incluse diverse librerie di Python di uso frequente:</span><span class="sxs-lookup"><span data-stu-id="93fc3-124">Besides the standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="93fc3-125">Messaggi di eccezione</span><span class="sxs-lookup"><span data-stu-id="93fc3-125">Exception Messages</span></span>
<span data-ttu-id="93fc3-126">Attualmente un'eccezione nel codice Python viene visualizzata come errore di vertice generico.</span><span class="sxs-lookup"><span data-stu-id="93fc3-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="93fc3-127">In futuro i messaggi di errore dei processi U-SQL visualizzeranno il messaggio dell'eccezione Python.</span><span class="sxs-lookup"><span data-stu-id="93fc3-127">In the future, the U-SQL Job error messages will display the Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="93fc3-128">Limitazioni delle dimensioni di input e output</span><span class="sxs-lookup"><span data-stu-id="93fc3-128">Input and Output size limitations</span></span>
<span data-ttu-id="93fc3-129">A ogni vertice è assegnata una quantità di memoria limitata,</span><span class="sxs-lookup"><span data-stu-id="93fc3-129">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="93fc3-130">che attualmente corrisponde a 6 GB per AU.</span><span class="sxs-lookup"><span data-stu-id="93fc3-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="93fc3-131">Poiché devono esistere intervalli di dati di input e di output in memoria nel codice Python, le dimensioni totali per l'input e per l'output non possono superare i 6 GB.</span><span class="sxs-lookup"><span data-stu-id="93fc3-131">Because the input and output DataFrames must exist in memory in the Python code, the total size for the input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="93fc3-132">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="93fc3-132">See also</span></span>
* [<span data-ttu-id="93fc3-133">Panoramica di Analisi Data Lake di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="93fc3-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="93fc3-134">Sviluppare script U-SQL mediante Strumenti di Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="93fc3-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="93fc3-135">Uso delle funzioni finestra di U-SQL per i processi di Analisi Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="93fc3-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

