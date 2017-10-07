---
title: indicazioni aaaGenerate utilizzando Mahout e HDInsight (SSH) - Azure | Documenti Microsoft
description: Informazioni su come toouse hello Apache Mahout di machine learning indicazioni di film libreria toogenerate con HDInsight (Hadoop).
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
ms.openlocfilehash: fedac9ceb4268f8421bce4623a5ad271041b8b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="b9900-103">Generare raccomandazioni di film tramite Apache Mahout con Hadoop basato su Linux in HDInsight (SSH)</span><span class="sxs-lookup"><span data-stu-id="b9900-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="b9900-104">Informazioni su come hello toouse [Mahout Apache](http://mahout.apache.org) libreria learning macchina con le raccomandazioni di Azure HDInsight toogenerate film.</span><span class="sxs-lookup"><span data-stu-id="b9900-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span>

<span data-ttu-id="b9900-105">Mahout è una libreria di [apprendimento automatico][ml] per Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b9900-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="b9900-106">Mahout contiene gli algoritmi per l'elaborazione dei dati, ad esempio applicazione di filtri, classificazione e clustering.</span><span class="sxs-lookup"><span data-stu-id="b9900-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="b9900-107">In questo articolo, si utilizzano una raccomandazione motore toogenerate film raccomandazioni basate su filmati sono visualizzati i tuoi amici.</span><span class="sxs-lookup"><span data-stu-id="b9900-107">In this article, you use a recommendation engine toogenerate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9900-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b9900-108">Prerequisites</span></span>

* <span data-ttu-id="b9900-109">Un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="b9900-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="b9900-110">Per informazioni su come crearne uno, vedere [Introduzione all'uso di Hadoop basato su Linux in HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="b9900-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9900-111">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="b9900-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b9900-112">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b9900-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="b9900-113">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="b9900-113">An SSH client.</span></span> <span data-ttu-id="b9900-114">Per ulteriori informazioni, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="b9900-114">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="b9900-115">Controllo delle versioni di Mahout</span><span class="sxs-lookup"><span data-stu-id="b9900-115">Mahout versioning</span></span>

<span data-ttu-id="b9900-116">Per ulteriori informazioni sulla versione di hello di Mahout in HDInsight, vedere [HDInsight versioni e i componenti di Hadoop](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b9900-116">For more information about hello version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="b9900-117"><a name="recommendations"></a>Informazioni sulle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="b9900-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="b9900-118">Una delle funzioni hello fornito da Mahout è un motore di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="b9900-118">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="b9900-119">Questo motore accetta i dati in formato hello `userID`, `itemId`, e `prefValue` (hello preferenza per l'elemento hello).</span><span class="sxs-lookup"><span data-stu-id="b9900-119">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello preference for hello item).</span></span> <span data-ttu-id="b9900-120">Mahout può quindi eseguire CO-occorrenza analisi toodetermine: *gli utenti che dispongono di una preferenza per un elemento hanno anche una preferenza per questi altri elementi*.</span><span class="sxs-lookup"><span data-stu-id="b9900-120">Mahout can then perform co-occurance analysis toodetermine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="b9900-121">Mahout determina quindi gli utenti con preferenze simili-item, che possono essere utilizzato toomake indicazioni.</span><span class="sxs-lookup"><span data-stu-id="b9900-121">Mahout then determines users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="b9900-122">Hello seguente flusso di lavoro è un esempio semplificato che utilizza dati film:</span><span class="sxs-lookup"><span data-stu-id="b9900-122">hello following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="b9900-123">**CO-occorrenza**: Joe, Alice e Bob tutti stato apprezzato *stella attraverso*, *hello Empire colpisce nuovamente*, e *restituzione di hello Jedi*.</span><span class="sxs-lookup"><span data-stu-id="b9900-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="b9900-124">Mahout determina che gli utenti come uno di questi film anche hello altri due.</span><span class="sxs-lookup"><span data-stu-id="b9900-124">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="b9900-125">**CO-occorrenza**: Bob e Alice anche ritengono *hello Phantom alieni*, *attacco dei cloni di hello*, e *ritorsioni di hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="b9900-125">**Co-occurance**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="b9900-126">Mahout determina che gli utenti che ritengono tre filmati precedente hello anche come questi tre film.</span><span class="sxs-lookup"><span data-stu-id="b9900-126">Mahout determines that users who liked hello previous three movies also like these three movies.</span></span>

* <span data-ttu-id="b9900-127">**Indicazione di somiglianza**: Joe perché ritengono hello primi tre film, Mahout esamina filmati che altri utenti con preferenze simili ritengono, ma Joe ha non controllata (ritengono/classificazione).</span><span class="sxs-lookup"><span data-stu-id="b9900-127">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="b9900-128">In questo caso, si consiglia Mahout *hello Phantom alieni*, *attacco dei cloni di hello*, e *ritorsioni di hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="b9900-128">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="b9900-129">Informazioni sui dati hello</span><span class="sxs-lookup"><span data-stu-id="b9900-129">Understanding hello data</span></span>

<span data-ttu-id="b9900-130">[GroupLens Research][movielens] fornisce i dati di classificazione dei film in un formato compatibile con Mahout.</span><span class="sxs-lookup"><span data-stu-id="b9900-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="b9900-131">Questi dati sono disponibili nello spazio di archiviazione predefinito del cluster in `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="b9900-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="b9900-132">Sono disponibili due file: `moviedb.txt` e `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="b9900-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="b9900-133">file utente ratings.txt Hello viene utilizzato durante l'analisi, mentre moviedb.txt è tooprovide utilizzato testo descrittivo informazioni quando si visualizzano i risultati di hello dell'analisi hello.</span><span class="sxs-lookup"><span data-stu-id="b9900-133">hello user-ratings.txt file is used during analysis, while moviedb.txt is used tooprovide user-friendly text information when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="b9900-134">dati contenuti in utente ratings.txt Hello presenta una struttura di `userID`, `movieID`, `userRating`, e `timestamp`, che indica come elevata ogni utente classificato un filmato.</span><span class="sxs-lookup"><span data-stu-id="b9900-134">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="b9900-135">Di seguito è riportato un esempio di dati hello:</span><span class="sxs-lookup"><span data-stu-id="b9900-135">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a><span data-ttu-id="b9900-136">Eseguire l'analisi di hello</span><span class="sxs-lookup"><span data-stu-id="b9900-136">Run hello analysis</span></span>

<span data-ttu-id="b9900-137">Da un cluster di toohello connessione SSH, utilizzare hello processo raccomandazione hello toorun di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b9900-137">From an SSH connection toohello cluster, use hello following command toorun hello recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="b9900-138">Hello processo potrebbe richiedere diversi minuti toocomplete e possono essere eseguite più processi di MapReduce.</span><span class="sxs-lookup"><span data-stu-id="b9900-138">hello job may take several minutes toocomplete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-hello-output"></a><span data-ttu-id="b9900-139">Visualizzazione output di hello</span><span class="sxs-lookup"><span data-stu-id="b9900-139">View hello output</span></span>

1. <span data-ttu-id="b9900-140">Al termine del processo di hello, hello utilizzo successivo comando tooview hello ha generato l'output:</span><span class="sxs-lookup"><span data-stu-id="b9900-140">Once hello job completes, use hello following command tooview hello generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="b9900-141">output di Hello viene visualizzato come segue:</span><span class="sxs-lookup"><span data-stu-id="b9900-141">hello output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="b9900-142">prima colonna Hello è hello `userID`.</span><span class="sxs-lookup"><span data-stu-id="b9900-142">hello first column is hello `userID`.</span></span> <span data-ttu-id="b9900-143">Hello valori contenuti in ' [' e ']' sono `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="b9900-143">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="b9900-144">È possibile utilizzare un output di hello, insieme a hello moviedb.txt, tooprovide ulteriori informazioni sui suggerimenti di hello.</span><span class="sxs-lookup"><span data-stu-id="b9900-144">You can use hello output, along with hello moviedb.txt, tooprovide more information on hello recommendations.</span></span> <span data-ttu-id="b9900-145">Innanzitutto, è necessario il file di hello toocopy localmente utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="b9900-145">First, we need toocopy hello files locally using hello following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="b9900-146">Questo comando copia hello file tooa dati di output denominata **recommendations.txt** nella directory corrente hello, insieme ai file di dati di hello film.</span><span class="sxs-lookup"><span data-stu-id="b9900-146">This command copies hello output data tooa file named **recommendations.txt** in hello current directory, along with hello movie data files.</span></span>

3. <span data-ttu-id="b9900-147">Utilizzare hello toocreate comando script Python che cerca i nomi di film per i dati di hello nell'output di hello indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9900-147">Use hello following command toocreate a Python script that looks up movie names for hello data in hello recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="b9900-148">Quando si apre l'editor di hello, utilizzare hello segue testo come contenuto di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="b9900-148">When hello editor opens, use hello following text as hello contents of hello file:</span></span>

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

    <span data-ttu-id="b9900-149">Premere **Ctrl + X**, **Y**e infine **invio** dati hello toosave.</span><span class="sxs-lookup"><span data-stu-id="b9900-149">Press **Ctrl-X**, **Y**, and finally **Enter** toosave hello data.</span></span>

4. <span data-ttu-id="b9900-150">Eseguire script Python hello.</span><span class="sxs-lookup"><span data-stu-id="b9900-150">Run hello Python script.</span></span> <span data-ttu-id="b9900-151">Hello comando riportato di seguito si presuppone che trovano nella directory hello in cui sono stati scaricati tutti i file hello:</span><span class="sxs-lookup"><span data-stu-id="b9900-151">hello following command assumes you are in hello directory where all hello files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="b9900-152">Questo comando vengono esaminati indicazioni hello generati per l'utente ID 4.</span><span class="sxs-lookup"><span data-stu-id="b9900-152">This command looks at hello recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="b9900-153">Hello **utente ratings.txt** file è utilizzato tooretrieve filmati che sono stati classificati.</span><span class="sxs-lookup"><span data-stu-id="b9900-153">hello **user-ratings.txt** file is used tooretrieve movies that have been rated.</span></span>

    * <span data-ttu-id="b9900-154">Hello **moviedb.txt** file è utilizzato tooretrieve hello nomi di film hello.</span><span class="sxs-lookup"><span data-stu-id="b9900-154">hello **moviedb.txt** file is used tooretrieve hello names of hello movies.</span></span>

    * <span data-ttu-id="b9900-155">Hello **recommendations.txt** è usato tooretrieve indicazioni film hello per questo utente.</span><span class="sxs-lookup"><span data-stu-id="b9900-155">hello **recommendations.txt** is used tooretrieve hello movie recommendations for this user.</span></span>

     <span data-ttu-id="b9900-156">Hello l'output di questo comando è simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="b9900-156">hello output from this command is similar toohello following text:</span></span>

        <span data-ttu-id="b9900-157">Periodo di 7 anni Tibet (1997), assegnare un punteggio = 5.0 Indiana Jones e hello Crusade ultimo (1989), assegnare un punteggio = 5.0 Jaws (1975), punteggio = 5.0 senso e Sensibility (1995), punteggio = 5.0 indipendenza giorno (ID4) (1996), punteggio = 5.0 il migliore amico matrimoni (1997), assegnare un punteggio = 5.0 Jerry Maguire (1996 ), punteggio = 5.0 Scream 2 (1997), punteggio = 5.0 tooKill ora, (1996), assegnare un punteggio = 5.0</span><span class="sxs-lookup"><span data-stu-id="b9900-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and hello Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time tooKill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="b9900-158">Eliminare i dati temporanei</span><span class="sxs-lookup"><span data-stu-id="b9900-158">Delete temporary data</span></span>

<span data-ttu-id="b9900-159">I processi di mahout non rimuovere i dati temporanei creati durante l'elaborazione di processi di hello.</span><span class="sxs-lookup"><span data-stu-id="b9900-159">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="b9900-160">Hello `--tempDir` viene specificato in file temporanei di hello esempio processo tooisolate hello in un percorso specifico per l'eliminazione semplice.</span><span class="sxs-lookup"><span data-stu-id="b9900-160">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="b9900-161">file temporanei hello tooremove, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b9900-161">tooremove hello temp files, use hello following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="b9900-162">Se si desidera che il comando di hello toorun nuovamente, è necessario eliminare anche la directory di output hello.</span><span class="sxs-lookup"><span data-stu-id="b9900-162">If you want toorun hello command again, you must also delete hello output directory.</span></span> <span data-ttu-id="b9900-163">Utilizzare hello seguente toodelete questa directory:</span><span class="sxs-lookup"><span data-stu-id="b9900-163">Use hello following toodelete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="b9900-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b9900-164">Next steps</span></span>

<span data-ttu-id="b9900-165">Ora che si è appreso come toouse Mahout, individuare altri modi di utilizzo dei dati in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b9900-165">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="b9900-166">Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9900-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b9900-167">Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9900-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="b9900-168">MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9900-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
