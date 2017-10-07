---
title: i processi di streaming MapReduce Python aaaDevelop con HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse Python in streaming i processi di MapReduce. Hadoop fornisce un'API di flusso per MapReduce per la scrittura in linguaggi diversi da Java.
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a6ae3ba650b665ecc5839a4ddf5282f8ccfb6bd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a>Sviluppare programmi MapReduce per la creazione di flussi Python per HDInsight

Informazioni su come toouse Python in MapReduce operazioni di flusso. Hadoop fornisce un'API di flusso per MapReduce che consente di toowrite mappa e ridurre le funzioni in linguaggi diversi da Java. Hello passaggi descritti in questo documento implementano hello mappa e ridurre i componenti di Python.

## <a name="prerequisites"></a>Prerequisiti

* Un cluster Hadoop basato su Linux in HDInsight

  > [!IMPORTANT]
  > passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un editor di testo

  > [!IMPORTANT]
  > editor di testo Hello devono utilizzare LF come terminazione di riga hello. Utilizzando una terminazione di riga di CRLF causa errori quando si esegue il processo MapReduce hello nei cluster HDInsight basati su Linux.

* Hello `ssh` e `scp` comandi, o [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)

## <a name="word-count"></a>Conteggio di parole

In questo esempio viene implementato un conteggio di parole di base in Python usando un mapper e un reducer. mapper Hello suddivide frasi in singole parole e riduttore hello aggrega parole hello e conta output di hello tooproduce.

Hello diagramma di flusso seguente viene illustrato ciò che accade durante la mappa hello e ridurre le fasi.

![illustrazione del processo mapreduce hello](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a>Flusso di MapReduce

Hadoop consente toospecify un file che contiene la mappa hello e riducono la logica utilizzata da un processo. requisiti specifici di Hello per hello mapping e riduzione logica sono:

* **Input**: hello mappa e ridurre i componenti devono leggere i dati di input da STDIN.
* **Output**: hello mappa e ridurre i componenti è necessario scrivere tooSTDOUT dati di output.
* **Formato dati**: hello i dati utilizzati e prodotto devono essere una coppia chiave/valore, separata da un carattere di tabulazione.

Python possibile facilmente gestire questi requisiti utilizzando hello `sys` tooread modulo da STDIN e l'utilizzo `print` tooprint tooSTDOUT. Hello attività rimanenti è semplicemente formattazione hello dei dati con una scheda (`\t`) carattere tra hello chiave e il valore.

## <a name="create-hello-mapper-and-reducer"></a>Creare riduttore e mapper hello

1. Creare un file denominato `mapper.py` e utilizzare hello seguendo il codice come contenuto hello:

   ```python
   #!/usr/bin/env python

   # Use hello sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read hello data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write tooSTDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. Creare un file denominato **reducer.py** e utilizzare hello seguendo il codice come contenuto hello:

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out hello separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read hello data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using hello word as hello key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull hello count(s) for hello word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write toostdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a>Esecuzione con PowerShell

tooensure che i file hanno terminazioni riga destra hello hello utilizzare lo script di PowerShell seguente:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

Utilizzare i seguenti file hello tooupload script di PowerShell hello, eseguire il processo di hello e visualizzare l'output di hello:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a>Eseguire da una sessione SSH

1. Nell'ambiente di sviluppo, hello nella stessa directory come `mapper.py` e `reducer.py` file, utilizzare hello comando seguente:

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    Sostituire `username` con nome utente di hello SSH per il cluster, e `clustername` con nome hello del cluster.

    Questo comando Copia file hello dal nodo head toohello di hello sistema locale.

    > [!NOTE]
    > Se si utilizza un toosecure password account SSH, richiesto per la password di hello. Se è stata utilizzata una chiave SSH, potrebbe essere hello toouse `-i` parametro e hello percorso toohello la chiave privata. ad esempio `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.

2. Connessione toohello cluster utilizzando SSH:

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. REDUCER.py e tooensure hello mapper.py hanno hello correggere terminazioni riga, utilizzare hello seguenti comandi:

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. Utilizzare hello processo MapReduce hello toostart il comando seguente.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    Questo comando è hello seguenti parti:

   * **hadoop-streaming.jar**: usato durante l'esecuzione di operazioni di flusso MapReduce. Hadoop si interfaccia con codice MapReduce esterno hello che è fornire.

   * **-file**: aggiunge hello specificato processo MapReduce toohello di file.

   * **-mapper**: Hadoop indica quale file toouse hello mapper.

   * **-riduttore**: Hadoop indica quale file toouse hello del reducer.

   * **-input**: file di input hello che è necessario contare le parole da.

   * **-output**: directory hello hello output viene scritto.

    Come funziona il processo MapReduce hello, processo hello è visualizzato come percentuali.

        15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%


5. l'output di hello tooview, utilizzare hello comando seguente:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Questo comando Visualizza un elenco di parole e quante volte la parola hello si è verificato.

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come processi di streaming MapRedcue toouse con HDInsight, utilizzare hello seguendo i collegamenti tooexplore toowork altri modi con Azure HDInsight.

* [Usare Hive con HDInsight](hdinsight-use-hive.md)
* [Usare Pig con HDInsight](hdinsight-use-pig.md)
* [Usare processi MapReduce con HDInsight](hdinsight-use-mapreduce.md)
