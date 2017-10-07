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
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="370e7-104">Sviluppare programmi MapReduce per la creazione di flussi Python per HDInsight</span><span class="sxs-lookup"><span data-stu-id="370e7-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="370e7-105">Informazioni su come toouse Python in MapReduce operazioni di flusso.</span><span class="sxs-lookup"><span data-stu-id="370e7-105">Learn how toouse Python in streaming MapReduce operations.</span></span> <span data-ttu-id="370e7-106">Hadoop fornisce un'API di flusso per MapReduce che consente di toowrite mappa e ridurre le funzioni in linguaggi diversi da Java.</span><span class="sxs-lookup"><span data-stu-id="370e7-106">Hadoop provides a streaming API for MapReduce that enables you toowrite map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="370e7-107">Hello passaggi descritti in questo documento implementano hello mappa e ridurre i componenti di Python.</span><span class="sxs-lookup"><span data-stu-id="370e7-107">hello steps in this document implement hello Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="370e7-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="370e7-108">Prerequisites</span></span>

* <span data-ttu-id="370e7-109">Un cluster Hadoop basato su Linux in HDInsight</span><span class="sxs-lookup"><span data-stu-id="370e7-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="370e7-110">passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux.</span><span class="sxs-lookup"><span data-stu-id="370e7-110">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="370e7-111">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="370e7-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="370e7-112">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="370e7-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="370e7-113">Un editor di testo</span><span class="sxs-lookup"><span data-stu-id="370e7-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="370e7-114">editor di testo Hello devono utilizzare LF come terminazione di riga hello.</span><span class="sxs-lookup"><span data-stu-id="370e7-114">hello text editor must use LF as hello line ending.</span></span> <span data-ttu-id="370e7-115">Utilizzando una terminazione di riga di CRLF causa errori quando si esegue il processo MapReduce hello nei cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="370e7-115">Using a line ending of CRLF causes errors when running hello MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="370e7-116">Hello `ssh` e `scp` comandi, o [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="370e7-116">hello `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="370e7-117">Conteggio di parole</span><span class="sxs-lookup"><span data-stu-id="370e7-117">Word count</span></span>

<span data-ttu-id="370e7-118">In questo esempio viene implementato un conteggio di parole di base in Python usando un mapper e un reducer.</span><span class="sxs-lookup"><span data-stu-id="370e7-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="370e7-119">mapper Hello suddivide frasi in singole parole e riduttore hello aggrega parole hello e conta output di hello tooproduce.</span><span class="sxs-lookup"><span data-stu-id="370e7-119">hello mapper breaks sentences into individual words, and hello reducer aggregates hello words and counts tooproduce hello output.</span></span>

<span data-ttu-id="370e7-120">Hello diagramma di flusso seguente viene illustrato ciò che accade durante la mappa hello e ridurre le fasi.</span><span class="sxs-lookup"><span data-stu-id="370e7-120">hello following flowchart illustrates what happens during hello map and reduce phases.</span></span>

![illustrazione del processo mapreduce hello](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="370e7-122">Flusso di MapReduce</span><span class="sxs-lookup"><span data-stu-id="370e7-122">Streaming MapReduce</span></span>

<span data-ttu-id="370e7-123">Hadoop consente toospecify un file che contiene la mappa hello e riducono la logica utilizzata da un processo.</span><span class="sxs-lookup"><span data-stu-id="370e7-123">Hadoop allows you toospecify a file that contains hello map and reduce logic that is used by a job.</span></span> <span data-ttu-id="370e7-124">requisiti specifici di Hello per hello mapping e riduzione logica sono:</span><span class="sxs-lookup"><span data-stu-id="370e7-124">hello specific requirements for hello map and reduce logic are:</span></span>

* <span data-ttu-id="370e7-125">**Input**: hello mappa e ridurre i componenti devono leggere i dati di input da STDIN.</span><span class="sxs-lookup"><span data-stu-id="370e7-125">**Input**: hello map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="370e7-126">**Output**: hello mappa e ridurre i componenti è necessario scrivere tooSTDOUT dati di output.</span><span class="sxs-lookup"><span data-stu-id="370e7-126">**Output**: hello map and reduce components must write output data tooSTDOUT.</span></span>
* <span data-ttu-id="370e7-127">**Formato dati**: hello i dati utilizzati e prodotto devono essere una coppia chiave/valore, separata da un carattere di tabulazione.</span><span class="sxs-lookup"><span data-stu-id="370e7-127">**Data format**: hello data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="370e7-128">Python possibile facilmente gestire questi requisiti utilizzando hello `sys` tooread modulo da STDIN e l'utilizzo `print` tooprint tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="370e7-128">Python can easily handle these requirements by using hello `sys` module tooread from STDIN and using `print` tooprint tooSTDOUT.</span></span> <span data-ttu-id="370e7-129">Hello attività rimanenti è semplicemente formattazione hello dei dati con una scheda (`\t`) carattere tra hello chiave e il valore.</span><span class="sxs-lookup"><span data-stu-id="370e7-129">hello remaining task is simply formatting hello data with a tab (`\t`) character between hello key and value.</span></span>

## <a name="create-hello-mapper-and-reducer"></a><span data-ttu-id="370e7-130">Creare riduttore e mapper hello</span><span class="sxs-lookup"><span data-stu-id="370e7-130">Create hello mapper and reducer</span></span>

1. <span data-ttu-id="370e7-131">Creare un file denominato `mapper.py` e utilizzare hello seguendo il codice come contenuto hello:</span><span class="sxs-lookup"><span data-stu-id="370e7-131">Create a file named `mapper.py` and use hello following code as hello content:</span></span>

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

2. <span data-ttu-id="370e7-132">Creare un file denominato **reducer.py** e utilizzare hello seguendo il codice come contenuto hello:</span><span class="sxs-lookup"><span data-stu-id="370e7-132">Create a file named **reducer.py** and use hello following code as hello content:</span></span>

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

## <a name="run-using-powershell"></a><span data-ttu-id="370e7-133">Esecuzione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="370e7-133">Run using PowerShell</span></span>

<span data-ttu-id="370e7-134">tooensure che i file hanno terminazioni riga destra hello hello utilizzare lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="370e7-134">tooensure that your files have hello right line endings, use hello following PowerShell script:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

<span data-ttu-id="370e7-135">Utilizzare i seguenti file hello tooupload script di PowerShell hello, eseguire il processo di hello e visualizzare l'output di hello:</span><span class="sxs-lookup"><span data-stu-id="370e7-135">Use hello following PowerShell script tooupload hello files, run hello job, and view hello output:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="370e7-136">Eseguire da una sessione SSH</span><span class="sxs-lookup"><span data-stu-id="370e7-136">Run from an SSH session</span></span>

1. <span data-ttu-id="370e7-137">Nell'ambiente di sviluppo, hello nella stessa directory come `mapper.py` e `reducer.py` file, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="370e7-137">From your development environment, in hello same directory as `mapper.py` and `reducer.py` files, use hello following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="370e7-138">Sostituire `username` con nome utente di hello SSH per il cluster, e `clustername` con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="370e7-138">Replace `username` with hello SSH user name for your cluster, and `clustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="370e7-139">Questo comando Copia file hello dal nodo head toohello di hello sistema locale.</span><span class="sxs-lookup"><span data-stu-id="370e7-139">This command copies hello files from hello local system toohello head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="370e7-140">Se si utilizza un toosecure password account SSH, richiesto per la password di hello.</span><span class="sxs-lookup"><span data-stu-id="370e7-140">If you used a password toosecure your SSH account, you are prompted for hello password.</span></span> <span data-ttu-id="370e7-141">Se è stata utilizzata una chiave SSH, potrebbe essere hello toouse `-i` parametro e hello percorso toohello la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="370e7-141">If you used an SSH key, you may have toouse hello `-i` parameter and hello path toohello private key.</span></span> <span data-ttu-id="370e7-142">ad esempio `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="370e7-142">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="370e7-143">Connessione toohello cluster utilizzando SSH:</span><span class="sxs-lookup"><span data-stu-id="370e7-143">Connect toohello cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="370e7-144">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="370e7-144">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="370e7-145">REDUCER.py e tooensure hello mapper.py hanno hello correggere terminazioni riga, utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="370e7-145">tooensure hello mapper.py and reducer.py have hello correct line endings, use hello following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="370e7-146">Utilizzare hello processo MapReduce hello toostart il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="370e7-146">Use hello following command toostart hello MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="370e7-147">Questo comando è hello seguenti parti:</span><span class="sxs-lookup"><span data-stu-id="370e7-147">This command has hello following parts:</span></span>

   * <span data-ttu-id="370e7-148">**hadoop-streaming.jar**: usato durante l'esecuzione di operazioni di flusso MapReduce.</span><span class="sxs-lookup"><span data-stu-id="370e7-148">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="370e7-149">Hadoop si interfaccia con codice MapReduce esterno hello che è fornire.</span><span class="sxs-lookup"><span data-stu-id="370e7-149">It interfaces Hadoop with hello external MapReduce code you provide.</span></span>

   * <span data-ttu-id="370e7-150">**-file**: aggiunge hello specificato processo MapReduce toohello di file.</span><span class="sxs-lookup"><span data-stu-id="370e7-150">**-files**: Adds hello specified files toohello MapReduce job.</span></span>

   * <span data-ttu-id="370e7-151">**-mapper**: Hadoop indica quale file toouse hello mapper.</span><span class="sxs-lookup"><span data-stu-id="370e7-151">**-mapper**: Tells Hadoop which file toouse as hello mapper.</span></span>

   * <span data-ttu-id="370e7-152">**-riduttore**: Hadoop indica quale file toouse hello del reducer.</span><span class="sxs-lookup"><span data-stu-id="370e7-152">**-reducer**: Tells Hadoop which file toouse as hello reducer.</span></span>

   * <span data-ttu-id="370e7-153">**-input**: file di input hello che è necessario contare le parole da.</span><span class="sxs-lookup"><span data-stu-id="370e7-153">**-input**: hello input file that we should count words from.</span></span>

   * <span data-ttu-id="370e7-154">**-output**: directory hello hello output viene scritto.</span><span class="sxs-lookup"><span data-stu-id="370e7-154">**-output**: hello directory that hello output is written to.</span></span>

    <span data-ttu-id="370e7-155">Come funziona il processo MapReduce hello, processo hello è visualizzato come percentuali.</span><span class="sxs-lookup"><span data-stu-id="370e7-155">As hello MapReduce job works, hello process is displayed as percentages.</span></span>

        <span data-ttu-id="370e7-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="370e7-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="370e7-157">l'output di hello tooview, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="370e7-157">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="370e7-158">Questo comando Visualizza un elenco di parole e quante volte la parola hello si è verificato.</span><span class="sxs-lookup"><span data-stu-id="370e7-158">This command displays a list of words and how many times hello word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="370e7-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="370e7-159">Next steps</span></span>

<span data-ttu-id="370e7-160">Ora che si è appreso come processi di streaming MapRedcue toouse con HDInsight, utilizzare hello seguendo i collegamenti tooexplore toowork altri modi con Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="370e7-160">Now that you have learned how toouse streaming MapRedcue jobs with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="370e7-161">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="370e7-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="370e7-162">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="370e7-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="370e7-163">Usare processi MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="370e7-163">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
