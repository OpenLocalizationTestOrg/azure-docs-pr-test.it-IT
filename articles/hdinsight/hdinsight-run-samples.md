---
title: esempi di hello aaaRun Hadoop in HDInsight - Azure | Documenti Microsoft
description: Introduzione all'uso del servizio Azure HDInsight hello con hello esempi forniti. Usare script PowerShell che eseguono programmi MapReduce su cluster di dati.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a>Eseguire esempi di Hadoop MapReduce in HDInsight basato su Windows
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Toohelp iniziare in esecuzione processi MapReduce in Hadoop cluster con Azure HDInsight è disponibile un set di campioni. Questi esempi vengono resi disponibili in ogni hello HDInsight cluster gestiti creato. In questi esempi di esecuzione di acquisire familiarità con Azure PowerShell cmdlet toorun processi nel cluster Hadoop.

* [**Conteggio delle parole**][hdinsight-sample-wordcount]: conta le occorrenze delle parole in un file di testo.
* [**Conteggio parole streaming c#**][hdinsight-sample-csharp-streaming]: conta le occorrenze di word in un file di testo utilizzando hello Hadoop streaming di interfaccia.
* [**Estimator pi**][hdinsight-sample-pi-estimator]: Usa una statistica (quasi Monte Carlo) tooestimate hello valore del metodo di pi greco.
* [**Graysort da 10 GB**][hdinsight-sample-10gb-graysort]: esegue un ordinamento GraySort per utilizzo generico in un file da 10 GB usando HDInsight. Esistono tre processi toorun: Teragen toogenerate hello dati, Terasort toosort hello e tooconfirm Teravalidate che dati hello siano stati ordinati correttamente.

> [!NOTE]
> codice sorgente Hello è reperibile in hello appendice.

Documentazione aggiuntiva molto esista nel web hello per le tecnologie correlate Hadoop, ad esempio la programmazione basata su Java MapReduce e streaming e documentazione sui cmdlet di hello utilizzabili in Windows PowerShell scripting. Per altre informazioni su queste risorse, vedere:

* [Sviluppare programmi MapReduce Java per Hadoop in HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [Inviare processi Hadoop in HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Introduzione tooAzure HDInsight][hdinsight-introduction]

Molte persone preferiscono oggi Hive e Pig rispetto a MapReduce.  Per altre informazioni, vedere:

* [Usare Hive in HDInsight](hdinsight-use-hive.md)
* [Usare Pig in HDInsight](hdinsight-use-pig.md)

**Prerequisiti**:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Un cluster HDInsight**. Per istruzioni su hello vari modi in cui è possibile creare cluster di questo tipo, vedere [cluster creare Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* **Workstation con Azure PowerShell**.

    > [!IMPORTANT]
    > Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** e verrà rimosso dal 1° gennaio 2017. Hello passaggi in questo documento usa hello nuovi cmdlet di HDInsight che funzionano con Gestione risorse di Azure.
    >
    > Seguire i passaggi di hello in [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello più recente di Azure PowerShell. Se si dispone di script che toobe necessità modificato toouse hello nuovi cmdlet che funzionano con Gestione risorse di Azure, vedere [di strumenti di migrazione tooAzure sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="hdinsight-sample-wordcount"></a>Conteggio delle parole: Java
un progetto di MapReduce toosubmit, creare innanzitutto la definizione di un processo MapReduce. Nella definizione di processo hello, è necessario specificare i file jar di programma MapReduce hello e hello del file jar di hello, che è **wasb:///example/jars/hadoop-mapreduce-examples.jar**, nome della classe hello e hello argomenti.  il programma MapReduce di Hello wordcount accetta due argomenti: file di origine hello parole toocount utilizzato e il percorso di hello per l'output.

codice sorgente Hello è reperibile in hello [appendice](#apendix-a---the-word-count-MapReduce-program-in-java).

Per procedure hello sviluppo MapReduce un linguaggio di programmazione, vedere - [MapReduce Java di sviluppare applicazioni per Hadoop in HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

**un processo MapReduce il conteggio word toosubmit**

1. Aprire **Windows PowerShell ISE**. Per istruzioni, vedere [Installare e configurare Azure PowerShell][powershell-install-configure].
2. Hello incollare lo script di PowerShell seguente:

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get hello job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    il processo MapReduce Hello produce un file denominato *parte-r-00000*, che contiene le parole e conta hello. script di Hello utilizza hello **findstr** comando toolist hello tutte le parole che contiene *"there"*.
3. Impostare hello innanzitutto tre variabili ed eseguire script hello.

## <a name="hdinsight-sample-csharp-streaming"></a>Conteggio delle parole: flusso in C#
Hadoop fornisce un flusso tooMapReduce API, che consente di toowrite mappa e ridurre le funzioni in linguaggi diversi da Java.

> [!NOTE]
> passaggi di Hello in questa esercitazione si applicano solo tooWindows basato su cluster di HDInsight. Per un esempio di flusso per cluster HDInsight basati su Linux, vedere [Sviluppare programmi di streaming Python per HDInsight](hdinsight-hadoop-streaming-python.md).

Nell'esempio hello mapper hello e riduttore hello sono eseguibili, leggono l'input hello da [stdin] [ stdin-stdout-stderr] (riga per riga) e crea l'output di hello troppo[stdout] [stdin-stdout-stderr]. programma Hello conta tutte le parole nel testo hello hello.

Quando un file eseguibile specificato per **BizTalk Mapper**, ogni attività mapper avvia hello eseguibile come un processo distinto quando viene inizializzato il mapper hello. Esegue attività mapper hello, converte l'input in righe e feed hello righe toohello [stdin] [ stdin-stdout-stderr] del processo di hello.

In hello frattempo mapper hello raccoglie output orientato alla riga hello da stdout hello del processo di hello. Converte ogni riga in una coppia chiave/valore, che viene raccolto nell'output di hello del mapper hello. Per impostazione predefinita, il prefisso di hello di una riga di toohello primo carattere di tabulazione è chiave hello e resto hello della riga di hello (esclusa hello carattere di tabulazione) è il valore di hello. Se non è presente alcun carattere di tabulazione nella riga hello, riga intera viene considerata come chiave hello e hello valore è null.

Quando un file eseguibile specificato per **riduttori**, ogni attività riduttore avvia hello eseguibile come un processo distinto quando viene inizializzato riduttore hello. Hello riduttore attività viene eseguita, relativo coppie chiave/valore di input viene convertito in righe e feed di hello righe toohello [stdin] [ stdin-stdout-stderr] del processo di hello.

In hello frattempo riduttore hello raccoglie output orientato alla riga hello dalla hello [stdout] [ stdin-stdout-stderr] del processo di hello. Converte ogni coppia chiave/valore tooa di riga, che viene raccolto nell'output di hello del reducer hello. Per impostazione predefinita, il prefisso di hello di una riga di toohello primo carattere di tabulazione è chiave hello e resto hello della riga di hello (esclusa hello carattere di tabulazione) è il valore di hello.

**processo di conteggio toosubmit c# streaming word**

* Attenersi alla procedura hello in [Word count - Java](#word-count-java)e sostituire la definizione di processo hello con hello seguente riga:

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    file di output di Hello dovrà essere:

        example/data/StreamingOutput/wc.txt/part-00000

## <a name="hdinsight-sample-pi-estimator"></a>Calcolo del Pi greco
Usa una statistica estimator pi Hello (quasi Monte Carlo) tooestimate hello valore del metodo di pi greco. Punti posizionati in modo casuale all'interno di un'unità quadrati anche rientrano in un cerchio figurare all'interno di tale quadrato con un'area toohello uguale probabilità del cerchio hello, pi/4. il valore di Hello di pi greco può essere stimato dal valore hello 4R, dove R è il rapporto di hello del numero di hello di punti che si trovano all'interno di hello cerchio toohello numero totale di punti che si trovano all'interno di quadrato di hello. esempio hello di dimensioni maggiore Hello di punti utilizzati stima più accurata hello hello è.

script Hello fornito per questo esempio invia un processo jar Hadoop e viene impostato toorun con un valore 16 mappe, ognuno dei quali è necessario toocompute 10 milioni di esempio punti dai valori di parametro hello. Questi parametri i valori possono essere modificate tooimprove hello stimato valore di pi greco. Per riferimento, hello primi 10 cifre decimali di pi greco sono 3.1415926535.

**un processo di stima pi toosubmit**

* Attenersi alla procedura hello in [Word count - Java](#word-count-java)e sostituire la definizione di processo hello con hello seguente riga:

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <a name="hdinsight-sample-10gb-graysort"></a>Graysort da 10 GB
In questo esempio vengono usati solo 10 GB di dati, in modo da consentire un'esecuzione relativamente rapida. Usa applicazioni MapReduce hello sviluppate da Owen O'Malley e Arun Murthy confermati benchmark ordinamento terabyte hello annuale utilizzo generale ("daytona") nel 2009 con una frequenza di 0.578 TB/min (100 TB in 173 minuti). Per ulteriori informazioni su questo e altri ordinamento benchmark, vedere hello [Sortbenchmark](http://sortbenchmark.org/) sito.

In questo esempio vengono utilizzati tre set di programmi MapReduce:

1. **TeraGen** è un programma MapReduce che è possibile utilizzare le righe di hello toogenerate di toosort di dati.
2. **TeraSort** Campiona i dati di input hello e utilizza i dati di hello toosort MapReduce in totale dell'ordine. TeraSort è un ordinamento standard delle funzioni di MapReduce, ad eccezione di un partitioner che utilizza un elenco ordinato di chiavi di n-1 campionate che definiscono l'intervallo di chiavi hello per ogni riduzione. In particolare, tutte le chiavi questo tipo di esempio [i-1] < = chiave < [i] di esempio vengono inviati tooreduce i. Ciò garantisce che l'output di hello di ridurre i sono tutti minore di output di hello di ridurre i + 1.
3. **TeraValidate** è un programma MapReduce che convalida l'output di hello globale viene ordinato. Crea una mappa per ogni file nella directory di output di hello e ogni mappa garantisce che ogni chiave è minore o uguale toohello precedente. funzione mappa Hello genera anche i record di hello prima e ultima chiavi di ogni file e hello reduce (funzione) garantisce che hello prima chiave del file i è maggiore di hello chiave ultimo di i-1 file. I problemi vengano segnalati come output di hello ridurre con chiavi hello che non sono disponibili.

input Hello e formato di output, utilizzato da tutte e tre le applicazioni, legge e scrive i file di testo hello in formato corretto hello. output di Hello di hello ridurre replica impostati too1, anziché predefinito hello 3, perché concorso benchmark hello non richiede che i dati di output di hello essere replicati nel toomultiple nodi.

Esempio hello, ogni tooone corrispondente di programmi MapReduce hello descritto nell'introduzione di hello, sono necessari tre attività:

1. Generare dati di hello per l'ordinamento eseguendo hello **TeraGen** processo MapReduce.
2. Ordinare i dati di hello eseguendo hello **TeraSort** processo MapReduce.
3. Verificare che i dati hello siano stati ordinati correttamente eseguendo hello **TeraValidate** processo MapReduce.

**processi di hello toosubmit**

* Attenersi alla procedura hello in [Word count - Java](#word-count-java), e utilizzare hello seguendo le definizioni dei processi:

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a>Passaggi successivi
Da questo articolo e gli articoli di hello in ognuno degli esempi di hello, si è appreso come esempi hello toorun incluso hello cluster HDInsight tramite Azure PowerShell. Per le esercitazioni sull'uso Pig, Hive e MapReduce con HDInsight, vedere hello seguenti argomenti:

* [Introduzione all'uso di Hadoop con Hive in uso di HDInsight tooanalyze palmari mobili][hdinsight-get-started]
* [Usare Pig con Hadoop in HDInsight][hdinsight-use-pig]
* [Usare Hive con Hadoop in HDInsight][hdinsight-use-hive]
* [Inviare processi Hadoop in HDInsight][hdinsight-submit-jobs]
* [Documentazione di Azure HDInsight SDK][hdinsight-sdk-documentation]

## <a name="appendix-a---hello-word-count-source-code"></a>Appendice A - hello codice sorgente conteggio di Word

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

## <a name="appendix-b---hello-word-count-streaming-source-code"></a>Appendice B - Conteggio parole hello streaming codice sorgente
programma MapReduce Hello utilizza un'applicazione cat.exe hello come testo hello toostream interfaccia mapping nella console di hello e un'applicazione hello wc.exe come hello ridurre il numero di hello toocount di interfaccia di parole che sono state trasmesse da un documento. Mapper hello sia riduttore di caratteri, riga per riga, di lettura dal flusso di input standard hello (stdin) e scrivere il flusso di output standard toohello (stdout).

```csharp
// hello source code for hello cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

Hello codice mapper hello cat.cs file utilizza un [StreamReader] [ streamreader] caratteri hello tooread hello in arrivo flusso toohello della console di, che quindi scrive hello flusso toohello flusso di output standard dell'oggetto con hello statico [console. WriteLine] [ console-writeline] metodo.

```csharp
// hello source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

Hello codice riduttore hello wc.cs file utilizza un [StreamReader] [ streamreader] tooread caratteri dell'oggetto da hello flusso di input standard che sono stati output mapper cat.exe hello. Durante la lettura di caratteri hello con hello [console. WriteLine] [ console-writeline] (metodo), vengono contate le parole hello contando spazi e caratteri di fine della riga alla fine di hello di ogni parola. Viene quindi scritto come flusso di output standard hello toohello totale con hello [console. WriteLine] [ console-writeline] metodo.

## <a name="appendix-c---hello-pi-estimator-source-code"></a>Appendice C - hello codice sorgente di pi greco estimator
estimator pi Hello codice Java che contiene funzioni di BizTalk mapper e del reducer hello è disponibile per l'ispezione riportato di seguito. programma mapper Hello genera un numero specificato di punti posizionato in modo casuale all'interno di un quadrato dell'unità e quindi conta il numero di hello di tali punti di un cerchio hello. programma riduttore Hello accumula punti conteggiati mediante BizTalk Mapper hello e quindi stima valore hello di pi greco dalla formula 4R hello, dove R è il rapporto di hello del numero di hello di punti conteggiati all'interno di hello cerchio toohello numero totale di punti che si trovano all'interno di quadrato di hello.

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume hello current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of hello inscribed circle of hello square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return hello estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers toohello same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---hello-10gb-graysort-source-code"></a>Appendice D - codice sorgente di hello 10gb graysort
codice Hello per il programma TeraSort MapReduce hello viene presentato per un controllo in questa sezione.

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on hello next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares toofigure out where hello given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up hello rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
