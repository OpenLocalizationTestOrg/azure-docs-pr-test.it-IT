---
title: aaaUse c# con MapReduce in Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse c# toocreate MapReduce soluzioni con Hadoop in HDInsight di Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a>Usare C# con lo streaming di MapReduce su Hadoop in HDInsight

Informazioni su come toouse c# toocreate una soluzione di MapReduce in HDInsight.

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere l'articolo sul [controllo delle versioni del componente di HDInsight](hdinsight-component-versioning.md).

Streaming di Hadoop è un'utilità che consente i processi MapReduce toorun utilizzando uno script o un file eseguibile. In questo esempio, .NET è utilizzata tooimplement hello mapper e riduttore per una soluzione di conteggio di word.

## <a name="net-on-hdinsight"></a>.NET su HDInsight

__HDInsight basati su Linux__ cluster utilizzare [Mono (https://mono-project.com)](https://mono-project.com) toorun le applicazioni .NET. La versione Mono 4.2.1 è inclusa nella versione 3.5 di HDInsight. Per ulteriori informazioni sulla versione di hello di Mono incluso in HDInsight, vedere [versioni dei componenti di HDInsight](hdinsight-component-versioning.md). toouse una versione specifica di Mono, vedere hello [installazione o aggiornamento Mono](hdinsight-hadoop-install-mono.md) documento.

Per altre informazioni sulla compatibilità Mono con le versioni di .NET Framework, vedere il documento relativo alla [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

## <a name="how-hadoop-streaming-works"></a>Come funziona lo streaming di Hadoop

il processo di base Hello utilizzato per i flussi in questo documento è il seguente:

1. STDIN Hadoop Invia mapping dei dati toohello (mapper.exe in questo esempio).
2. mapper Hello elabora i dati di hello e genera tooSTDOUT di coppie chiave/valore delimitato da tabulazioni.
3. output di Hello letta da Hadoop e quindi passato riduttore toohello (reducer.exe in questo esempio) su STDIN.
4. riduttore Hello legge le coppie chiave/valore hello delimitato da tabulazione, elabora i dati di hello e quindi genera risultati hello come coppie chiave/valore delimitato da tabulazione in STDOUT.
5. output di Hello letta Hadoop e scritta toohello directory di output.

Per altre informazioni sui flussi, vedere il documento [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).

## <a name="prerequisites"></a>Prerequisiti

* Una familiarità nello scrivere e nel compilare il codice C# destinato a .NET Framework 4.5. Hello passaggi di questo utilizzo di documento, Visual Studio 2017.

* Un cluster di toohello file modo tooupload .exe. Hello passaggi in questo documento usano hello Data Lake Tools per Visual Studio tooupload hello file tooprimary spazio di memorizzazione per i cluster di hello.

* Azure PowerShell o un client SSH.

* Un cluster Hadoop in HDInsight. Per altre informazioni sulla creazione di un cluster, vedere [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md).

## <a name="create-hello-mapper"></a>Creare il mapper hello

In Visual Studio creare una nuova __applicazione console__ denominata __mapper__. Utilizzare hello seguente codice per un'applicazione hello:

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

Dopo aver creato un'applicazione hello, compilarlo hello tooproduce `/bin/Debug/mapper.exe` file nella directory di progetto hello.

## <a name="create-hello-reducer"></a>Creare riduttore hello

In Visual Studio creare una nuova __applicazione console__ denominata __reducer__. Utilizzare hello seguente codice per un'applicazione hello:

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

Dopo aver creato un'applicazione hello, compilarlo hello tooproduce `/bin/Debug/reducer.exe` file nella directory di progetto hello.

## <a name="upload-toostorage"></a>Caricare toostorage

1. In Visual Studio aprire **Esplora server**.

2. Espandere **Azure** e quindi **HDInsight**.

3. Se richiesto, immettere le credenziali della sottoscrizione di Azure, quindi fare clic su **Accedi**.

4. Espandere i cluster HDInsight hello che si desidera toodeploy per questa applicazione. Una voce con il testo hello __(Account di archiviazione predefinito)__ è elencato.

    ![Esplora server con l'account di archiviazione hello per cluster hello](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Se questa voce può essere espanso, si utilizza un __Account di archiviazione Azure__ come spazio di archiviazione predefinito per il cluster hello. tooview hello i file di archiviazione predefiniti hello per cluster hello, espandere la voce hello e quindi fare doppio clic su hello __(contenitore predefinito)__.

    * Se non è possibile espandere questa voce, si utilizza __archivio Azure Data Lake__ come spazio di archiviazione predefinito hello per cluster hello. file di hello tooview in spazio di archiviazione predefinito hello for cluster hello, fare doppio clic su hello __(Account di archiviazione predefinito)__ voce.

5. file di .exe tooupload hello, utilizzare uno dei seguenti metodi hello:

    * Se si utilizza un __Account di archiviazione Azure__, fare clic sull'icona di caricamento hello e quindi selezionare toohello **bin\debug** cartella per hello **mapper** progetto. Infine, selezionare hello **mapper.exe** file e fare clic su **Ok**.

        ![icona relativa al caricamento](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Se si utilizza __archivio Azure Data Lake__, fare doppio clic su un'area vuota nell'elenco di file hello e quindi selezionare __caricare__. Infine, selezionare hello **mapper.exe** file e fare clic su **aprire**.

    Una volta hello __mapper.exe__ ha completato il caricamento, il processo di caricamento hello ripetizione per hello __reducer.exe__ file.

## <a name="run-a-job-using-an-ssh-session"></a>Eseguire un processo: uso di una sessione SSH

1. Utilizzare cluster di HDInsight toohello tooconnect SSH. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Utilizzare uno dei hello processo MapReduce hello toostart il comando seguente:

    * Se si usa __Azure Data Lake Store__ come risorsa di archiviazione predefinita:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * Se si usa __Archiviazione di Azure__ come risorsa di archiviazione predefinita:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    Hello seguente elenco descrive lo scopo ogni parametro:

    * `hadoop-streaming.jar`: file jar hello contenente hello MapReduce funzionalità dei flussi.
    * `-files`: Aggiunge hello `mapper.exe` e `reducer.exe` processo toothis file. Hello `adl:///` o `wasb:///` prima di ogni file è una radice di toohello hello percorso di archiviazione predefinita per i cluster di hello.
    * `-mapper`: Specifica il file implementa mapper hello.
    * `-reducer`: Specifica il file implementa riduttore hello.
    * `-input`: hello dati di input.
    * `-output`: directory di output di hello.

3. Al termine del processo MapReduce hello, utilizzare hello risultati hello tooview seguenti:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Hello testo riportato di seguito è riportato un esempio di dati hello restituiti da questo comando:

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a>Esecuzione di un processo: Uso di PowerShell

Utilizzare la seguente script di PowerShell toorun un processo MapReduce hello e scaricare i risultati di hello.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

Questo script viene chiesta hello cluster nome account e password, insieme al nome del cluster HDInsight hello. Al termine del processo di hello, l'output di hello è scaricato toohello `output.txt` file nello script di hello hello directory è stato eseguito da. testo Hello è riportato un esempio di dati hello in hello `output.txt` file:

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'uso di MapReduce con HDInsight, vedere l'articolo [Usare MapReduce in Hadoop su HDInsight](hdinsight-use-mapreduce.md).

Per informazioni sull'uso di C# con Hive e Pig, vedere [Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).

Per informazioni sull'uso di C# con Storm in HDInsight tramite, vedere [Sviluppare topologie C# per Apache Storm in HDInsight tramite gli strumenti Hadoop per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).