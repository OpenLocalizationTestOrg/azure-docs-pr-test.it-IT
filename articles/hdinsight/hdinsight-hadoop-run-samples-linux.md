---
title: Eseguire esempi di Handoop MapReduce in HDInsight | Microsoft Docs
description: Introduzione all'uso di esempi di MapReduce in file JAR inclusi in HDInsight. Usare SSH per connettersi al cluster e quindi usare il comando di Hadoop per eseguire i processi di esempio.
keywords: jar esempio di hadoop, jar esempi di hadoop, esempi di hadoop mapreduce, esempi di mapreduce
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 447c07f869ff9a2a2a00089248be98e6729d6dc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="run-the-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="8a3a5-105">Eseguire gli esempi di MapReduce inclusi in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8a3a5-105">Run the MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="8a3a5-106">Informazioni su come eseguire esempi di MapReduce inclusi con Hadoop su HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-106">Learn how to run the MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a3a5-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8a3a5-107">Prerequisites</span></span>

* <span data-ttu-id="8a3a5-108">**Un cluster HDInsight**: vedere [Introduzione all'uso di Hadoop con Hive in HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="8a3a5-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8a3a5-109">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8a3a5-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8a3a5-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="8a3a5-111">**Un client SSH**: per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8a3a5-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="the-mapreduce-examples"></a><span data-ttu-id="8a3a5-112">Gli esempi di MapReduce</span><span class="sxs-lookup"><span data-stu-id="8a3a5-112">The MapReduce examples</span></span>

<span data-ttu-id="8a3a5-113">**Percorso**: gli esempi si trovano nel cluster HDInsight in `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-113">**Location**: The samples are located on the HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="8a3a5-114">**Contenuto**: gli esempi seguenti sono contenuti in questo archivio:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-114">**Contents**: The following samples are contained in this archive:</span></span>

* <span data-ttu-id="8a3a5-115">`aggregatewordcount`: programma MapReduce basato su aggregazione che conta le parole nei file di input.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="8a3a5-116">`aggregatewordhist`: programma MapReduce basato su aggregazione che calcola l'istogramma delle parole nei file di input.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes the histogram of the words in the input files.</span></span>
* <span data-ttu-id="8a3a5-117">`bbp`: programma MapReduce che usa la formula Bailey-Borwein-Plouffe per calcolare le cifre esatte del pi greco.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.</span></span>
* <span data-ttu-id="8a3a5-118">`dbcount`: processo di esempio che conta i log di pageview archiviati in un database.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-118">`dbcount`: An example job that counts the pageview logs stored in a database.</span></span>
* <span data-ttu-id="8a3a5-119">`distbbp`: programma MapReduce che usa una formula di tipo BBP per calcolare i bit esatti del pi greco.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-119">`distbbp`: A mapreduce program that uses a BBP-type formula to compute exact bits of Pi.</span></span>
* <span data-ttu-id="8a3a5-120">`grep`: programma MapReduce che conta le corrispondenze di un regex nell'input.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-120">`grep`: A mapreduce program that counts the matches of a regex in the input.</span></span>
* <span data-ttu-id="8a3a5-121">`join`: processo che esegue un join su set di dati ordinati ed equamente partizionati.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="8a3a5-122">`multifilewc`: processo che conta le parole da più file.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="8a3a5-123">`pentomino`: programma di tassellatura MapReduce per trovare soluzioni ai problemi relativi ai pentamini.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-123">`pentomino`: A mapreduce tile laying program to find solutions to pentomino problems.</span></span>
* <span data-ttu-id="8a3a5-124">`pi`: programma MapReduce che stima il pi greco usando un metodo simile al metodo Monte Carlo.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="8a3a5-125">`randomtextwriter`: programma MapReduce che scrive 10 GB di dati testuali casuali per nodo.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="8a3a5-126">`randomwriter`: programma MapReduce che scrive 10 GB di dati casuali per nodo.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="8a3a5-127">`secondarysort`: esempio che definisce un ordinamento secondario per la fase di riduzione.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-127">`secondarysort`: An example defining a secondary sort to the reduce phase.</span></span>
* <span data-ttu-id="8a3a5-128">`sort`: programma MapReduce che ordina i dati scritti dal writer casuale.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-128">`sort`: A mapreduce program that sorts the data written by the random writer.</span></span>
* <span data-ttu-id="8a3a5-129">`sudoku`: risolutore di sudoku.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="8a3a5-130">`teragen`: genera dati per terasort.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-130">`teragen`: Generate data for the terasort.</span></span>
* <span data-ttu-id="8a3a5-131">`terasort`: esegue il processo terasort.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-131">`terasort`: Run the terasort.</span></span>
* <span data-ttu-id="8a3a5-132">`teravalidate`: verifica i risultati di terasort.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="8a3a5-133">`wordcount`: programma MapReduce che conta le parole nei file di input.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-133">`wordcount`: A mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="8a3a5-134">`wordmean`: programma MapReduce che conta la lunghezza media delle parole nei file di input.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-134">`wordmean`: A mapreduce program that counts the average length of the words in the input files.</span></span>
* <span data-ttu-id="8a3a5-135">`wordmedian`: programma MapReduce che conta la lunghezza mediana delle parole nei file di input.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-135">`wordmedian`: A mapreduce program that counts the median length of the words in the input files.</span></span>
* <span data-ttu-id="8a3a5-136">`wordstandarddeviation`: programma MapReduce che conta la deviazione standard della lunghezza delle parole nei file di input.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-136">`wordstandarddeviation`: A mapreduce program that counts the standard deviation of the length of the words in the input files.</span></span>

<span data-ttu-id="8a3a5-137">**Codice sorgente**: il codice sorgente per questi esempi è incluso nel cluster HDInsight in `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-137">**Source code**: Source code for these samples is included on the HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="8a3a5-138">La parte di percorso `2.2.4.9-1` è la versione di Hortonworks Data Platform per il cluster HDInsight e può essere diversa da quella del cluster che si sta usando.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-138">The `2.2.4.9-1` in the path is the version of the Hortonworks Data Platform for the HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-the-wordcount-example"></a><span data-ttu-id="8a3a5-139">Eseguire l'esempio wordcount</span><span class="sxs-lookup"><span data-stu-id="8a3a5-139">Run the wordcount example</span></span>

1. <span data-ttu-id="8a3a5-140">Connettersi a HDInsight tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-140">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="8a3a5-141">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8a3a5-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="8a3a5-142">Dal prompt di `username@#######:~$` usare il comando seguente per ottenere l'elenco degli esempi:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-142">From the `username@#######:~$` prompt, use the following command to list the samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="8a3a5-143">Tale comando consente di generare l'elenco degli esempi presenti nella sezione precedente del documento.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-143">This command generates the list of sample from the previous section of this document.</span></span>

3. <span data-ttu-id="8a3a5-144">Usare il comando seguente per ottenere informazioni della guida su un esempio specifico.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-144">Use the following command to get help on a specific sample.</span></span> <span data-ttu-id="8a3a5-145">In questo caso, l'esempio **wordcount** :</span><span class="sxs-lookup"><span data-stu-id="8a3a5-145">In this case, the **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="8a3a5-146">Viene visualizzato il messaggio seguente:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-146">You receive the following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="8a3a5-147">Tale messaggio indica che è possibile specificare più percorsi di input per i documenti di origine.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-147">This message indicates that you can provide several input paths for the source documents.</span></span> <span data-ttu-id="8a3a5-148">Il percorso finale corrisponde alla posizione in cui verrà memorizzato l'output (conteggio delle parole nei documenti di origine).</span><span class="sxs-lookup"><span data-stu-id="8a3a5-148">The final path is where the output (count of words in the source documents) is stored.</span></span>

4. <span data-ttu-id="8a3a5-149">Usare il comando seguente per contare tutte le parole nei Codici di Leonardo da Vinci, forniti come dati di esempio con il cluster:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-149">Use the following to count all words in the Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="8a3a5-150">L'input per questo processo viene letto da `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="8a3a5-151">L'output per questo esempio viene archiviato in `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="8a3a5-152">Entrambi i percorsi si trovano nella risorsa di archiviazione predefinita per il cluster, non nel file system locale.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-152">Both paths are located on default storage for the cluster, not the local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8a3a5-153">Come indicato nelle informazioni della guida per l'esempio wordcount, è anche possibile specificare più file di input.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-153">As noted in the help for the wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="8a3a5-154">Ad esempio, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` eseguirebbe il conteggio delle parole in davinci.txt e in ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="8a3a5-155">Dopo il completamento del processo, usare il comando seguente per visualizzare l'output:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-155">Once the job completes, use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="8a3a5-156">Il comando esegue la concatenazione di tutti i file di output prodotti dal processo.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-156">This command concatenates all the output files produced by the job.</span></span> <span data-ttu-id="8a3a5-157">In seguito visualizza l'output nella console.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-157">It displays the output to the console.</span></span> <span data-ttu-id="8a3a5-158">L'output è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-158">The output is similar to the following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="8a3a5-159">Ogni riga rappresenta una parola e quante volte ricorre nei dati di input.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-159">Each line represents a word and how many times it occurred in the input data.</span></span>

## <a name="the-sudoku-example"></a><span data-ttu-id="8a3a5-160">L'esempio di Sudoku</span><span class="sxs-lookup"><span data-stu-id="8a3a5-160">The Sudoku example</span></span>

<span data-ttu-id="8a3a5-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) è un rompicapo logico composto da griglie di 9 celle in formato 3x3.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="8a3a5-162">Alcune celle della griglia contengono numeri, altre sono vuote e l'obiettivo consiste nel risolvere le celle vuote.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-162">Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells.</span></span> <span data-ttu-id="8a3a5-163">Il collegamento precedente contiene altre informazioni sul puzzle, ma lo scopo di questo esempio consiste nel risolvere le celle vuote.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-163">The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells.</span></span> <span data-ttu-id="8a3a5-164">L'input dovrà essere un file nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-164">So our input should be a file that is in the following format:</span></span>

* <span data-ttu-id="8a3a5-165">Nove righe di nove colonne.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="8a3a5-166">Ogni colonna può contenere un numero o `?` (che indica una cella vuota)</span><span class="sxs-lookup"><span data-stu-id="8a3a5-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="8a3a5-167">Le celle sono separate da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-167">Cells are separated by a space</span></span>

<span data-ttu-id="8a3a5-168">Esiste un modo certo per creare un puzzle Sudoku in base al quale non è possibile ripetere un numero in una colonna o una riga.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-168">There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="8a3a5-169">Nel cluster di HDInsight è disponibile un esempio realizzato correttamente.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-169">There's an example on the HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="8a3a5-170">Si trova in `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` e contiene il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains the following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="8a3a5-171">Per eseguire questo esempio di Sudoku, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-171">To run this example problem through the Sudoku example, use the following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="8a3a5-172">Il risultato è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-172">The results appear similar to the following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="8a3a5-173">Esempio di pi greco (π)</span><span class="sxs-lookup"><span data-stu-id="8a3a5-173">Pi (π) example</span></span>

<span data-ttu-id="8a3a5-174">Per calcolare il valore di Pi greco, l'esempio usa un metodo statistico simile al metodo Monte Carlo.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-174">The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span></span> <span data-ttu-id="8a3a5-175">I punti vengono posizionati in modo casuale in un quadrato unitario.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="8a3a5-176">Il quadrato contiene anche un cerchio.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-176">The square also contains a circle.</span></span> <span data-ttu-id="8a3a5-177">La probabilità che i punti siano compresi nel cerchio sono uguali all'area del cerchio, pi greco/4.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-177">The probability that the points fall within the circle are equal to the area of the circle, pi/4.</span></span> <span data-ttu-id="8a3a5-178">Il valore di pi greco può essere stimato dal valore di 4R.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-178">The value of pi can be estimated from the value of 4R.</span></span> <span data-ttu-id="8a3a5-179">R indica il rapporto tra il numero di punti che si trovano all'interno del cerchio e il numero totale di punti che si trovano all'interno del quadrato.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-179">R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span></span> <span data-ttu-id="8a3a5-180">La precisione del calcolo è direttamente proporzionale al numero di punti utilizzati.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-180">The larger the sample of points used, the better the estimate is.</span></span>

<span data-ttu-id="8a3a5-181">Usare il comando seguente per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-181">Use the following command to run this sample.</span></span> <span data-ttu-id="8a3a5-182">Il comando usa 16 mappe con 10.000.000 di esempi, ognuno per il calcolo del pi greco:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-182">This command uses 16 maps with 10,000,000 samples each to estimate the value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="8a3a5-183">Il valore restituito da questo comando è simile a **3,14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-183">The value returned by this command is similar to **3.14159155000000000000**.</span></span> <span data-ttu-id="8a3a5-184">A scopo di riferimento, le prime 10 cifre decimali del pi greco sono 3,1415926535.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-184">For references, the first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="8a3a5-185">Esempio di Greysort 10 GB</span><span class="sxs-lookup"><span data-stu-id="8a3a5-185">10 GB Greysort example</span></span>

<span data-ttu-id="8a3a5-186">GraySort è un ordinamento benchmark.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="8a3a5-187">La metrica è la velocità di ordinamento (TB/minuto) ottenuta durante l'ordinamento di quantità di dati elevate, in genere almeno 100 TB.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-187">The metric is the sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="8a3a5-188">In questo esempio vengono usati solo 10 GB di dati, in modo da consentire un'esecuzione relativamente rapida.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="8a3a5-189">Usa le applicazioni di MapReduce sviluppate da Owen O'Malley e Arun Murthy.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-189">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="8a3a5-190">Queste applicazioni sono vincitrici del benchmark annuale di ordinamento generico di terabyte ("daytona") nel 2009 con una velocità pari a 0,578 TB/min (100 TB in 173 minuti).</span><span class="sxs-lookup"><span data-stu-id="8a3a5-190">These applications won the annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="8a3a5-191">Per ulteriori informazioni su questo e su altri benchmark di ordinamento, vedere il sito [Sortbenchmark](http://sortbenchmark.org/) .</span><span class="sxs-lookup"><span data-stu-id="8a3a5-191">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="8a3a5-192">In questo esempio vengono utilizzati tre set di programmi MapReduce:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="8a3a5-193">**TeraGen**: programma MapReduce che genera righe di dati da ordinare.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-193">**TeraGen**: A MapReduce program that generates rows of data to sort</span></span>

* <span data-ttu-id="8a3a5-194">**TeraSort**esegue il campionamento dei dati di input e usa MapReduce per organizzare i dati in un ordine totale.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-194">**TeraSort**: Samples the input data and uses MapReduce to sort the data into a total order</span></span>

    <span data-ttu-id="8a3a5-195">TeraSort è un ordinamento standard di MapReduce, ad eccezione di un partitioner personalizzato.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="8a3a5-196">Il partitioner usa un elenco ordinato di chiavi campionate N-1 che definiscono l'intervallo di chiavi per ogni riduzione.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-196">The partitioner uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span></span> <span data-ttu-id="8a3a5-197">In particolare, tutte le chiavi corrispondenti al criterio sample[i-1]<= chiave < sample[i] vengono inviate alla funzione reduce i.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span></span> <span data-ttu-id="8a3a5-198">Il partitioner garantisce che tutti gli output di reduce i siano inferiori all'output della funzione reduce i+1.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-198">This partitioner guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span></span>

* <span data-ttu-id="8a3a5-199">**TeraValidate**: un programma MapReduce che convalida l'ordinamento globale dell'output</span><span class="sxs-lookup"><span data-stu-id="8a3a5-199">**TeraValidate**: A MapReduce program that validates that the output is globally sorted</span></span>

    <span data-ttu-id="8a3a5-200">Crea una funzione map per ogni file nella directory di output e ogni funzione map assicura che ogni chiave sia inferiore o uguale alla precedente.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-200">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span></span> <span data-ttu-id="8a3a5-201">La funzione map genera i record delle prime e delle ultime chiavi di ogni file.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-201">The map function generates records of the first and last keys of each file.</span></span> <span data-ttu-id="8a3a5-202">La funzione reduce assicura che la prima chiave del file i sia maggiore dell'ultima chiave del file i-1.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-202">The reduce function ensures that the first key of file i is greater than the last key of file i-1.</span></span> <span data-ttu-id="8a3a5-203">Eventuali problemi vengono segnalati come output della fase reduce insieme alle chiavi che non rispettano l'ordinamento.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-203">Any problems are reported as an output of the reduce phase, with the keys that are out of order.</span></span>

<span data-ttu-id="8a3a5-204">Usare i passaggi seguenti per generare dati, ordinarli e quindi convalidare l'output:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-204">Use the following steps to generate data, sort, and then validate the output:</span></span>

1. <span data-ttu-id="8a3a5-205">Generare 10 GB di dati, che vengono archiviati nella risorsa di archiviazione predefinita del cluster HDInsight in `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-205">Generate 10 GB of data, which is stored to the HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="8a3a5-206">`-Dmapred.map.tasks` indica ad Hadoop quante attività di mapping usare per questo processo.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-206">The `-Dmapred.map.tasks` tells Hadoop how many map tasks to use for this job.</span></span> <span data-ttu-id="8a3a5-207">I due parametri finali indicano al processo di creare 10 GB di dati e di archiviarli in `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-207">The final two parameters instruct the job to create 10 GB of data and to store it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="8a3a5-208">Eseguire il comando seguente per ordinare i dati:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-208">Use the following command to sort the data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="8a3a5-209">`-Dmapred.reduce.tasks` indica ad Hadoop quante attività di riduzione usare per questo processo.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-209">The `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks to use for the job.</span></span> <span data-ttu-id="8a3a5-210">I due parametri finali sono solo i percorsi di input e output per i dati.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-210">The final two parameters are just the input and output locations for data.</span></span>

3. <span data-ttu-id="8a3a5-211">Per convalidare i dati generati dall'ordinamento, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-211">Use the following to validate the data generated by the sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="8a3a5-212">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a3a5-212">Next steps</span></span>

<span data-ttu-id="8a3a5-213">In questo articolo si è appreso come eseguire gli esempi inclusi nei cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="8a3a5-213">From this article, you learned how to run the samples included with the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="8a3a5-214">Per le esercitazioni sull'uso di Pig, Hive e MapReduce con HDInsight, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a3a5-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span></span>

* <span data-ttu-id="8a3a5-215">[Usare Pig con Hadoop in HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="8a3a5-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="8a3a5-216">[Usare Hive con Hadoop in HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="8a3a5-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="8a3a5-217">[Usare MapReduce con Hadoop in HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="8a3a5-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
