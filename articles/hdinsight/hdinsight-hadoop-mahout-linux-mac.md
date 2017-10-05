---
title: Generare raccomandazioni con Mahout e HDInsight (SSH) - Azure | Documentazione Microsoft
description: Informazioni su come usare la libreria di Machine Learning Apache Mahout per generare raccomandazioni di film con HDInsight (Hadoop).
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c78ec37c-9a8c-4bb6-9e38-0bdb9e89fbd7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 28450d72f19a5467d88bc787d11f6c37c5afbf9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="05b85-103">Generare raccomandazioni di film tramite Apache Mahout con Hadoop basato su Linux in HDInsight (SSH)</span><span class="sxs-lookup"><span data-stu-id="05b85-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="05b85-104">Informazioni su come usare la libreria di Machine Learning [Apache Mahout](http://mahout.apache.org) con Azure HDInsight per generare raccomandazioni di film.</span><span class="sxs-lookup"><span data-stu-id="05b85-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span>

<span data-ttu-id="05b85-105">Mahout è una libreria di [apprendimento automatico][ml] per Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="05b85-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="05b85-106">Mahout contiene gli algoritmi per l'elaborazione dei dati, ad esempio applicazione di filtri, classificazione e clustering.</span><span class="sxs-lookup"><span data-stu-id="05b85-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="05b85-107">In questo articolo si userà un motore di raccomandazione per generare consigli cinematografici in base ai film visti dai propri amici.</span><span class="sxs-lookup"><span data-stu-id="05b85-107">In this article, you use a recommendation engine to generate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05b85-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="05b85-108">Prerequisites</span></span>

* <span data-ttu-id="05b85-109">Un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="05b85-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="05b85-110">Per informazioni su come crearne uno, vedere [Introduzione all'uso di Hadoop basato su Linux in HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="05b85-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05b85-111">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="05b85-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="05b85-112">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="05b85-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="05b85-113">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="05b85-113">An SSH client.</span></span> <span data-ttu-id="05b85-114">Per altre informazioni, vedere il documento [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="05b85-114">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="05b85-115">Controllo delle versioni di Mahout</span><span class="sxs-lookup"><span data-stu-id="05b85-115">Mahout versioning</span></span>

<span data-ttu-id="05b85-116">Per altre informazioni sulla versione di Mahout in HDInsight, vedere l'articolo relativo a [versioni di HDInsight e componenti di Hadoop](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="05b85-116">For more information about the version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="05b85-117"><a name="recommendations"></a>Informazioni sulle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="05b85-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="05b85-118">Una delle funzioni fornite da Mahout è un motore di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="05b85-118">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="05b85-119">Questo motore accetta i dati nei formati `userID`, `itemId` e `prefValue` (la preferenza per l'elemento).</span><span class="sxs-lookup"><span data-stu-id="05b85-119">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the preference for the item).</span></span> <span data-ttu-id="05b85-120">Mahout può quindi eseguire l'analisi delle co-occorrenze per determinare che gli *utenti con una preferenza per un elemento hanno anche una preferenza per altri elementi*.</span><span class="sxs-lookup"><span data-stu-id="05b85-120">Mahout can then perform co-occurance analysis to determine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="05b85-121">Mahout determina quindi gli utenti con preferenze di elementi simili, che possono essere usate per le raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="05b85-121">Mahout then determines users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="05b85-122">Il flusso di lavoro seguente costituisce un esempio semplificato che usa dati relativi ai film:</span><span class="sxs-lookup"><span data-stu-id="05b85-122">The following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="05b85-123">**Co-occorrenza**: a Joe, Alice e Bob piacciono *Guerre stellari*, *L'Impero colpisce ancora* e *Il ritorno dello Jedi*.</span><span class="sxs-lookup"><span data-stu-id="05b85-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="05b85-124">Mahout determina che agli utenti a cui piace uno di questi film piacciono anche gli altri due.</span><span class="sxs-lookup"><span data-stu-id="05b85-124">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="05b85-125">**Co-occorrenza**: a Bob e Alice piacciono anche *La minaccia fantasma*, *L'attacco dei cloni* e *La vendetta dei Sith*.</span><span class="sxs-lookup"><span data-stu-id="05b85-125">**Co-occurance**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="05b85-126">Mahout determina che agli utenti a cui piacciono i tre film precedenti piacciono anche questi tre.</span><span class="sxs-lookup"><span data-stu-id="05b85-126">Mahout determines that users who liked the previous three movies also like these three movies.</span></span>

* <span data-ttu-id="05b85-127">**Raccomandazione per somiglianza**: poiché a Joe piacciono i primi tre film, Mahout cerca i film che piacciono ad altri utenti con preferenze simili ma che Joe non ha guardato o per i quali non ha ancora espresso una preferenza o una valutazione.</span><span class="sxs-lookup"><span data-stu-id="05b85-127">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="05b85-128">In questo caso, Mahout raccomanda *La minaccia fantasma*, *L'attacco dei cloni* e *La vendetta dei Sith*.</span><span class="sxs-lookup"><span data-stu-id="05b85-128">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="05b85-129">Informazioni sui dati</span><span class="sxs-lookup"><span data-stu-id="05b85-129">Understanding the data</span></span>

<span data-ttu-id="05b85-130">[GroupLens Research][movielens] fornisce i dati di classificazione dei film in un formato compatibile con Mahout.</span><span class="sxs-lookup"><span data-stu-id="05b85-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="05b85-131">Questi dati sono disponibili nello spazio di archiviazione predefinito del cluster in `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="05b85-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="05b85-132">Sono disponibili due file: `moviedb.txt` e `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="05b85-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="05b85-133">Il file user-ratings.txt viene usato durante l'analisi, mentre moviedb.txt viene usato per offrire informazioni di testo descrittive quando si visualizzano i risultati dell'analisi.</span><span class="sxs-lookup"><span data-stu-id="05b85-133">The user-ratings.txt file is used during analysis, while moviedb.txt is used to provide user-friendly text information when displaying the results of the analysis.</span></span>

<span data-ttu-id="05b85-134">I dati contenuti in user-ratings.txt presentano una struttura `userID`, `movieID`, `userRating` e `timestamp` che indica come ogni utente ha classificato un film.</span><span class="sxs-lookup"><span data-stu-id="05b85-134">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="05b85-135">Di seguito è riportato un esempio dei dati:</span><span class="sxs-lookup"><span data-stu-id="05b85-135">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-the-analysis"></a><span data-ttu-id="05b85-136">Eseguire l'analisi</span><span class="sxs-lookup"><span data-stu-id="05b85-136">Run the analysis</span></span>

<span data-ttu-id="05b85-137">Da una connessione SSH al cluster usare questi comandi per eseguire il processo di raccomandazione:</span><span class="sxs-lookup"><span data-stu-id="05b85-137">From an SSH connection to the cluster, use the following command to run the recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="05b85-138">Il completamento del processo potrebbe richiedere alcuni minuti ed è possibile eseguire più processi MapReduce.</span><span class="sxs-lookup"><span data-stu-id="05b85-138">The job may take several minutes to complete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-the-output"></a><span data-ttu-id="05b85-139">Visualizzare l'output</span><span class="sxs-lookup"><span data-stu-id="05b85-139">View the output</span></span>

1. <span data-ttu-id="05b85-140">Una volta completato il processo, usare il seguente comando per visualizzare l'output generato:</span><span class="sxs-lookup"><span data-stu-id="05b85-140">Once the job completes, use the following command to view the generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="05b85-141">L'output viene visualizzato come segue:</span><span class="sxs-lookup"><span data-stu-id="05b85-141">The output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="05b85-142">La prima colonna rappresenta il valore `userID`.</span><span class="sxs-lookup"><span data-stu-id="05b85-142">The first column is the `userID`.</span></span> <span data-ttu-id="05b85-143">I valori racchiusi tra "[" e "]" sono `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="05b85-143">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="05b85-144">È possibile usare l'output, insieme a moviedb.txt, per fornire altre informazioni sulle raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="05b85-144">You can use the output, along with the moviedb.txt, to provide more information on the recommendations.</span></span> <span data-ttu-id="05b85-145">È necessario innanzitutto copiare i file localmente usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="05b85-145">First, we need to copy the files locally using the following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="05b85-146">I dati di output vengono copiati da questo comando in un file denominato **recommendations.txt** nella directory corrente insieme ai file dei dati relativi ai film.</span><span class="sxs-lookup"><span data-stu-id="05b85-146">This command copies the output data to a file named **recommendations.txt** in the current directory, along with the movie data files.</span></span>

3. <span data-ttu-id="05b85-147">Usare il comando seguente per creare uno script Python che cerca i nomi dei film per i dati presenti nell'output delle raccomandazioni:</span><span class="sxs-lookup"><span data-stu-id="05b85-147">Use the following command to create a Python script that looks up movie names for the data in the recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="05b85-148">All'apertura dell'editor usare il testo seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="05b85-148">When the editor opens, use the following text as the contents of the file:</span></span>

   ```python
   #!/usr/bin/env python

   import sys

   if len(sys.argv) != 5:
        print "Arguments: userId userDataFilename movieFilename recommendationFilename"
        sys.exit(1)

   userId, userDataFilename, movieFilename, recommendationFilename = sys.argv[1:]

   print "Reading Movies Descriptions"
   movieFile = open(movieFilename)
   movieById = {}
   for line in movieFile:
       tokens = line.split("|")
       movieById[tokens[0]] = tokens[1:]
   movieFile.close()

   print "Reading Rated Movies"
   userDataFile = open(userDataFilename)
   ratedMovieIds = []
   for line in userDataFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           ratedMovieIds.append((tokens[1],tokens[2]))
   userDataFile.close()

   print "Reading Recommendations"
   recommendationFile = open(recommendationFilename)
   recommendations = []
   for line in recommendationFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           movieIdAndScores = tokens[1].strip("[]\n").split(",")
           recommendations = [ movieIdAndScore.split(":") for movieIdAndScore in movieIdAndScores ]
           break
   recommendationFile.close()

   print "Rated Movies"
   print "------------------------"
   for movieId, rating in ratedMovieIds:
       print "%s, rating=%s" % (movieById[movieId][0], rating)
   print "------------------------"

   print "Recommended Movies"
   print "------------------------"
   for movieId, score in recommendations:
       print "%s, score=%s" % (movieById[movieId][0], score)
   print "------------------------"
   ```

    <span data-ttu-id="05b85-149">Premere **CTRL-X**, **Y** e infine **INVIO** per salvare i dati.</span><span class="sxs-lookup"><span data-stu-id="05b85-149">Press **Ctrl-X**, **Y**, and finally **Enter** to save the data.</span></span>

4. <span data-ttu-id="05b85-150">Eseguire lo script Python.</span><span class="sxs-lookup"><span data-stu-id="05b85-150">Run the Python script.</span></span> <span data-ttu-id="05b85-151">Il comando seguente presuppone che l'utente si trovi nella directory in cui sono stati scaricati tutti i file:</span><span class="sxs-lookup"><span data-stu-id="05b85-151">The following command assumes you are in the directory where all the files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="05b85-152">Questo comando esamina le raccomandazioni generate per l'ID utente 4.</span><span class="sxs-lookup"><span data-stu-id="05b85-152">This command looks at the recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="05b85-153">Il file **user-ratings.txt** viene usato per recuperare i film che sono stati classificati.</span><span class="sxs-lookup"><span data-stu-id="05b85-153">The **user-ratings.txt** file is used to retrieve movies that have been rated.</span></span>

    * <span data-ttu-id="05b85-154">Il file **moviedb.txt** viene usato per recuperare i nomi dei film.</span><span class="sxs-lookup"><span data-stu-id="05b85-154">The **moviedb.txt** file is used to retrieve the names of the movies.</span></span>

    * <span data-ttu-id="05b85-155">Il file **recommendations.txt** viene usato per recuperare le raccomandazioni di film per questo utente.</span><span class="sxs-lookup"><span data-stu-id="05b85-155">The **recommendations.txt** is used to retrieve the movie recommendations for this user.</span></span>

     <span data-ttu-id="05b85-156">L'output di questo comando è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="05b85-156">The output from this command is similar to the following text:</span></span>

        <span data-ttu-id="05b85-157">Sette anni in Tibet (1997), punteggio = 5.0   Indiana Jones e l'ultima crociata (1989), punteggio = 5.0   Lo squalo (1975), punteggio = 5.0   Ragione e sentimento (1995), punteggio = 5.0 Independence Day (ID4) (1996), punteggio = 5.0   Il matrimonio del mio migliore amico (1997), punteggio = 5.0   Jerry Maguire (1996), punteggio = 5.0   Scream 2 (1997), punteggio = 5.0   Il momento di uccidere (1996), punteggio = 5.0</span><span class="sxs-lookup"><span data-stu-id="05b85-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="05b85-158">Eliminare i dati temporanei</span><span class="sxs-lookup"><span data-stu-id="05b85-158">Delete temporary data</span></span>

<span data-ttu-id="05b85-159">I processi Mahout non rimuovono i dati temporanei creati durante l'elaborazione del processo.</span><span class="sxs-lookup"><span data-stu-id="05b85-159">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="05b85-160">Nel processo di esempio è specificato il parametro `--tempDir` per isolare i file temporanei in un percorso specifico per semplificarne l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="05b85-160">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="05b85-161">Per rimuovere i file temporanei, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="05b85-161">To remove the temp files, use the following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="05b85-162">Se si vuole eseguire nuovamente il comando, è inoltre necessario eliminare la directory di output.</span><span class="sxs-lookup"><span data-stu-id="05b85-162">If you want to run the command again, you must also delete the output directory.</span></span> <span data-ttu-id="05b85-163">Per eliminare la directory, usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="05b85-163">Use the following to delete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="05b85-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="05b85-164">Next steps</span></span>

<span data-ttu-id="05b85-165">A questo punto, dopo aver appreso come usare Mahout, trovare altri modi per usare i dati in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="05b85-165">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="05b85-166">Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="05b85-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="05b85-167">Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="05b85-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="05b85-168">MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="05b85-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
