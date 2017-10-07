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
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a>Usare MapReduce in Hadoop su HDInsight

Informazioni su come toorun MapReduce processi nel cluster HDInsight. Utilizzare hello hello toodiscover tabella vari modi MapReduce può essere utilizzato con HDInsight seguenti:

| **Usare questo**... | **... .toodo questo** | ...con questo **sistema operativo cluster** | ...da questo **sistema operativo client** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Utilizzare il comando Hadoop hello tramite **SSH** |Linux |Linux, Unix, Mac OS X o Windows |
| [REST](hdinsight-hadoop-use-mapreduce-curl.md) |Inviare il processo di hello in modalità remota utilizzando **REST** (esempi usano cURL) |Linux o Windows |Linux, Unix, Mac OS X o Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Inviare il processo di hello in modalità remota tramite **Windows PowerShell** |Linux o Windows |Windows |
| [Desktop remoto](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 e 3.3) |Utilizzare il comando Hadoop hello tramite **Desktop remoto** |Windows |Windows |

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="whatis"></a>Definizione di MapReduce

Hadoop MapReduce è un framework software per la scrittura di processi in grado di elaborare grandi quantità di dati. Dati di input sono suddiviso in blocchi indipendenti, che vengono quindi elaborati in parallelo tra i nodi del cluster hello. Un processo MapReduce è costituito da due funzioni:

* **Mapper**: usa i dati di input, li analizza (in genere mediante operazioni di filtro e ordinamento) e quindi genera tuple (coppie chiave-valore)

* **Riduttore**: utilizza tuple generate da BizTalk Mapper hello ed esegue un'operazione di riepilogo che crea un risultato di dimensioni inferiore e quindi combinato da hello dati Mapper

Un esempio di processo di base in word conteggio MapReduce viene illustrato nel seguente diagramma hello:

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

output di Hello del processo è un conteggio di quante volte si è verificato ogni parola hello testo in cui è stato analizzato.

* mapper Hello accetta ogni riga hello testo di input come input e suddivide in parole. Genera una chiave/valore coppia ogni volta che si verifica una parola di parola hello è seguita da 1. output di Hello viene ordinato prima di inviarlo tooreducer.
* riduttore Hello somma questi conteggi singoli per ogni parola e genera una coppia chiave/valore singolo che contiene una parola hello seguita da somma hello dei casi.

MapReduce può essere implementato in vari tipi di linguaggio. Java è hello di implementazione più comune e viene utilizzato per scopi dimostrativi in questo documento.

## <a name="development-languages"></a>Linguaggi di sviluppo

Lingue o Framework che si basano su Java e hello macchina virtuale Java può essere eseguito direttamente come un processo MapReduce. esempio Hello utilizzato in questo documento è un'applicazione Java MapReduce. I linguaggi diversi da Java, ad esempio C# o Python, o file eseguibili autonomi devono usare lo streaming di Hadoop.

Hadoop streaming comunica con BizTalk mapper hello e riduttore STDIN e STDOUT. riduttore mapper hello leggere dati di una riga alla volta da STDIN e scrivere hello tooSTDOUT di output. Ogni riga di lettura o generato dal mapper hello riduttore deve essere nel formato hello di coppia chiave/valore delimitata da un carattere di tabulazione:

    [key]/t[value]

Per altre informazioni, vedere l'argomento relativo a [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).

Per esempi di utilizzo di Hadoop streaming con HDInsight, vedere hello seguenti documenti:

* [Sviluppare processi C# MapReduce](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Sviluppare processi Python MapReduce](hdinsight-hadoop-streaming-python.md)

## <a id="data"></a>Dati di esempio

HDInsight fornisce vari set di dati esempio, che vengono archiviati in hello `/example/data` e `/HdiSamples` directory. Queste directory sono in spazio di archiviazione di hello predefinito per il cluster. In questo documento, utilizziamo hello `/example/data/gutenberg/davinci.txt` file. Questo file contiene blocchi appunti di Leonardo Da Vinci hello.

## <a id="job"></a>MapReduce di esempio

Un'applicazione di esempio per il conteggio parole di MapReduce è inclusa nel cluster HDInsight. In questo esempio si trova in `/example/jars/hadoop-mapreduce-examples.jar` in spazio di archiviazione di hello predefinito per il cluster.

codice Java seguente Hello è origine hello hello applicazione MapReduce contenuti in hello `hadoop-mapreduce-examples.jar` file:

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

Per istruzioni toowrite MapReduce applicazioni personalizzate, vedere hello seguenti documenti:

* [Sviluppare applicazioni Java MapReduce per HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Sviluppare applicazioni Python MapReduce per HDInsight](hdinsight-hadoop-streaming-python.md)

## <a id="run"></a>Eseguire hello MapReduce

HDInsight è in grado di eseguire processi HiveQL in vari modi. Utilizzare hello seguente toodecide tabella quale metodo si adatta alle proprie esigenze, quindi seguire il collegamento hello per una procedura dettagliata.

| **Usare questo**... | **... .toodo questo** | ...con questo **sistema operativo cluster** | ...da questo **sistema operativo client** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Utilizzare il comando Hadoop hello tramite **SSH** |Linux |Linux, Unix, Mac OS X o Windows |
| [Curl](hdinsight-hadoop-use-mapreduce-curl.md) |Inviare il processo di hello in modalità remota tramite **REST** |Linux o Windows |Linux, Unix, Mac OS X o Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Inviare il processo di hello in modalità remota tramite **Windows PowerShell** |Linux o Windows |Windows |
| [Desktop remoto](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 e 3.3) |Utilizzare il comando Hadoop hello tramite **Desktop remoto** |Windows |Windows |

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="nextsteps"></a>Passaggi successivi

toolearn più sull'uso dei dati in HDInsight, vedere hello seguenti documenti:

* [Sviluppare programmi MapReduce Java per HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Sviluppare programmi MapReduce per la creazione di flussi Python per HDInsight](hdinsight-hadoop-streaming-python.md)

* [Sviluppare processi MapReduce in Scalding con Apache Hadoop in HDInsight](hdinsight-hadoop-mapreduce-scalding.md)

* [Usare Hive con HDInsight][hdinsight-use-hive]

* [Usare Pig con HDInsight][hdinsight-use-pig]


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
