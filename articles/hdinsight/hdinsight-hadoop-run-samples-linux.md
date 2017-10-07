---
title: esempi di aaaRun MapReduce Hadoop in HDInsight - Azure | Documenti Microsoft
description: Introduzione all'uso di esempi di MapReduce in file JAR inclusi in HDInsight. Utilizzo di SSH tooconnect toohello cluster e quindi utilizzare processi di esempio toorun comando Hadoop hello.
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
ms.openlocfilehash: 7a16bbd51eb17570fcaa3b1e0f5990fa889c106a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="adc7a-105">Eseguire hello MapReduce esempi inclusi in HDInsight</span><span class="sxs-lookup"><span data-stu-id="adc7a-105">Run hello MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="adc7a-106">Informazioni su come esempi di MapReduce hello toorun incluso con Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="adc7a-106">Learn how toorun hello MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adc7a-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="adc7a-107">Prerequisites</span></span>

* <span data-ttu-id="adc7a-108">**Un cluster HDInsight**: vedere [Introduzione all'uso di Hadoop con Hive in HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="adc7a-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="adc7a-109">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="adc7a-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="adc7a-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="adc7a-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="adc7a-111">**Un client SSH**: per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="adc7a-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="hello-mapreduce-examples"></a><span data-ttu-id="adc7a-112">esempi di Hello MapReduce</span><span class="sxs-lookup"><span data-stu-id="adc7a-112">hello MapReduce examples</span></span>

<span data-ttu-id="adc7a-113">**Percorso**: hello esempi si troveranno nel cluster HDInsight in hello `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="adc7a-113">**Location**: hello samples are located on hello HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="adc7a-114">**Contenuto**: hello seguendo gli esempi contenuto in questo archivio:</span><span class="sxs-lookup"><span data-stu-id="adc7a-114">**Contents**: hello following samples are contained in this archive:</span></span>

* <span data-ttu-id="adc7a-115">`aggregatewordcount`: Un'aggregazione basata programma mapreduce che conta hello parole nei file di input hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="adc7a-116">`aggregatewordhist`: Un'aggregazione basata programma mapreduce che calcola l'istogramma hello di parole hello nei file di input hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes hello histogram of hello words in hello input files.</span></span>
* <span data-ttu-id="adc7a-117">`bbp`: Un programma mapreduce che utilizza Bailey-Borwein-Plouffe toocompute di cifre esatte di pi greco.</span><span class="sxs-lookup"><span data-stu-id="adc7a-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe toocompute exact digits of Pi.</span></span>
* <span data-ttu-id="adc7a-118">`dbcount`: Un processo di esempio che conta registri pageview hello archiviati in un database.</span><span class="sxs-lookup"><span data-stu-id="adc7a-118">`dbcount`: An example job that counts hello pageview logs stored in a database.</span></span>
* <span data-ttu-id="adc7a-119">`distbbp`: Un programma mapreduce che utilizza un bit di esatta toocompute formula BBP-tipo di pi greco.</span><span class="sxs-lookup"><span data-stu-id="adc7a-119">`distbbp`: A mapreduce program that uses a BBP-type formula toocompute exact bits of Pi.</span></span>
* <span data-ttu-id="adc7a-120">`grep`: Un programma mapreduce che conta hello trova la corrispondenza di un'espressione regolare in input hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-120">`grep`: A mapreduce program that counts hello matches of a regex in hello input.</span></span>
* <span data-ttu-id="adc7a-121">`join`: processo che esegue un join su set di dati ordinati ed equamente partizionati.</span><span class="sxs-lookup"><span data-stu-id="adc7a-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="adc7a-122">`multifilewc`: processo che conta le parole da più file.</span><span class="sxs-lookup"><span data-stu-id="adc7a-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="adc7a-123">`pentomino`: Un riquadro mapreduce layout soluzioni toofind programma toopentomino problemi.</span><span class="sxs-lookup"><span data-stu-id="adc7a-123">`pentomino`: A mapreduce tile laying program toofind solutions toopentomino problems.</span></span>
* <span data-ttu-id="adc7a-124">`pi`: programma MapReduce che stima il pi greco usando un metodo simile al metodo Monte Carlo.</span><span class="sxs-lookup"><span data-stu-id="adc7a-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="adc7a-125">`randomtextwriter`: programma MapReduce che scrive 10 GB di dati testuali casuali per nodo.</span><span class="sxs-lookup"><span data-stu-id="adc7a-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="adc7a-126">`randomwriter`: programma MapReduce che scrive 10 GB di dati casuali per nodo.</span><span class="sxs-lookup"><span data-stu-id="adc7a-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="adc7a-127">`secondarysort`: Un esempio di definizione toohello un ordinamento secondario ridurre fase.</span><span class="sxs-lookup"><span data-stu-id="adc7a-127">`secondarysort`: An example defining a secondary sort toohello reduce phase.</span></span>
* <span data-ttu-id="adc7a-128">`sort`: Un programma mapreduce che ordina i dati di hello scritti dal writer di hello casuale.</span><span class="sxs-lookup"><span data-stu-id="adc7a-128">`sort`: A mapreduce program that sorts hello data written by hello random writer.</span></span>
* <span data-ttu-id="adc7a-129">`sudoku`: risolutore di sudoku.</span><span class="sxs-lookup"><span data-stu-id="adc7a-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="adc7a-130">`teragen`: Generare dati per terasort hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-130">`teragen`: Generate data for hello terasort.</span></span>
* <span data-ttu-id="adc7a-131">`terasort`: Eseguire terasort hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-131">`terasort`: Run hello terasort.</span></span>
* <span data-ttu-id="adc7a-132">`teravalidate`: verifica i risultati di terasort.</span><span class="sxs-lookup"><span data-stu-id="adc7a-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="adc7a-133">`wordcount`: File di input un programma mapreduce che conta le parole hello in hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-133">`wordcount`: A mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="adc7a-134">`wordmean`: File di input un programma mapreduce che conta lunghezza media di hello delle parole hello hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-134">`wordmean`: A mapreduce program that counts hello average length of hello words in hello input files.</span></span>
* <span data-ttu-id="adc7a-135">`wordmedian`: File di input un programma mapreduce che conta hello mediano lunghezza parole hello hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-135">`wordmedian`: A mapreduce program that counts hello median length of hello words in hello input files.</span></span>
* <span data-ttu-id="adc7a-136">`wordstandarddeviation`: File di input un programma mapreduce che conta hello di deviazione standard di lunghezza hello parole hello hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-136">`wordstandarddeviation`: A mapreduce program that counts hello standard deviation of hello length of hello words in hello input files.</span></span>

<span data-ttu-id="adc7a-137">**Codice sorgente**: il codice sorgente per questi esempi è incluso nel cluster HDInsight in hello `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="adc7a-137">**Source code**: Source code for these samples is included on hello HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="adc7a-138">Hello `2.2.4.9-1` in hello hello versione di hello Hortonworks Data Platform per il cluster HDInsight hello, percorso e può essere diverso per il cluster.</span><span class="sxs-lookup"><span data-stu-id="adc7a-138">hello `2.2.4.9-1` in hello path is hello version of hello Hortonworks Data Platform for hello HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-hello-wordcount-example"></a><span data-ttu-id="adc7a-139">Eseguire l'esempio wordcount hello</span><span class="sxs-lookup"><span data-stu-id="adc7a-139">Run hello wordcount example</span></span>

1. <span data-ttu-id="adc7a-140">Connettersi tramite SSH tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="adc7a-140">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="adc7a-141">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="adc7a-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="adc7a-142">Da hello `username@#######:~$` richiesta, utilizzare i seguenti esempi di comando toolist hello hello:</span><span class="sxs-lookup"><span data-stu-id="adc7a-142">From hello `username@#######:~$` prompt, use hello following command toolist hello samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="adc7a-143">Questo comando Genera elenco hello di esempio dalla sezione precedente di hello di questo documento.</span><span class="sxs-lookup"><span data-stu-id="adc7a-143">This command generates hello list of sample from hello previous section of this document.</span></span>

3. <span data-ttu-id="adc7a-144">Seguente hello utilizzare il comando tooget su un campione specifico.</span><span class="sxs-lookup"><span data-stu-id="adc7a-144">Use hello following command tooget help on a specific sample.</span></span> <span data-ttu-id="adc7a-145">In questo caso, hello **wordcount** esempio:</span><span class="sxs-lookup"><span data-stu-id="adc7a-145">In this case, hello **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="adc7a-146">Viene visualizzato hello seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="adc7a-146">You receive hello following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="adc7a-147">Questo messaggio indica che è possibile specificare più percorsi di input per i documenti di origine hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-147">This message indicates that you can provide several input paths for hello source documents.</span></span> <span data-ttu-id="adc7a-148">percorso finale Hello è memorizzazione dell'output di hello (conteggio delle parole nei documenti di origine hello).</span><span class="sxs-lookup"><span data-stu-id="adc7a-148">hello final path is where hello output (count of words in hello source documents) is stored.</span></span>

4. <span data-ttu-id="adc7a-149">Utilizzare hello seguente toocount tutte le parole hello notebook di Leonardo Da Vinci, che sono fornite come dati di esempio con il cluster:</span><span class="sxs-lookup"><span data-stu-id="adc7a-149">Use hello following toocount all words in hello Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="adc7a-150">L'input per questo processo viene letto da `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="adc7a-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="adc7a-151">L'output per questo esempio viene archiviato in `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="adc7a-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="adc7a-152">Entrambi i percorsi si trovano in archivio predefinito per i cluster di hello, non hello file system locale.</span><span class="sxs-lookup"><span data-stu-id="adc7a-152">Both paths are located on default storage for hello cluster, not hello local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="adc7a-153">Come indicato nella Guida di hello per esempio wordcount hello, è anche possibile specificare più file di input.</span><span class="sxs-lookup"><span data-stu-id="adc7a-153">As noted in hello help for hello wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="adc7a-154">Ad esempio, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` eseguirebbe il conteggio delle parole in davinci.txt e in ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="adc7a-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="adc7a-155">Al termine del processo di hello, utilizzare hello output hello tooview del comando seguente:</span><span class="sxs-lookup"><span data-stu-id="adc7a-155">Once hello job completes, use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="adc7a-156">Questo comando consente di concatenare tutti i file di output di hello generati dal processo hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-156">This command concatenates all hello output files produced by hello job.</span></span> <span data-ttu-id="adc7a-157">Visualizza console toohello output di hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-157">It displays hello output toohello console.</span></span> <span data-ttu-id="adc7a-158">Hello l'output è simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="adc7a-158">hello output is similar toohello following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="adc7a-159">Ogni riga rappresenta una parola e quante volte si è verificata nel hello dati di input.</span><span class="sxs-lookup"><span data-stu-id="adc7a-159">Each line represents a word and how many times it occurred in hello input data.</span></span>

## <a name="hello-sudoku-example"></a><span data-ttu-id="adc7a-160">esempio di Sudoku Hello</span><span class="sxs-lookup"><span data-stu-id="adc7a-160">hello Sudoku example</span></span>

<span data-ttu-id="adc7a-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) è un rompicapo logico composto da griglie di 9 celle in formato 3x3.</span><span class="sxs-lookup"><span data-stu-id="adc7a-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="adc7a-162">Alcune celle nella griglia hello includono numeri, mentre altri sono vuoti, con hello obiettivo toosolve per le celle vuote hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-162">Some cells in hello grid have numbers, while others are blank, and hello goal is toosolve for hello blank cells.</span></span> <span data-ttu-id="adc7a-163">collegamento precedente Hello contiene ulteriori informazioni sulla puzzle hello e scopo hello di questo esempio è toosolve per le celle vuote hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-163">hello previous link has more information on hello puzzle, but hello purpose of this sample is toosolve for hello blank cells.</span></span> <span data-ttu-id="adc7a-164">Pertanto, l'input deve essere un file in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="adc7a-164">So our input should be a file that is in hello following format:</span></span>

* <span data-ttu-id="adc7a-165">Nove righe di nove colonne.</span><span class="sxs-lookup"><span data-stu-id="adc7a-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="adc7a-166">Ogni colonna può contenere un numero o `?` (che indica una cella vuota)</span><span class="sxs-lookup"><span data-stu-id="adc7a-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="adc7a-167">Le celle sono separate da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="adc7a-167">Cells are separated by a space</span></span>

<span data-ttu-id="adc7a-168">È presente un determinato tooconstruct modo puzzle Sudoku; non è possibile ripetere un numero in una colonna o riga.</span><span class="sxs-lookup"><span data-stu-id="adc7a-168">There is a certain way tooconstruct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="adc7a-169">Ecco un esempio in cluster di HDInsight hello sia strutturato correttamente.</span><span class="sxs-lookup"><span data-stu-id="adc7a-169">There's an example on hello HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="adc7a-170">Si trova nel `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` e contiene hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="adc7a-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains hello following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="adc7a-171">Utilizzare questo problema di esempio tramite hello Sudoku esempio toorun hello il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="adc7a-171">toorun this example problem through hello Sudoku example, use hello following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="adc7a-172">risultati Hello visualizzato toohello simile, il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="adc7a-172">hello results appear similar toohello following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="adc7a-173">Esempio di pi greco (π)</span><span class="sxs-lookup"><span data-stu-id="adc7a-173">Pi (π) example</span></span>

<span data-ttu-id="adc7a-174">esempio di pi greco Hello utilizza una statistica (quasi Monte Carlo) tooestimate hello valore del metodo di pi greco.</span><span class="sxs-lookup"><span data-stu-id="adc7a-174">hello pi sample uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="adc7a-175">I punti vengono posizionati in modo casuale in un quadrato unitario.</span><span class="sxs-lookup"><span data-stu-id="adc7a-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="adc7a-176">quadrato Hello contiene inoltre un cerchio.</span><span class="sxs-lookup"><span data-stu-id="adc7a-176">hello square also contains a circle.</span></span> <span data-ttu-id="adc7a-177">probabilità che i punti di hello rientrano cerchio hello Hello sono area toohello uguale di hello circle, pi/4.</span><span class="sxs-lookup"><span data-stu-id="adc7a-177">hello probability that hello points fall within hello circle are equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="adc7a-178">il valore di Hello di pi greco può essere stimato dal valore hello 4R.</span><span class="sxs-lookup"><span data-stu-id="adc7a-178">hello value of pi can be estimated from hello value of 4R.</span></span> <span data-ttu-id="adc7a-179">R è il rapporto di hello del numero di hello di punti che si trovano all'interno di hello cerchio toohello numero totale di punti che si trovano all'interno di quadrato di hello.</span><span class="sxs-lookup"><span data-stu-id="adc7a-179">R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="adc7a-180">esempio hello di dimensioni maggiore Hello di punti utilizzati stima più accurata hello hello è.</span><span class="sxs-lookup"><span data-stu-id="adc7a-180">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="adc7a-181">Utilizzare hello comando che segue toorun in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="adc7a-181">Use hello following command toorun this sample.</span></span> <span data-ttu-id="adc7a-182">Questo comando Usa 16 mappe con 10.000.000 esempi tooestimate hello valore pi:</span><span class="sxs-lookup"><span data-stu-id="adc7a-182">This command uses 16 maps with 10,000,000 samples each tooestimate hello value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="adc7a-183">Hello valore restituito da questo comando è simile troppo**3.14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="adc7a-183">hello value returned by this command is similar too**3.14159155000000000000**.</span></span> <span data-ttu-id="adc7a-184">Per i riferimenti, hello primi 10 cifre decimali di pi greco sono 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="adc7a-184">For references, hello first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="adc7a-185">Esempio di Greysort 10 GB</span><span class="sxs-lookup"><span data-stu-id="adc7a-185">10 GB Greysort example</span></span>

<span data-ttu-id="adc7a-186">GraySort è un ordinamento benchmark.</span><span class="sxs-lookup"><span data-stu-id="adc7a-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="adc7a-187">metrica di Hello è hello ordinamento velocità (TB al minuto) il risultato viene ottenuto durante l'ordinamento di grandi quantità di dati, in genere un 100 TB minimo.</span><span class="sxs-lookup"><span data-stu-id="adc7a-187">hello metric is hello sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="adc7a-188">In questo esempio vengono usati solo 10 GB di dati, in modo da consentire un'esecuzione relativamente rapida.</span><span class="sxs-lookup"><span data-stu-id="adc7a-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="adc7a-189">Usa applicazioni MapReduce hello sviluppate da Owen O'Malley e Arun Murthy.</span><span class="sxs-lookup"><span data-stu-id="adc7a-189">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="adc7a-190">Queste applicazioni vinto benchmark ordinamento terabyte hello annuale utilizzo generale ("daytona") nel 2009, con una frequenza di 0.578 TB/min (100 TB in 173 minuti).</span><span class="sxs-lookup"><span data-stu-id="adc7a-190">These applications won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="adc7a-191">Per ulteriori informazioni su questo e altri ordinamento benchmark, vedere hello [Sortbenchmark](http://sortbenchmark.org/) sito.</span><span class="sxs-lookup"><span data-stu-id="adc7a-191">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="adc7a-192">In questo esempio vengono utilizzati tre set di programmi MapReduce:</span><span class="sxs-lookup"><span data-stu-id="adc7a-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="adc7a-193">**TeraGen**: MapReduce un programma che genera le righe di dati toosort</span><span class="sxs-lookup"><span data-stu-id="adc7a-193">**TeraGen**: A MapReduce program that generates rows of data toosort</span></span>

* <span data-ttu-id="adc7a-194">**TeraSort**: esempi di dati di input hello e utilizza i dati di hello toosort MapReduce in un ordine totale</span><span class="sxs-lookup"><span data-stu-id="adc7a-194">**TeraSort**: Samples hello input data and uses MapReduce toosort hello data into a total order</span></span>

    <span data-ttu-id="adc7a-195">TeraSort è un ordinamento standard di MapReduce, ad eccezione di un partitioner personalizzato.</span><span class="sxs-lookup"><span data-stu-id="adc7a-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="adc7a-196">partitioner Hello utilizza un elenco ordinato di chiavi di n-1 campionate che definiscono l'intervallo di chiavi hello per ogni riduzione.</span><span class="sxs-lookup"><span data-stu-id="adc7a-196">hello partitioner uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="adc7a-197">In particolare, tutte le chiavi questo tipo di esempio [i-1] < = chiave < [i] di esempio vengono inviati tooreduce i.</span><span class="sxs-lookup"><span data-stu-id="adc7a-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="adc7a-198">Questo partitioner garanzie che l'output di hello di ridurre i sono tutti minore di output di hello di ridurre i + 1.</span><span class="sxs-lookup"><span data-stu-id="adc7a-198">This partitioner guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>

* <span data-ttu-id="adc7a-199">**TeraValidate**: MapReduce un programma che convalida l'output di hello globale viene ordinato</span><span class="sxs-lookup"><span data-stu-id="adc7a-199">**TeraValidate**: A MapReduce program that validates that hello output is globally sorted</span></span>

    <span data-ttu-id="adc7a-200">Crea una mappa per ogni file nella directory di output di hello e ogni mappa garantisce che ogni chiave è minore o uguale toohello precedente.</span><span class="sxs-lookup"><span data-stu-id="adc7a-200">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="adc7a-201">funzione mappa Hello genera record di hello prima e ultima chiavi di ogni file.</span><span class="sxs-lookup"><span data-stu-id="adc7a-201">hello map function generates records of hello first and last keys of each file.</span></span> <span data-ttu-id="adc7a-202">Hello reduce (funzione) garantisce che hello prima chiave del file i è maggiore di hello chiave ultimo di i-1 file.</span><span class="sxs-lookup"><span data-stu-id="adc7a-202">hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="adc7a-203">Eventuali problemi vengono segnalati come un output di hello ridurre fase, con chiavi hello che non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="adc7a-203">Any problems are reported as an output of hello reduce phase, with hello keys that are out of order.</span></span>

<span data-ttu-id="adc7a-204">Utilizzare hello seguenti passaggi viene toogenerate dati, ordinare e quindi convalidare l'output di hello:</span><span class="sxs-lookup"><span data-stu-id="adc7a-204">Use hello following steps toogenerate data, sort, and then validate hello output:</span></span>

1. <span data-ttu-id="adc7a-205">Generare 10 GB di dati, ovvero l'archivio predefinito del cluster HDInsight toohello stored in `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="adc7a-205">Generate 10 GB of data, which is stored toohello HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="adc7a-206">Hello `-Dmapred.map.tasks` indica quanti toouse di attività di mapping per questo processo di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="adc7a-206">hello `-Dmapred.map.tasks` tells Hadoop how many map tasks toouse for this job.</span></span> <span data-ttu-id="adc7a-207">i parametri di Hello finale indicano hello processo toocreate 10 GB di dati e toostore in `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="adc7a-207">hello final two parameters instruct hello job toocreate 10 GB of data and toostore it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="adc7a-208">Utilizzare hello comando toosort hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="adc7a-208">Use hello following command toosort hello data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="adc7a-209">Hello `-Dmapred.reduce.tasks` indica Hadoop toouse di attività per processo hello di ridurre il numero.</span><span class="sxs-lookup"><span data-stu-id="adc7a-209">hello `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks toouse for hello job.</span></span> <span data-ttu-id="adc7a-210">parametri di Hello finale sono hello solo input e output percorsi per i dati.</span><span class="sxs-lookup"><span data-stu-id="adc7a-210">hello final two parameters are just hello input and output locations for data.</span></span>

3. <span data-ttu-id="adc7a-211">Utilizzare hello toovalidate hello dati generati dall'ordinamento hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="adc7a-211">Use hello following toovalidate hello data generated by hello sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="adc7a-212">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="adc7a-212">Next steps</span></span>

<span data-ttu-id="adc7a-213">In questo articolo, si è appreso come esempi hello toorun incluso hello cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="adc7a-213">From this article, you learned how toorun hello samples included with hello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="adc7a-214">Per le esercitazioni sull'uso Pig, Hive e MapReduce con HDInsight, vedere hello seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="adc7a-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="adc7a-215">[Usare Pig con Hadoop in HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="adc7a-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="adc7a-216">[Usare Hive con Hadoop in HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="adc7a-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="adc7a-217">[Usare MapReduce con Hadoop in HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="adc7a-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
