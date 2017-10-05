---
title: Sviluppare processi MapReduce per la creazione di flussi Python con HDInsight - Azure | Documentazione Microsoft
description: Informazioni su come usare Python nel flusso di processi MapReduce. Hadoop fornisce un'API di flusso per MapReduce per la scrittura in linguaggi diversi da Java.
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
ms.openlocfilehash: b86605c49291a99f49c4b2841d46324cfd0db56d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="aa973-104">Sviluppare programmi MapReduce per la creazione di flussi Python per HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa973-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="aa973-105">Informazioni su come usare Python nel flusso di operazioni MapReduce.</span><span class="sxs-lookup"><span data-stu-id="aa973-105">Learn how to use Python in streaming MapReduce operations.</span></span> <span data-ttu-id="aa973-106">In Hadoop è disponibile un'API di flusso per MapReduce che consente di scrivere funzioni di mapping e riduzione in linguaggi diversi da Java.</span><span class="sxs-lookup"><span data-stu-id="aa973-106">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="aa973-107">La procedura descritta in questo documento implementa i componenti di mapping e riduzione in Python.</span><span class="sxs-lookup"><span data-stu-id="aa973-107">The steps in this document implement the Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa973-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="aa973-108">Prerequisites</span></span>

* <span data-ttu-id="aa973-109">Un cluster Hadoop basato su Linux in HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa973-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="aa973-110">I passaggi descritti in questo documento richiedono un cluster HDInsight che usa Linux.</span><span class="sxs-lookup"><span data-stu-id="aa973-110">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="aa973-111">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="aa973-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aa973-112">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="aa973-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="aa973-113">Un editor di testo</span><span class="sxs-lookup"><span data-stu-id="aa973-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="aa973-114">L'editor di testo deve usare LF come terminazione di riga.</span><span class="sxs-lookup"><span data-stu-id="aa973-114">The text editor must use LF as the line ending.</span></span> <span data-ttu-id="aa973-115">L'uso di una terminazione di riga di CRLF causerà errori in seguito all'esecuzione del processo MapReduce su cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="aa973-115">Using a line ending of CRLF causes errors when running the MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="aa973-116">I comandi `ssh` e `scp` oppure [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="aa973-116">The `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="aa973-117">Conteggio di parole</span><span class="sxs-lookup"><span data-stu-id="aa973-117">Word count</span></span>

<span data-ttu-id="aa973-118">In questo esempio viene implementato un conteggio di parole di base in Python usando un mapper e un reducer.</span><span class="sxs-lookup"><span data-stu-id="aa973-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="aa973-119">Il mapper scompone le frasi in singole parole e il reducer aggrega le parole e i conteggi per produrre l'output.</span><span class="sxs-lookup"><span data-stu-id="aa973-119">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span></span>

<span data-ttu-id="aa973-120">Il diagramma di flusso illustra ciò che accade durante le fasi di mapping e riduzione.</span><span class="sxs-lookup"><span data-stu-id="aa973-120">The following flowchart illustrates what happens during the map and reduce phases.</span></span>

![illustrazione del processo MapReduce](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="aa973-122">Flusso di MapReduce</span><span class="sxs-lookup"><span data-stu-id="aa973-122">Streaming MapReduce</span></span>

<span data-ttu-id="aa973-123">Hadoop consente di specificare un file che contiene la logica di mapping e riduzione usata da un processo.</span><span class="sxs-lookup"><span data-stu-id="aa973-123">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span></span> <span data-ttu-id="aa973-124">I requisiti specifici per la logica di mapping e riduzione sono:</span><span class="sxs-lookup"><span data-stu-id="aa973-124">The specific requirements for the map and reduce logic are:</span></span>

* <span data-ttu-id="aa973-125">**Input**: i componenti di mapping e riduzione devono leggere i dati di input da STDIN.</span><span class="sxs-lookup"><span data-stu-id="aa973-125">**Input**: The map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="aa973-126">**Output**: i componenti di mapping e riduzione devono scrivere i dati di output in STDOUT.</span><span class="sxs-lookup"><span data-stu-id="aa973-126">**Output**: The map and reduce components must write output data to STDOUT.</span></span>
* <span data-ttu-id="aa973-127">**Formato dati**: i dati usati e prodotti devono essere una coppia chiave/valore, separati da un carattere di tabulazione.</span><span class="sxs-lookup"><span data-stu-id="aa973-127">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="aa973-128">Python è in grado di gestire facilmente questi requisiti usando il modulo `sys` per leggere da STDIN e il modulo `print` per stampare in STDOUT.</span><span class="sxs-lookup"><span data-stu-id="aa973-128">Python can easily handle these requirements by using the `sys` module to read from STDIN and using `print` to print to STDOUT.</span></span> <span data-ttu-id="aa973-129">Il resto dell'attività consiste semplicemente nella formattazione dei dati con un carattere di tabulazione (`\t`) tra la chiave e il valore.</span><span class="sxs-lookup"><span data-stu-id="aa973-129">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span></span>

## <a name="create-the-mapper-and-reducer"></a><span data-ttu-id="aa973-130">Creare il mapper e il reducer</span><span class="sxs-lookup"><span data-stu-id="aa973-130">Create the mapper and reducer</span></span>

1. <span data-ttu-id="aa973-131">Creare un file denominato `mapper.py` e usare il codice seguente come contenuto:</span><span class="sxs-lookup"><span data-stu-id="aa973-131">Create a file named `mapper.py` and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use the sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read the data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write to STDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="aa973-132">Creare un file denominato **reducer.py** e usare il codice seguente come contenuto:</span><span class="sxs-lookup"><span data-stu-id="aa973-132">Create a file named **reducer.py** and use the following code as the content:</span></span>

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
           # Strip out the separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read the data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using the word as the key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull the count(s) for the word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write to stdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="aa973-133">Esecuzione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa973-133">Run using PowerShell</span></span>

<span data-ttu-id="aa973-134">Per garantire che i file abbiano le terminazioni di riga corrette, usare lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="aa973-134">To ensure that your files have the right line endings, use the following PowerShell script:</span></span>

<span data-ttu-id="aa973-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span><span class="sxs-lookup"><span data-stu-id="aa973-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span></span>

<span data-ttu-id="aa973-136">Usare lo script di PowerShell seguente per caricare i file, eseguire il processo e visualizzare l'output:</span><span class="sxs-lookup"><span data-stu-id="aa973-136">Use the following PowerShell script to upload the files, run the job, and view the output:</span></span>

<span data-ttu-id="aa973-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span><span class="sxs-lookup"><span data-stu-id="aa973-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span></span>

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="aa973-138">Eseguire da una sessione SSH</span><span class="sxs-lookup"><span data-stu-id="aa973-138">Run from an SSH session</span></span>

1. <span data-ttu-id="aa973-139">Nell'ambiente di sviluppo, usare il comando seguente dalla stessa directory dei file `mapper.py` e `reducer.py`:</span><span class="sxs-lookup"><span data-stu-id="aa973-139">From your development environment, in the same directory as `mapper.py` and `reducer.py` files, use the following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="aa973-140">Sostituire `username` con il nome utente SSH del cluster e `clustername` con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="aa973-140">Replace `username` with the SSH user name for your cluster, and `clustername` with the name of your cluster.</span></span>

    <span data-ttu-id="aa973-141">Questo comando copia i file dal sistema locale nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="aa973-141">This command copies the files from the local system to the head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="aa973-142">Se è stata usata una password per proteggere l'account SSH, viene richiesto di specificarla.</span><span class="sxs-lookup"><span data-stu-id="aa973-142">If you used a password to secure your SSH account, you are prompted for the password.</span></span> <span data-ttu-id="aa973-143">Se è stata usata una chiave SSH, potrebbe essere necessario usare il parametro `-i` e il percorso della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="aa973-143">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span></span> <span data-ttu-id="aa973-144">Ad esempio, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="aa973-144">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="aa973-145">Connettersi al cluster usando SSH:</span><span class="sxs-lookup"><span data-stu-id="aa973-145">Connect to the cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="aa973-146">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aa973-146">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="aa973-147">Per garantire che mapper.py e reducer.py abbiano le terminazioni di riga corrette, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa973-147">To ensure the mapper.py and reducer.py have the correct line endings, use the following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="aa973-148">Usare il seguente comando per avviare il processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="aa973-148">Use the following command to start the MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="aa973-149">Questo comando include le seguenti parti:</span><span class="sxs-lookup"><span data-stu-id="aa973-149">This command has the following parts:</span></span>

   * <span data-ttu-id="aa973-150">**hadoop-streaming.jar**: usato durante l'esecuzione di operazioni di flusso MapReduce.</span><span class="sxs-lookup"><span data-stu-id="aa973-150">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="aa973-151">Consente ad Hadoop di interagire con il codice MapReduce esterno fornito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="aa973-151">It interfaces Hadoop with the external MapReduce code you provide.</span></span>

   * <span data-ttu-id="aa973-152">**-file**: aggiunge i file specificati al processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="aa973-152">**-files**: Adds the specified files to the MapReduce job.</span></span>

   * <span data-ttu-id="aa973-153">**-mapper**: indica ad Hadoop quale file usare come mapper.</span><span class="sxs-lookup"><span data-stu-id="aa973-153">**-mapper**: Tells Hadoop which file to use as the mapper.</span></span>

   * <span data-ttu-id="aa973-154">**-reducer**: indica ad Hadoop quale file usare come reducer.</span><span class="sxs-lookup"><span data-stu-id="aa973-154">**-reducer**: Tells Hadoop which file to use as the reducer.</span></span>

   * <span data-ttu-id="aa973-155">**-input**: il file di input di cui devono essere contate le parole.</span><span class="sxs-lookup"><span data-stu-id="aa973-155">**-input**: The input file that we should count words from.</span></span>

   * <span data-ttu-id="aa973-156">**-output**: la directory in cui viene scritto l'output.</span><span class="sxs-lookup"><span data-stu-id="aa973-156">**-output**: The directory that the output is written to.</span></span>

    <span data-ttu-id="aa973-157">Mentre il processo MapReduce è in esecuzione, il processo viene visualizzato sotto forma di valori percentuali.</span><span class="sxs-lookup"><span data-stu-id="aa973-157">As the MapReduce job works, the process is displayed as percentages.</span></span>

        <span data-ttu-id="aa973-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="aa973-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="aa973-159">Per visualizzare l'output, usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="aa973-159">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="aa973-160">Viene visualizzato un elenco di parole con l'indicazione del numero di occorrenze di ogni parola.</span><span class="sxs-lookup"><span data-stu-id="aa973-160">This command displays a list of words and how many times the word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa973-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aa973-161">Next steps</span></span>

<span data-ttu-id="aa973-162">Dopo aver appreso come usare i processi di flusso MapReduce con HDInsight, vedere i seguenti collegamenti per esplorare altri modi di uso di Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aa973-162">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="aa973-163">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa973-163">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="aa973-164">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa973-164">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="aa973-165">Usare processi MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa973-165">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
