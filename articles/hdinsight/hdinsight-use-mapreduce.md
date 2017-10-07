---
title: aaaMapReduce con Hadoop in HDInsight | Documenti Microsoft
description: Informazioni su come processi di toorun MapReduce in Hadoop in cluster HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f321501-d62c-4ffc-b5d6-102ecba6dd76
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0cf7ad0e6769e678be64f9e4ec8ed7a214ab7af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="86f40-103">Usare MapReduce in Hadoop su HDInsight</span><span class="sxs-lookup"><span data-stu-id="86f40-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="86f40-104">Informazioni su come toorun MapReduce processi nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86f40-104">Learn how toorun MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="86f40-105">Utilizzare hello hello toodiscover tabella vari modi MapReduce può essere utilizzato con HDInsight seguenti:</span><span class="sxs-lookup"><span data-stu-id="86f40-105">Use hello following table toodiscover hello various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="86f40-106">**Usare questo**...</span><span class="sxs-lookup"><span data-stu-id="86f40-106">**Use this**...</span></span> | <span data-ttu-id="86f40-107">**... .toodo questo**</span><span class="sxs-lookup"><span data-stu-id="86f40-107">**...toodo this**</span></span> | <span data-ttu-id="86f40-108">...con questo **sistema operativo cluster**</span><span class="sxs-lookup"><span data-stu-id="86f40-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="86f40-109">...da questo **sistema operativo client**</span><span class="sxs-lookup"><span data-stu-id="86f40-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="86f40-110">SSH</span><span class="sxs-lookup"><span data-stu-id="86f40-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="86f40-111">Utilizzare il comando Hadoop hello tramite **SSH**</span><span class="sxs-lookup"><span data-stu-id="86f40-111">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="86f40-112">Linux</span><span class="sxs-lookup"><span data-stu-id="86f40-112">Linux</span></span> |<span data-ttu-id="86f40-113">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="86f40-114">REST</span><span class="sxs-lookup"><span data-stu-id="86f40-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="86f40-115">Inviare il processo di hello in modalità remota utilizzando **REST** (esempi usano cURL)</span><span class="sxs-lookup"><span data-stu-id="86f40-115">Submit hello job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="86f40-116">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-116">Linux or Windows</span></span> |<span data-ttu-id="86f40-117">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="86f40-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="86f40-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="86f40-119">Inviare il processo di hello in modalità remota tramite **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="86f40-119">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="86f40-120">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-120">Linux or Windows</span></span> |<span data-ttu-id="86f40-121">Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-121">Windows</span></span> |
| <span data-ttu-id="86f40-122">[Desktop remoto](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="86f40-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="86f40-123">Utilizzare il comando Hadoop hello tramite **Desktop remoto**</span><span class="sxs-lookup"><span data-stu-id="86f40-123">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="86f40-124">Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-124">Windows</span></span> |<span data-ttu-id="86f40-125">Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="86f40-126">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="86f40-126">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="86f40-127">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="86f40-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="86f40-128"><a id="whatis"></a>Definizione di MapReduce</span><span class="sxs-lookup"><span data-stu-id="86f40-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="86f40-129">Hadoop MapReduce è un framework software per la scrittura di processi in grado di elaborare grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="86f40-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="86f40-130">Dati di input sono suddiviso in blocchi indipendenti, che vengono quindi elaborati in parallelo tra i nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="86f40-130">Input data is split into independent chunks, which are then processed in parallel across hello nodes in your cluster.</span></span> <span data-ttu-id="86f40-131">Un processo MapReduce è costituito da due funzioni:</span><span class="sxs-lookup"><span data-stu-id="86f40-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="86f40-132">**Mapper**: usa i dati di input, li analizza (in genere mediante operazioni di filtro e ordinamento) e quindi genera tuple (coppie chiave-valore)</span><span class="sxs-lookup"><span data-stu-id="86f40-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="86f40-133">**Riduttore**: utilizza tuple generate da BizTalk Mapper hello ed esegue un'operazione di riepilogo che crea un risultato di dimensioni inferiore e quindi combinato da hello dati Mapper</span><span class="sxs-lookup"><span data-stu-id="86f40-133">**Reducer**: Consumes tuples emitted by hello Mapper and performs a summary operation that creates a smaller, combined result from hello Mapper data</span></span>

<span data-ttu-id="86f40-134">Un esempio di processo di base in word conteggio MapReduce viene illustrato nel seguente diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="86f40-134">A basic word count MapReduce job example is illustrated in hello following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="86f40-136">output di Hello del processo è un conteggio di quante volte si è verificato ogni parola hello testo in cui è stato analizzato.</span><span class="sxs-lookup"><span data-stu-id="86f40-136">hello output of this job is a count of how many times each word occurred in hello text that was analyzed.</span></span>

* <span data-ttu-id="86f40-137">mapper Hello accetta ogni riga hello testo di input come input e suddivide in parole.</span><span class="sxs-lookup"><span data-stu-id="86f40-137">hello mapper takes each line from hello input text as an input and breaks it into words.</span></span> <span data-ttu-id="86f40-138">Genera una chiave/valore coppia ogni volta che si verifica una parola di parola hello è seguita da 1.</span><span class="sxs-lookup"><span data-stu-id="86f40-138">It emits a key/value pair each time a word occurs of hello word is followed by a 1.</span></span> <span data-ttu-id="86f40-139">output di Hello viene ordinato prima di inviarlo tooreducer.</span><span class="sxs-lookup"><span data-stu-id="86f40-139">hello output is sorted before sending it tooreducer.</span></span>
* <span data-ttu-id="86f40-140">riduttore Hello somma questi conteggi singoli per ogni parola e genera una coppia chiave/valore singolo che contiene una parola hello seguita da somma hello dei casi.</span><span class="sxs-lookup"><span data-stu-id="86f40-140">hello reducer sums these individual counts for each word and emits a single key/value pair that contains hello word followed by hello sum of its occurrences.</span></span>

<span data-ttu-id="86f40-141">MapReduce può essere implementato in vari tipi di linguaggio.</span><span class="sxs-lookup"><span data-stu-id="86f40-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="86f40-142">Java è hello di implementazione più comune e viene utilizzato per scopi dimostrativi in questo documento.</span><span class="sxs-lookup"><span data-stu-id="86f40-142">Java is hello most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="86f40-143">Linguaggi di sviluppo</span><span class="sxs-lookup"><span data-stu-id="86f40-143">Development languages</span></span>

<span data-ttu-id="86f40-144">Lingue o Framework che si basano su Java e hello macchina virtuale Java può essere eseguito direttamente come un processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="86f40-144">Languages or frameworks that are based on Java and hello Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="86f40-145">esempio Hello utilizzato in questo documento è un'applicazione Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="86f40-145">hello example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="86f40-146">I linguaggi diversi da Java, ad esempio C# o Python, o file eseguibili autonomi devono usare lo streaming di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="86f40-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="86f40-147">Hadoop streaming comunica con BizTalk mapper hello e riduttore STDIN e STDOUT.</span><span class="sxs-lookup"><span data-stu-id="86f40-147">Hadoop streaming communicates with hello mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="86f40-148">riduttore mapper hello leggere dati di una riga alla volta da STDIN e scrivere hello tooSTDOUT di output.</span><span class="sxs-lookup"><span data-stu-id="86f40-148">hello mapper and reducer read data a line at a time from STDIN, and write hello output tooSTDOUT.</span></span> <span data-ttu-id="86f40-149">Ogni riga di lettura o generato dal mapper hello riduttore deve essere nel formato hello di coppia chiave/valore delimitata da un carattere di tabulazione:</span><span class="sxs-lookup"><span data-stu-id="86f40-149">Each line read or emitted by hello mapper and reducer must be in hello format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="86f40-150">Per altre informazioni, vedere l'argomento relativo a [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="86f40-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="86f40-151">Per esempi di utilizzo di Hadoop streaming con HDInsight, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="86f40-151">For examples of using Hadoop streaming with HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="86f40-152">Sviluppare processi C# MapReduce</span><span class="sxs-lookup"><span data-stu-id="86f40-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="86f40-153">Sviluppare processi Python MapReduce</span><span class="sxs-lookup"><span data-stu-id="86f40-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="86f40-154"><a id="data"></a>Dati di esempio</span><span class="sxs-lookup"><span data-stu-id="86f40-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="86f40-155">HDInsight fornisce vari set di dati esempio, che vengono archiviati in hello `/example/data` e `/HdiSamples` directory.</span><span class="sxs-lookup"><span data-stu-id="86f40-155">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="86f40-156">Queste directory sono in spazio di archiviazione di hello predefinito per il cluster.</span><span class="sxs-lookup"><span data-stu-id="86f40-156">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="86f40-157">In questo documento, utilizziamo hello `/example/data/gutenberg/davinci.txt` file.</span><span class="sxs-lookup"><span data-stu-id="86f40-157">In this document, we use hello `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="86f40-158">Questo file contiene blocchi appunti di Leonardo Da Vinci hello.</span><span class="sxs-lookup"><span data-stu-id="86f40-158">This file contains hello notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="86f40-159"><a id="job"></a>MapReduce di esempio</span><span class="sxs-lookup"><span data-stu-id="86f40-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="86f40-160">Un'applicazione di esempio per il conteggio parole di MapReduce è inclusa nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86f40-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="86f40-161">In questo esempio si trova in `/example/jars/hadoop-mapreduce-examples.jar` in spazio di archiviazione di hello predefinito per il cluster.</span><span class="sxs-lookup"><span data-stu-id="86f40-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on hello default storage for your cluster.</span></span>

<span data-ttu-id="86f40-162">codice Java seguente Hello è origine hello hello applicazione MapReduce contenuti in hello `hadoop-mapreduce-examples.jar` file:</span><span class="sxs-lookup"><span data-stu-id="86f40-162">hello following Java code is hello source of hello MapReduce application contained in hello `hadoop-mapreduce-examples.jar` file:</span></span>

```java
package org.apache.hadoop.examples;

import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
        extends Mapper<Object, Text, Text, IntWritable>{

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
        StringTokenizer itr = new StringTokenizer(value.toString());
        while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
        extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();

    public void reduce(Text key, Iterable<IntWritable> values,
                        Context context
                        ) throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable val : values) {
        sum += val.get();
        }
        result.set(sum);
        context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
    if (otherArgs.length != 2) {
        System.err.println("Usage: wordcount <in> <out>");
        System.exit(2);
    }
    Job job = new Job(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
    FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

<span data-ttu-id="86f40-163">Per istruzioni toowrite MapReduce applicazioni personalizzate, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="86f40-163">For instructions toowrite your own MapReduce applications, see hello following documents:</span></span>

* [<span data-ttu-id="86f40-164">Sviluppare applicazioni Java MapReduce per HDInsight</span><span class="sxs-lookup"><span data-stu-id="86f40-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="86f40-165">Sviluppare applicazioni Python MapReduce per HDInsight</span><span class="sxs-lookup"><span data-stu-id="86f40-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="86f40-166"><a id="run"></a>Eseguire hello MapReduce</span><span class="sxs-lookup"><span data-stu-id="86f40-166"><a id="run"></a>Run hello MapReduce</span></span>

<span data-ttu-id="86f40-167">HDInsight è in grado di eseguire processi HiveQL in vari modi.</span><span class="sxs-lookup"><span data-stu-id="86f40-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="86f40-168">Utilizzare hello seguente toodecide tabella quale metodo si adatta alle proprie esigenze, quindi seguire il collegamento hello per una procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="86f40-168">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="86f40-169">**Usare questo**...</span><span class="sxs-lookup"><span data-stu-id="86f40-169">**Use this**...</span></span> | <span data-ttu-id="86f40-170">**... .toodo questo**</span><span class="sxs-lookup"><span data-stu-id="86f40-170">**...toodo this**</span></span> | <span data-ttu-id="86f40-171">...con questo **sistema operativo cluster**</span><span class="sxs-lookup"><span data-stu-id="86f40-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="86f40-172">...da questo **sistema operativo client**</span><span class="sxs-lookup"><span data-stu-id="86f40-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="86f40-173">SSH</span><span class="sxs-lookup"><span data-stu-id="86f40-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="86f40-174">Utilizzare il comando Hadoop hello tramite **SSH**</span><span class="sxs-lookup"><span data-stu-id="86f40-174">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="86f40-175">Linux</span><span class="sxs-lookup"><span data-stu-id="86f40-175">Linux</span></span> |<span data-ttu-id="86f40-176">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="86f40-177">Curl</span><span class="sxs-lookup"><span data-stu-id="86f40-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="86f40-178">Inviare il processo di hello in modalità remota tramite **REST**</span><span class="sxs-lookup"><span data-stu-id="86f40-178">Submit hello job remotely by using **REST**</span></span> |<span data-ttu-id="86f40-179">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-179">Linux or Windows</span></span> |<span data-ttu-id="86f40-180">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="86f40-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="86f40-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="86f40-182">Inviare il processo di hello in modalità remota tramite **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="86f40-182">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="86f40-183">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-183">Linux or Windows</span></span> |<span data-ttu-id="86f40-184">Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-184">Windows</span></span> |
| <span data-ttu-id="86f40-185">[Desktop remoto](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="86f40-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="86f40-186">Utilizzare il comando Hadoop hello tramite **Desktop remoto**</span><span class="sxs-lookup"><span data-stu-id="86f40-186">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="86f40-187">Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-187">Windows</span></span> |<span data-ttu-id="86f40-188">Windows</span><span class="sxs-lookup"><span data-stu-id="86f40-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="86f40-189">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="86f40-189">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="86f40-190">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="86f40-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="86f40-191"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86f40-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="86f40-192">toolearn più sull'uso dei dati in HDInsight, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="86f40-192">toolearn more about working with data in HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="86f40-193">Sviluppare programmi MapReduce Java per HDInsight</span><span class="sxs-lookup"><span data-stu-id="86f40-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="86f40-194">Sviluppare programmi MapReduce per la creazione di flussi Python per HDInsight</span><span class="sxs-lookup"><span data-stu-id="86f40-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="86f40-195">Sviluppare processi MapReduce in Scalding con Apache Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="86f40-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="86f40-196">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="86f40-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="86f40-197">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="86f40-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
