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
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a>Eseguire hello MapReduce esempi inclusi in HDInsight

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Informazioni su come esempi di MapReduce hello toorun incluso con Hadoop in HDInsight.

## <a name="prerequisites"></a>Prerequisiti

* **Un cluster HDInsight**: vedere [Introduzione all'uso di Hadoop con Hive in HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

    > [!IMPORTANT]
    > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Un client SSH**: per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="hello-mapreduce-examples"></a>esempi di Hello MapReduce

**Percorso**: hello esempi si troveranno nel cluster HDInsight in hello `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.

**Contenuto**: hello seguendo gli esempi contenuto in questo archivio:

* `aggregatewordcount`: Un'aggregazione basata programma mapreduce che conta hello parole nei file di input hello.
* `aggregatewordhist`: Un'aggregazione basata programma mapreduce che calcola l'istogramma hello di parole hello nei file di input hello.
* `bbp`: Un programma mapreduce che utilizza Bailey-Borwein-Plouffe toocompute di cifre esatte di pi greco.
* `dbcount`: Un processo di esempio che conta registri pageview hello archiviati in un database.
* `distbbp`: Un programma mapreduce che utilizza un bit di esatta toocompute formula BBP-tipo di pi greco.
* `grep`: Un programma mapreduce che conta hello trova la corrispondenza di un'espressione regolare in input hello.
* `join`: processo che esegue un join su set di dati ordinati ed equamente partizionati.
* `multifilewc`: processo che conta le parole da più file.
* `pentomino`: Un riquadro mapreduce layout soluzioni toofind programma toopentomino problemi.
* `pi`: programma MapReduce che stima il pi greco usando un metodo simile al metodo Monte Carlo.
* `randomtextwriter`: programma MapReduce che scrive 10 GB di dati testuali casuali per nodo.
* `randomwriter`: programma MapReduce che scrive 10 GB di dati casuali per nodo.
* `secondarysort`: Un esempio di definizione toohello un ordinamento secondario ridurre fase.
* `sort`: Un programma mapreduce che ordina i dati di hello scritti dal writer di hello casuale.
* `sudoku`: risolutore di sudoku.
* `teragen`: Generare dati per terasort hello.
* `terasort`: Eseguire terasort hello.
* `teravalidate`: verifica i risultati di terasort.
* `wordcount`: File di input un programma mapreduce che conta le parole hello in hello.
* `wordmean`: File di input un programma mapreduce che conta lunghezza media di hello delle parole hello hello.
* `wordmedian`: File di input un programma mapreduce che conta hello mediano lunghezza parole hello hello.
* `wordstandarddeviation`: File di input un programma mapreduce che conta hello di deviazione standard di lunghezza hello parole hello hello.

**Codice sorgente**: il codice sorgente per questi esempi è incluso nel cluster HDInsight in hello `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.

> [!NOTE]
> Hello `2.2.4.9-1` in hello hello versione di hello Hortonworks Data Platform per il cluster HDInsight hello, percorso e può essere diverso per il cluster.

## <a name="run-hello-wordcount-example"></a>Eseguire l'esempio wordcount hello

1. Connettersi tramite SSH tooHDInsight. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Da hello `username@#######:~$` richiesta, utilizzare i seguenti esempi di comando toolist hello hello:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    Questo comando Genera elenco hello di esempio dalla sezione precedente di hello di questo documento.

3. Seguente hello utilizzare il comando tooget su un campione specifico. In questo caso, hello **wordcount** esempio:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    Viene visualizzato hello seguente messaggio:

        Usage: wordcount <in> [<in>...] <out>

    Questo messaggio indica che è possibile specificare più percorsi di input per i documenti di origine hello. percorso finale Hello è memorizzazione dell'output di hello (conteggio delle parole nei documenti di origine hello).

4. Utilizzare hello seguente toocount tutte le parole hello notebook di Leonardo Da Vinci, che sono fornite come dati di esempio con il cluster:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    L'input per questo processo viene letto da `/example/data/gutenberg/davinci.txt`. L'output per questo esempio viene archiviato in `/example/data/davinciwordcount`. Entrambi i percorsi si trovano in archivio predefinito per i cluster di hello, non hello file system locale.

   > [!NOTE]
   > Come indicato nella Guida di hello per esempio wordcount hello, è anche possibile specificare più file di input. Ad esempio, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` eseguirebbe il conteggio delle parole in davinci.txt e in ulysses.txt.

5. Al termine del processo di hello, utilizzare hello output hello tooview del comando seguente:

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    Questo comando consente di concatenare tutti i file di output di hello generati dal processo hello. Visualizza console toohello output di hello. Hello l'output è simile toohello seguente testo:

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    Ogni riga rappresenta una parola e quante volte si è verificata nel hello dati di input.

## <a name="hello-sudoku-example"></a>esempio di Sudoku Hello

[Sudoku](https://en.wikipedia.org/wiki/Sudoku) è un rompicapo logico composto da griglie di 9 celle in formato 3x3. Alcune celle nella griglia hello includono numeri, mentre altri sono vuoti, con hello obiettivo toosolve per le celle vuote hello. collegamento precedente Hello contiene ulteriori informazioni sulla puzzle hello e scopo hello di questo esempio è toosolve per le celle vuote hello. Pertanto, l'input deve essere un file in hello seguente formato:

* Nove righe di nove colonne.
* Ogni colonna può contenere un numero o `?` (che indica una cella vuota)
* Le celle sono separate da uno spazio.

È presente un determinato tooconstruct modo puzzle Sudoku; non è possibile ripetere un numero in una colonna o riga. Ecco un esempio in cluster di HDInsight hello sia strutturato correttamente. Si trova nel `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` e contiene hello seguente testo:

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

Utilizzare questo problema di esempio tramite hello Sudoku esempio toorun hello il seguente comando:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

risultati Hello visualizzato toohello simile, il testo seguente:

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a>Esempio di pi greco (π)

esempio di pi greco Hello utilizza una statistica (quasi Monte Carlo) tooestimate hello valore del metodo di pi greco. I punti vengono posizionati in modo casuale in un quadrato unitario. quadrato Hello contiene inoltre un cerchio. probabilità che i punti di hello rientrano cerchio hello Hello sono area toohello uguale di hello circle, pi/4. il valore di Hello di pi greco può essere stimato dal valore hello 4R. R è il rapporto di hello del numero di hello di punti che si trovano all'interno di hello cerchio toohello numero totale di punti che si trovano all'interno di quadrato di hello. esempio hello di dimensioni maggiore Hello di punti utilizzati stima più accurata hello hello è.

Utilizzare hello comando che segue toorun in questo esempio. Questo comando Usa 16 mappe con 10.000.000 esempi tooestimate hello valore pi:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

Hello valore restituito da questo comando è simile troppo**3.14159155000000000000**. Per i riferimenti, hello primi 10 cifre decimali di pi greco sono 3.1415926535.

## <a name="10-gb-greysort-example"></a>Esempio di Greysort 10 GB

GraySort è un ordinamento benchmark. metrica di Hello è hello ordinamento velocità (TB al minuto) il risultato viene ottenuto durante l'ordinamento di grandi quantità di dati, in genere un 100 TB minimo.

In questo esempio vengono usati solo 10 GB di dati, in modo da consentire un'esecuzione relativamente rapida. Usa applicazioni MapReduce hello sviluppate da Owen O'Malley e Arun Murthy. Queste applicazioni vinto benchmark ordinamento terabyte hello annuale utilizzo generale ("daytona") nel 2009, con una frequenza di 0.578 TB/min (100 TB in 173 minuti). Per ulteriori informazioni su questo e altri ordinamento benchmark, vedere hello [Sortbenchmark](http://sortbenchmark.org/) sito.

In questo esempio vengono utilizzati tre set di programmi MapReduce:

* **TeraGen**: MapReduce un programma che genera le righe di dati toosort

* **TeraSort**: esempi di dati di input hello e utilizza i dati di hello toosort MapReduce in un ordine totale

    TeraSort è un ordinamento standard di MapReduce, ad eccezione di un partitioner personalizzato. partitioner Hello utilizza un elenco ordinato di chiavi di n-1 campionate che definiscono l'intervallo di chiavi hello per ogni riduzione. In particolare, tutte le chiavi questo tipo di esempio [i-1] < = chiave < [i] di esempio vengono inviati tooreduce i. Questo partitioner garanzie che l'output di hello di ridurre i sono tutti minore di output di hello di ridurre i + 1.

* **TeraValidate**: MapReduce un programma che convalida l'output di hello globale viene ordinato

    Crea una mappa per ogni file nella directory di output di hello e ogni mappa garantisce che ogni chiave è minore o uguale toohello precedente. funzione mappa Hello genera record di hello prima e ultima chiavi di ogni file. Hello reduce (funzione) garantisce che hello prima chiave del file i è maggiore di hello chiave ultimo di i-1 file. Eventuali problemi vengono segnalati come un output di hello ridurre fase, con chiavi hello che non sono disponibili.

Utilizzare hello seguenti passaggi viene toogenerate dati, ordinare e quindi convalidare l'output di hello:

1. Generare 10 GB di dati, ovvero l'archivio predefinito del cluster HDInsight toohello stored in `/example/data/10GB-sort-input`:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    Hello `-Dmapred.map.tasks` indica quanti toouse di attività di mapping per questo processo di Hadoop. i parametri di Hello finale indicano hello processo toocreate 10 GB di dati e toostore in `/example/data/10GB-sort-input`.

2. Utilizzare hello comando toosort hello dati seguenti:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    Hello `-Dmapred.reduce.tasks` indica Hadoop toouse di attività per processo hello di ridurre il numero. parametri di Hello finale sono hello solo input e output percorsi per i dati.

3. Utilizzare hello toovalidate hello dati generati dall'ordinamento hello seguenti:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a>Passaggi successivi

In questo articolo, si è appreso come esempi hello toorun incluso hello cluster HDInsight basati su Linux. Per le esercitazioni sull'uso Pig, Hive e MapReduce con HDInsight, vedere hello seguenti argomenti:

* [Usare Pig con Hadoop in HDInsight][hdinsight-use-pig]
* [Usare Hive con Hadoop in HDInsight][hdinsight-use-hive]
* [Usare MapReduce con Hadoop in HDInsight][hdinsight-use-mapreduce]

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
