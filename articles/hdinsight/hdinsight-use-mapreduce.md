---
title: MapReduce con Hadoop in HDInsight | Documentazione Microsoft
description: Informazioni su come eseguire processi MapReduce in un cluster Hadoop in HDInsight.
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
ms.openlocfilehash: df8ac578a56de72df667b1fa7f90f981c79d9999
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="47983-103">Usare MapReduce in Hadoop su HDInsight</span><span class="sxs-lookup"><span data-stu-id="47983-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="47983-104">Informazioni su come eseguire i processi MapReduce nei cluster di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47983-104">Learn how to run MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="47983-105">Usare la tabella seguente per individuare i vari modi in cui MapReduce può essere usato con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="47983-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="47983-106">**Usare questo**...</span><span class="sxs-lookup"><span data-stu-id="47983-106">**Use this**...</span></span> | <span data-ttu-id="47983-107">**...per eseguire questa operazione**</span><span class="sxs-lookup"><span data-stu-id="47983-107">**...to do this**</span></span> | <span data-ttu-id="47983-108">...con questo **sistema operativo cluster**</span><span class="sxs-lookup"><span data-stu-id="47983-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="47983-109">...da questo **sistema operativo client**</span><span class="sxs-lookup"><span data-stu-id="47983-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="47983-110">SSH</span><span class="sxs-lookup"><span data-stu-id="47983-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="47983-111">Usare il comando Hadoop tramite **SSH**</span><span class="sxs-lookup"><span data-stu-id="47983-111">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="47983-112">Linux</span><span class="sxs-lookup"><span data-stu-id="47983-112">Linux</span></span> |<span data-ttu-id="47983-113">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="47983-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="47983-114">REST</span><span class="sxs-lookup"><span data-stu-id="47983-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="47983-115">Inviare il processo in remoto tramite **REST** (negli esempi viene usato cURL)</span><span class="sxs-lookup"><span data-stu-id="47983-115">Submit the job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="47983-116">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="47983-116">Linux or Windows</span></span> |<span data-ttu-id="47983-117">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="47983-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="47983-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="47983-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="47983-119">Inviare il processo in remoto tramite **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="47983-119">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="47983-120">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="47983-120">Linux or Windows</span></span> |<span data-ttu-id="47983-121">Windows</span><span class="sxs-lookup"><span data-stu-id="47983-121">Windows</span></span> |
| <span data-ttu-id="47983-122">[Desktop remoto](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="47983-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="47983-123">Usare il comando Hadoop tramite **Desktop remoto**</span><span class="sxs-lookup"><span data-stu-id="47983-123">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="47983-124">Windows</span><span class="sxs-lookup"><span data-stu-id="47983-124">Windows</span></span> |<span data-ttu-id="47983-125">Windows</span><span class="sxs-lookup"><span data-stu-id="47983-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="47983-126">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="47983-126">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="47983-127">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="47983-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="47983-128"><a id="whatis"></a>Definizione di MapReduce</span><span class="sxs-lookup"><span data-stu-id="47983-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="47983-129">Hadoop MapReduce è un framework software per la scrittura di processi in grado di elaborare grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="47983-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="47983-130">I dati di input sono suddivisi in blocchi indipendenti, che vengono successivamente elaborati in parallelo tra i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="47983-130">Input data is split into independent chunks, which are then processed in parallel across the nodes in your cluster.</span></span> <span data-ttu-id="47983-131">Un processo MapReduce è costituito da due funzioni:</span><span class="sxs-lookup"><span data-stu-id="47983-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="47983-132">**Mapper**: usa i dati di input, li analizza (in genere mediante operazioni di filtro e ordinamento) e quindi genera tuple (coppie chiave-valore)</span><span class="sxs-lookup"><span data-stu-id="47983-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="47983-133">**Reducer**: usa le tuple generate dal Mapper ed esegue un'operazione di riepilogo che crea un risultato combinato più piccolo a partire dai dati del Mapper</span><span class="sxs-lookup"><span data-stu-id="47983-133">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span></span>

<span data-ttu-id="47983-134">La figura seguente illustra un esempio di processo di base di conteggio parole in MapReduce.</span><span class="sxs-lookup"><span data-stu-id="47983-134">A basic word count MapReduce job example is illustrated in the following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="47983-136">L'output del processo consentirà di conoscere il numero totale di occorrenze di ogni parola presente nel testo analizzato.</span><span class="sxs-lookup"><span data-stu-id="47983-136">The output of this job is a count of how many times each word occurred in the text that was analyzed.</span></span>

* <span data-ttu-id="47983-137">Il mapper accetta come input ciascuna riga del testo di input e la suddivide in parole.</span><span class="sxs-lookup"><span data-stu-id="47983-137">The mapper takes each line from the input text as an input and breaks it into words.</span></span> <span data-ttu-id="47983-138">Emette quindi una coppia chiave-valore ogni volta che viene riscontrata un'occorrenza della parola seguita da 1.</span><span class="sxs-lookup"><span data-stu-id="47983-138">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span></span> <span data-ttu-id="47983-139">L'output viene ordinato e inviato al reducer.</span><span class="sxs-lookup"><span data-stu-id="47983-139">The output is sorted before sending it to reducer.</span></span>
* <span data-ttu-id="47983-140">Il reducer somma i singoli conteggi relativi a ciascuna parola ed emette una sola coppia chiave-valore contenente la parola seguita dal numero di occorrenze.</span><span class="sxs-lookup"><span data-stu-id="47983-140">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span></span>

<span data-ttu-id="47983-141">MapReduce può essere implementato in vari tipi di linguaggio.</span><span class="sxs-lookup"><span data-stu-id="47983-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="47983-142">A scopo dimostrativo, in questo esempio si userà l'implementazione più comune: Java.</span><span class="sxs-lookup"><span data-stu-id="47983-142">Java is the most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="47983-143">Linguaggi di sviluppo</span><span class="sxs-lookup"><span data-stu-id="47983-143">Development languages</span></span>

<span data-ttu-id="47983-144">I linguaggi o i framework basati su Java e Java Virtual Machine possono essere eseguiti direttamente come processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="47983-144">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="47983-145">Nell'esempio in questo documento viene usata un'applicazione Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="47983-145">The example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="47983-146">I linguaggi diversi da Java, ad esempio C# o Python, o file eseguibili autonomi devono usare lo streaming di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="47983-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="47983-147">Lo streaming di Hadoop comunica con il mapper e il riduttore tramite STDIN e STDOUT.</span><span class="sxs-lookup"><span data-stu-id="47983-147">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="47983-148">Il mapper e il riduttore leggono i dati di una riga alla volta da STDIN e scrivono l'output in STDOUT.</span><span class="sxs-lookup"><span data-stu-id="47983-148">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span></span> <span data-ttu-id="47983-149">Ogni riga letta o generata dal mapper e dal riduttore deve essere in formato coppia chiave/valore, separata da un carattere di tabulazione:</span><span class="sxs-lookup"><span data-stu-id="47983-149">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="47983-150">Per altre informazioni, vedere l'argomento relativo a [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="47983-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="47983-151">Per esempi di uso dello streaming di Hadoop con HDInsight, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="47983-151">For examples of using Hadoop streaming with HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="47983-152">Sviluppare processi C# MapReduce</span><span class="sxs-lookup"><span data-stu-id="47983-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="47983-153">Sviluppare processi Python MapReduce</span><span class="sxs-lookup"><span data-stu-id="47983-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="47983-154"><a id="data"></a>Dati di esempio</span><span class="sxs-lookup"><span data-stu-id="47983-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="47983-155">HDInsight offre diversi set di dati di esempio, archiviati nelle directory `/example/data` e `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="47983-155">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="47983-156">Queste directory si trovano nella risorsa di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="47983-156">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="47983-157">In questo documento, viene usato il file `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="47983-157">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="47983-158">Questo file contiene i quaderni di Leonardo Da Vinci.</span><span class="sxs-lookup"><span data-stu-id="47983-158">This file contains the notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="47983-159"><a id="job"></a>MapReduce di esempio</span><span class="sxs-lookup"><span data-stu-id="47983-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="47983-160">Un'applicazione di esempio per il conteggio parole di MapReduce è inclusa nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47983-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="47983-161">Questo esempio si trova in `/example/jars/hadoop-mapreduce-examples.jar` nello spazio di archiviazione predefinito del cluster.</span><span class="sxs-lookup"><span data-stu-id="47983-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span></span>

<span data-ttu-id="47983-162">Il codice Java seguente è l'origine dell'applicazione MapReduce contenuta nel file `hadoop-mapreduce-examples.jar`:</span><span class="sxs-lookup"><span data-stu-id="47983-162">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="47983-163">Per istruzioni sulla scrittura di applicazioni MapReduce, vedere i seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="47983-163">For instructions to write your own MapReduce applications, see the following documents:</span></span>

* [<span data-ttu-id="47983-164">Sviluppare applicazioni Java MapReduce per HDInsight</span><span class="sxs-lookup"><span data-stu-id="47983-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="47983-165">Sviluppare applicazioni Python MapReduce per HDInsight</span><span class="sxs-lookup"><span data-stu-id="47983-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="47983-166"><a id="run"></a>Eseguire il processo MapReduce</span><span class="sxs-lookup"><span data-stu-id="47983-166"><a id="run"></a>Run the MapReduce</span></span>

<span data-ttu-id="47983-167">HDInsight è in grado di eseguire processi HiveQL in vari modi.</span><span class="sxs-lookup"><span data-stu-id="47983-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="47983-168">Usare la tabella seguente per decidere il metodo più adatto alle proprie esigenze, quindi fare clic sul collegamento per visualizzare una procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="47983-168">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="47983-169">**Usare questo**...</span><span class="sxs-lookup"><span data-stu-id="47983-169">**Use this**...</span></span> | <span data-ttu-id="47983-170">**...per eseguire questa operazione**</span><span class="sxs-lookup"><span data-stu-id="47983-170">**...to do this**</span></span> | <span data-ttu-id="47983-171">...con questo **sistema operativo cluster**</span><span class="sxs-lookup"><span data-stu-id="47983-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="47983-172">...da questo **sistema operativo client**</span><span class="sxs-lookup"><span data-stu-id="47983-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="47983-173">SSH</span><span class="sxs-lookup"><span data-stu-id="47983-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="47983-174">Usare il comando Hadoop tramite **SSH**</span><span class="sxs-lookup"><span data-stu-id="47983-174">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="47983-175">Linux</span><span class="sxs-lookup"><span data-stu-id="47983-175">Linux</span></span> |<span data-ttu-id="47983-176">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="47983-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="47983-177">Curl</span><span class="sxs-lookup"><span data-stu-id="47983-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="47983-178">Inviare il processo in remoto tramite **REST**</span><span class="sxs-lookup"><span data-stu-id="47983-178">Submit the job remotely by using **REST**</span></span> |<span data-ttu-id="47983-179">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="47983-179">Linux or Windows</span></span> |<span data-ttu-id="47983-180">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="47983-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="47983-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="47983-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="47983-182">Inviare il processo in remoto tramite **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="47983-182">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="47983-183">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="47983-183">Linux or Windows</span></span> |<span data-ttu-id="47983-184">Windows</span><span class="sxs-lookup"><span data-stu-id="47983-184">Windows</span></span> |
| <span data-ttu-id="47983-185">[Desktop remoto](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="47983-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="47983-186">Usare il comando Hadoop tramite **Desktop remoto**</span><span class="sxs-lookup"><span data-stu-id="47983-186">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="47983-187">Windows</span><span class="sxs-lookup"><span data-stu-id="47983-187">Windows</span></span> |<span data-ttu-id="47983-188">Windows</span><span class="sxs-lookup"><span data-stu-id="47983-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="47983-189">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="47983-189">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="47983-190">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="47983-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="47983-191"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47983-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="47983-192">Per altre informazioni su come usare i dati in HDInsight, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="47983-192">To learn more about working with data in HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="47983-193">Sviluppare programmi MapReduce Java per HDInsight</span><span class="sxs-lookup"><span data-stu-id="47983-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="47983-194">Sviluppare programmi MapReduce per la creazione di flussi Python per HDInsight</span><span class="sxs-lookup"><span data-stu-id="47983-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="47983-195">Sviluppare processi MapReduce in Scalding con Apache Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="47983-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="47983-196">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="47983-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="47983-197">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="47983-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
