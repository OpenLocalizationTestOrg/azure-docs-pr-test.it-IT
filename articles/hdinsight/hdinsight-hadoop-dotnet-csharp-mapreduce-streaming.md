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
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="5c2aa-103">Usare C# con lo streaming di MapReduce su Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5c2aa-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="5c2aa-104">Informazioni su come toouse c# toocreate una soluzione di MapReduce in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-104">Learn how toouse C# toocreate a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c2aa-105">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5c2aa-106">Per altre informazioni, vedere l'articolo sul [controllo delle versioni del componente di HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="5c2aa-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="5c2aa-107">Streaming di Hadoop è un'utilità che consente i processi MapReduce toorun utilizzando uno script o un file eseguibile.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-107">Hadoop streaming is a utility that allows you toorun MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="5c2aa-108">In questo esempio, .NET è utilizzata tooimplement hello mapper e riduttore per una soluzione di conteggio di word.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-108">In this example, .NET is used tooimplement hello mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="5c2aa-109">.NET su HDInsight</span><span class="sxs-lookup"><span data-stu-id="5c2aa-109">.NET on HDInsight</span></span>

<span data-ttu-id="5c2aa-110">__HDInsight basati su Linux__ cluster utilizzare [Mono (https://mono-project.com)](https://mono-project.com) toorun le applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="5c2aa-111">La versione Mono 4.2.1 è inclusa nella versione 3.5 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="5c2aa-112">Per ulteriori informazioni sulla versione di hello di Mono incluso in HDInsight, vedere [versioni dei componenti di HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="5c2aa-112">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="5c2aa-113">toouse una versione specifica di Mono, vedere hello [installazione o aggiornamento Mono](hdinsight-hadoop-install-mono.md) documento.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-113">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="5c2aa-114">Per altre informazioni sulla compatibilità Mono con le versioni di .NET Framework, vedere il documento relativo alla [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="5c2aa-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="5c2aa-115">Come funziona lo streaming di Hadoop</span><span class="sxs-lookup"><span data-stu-id="5c2aa-115">How Hadoop streaming works</span></span>

<span data-ttu-id="5c2aa-116">il processo di base Hello utilizzato per i flussi in questo documento è il seguente:</span><span class="sxs-lookup"><span data-stu-id="5c2aa-116">hello basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="5c2aa-117">STDIN Hadoop Invia mapping dei dati toohello (mapper.exe in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="5c2aa-117">Hadoop passes data toohello mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="5c2aa-118">mapper Hello elabora i dati di hello e genera tooSTDOUT di coppie chiave/valore delimitato da tabulazioni.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-118">hello mapper processes hello data, and emits tab-delimited key/value pairs tooSTDOUT.</span></span>
3. <span data-ttu-id="5c2aa-119">output di Hello letta da Hadoop e quindi passato riduttore toohello (reducer.exe in questo esempio) su STDIN.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-119">hello output is read by Hadoop, and then passed toohello reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="5c2aa-120">riduttore Hello legge le coppie chiave/valore hello delimitato da tabulazione, elabora i dati di hello e quindi genera risultati hello come coppie chiave/valore delimitato da tabulazione in STDOUT.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-120">hello reducer reads hello tab-delimited key/value pairs, processes hello data, and then emits hello result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="5c2aa-121">output di Hello letta Hadoop e scritta toohello directory di output.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-121">hello output is read by Hadoop and written toohello output directory.</span></span>

<span data-ttu-id="5c2aa-122">Per altre informazioni sui flussi, vedere il documento [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span><span class="sxs-lookup"><span data-stu-id="5c2aa-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c2aa-123">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5c2aa-123">Prerequisites</span></span>

* <span data-ttu-id="5c2aa-124">Una familiarità nello scrivere e nel compilare il codice C# destinato a .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="5c2aa-125">Hello passaggi di questo utilizzo di documento, Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-125">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="5c2aa-126">Un cluster di toohello file modo tooupload .exe.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-126">A way tooupload .exe files toohello cluster.</span></span> <span data-ttu-id="5c2aa-127">Hello passaggi in questo documento usano hello Data Lake Tools per Visual Studio tooupload hello file tooprimary spazio di memorizzazione per i cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-127">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files tooprimary storage for hello cluster.</span></span>

* <span data-ttu-id="5c2aa-128">Azure PowerShell o un client SSH.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="5c2aa-129">Un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="5c2aa-130">Per altre informazioni sulla creazione di un cluster, vedere [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5c2aa-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-hello-mapper"></a><span data-ttu-id="5c2aa-131">Creare il mapper hello</span><span class="sxs-lookup"><span data-stu-id="5c2aa-131">Create hello mapper</span></span>

<span data-ttu-id="5c2aa-132">In Visual Studio creare una nuova __applicazione console__ denominata __mapper__.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="5c2aa-133">Utilizzare hello seguente codice per un'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="5c2aa-133">Use hello following code for hello application:</span></span>

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

<span data-ttu-id="5c2aa-134">Dopo aver creato un'applicazione hello, compilarlo hello tooproduce `/bin/Debug/mapper.exe` file nella directory di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-134">After creating hello application, build it tooproduce hello `/bin/Debug/mapper.exe` file in hello project directory.</span></span>

## <a name="create-hello-reducer"></a><span data-ttu-id="5c2aa-135">Creare riduttore hello</span><span class="sxs-lookup"><span data-stu-id="5c2aa-135">Create hello reducer</span></span>

<span data-ttu-id="5c2aa-136">In Visual Studio creare una nuova __applicazione console__ denominata __reducer__.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="5c2aa-137">Utilizzare hello seguente codice per un'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="5c2aa-137">Use hello following code for hello application:</span></span>

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

<span data-ttu-id="5c2aa-138">Dopo aver creato un'applicazione hello, compilarlo hello tooproduce `/bin/Debug/reducer.exe` file nella directory di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-138">After creating hello application, build it tooproduce hello `/bin/Debug/reducer.exe` file in hello project directory.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="5c2aa-139">Caricare toostorage</span><span class="sxs-lookup"><span data-stu-id="5c2aa-139">Upload toostorage</span></span>

1. <span data-ttu-id="5c2aa-140">In Visual Studio aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="5c2aa-141">Espandere **Azure** e quindi **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="5c2aa-142">Se richiesto, immettere le credenziali della sottoscrizione di Azure, quindi fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="5c2aa-143">Espandere i cluster HDInsight hello che si desidera toodeploy per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-143">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="5c2aa-144">Una voce con il testo hello __(Account di archiviazione predefinito)__ è elencato.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-144">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Esplora server con l'account di archiviazione hello per cluster hello](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="5c2aa-146">Se questa voce può essere espanso, si utilizza un __Account di archiviazione Azure__ come spazio di archiviazione predefinito per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="5c2aa-147">tooview hello i file di archiviazione predefiniti hello per cluster hello, espandere la voce hello e quindi fare doppio clic su hello __(contenitore predefinito)__.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-147">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="5c2aa-148">Se non è possibile espandere questa voce, si utilizza __archivio Azure Data Lake__ come spazio di archiviazione predefinito hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="5c2aa-149">file di hello tooview in spazio di archiviazione predefinito hello for cluster hello, fare doppio clic su hello __(Account di archiviazione predefinito)__ voce.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-149">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="5c2aa-150">file di .exe tooupload hello, utilizzare uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="5c2aa-150">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="5c2aa-151">Se si utilizza un __Account di archiviazione Azure__, fare clic sull'icona di caricamento hello e quindi selezionare toohello **bin\debug** cartella per hello **mapper** progetto.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-151">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **mapper** project.</span></span> <span data-ttu-id="5c2aa-152">Infine, selezionare hello **mapper.exe** file e fare clic su **Ok**.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-152">Finally, select hello **mapper.exe** file and click **Ok**.</span></span>

        ![icona relativa al caricamento](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="5c2aa-154">Se si utilizza __archivio Azure Data Lake__, fare doppio clic su un'area vuota nell'elenco di file hello e quindi selezionare __caricare__.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-154">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="5c2aa-155">Infine, selezionare hello **mapper.exe** file e fare clic su **aprire**.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-155">Finally, select hello **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="5c2aa-156">Una volta hello __mapper.exe__ ha completato il caricamento, il processo di caricamento hello ripetizione per hello __reducer.exe__ file.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-156">Once hello __mapper.exe__ upload has finished, repeat hello upload process for hello __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="5c2aa-157">Eseguire un processo: uso di una sessione SSH</span><span class="sxs-lookup"><span data-stu-id="5c2aa-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="5c2aa-158">Utilizzare cluster di HDInsight toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-158">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="5c2aa-159">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5c2aa-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="5c2aa-160">Utilizzare uno dei hello processo MapReduce hello toostart il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5c2aa-160">Use one of hello following command toostart hello MapReduce job:</span></span>

    * <span data-ttu-id="5c2aa-161">Se si usa __Azure Data Lake Store__ come risorsa di archiviazione predefinita:</span><span class="sxs-lookup"><span data-stu-id="5c2aa-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="5c2aa-162">Se si usa __Archiviazione di Azure__ come risorsa di archiviazione predefinita:</span><span class="sxs-lookup"><span data-stu-id="5c2aa-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="5c2aa-163">Hello seguente elenco descrive lo scopo ogni parametro:</span><span class="sxs-lookup"><span data-stu-id="5c2aa-163">hello following list describes what each parameter does:</span></span>

    * <span data-ttu-id="5c2aa-164">`hadoop-streaming.jar`: file jar hello contenente hello MapReduce funzionalità dei flussi.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-164">`hadoop-streaming.jar`: hello jar file that contains hello streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="5c2aa-165">`-files`: Aggiunge hello `mapper.exe` e `reducer.exe` processo toothis file.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-165">`-files`: Adds hello `mapper.exe` and `reducer.exe` files toothis job.</span></span> <span data-ttu-id="5c2aa-166">Hello `adl:///` o `wasb:///` prima di ogni file è una radice di toohello hello percorso di archiviazione predefinita per i cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-166">hello `adl:///` or `wasb:///` before each file is hello path toohello root of default storage for hello cluster.</span></span>
    * <span data-ttu-id="5c2aa-167">`-mapper`: Specifica il file implementa mapper hello.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-167">`-mapper`: Specifies which file implements hello mapper.</span></span>
    * <span data-ttu-id="5c2aa-168">`-reducer`: Specifica il file implementa riduttore hello.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-168">`-reducer`: Specifies which file implements hello reducer.</span></span>
    * <span data-ttu-id="5c2aa-169">`-input`: hello dati di input.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-169">`-input`: hello input data.</span></span>
    * <span data-ttu-id="5c2aa-170">`-output`: directory di output di hello.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-170">`-output`: hello output directory.</span></span>

3. <span data-ttu-id="5c2aa-171">Al termine del processo MapReduce hello, utilizzare hello risultati hello tooview seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c2aa-171">Once hello MapReduce job completes, use hello following tooview hello results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="5c2aa-172">Hello testo riportato di seguito è riportato un esempio di dati hello restituiti da questo comando:</span><span class="sxs-lookup"><span data-stu-id="5c2aa-172">hello following text is an example of hello data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="5c2aa-173">Esecuzione di un processo: Uso di PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c2aa-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="5c2aa-174">Utilizzare la seguente script di PowerShell toorun un processo MapReduce hello e scaricare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-174">Use hello following PowerShell script toorun a MapReduce job and download hello results.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

<span data-ttu-id="5c2aa-175">Questo script viene chiesta hello cluster nome account e password, insieme al nome del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-175">This script prompts you for hello cluster login account name and password, along with hello HDInsight cluster name.</span></span> <span data-ttu-id="5c2aa-176">Al termine del processo di hello, l'output di hello è scaricato toohello `output.txt` file nello script di hello hello directory è stato eseguito da.</span><span class="sxs-lookup"><span data-stu-id="5c2aa-176">Once hello job completes, hello output is downloaded toohello `output.txt` file in hello directory hello script is ran from.</span></span> <span data-ttu-id="5c2aa-177">testo Hello è riportato un esempio di dati hello in hello `output.txt` file:</span><span class="sxs-lookup"><span data-stu-id="5c2aa-177">hello following text is an example of hello data in hello `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="5c2aa-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c2aa-178">Next steps</span></span>

<span data-ttu-id="5c2aa-179">Per altre informazioni sull'uso di MapReduce con HDInsight, vedere l'articolo [Usare MapReduce in Hadoop su HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="5c2aa-179">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="5c2aa-180">Per informazioni sull'uso di C# con Hive e Pig, vedere [Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="5c2aa-180">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="5c2aa-181">Per informazioni sull'uso di C# con Storm in HDInsight tramite, vedere [Sviluppare topologie C# per Apache Storm in HDInsight tramite gli strumenti Hadoop per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="5c2aa-181">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>