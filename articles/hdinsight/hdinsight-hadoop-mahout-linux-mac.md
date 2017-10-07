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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a>Generare raccomandazioni di film tramite Apache Mahout con Hadoop basato su Linux in HDInsight (SSH)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Informazioni su come hello toouse [Mahout Apache](http://mahout.apache.org) libreria learning macchina con le raccomandazioni di Azure HDInsight toogenerate film.

Mahout è una libreria di [apprendimento automatico][ml] per Apache Hadoop. Mahout contiene gli algoritmi per l'elaborazione dei dati, ad esempio applicazione di filtri, classificazione e clustering. In questo articolo, si utilizzano una raccomandazione motore toogenerate film raccomandazioni basate su filmati sono visualizzati i tuoi amici.

## <a name="prerequisites"></a>Prerequisiti

* Un cluster HDInsight basato su Linux. Per informazioni su come crearne uno, vedere [Introduzione all'uso di Hadoop basato su Linux in HDInsight][getstarted].

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un client SSH. Per ulteriori informazioni, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

## <a name="mahout-versioning"></a>Controllo delle versioni di Mahout

Per ulteriori informazioni sulla versione di hello di Mahout in HDInsight, vedere [HDInsight versioni e i componenti di Hadoop](hdinsight-component-versioning.md).

## <a name="recommendations"></a>Informazioni sulle raccomandazioni

Una delle funzioni hello fornito da Mahout è un motore di raccomandazione. Questo motore accetta i dati in formato hello `userID`, `itemId`, e `prefValue` (hello preferenza per l'elemento hello). Mahout può quindi eseguire CO-occorrenza analisi toodetermine: *gli utenti che dispongono di una preferenza per un elemento hanno anche una preferenza per questi altri elementi*. Mahout determina quindi gli utenti con preferenze simili-item, che possono essere utilizzato toomake indicazioni.

Hello seguente flusso di lavoro è un esempio semplificato che utilizza dati film:

* **CO-occorrenza**: Joe, Alice e Bob tutti stato apprezzato *stella attraverso*, *hello Empire colpisce nuovamente*, e *restituzione di hello Jedi*. Mahout determina che gli utenti come uno di questi film anche hello altri due.

* **CO-occorrenza**: Bob e Alice anche ritengono *hello Phantom alieni*, *attacco dei cloni di hello*, e *ritorsioni di hello Sith*. Mahout determina che gli utenti che ritengono tre filmati precedente hello anche come questi tre film.

* **Indicazione di somiglianza**: Joe perché ritengono hello primi tre film, Mahout esamina filmati che altri utenti con preferenze simili ritengono, ma Joe ha non controllata (ritengono/classificazione). In questo caso, si consiglia Mahout *hello Phantom alieni*, *attacco dei cloni di hello*, e *ritorsioni di hello Sith*.

### <a name="understanding-hello-data"></a>Informazioni sui dati hello

[GroupLens Research][movielens] fornisce i dati di classificazione dei film in un formato compatibile con Mahout. Questi dati sono disponibili nello spazio di archiviazione predefinito del cluster in `/HdiSamples/HdiSamples/MahoutMovieData`.

Sono disponibili due file: `moviedb.txt` e `user-ratings.txt`. file utente ratings.txt Hello viene utilizzato durante l'analisi, mentre moviedb.txt è tooprovide utilizzato testo descrittivo informazioni quando si visualizzano i risultati di hello dell'analisi hello.

dati contenuti in utente ratings.txt Hello presenta una struttura di `userID`, `movieID`, `userRating`, e `timestamp`, che indica come elevata ogni utente classificato un filmato. Di seguito è riportato un esempio di dati hello:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a>Eseguire l'analisi di hello

Da un cluster di toohello connessione SSH, utilizzare hello processo raccomandazione hello toorun di comando seguente:

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> Hello processo potrebbe richiedere diversi minuti toocomplete e possono essere eseguite più processi di MapReduce.

## <a name="view-hello-output"></a>Visualizzazione output di hello

1. Al termine del processo di hello, hello utilizzo successivo comando tooview hello ha generato l'output:

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    output di Hello viene visualizzato come segue:

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    prima colonna Hello è hello `userID`. Hello valori contenuti in ' [' e ']' sono `movieId`:`recommendationScore`.

2. È possibile utilizzare un output di hello, insieme a hello moviedb.txt, tooprovide ulteriori informazioni sui suggerimenti di hello. Innanzitutto, è necessario il file di hello toocopy localmente utilizzando hello seguenti comandi:

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    Questo comando copia hello file tooa dati di output denominata **recommendations.txt** nella directory corrente hello, insieme ai file di dati di hello film.

3. Utilizzare hello toocreate comando script Python che cerca i nomi di film per i dati di hello nell'output di hello indicazioni seguenti:

    ```bash
    nano show_recommendations.py
    ```

    Quando si apre l'editor di hello, utilizzare hello segue testo come contenuto di hello del file hello:

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

    Premere **Ctrl + X**, **Y**e infine **invio** dati hello toosave.

4. Eseguire script Python hello. Hello comando riportato di seguito si presuppone che trovano nella directory hello in cui sono stati scaricati tutti i file hello:

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    Questo comando vengono esaminati indicazioni hello generati per l'utente ID 4.

    * Hello **utente ratings.txt** file è utilizzato tooretrieve filmati che sono stati classificati.

    * Hello **moviedb.txt** file è utilizzato tooretrieve hello nomi di film hello.

    * Hello **recommendations.txt** è usato tooretrieve indicazioni film hello per questo utente.

     Hello l'output di questo comando è simile toohello seguente testo:

        Periodo di 7 anni Tibet (1997), assegnare un punteggio = 5.0 Indiana Jones e hello Crusade ultimo (1989), assegnare un punteggio = 5.0 Jaws (1975), punteggio = 5.0 senso e Sensibility (1995), punteggio = 5.0 indipendenza giorno (ID4) (1996), punteggio = 5.0 il migliore amico matrimoni (1997), assegnare un punteggio = 5.0 Jerry Maguire (1996 ), punteggio = 5.0 Scream 2 (1997), punteggio = 5.0 tooKill ora, (1996), assegnare un punteggio = 5.0

## <a name="delete-temporary-data"></a>Eliminare i dati temporanei

I processi di mahout non rimuovere i dati temporanei creati durante l'elaborazione di processi di hello. Hello `--tempDir` viene specificato in file temporanei di hello esempio processo tooisolate hello in un percorso specifico per l'eliminazione semplice. file temporanei hello tooremove, utilizzare hello comando seguente:

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> Se si desidera che il comando di hello toorun nuovamente, è necessario eliminare anche la directory di output hello. Utilizzare hello seguente toodelete questa directory:
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come toouse Mahout, individuare altri modi di utilizzo dei dati in HDInsight:

* [Hive con HDInsight](hdinsight-use-hive.md)
* [Pig con HDInsight](hdinsight-use-pig.md)
* [MapReduce con HDInsight](hdinsight-use-mapreduce.md)

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
