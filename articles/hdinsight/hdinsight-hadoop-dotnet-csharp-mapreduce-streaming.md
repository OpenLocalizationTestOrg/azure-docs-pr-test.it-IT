---
title: Usare C# con MapReduce in Hadoop in HDInsight - Azure | Microsoft Docs
description: Informazioni su come usare C# per creare soluzioni di MapReduce con Hadoop in HDInsight di Azure.
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
ms.openlocfilehash: adb454e56378a800c671614735aec78b6851aeb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="57fb5-103">Usare C# con lo streaming di MapReduce su Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="57fb5-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="57fb5-104">Informazioni su come usare C# per creare una soluzione di MapReduce su HDInsight.</span><span class="sxs-lookup"><span data-stu-id="57fb5-104">Learn how to use C# to create a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57fb5-105">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="57fb5-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="57fb5-106">Per altre informazioni, vedere [Componenti e versioni di Hadoop disponibili in HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="57fb5-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="57fb5-107">Hadoop streaming è un'utilità che consente di eseguire processi MapReduce tramite uno script o eseguibile.</span><span class="sxs-lookup"><span data-stu-id="57fb5-107">Hadoop streaming is a utility that allows you to run MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="57fb5-108">In questo esempio, .NET è usato per implementare il mapper e il reducer per una soluzione di conteggio parole.</span><span class="sxs-lookup"><span data-stu-id="57fb5-108">In this example, .NET is used to implement the mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="57fb5-109">.NET su HDInsight</span><span class="sxs-lookup"><span data-stu-id="57fb5-109">.NET on HDInsight</span></span>

<span data-ttu-id="57fb5-110">__I cluster HDInsight basati su Linux__ usano [Mono (https://mono-project.com)](https://mono-project.com) per eseguire le applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="57fb5-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="57fb5-111">La versione Mono 4.2.1 è inclusa nella versione 3.5 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="57fb5-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="57fb5-112">Per altre informazioni sulla versione Mono compresa in HDInsight, vedere [Componenti e versioni di Hadoop disponibili in HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="57fb5-112">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="57fb5-113">Per usare una versione specifica di Mono, vedere il documento [Install or update Mono](hdinsight-hadoop-install-mono.md) (Installare o aggiornare Mono).</span><span class="sxs-lookup"><span data-stu-id="57fb5-113">To use a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="57fb5-114">Per altre informazioni sulla compatibilità Mono con le versioni di .NET Framework, vedere il documento relativo alla [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="57fb5-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="57fb5-115">Come funziona lo streaming di Hadoop</span><span class="sxs-lookup"><span data-stu-id="57fb5-115">How Hadoop streaming works</span></span>

<span data-ttu-id="57fb5-116">Il processo di base usato per il flusso in questo documento è il seguente:</span><span class="sxs-lookup"><span data-stu-id="57fb5-116">The basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="57fb5-117">Hadoop passa i dati al mapper (mapper.exe in questo esempio) su STDIN.</span><span class="sxs-lookup"><span data-stu-id="57fb5-117">Hadoop passes data to the mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="57fb5-118">Il mapper elabora i dati ed emette una coppia chiave/valore delimitata da tabulazione su STDOUT.</span><span class="sxs-lookup"><span data-stu-id="57fb5-118">The mapper processes the data, and emits tab-delimited key/value pairs to STDOUT.</span></span>
3. <span data-ttu-id="57fb5-119">L'output viene letto da Hadoop e quindi passato al riduttore (reducer.exe in questo esempio) su STDIN.</span><span class="sxs-lookup"><span data-stu-id="57fb5-119">The output is read by Hadoop, and then passed to the reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="57fb5-120">Il riduttore legge le coppie chiave/valore delimitate da tabulazioni, elabora i dati e quindi genera il risultato come coppie chiave/valore delimitate da tabulazione su STDOUT.</span><span class="sxs-lookup"><span data-stu-id="57fb5-120">The reducer reads the tab-delimited key/value pairs, processes the data, and then emits the result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="57fb5-121">L'output viene letto da Hadoop e scritto nella directory di output.</span><span class="sxs-lookup"><span data-stu-id="57fb5-121">The output is read by Hadoop and written to the output directory.</span></span>

<span data-ttu-id="57fb5-122">Per altre informazioni sui flussi, vedere il documento [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span><span class="sxs-lookup"><span data-stu-id="57fb5-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57fb5-123">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="57fb5-123">Prerequisites</span></span>

* <span data-ttu-id="57fb5-124">Una familiarità nello scrivere e nel compilare il codice C# destinato a .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="57fb5-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="57fb5-125">Nella procedura di questo documento viene usato Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="57fb5-125">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="57fb5-126">Un modo per caricare i file .exe sul cluster.</span><span class="sxs-lookup"><span data-stu-id="57fb5-126">A way to upload .exe files to the cluster.</span></span> <span data-ttu-id="57fb5-127">La procedura in questo documento usa gli strumenti Data Lake per Visual Studio per caricare i file nell'archiviazione primaria per il cluster.</span><span class="sxs-lookup"><span data-stu-id="57fb5-127">The steps in this document use the Data Lake Tools for Visual Studio to upload the files to primary storage for the cluster.</span></span>

* <span data-ttu-id="57fb5-128">Azure PowerShell o un client SSH.</span><span class="sxs-lookup"><span data-stu-id="57fb5-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="57fb5-129">Un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="57fb5-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="57fb5-130">Per altre informazioni sulla creazione di un cluster, vedere [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="57fb5-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-the-mapper"></a><span data-ttu-id="57fb5-131">Creare il mapper</span><span class="sxs-lookup"><span data-stu-id="57fb5-131">Create the mapper</span></span>

<span data-ttu-id="57fb5-132">In Visual Studio creare una nuova __applicazione console__ denominata __mapper__.</span><span class="sxs-lookup"><span data-stu-id="57fb5-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="57fb5-133">Usare il codice seguente per l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="57fb5-133">Use the following code for the application:</span></span>

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
            //Hadoop passes data to the mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over the words
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

<span data-ttu-id="57fb5-134">Dopo aver creato l'applicazione, compilarla per produrre il file `/bin/Debug/mapper.exe` nella directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="57fb5-134">After creating the application, build it to produce the `/bin/Debug/mapper.exe` file in the project directory.</span></span>

## <a name="create-the-reducer"></a><span data-ttu-id="57fb5-135">Creare il reducer</span><span class="sxs-lookup"><span data-stu-id="57fb5-135">Create the reducer</span></span>

<span data-ttu-id="57fb5-136">In Visual Studio creare una nuova __applicazione console__ denominata __reducer__.</span><span class="sxs-lookup"><span data-stu-id="57fb5-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="57fb5-137">Usare il codice seguente per l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="57fb5-137">Use the following code for the application:</span></span>

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
                // Get the word
                string word = sArr[0];
                // Get the count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for the word?
                if(words.ContainsKey(word))
                {
                    //If so, increment the count
                    words[word] += count;
                } else
                {
                    //Add the key to the collection
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

<span data-ttu-id="57fb5-138">Dopo aver creato l'applicazione, compilarla per produrre il file `/bin/Debug/reducer.exe` nella directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="57fb5-138">After creating the application, build it to produce the `/bin/Debug/reducer.exe` file in the project directory.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="57fb5-139">Caricare nella risorsa di archiviazione</span><span class="sxs-lookup"><span data-stu-id="57fb5-139">Upload to storage</span></span>

1. <span data-ttu-id="57fb5-140">In Visual Studio aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="57fb5-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="57fb5-141">Espandere **Azure** e quindi **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="57fb5-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="57fb5-142">Se richiesto, immettere le credenziali della sottoscrizione di Azure, quindi fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="57fb5-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="57fb5-143">Espandere il cluster HDInsight in cui si desidera distribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57fb5-143">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="57fb5-144">Viene elencata una voce con il testo __(Account di archiviazione predefinito)__.</span><span class="sxs-lookup"><span data-stu-id="57fb5-144">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![Esplora server con account di archiviazione per il cluster](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="57fb5-146">Se è possibile espandere questa voce, si usa un __Account di archiviazione di Azure__ come risorsa di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="57fb5-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="57fb5-147">Per visualizzare i file nel percorso di archiviazione predefinito per il cluster, espandere la voce e quindi fare doppio clic su __(Contenitore predefinito)__.</span><span class="sxs-lookup"><span data-stu-id="57fb5-147">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="57fb5-148">Se non è possibile espandere questa voce, si usa un __Azure Data Lake Store__ come risorsa di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="57fb5-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="57fb5-149">Per visualizzare i file nel percorso di archiviazione predefinito per il cluster, fare doppio clic sulla voce __(Account di archiviazione predefinito)__.</span><span class="sxs-lookup"><span data-stu-id="57fb5-149">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="57fb5-150">Per caricare i file con estensione .exe, usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="57fb5-150">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="57fb5-151">Se si usa un __Account di Archiviazione di Azure__, fare clic sull'icona per il caricamento, quindi passare alla cartella **bin\debug** per il progetto **mapper**.</span><span class="sxs-lookup"><span data-stu-id="57fb5-151">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **mapper** project.</span></span> <span data-ttu-id="57fb5-152">Selezionare infine il file **mapper.exe** e fare clic su **Ok**.</span><span class="sxs-lookup"><span data-stu-id="57fb5-152">Finally, select the **mapper.exe** file and click **Ok**.</span></span>

        ![icona relativa al caricamento](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="57fb5-154">Se si usa __Azure Data Lake Store__, fare doppio clic su un'area vuota nell'elenco di file e quindi selezionare __Carica__.</span><span class="sxs-lookup"><span data-stu-id="57fb5-154">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="57fb5-155">Selezionare infine il file **mapper.exe** e fare clic su **Apri**.</span><span class="sxs-lookup"><span data-stu-id="57fb5-155">Finally, select the **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="57fb5-156">Una volta terminato il caricamento __mapper.exe__, ripetere il processo di caricamento per il file __reducer.exe__.</span><span class="sxs-lookup"><span data-stu-id="57fb5-156">Once the __mapper.exe__ upload has finished, repeat the upload process for the __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="57fb5-157">Eseguire un processo: uso di una sessione SSH</span><span class="sxs-lookup"><span data-stu-id="57fb5-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="57fb5-158">Connettersi al cluster HDInsight usando SSH.</span><span class="sxs-lookup"><span data-stu-id="57fb5-158">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="57fb5-159">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="57fb5-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="57fb5-160">Usare uno dei seguenti comandi per avviare il processo MapReduce:</span><span class="sxs-lookup"><span data-stu-id="57fb5-160">Use one of the following command to start the MapReduce job:</span></span>

    * <span data-ttu-id="57fb5-161">Se si usa __Azure Data Lake Store__ come risorsa di archiviazione predefinita:</span><span class="sxs-lookup"><span data-stu-id="57fb5-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="57fb5-162">Se si usa __Archiviazione di Azure__ come risorsa di archiviazione predefinita:</span><span class="sxs-lookup"><span data-stu-id="57fb5-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="57fb5-163">L'elenco seguente descrive le operazioni eseguite da ogni parametro:</span><span class="sxs-lookup"><span data-stu-id="57fb5-163">The following list describes what each parameter does:</span></span>

    * <span data-ttu-id="57fb5-164">`hadoop-streaming.jar`: il file con estensione jar che contiene la funzionalità di streaming MapReduce.</span><span class="sxs-lookup"><span data-stu-id="57fb5-164">`hadoop-streaming.jar`: The jar file that contains the streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="57fb5-165">`-files`: aggiunge i file `mapper.exe` e `reducer.exe` a questo processo.</span><span class="sxs-lookup"><span data-stu-id="57fb5-165">`-files`: Adds the `mapper.exe` and `reducer.exe` files to this job.</span></span> <span data-ttu-id="57fb5-166">`adl:///` o `wasb:///` prima di ogni file rappresenta il percorso della radice di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="57fb5-166">The `adl:///` or `wasb:///` before each file is the path to the root of default storage for the cluster.</span></span>
    * <span data-ttu-id="57fb5-167">`-mapper`: specifica il file che implementa il mapper.</span><span class="sxs-lookup"><span data-stu-id="57fb5-167">`-mapper`: Specifies which file implements the mapper.</span></span>
    * <span data-ttu-id="57fb5-168">`-reducer`: specifica il file che implementa il reducer.</span><span class="sxs-lookup"><span data-stu-id="57fb5-168">`-reducer`: Specifies which file implements the reducer.</span></span>
    * <span data-ttu-id="57fb5-169">`-input`: dati di input.</span><span class="sxs-lookup"><span data-stu-id="57fb5-169">`-input`: The input data.</span></span>
    * <span data-ttu-id="57fb5-170">`-output`: directory di output.</span><span class="sxs-lookup"><span data-stu-id="57fb5-170">`-output`: The output directory.</span></span>

3. <span data-ttu-id="57fb5-171">Dopo il completamento del processo di MapReduce, usare il comando seguente per visualizzare i risultati:</span><span class="sxs-lookup"><span data-stu-id="57fb5-171">Once the MapReduce job completes, use the following to view the results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="57fb5-172">L'elenco seguente è un esempio dei dati restituiti da questo comando:</span><span class="sxs-lookup"><span data-stu-id="57fb5-172">The following text is an example of the data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="57fb5-173">Esecuzione di un processo: Uso di PowerShell</span><span class="sxs-lookup"><span data-stu-id="57fb5-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="57fb5-174">Usare il seguente script di PowerShell per eseguire un processo MapReduce e scaricare i risultati.</span><span class="sxs-lookup"><span data-stu-id="57fb5-174">Use the following PowerShell script to run a MapReduce job and download the results.</span></span>

<span data-ttu-id="57fb5-175">[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span><span class="sxs-lookup"><span data-stu-id="57fb5-175">[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span></span>

<span data-ttu-id="57fb5-176">Questo script richiede l'account di accesso del cluster e la password, insieme al nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="57fb5-176">This script prompts you for the cluster login account name and password, along with the HDInsight cluster name.</span></span> <span data-ttu-id="57fb5-177">Al termine del processo, l'output è scaricato nel file `output.txt` nella directory da cui viene eseguito lo script.</span><span class="sxs-lookup"><span data-stu-id="57fb5-177">Once the job completes, the output is downloaded to the `output.txt` file in the directory the script is ran from.</span></span> <span data-ttu-id="57fb5-178">Il testo seguente è un esempio dei dati nel file `output.txt`:</span><span class="sxs-lookup"><span data-stu-id="57fb5-178">The following text is an example of the data in the `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="57fb5-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57fb5-179">Next steps</span></span>

<span data-ttu-id="57fb5-180">Per altre informazioni sull'uso di MapReduce con HDInsight, vedere l'articolo [Usare MapReduce in Hadoop su HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="57fb5-180">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="57fb5-181">Per informazioni sull'uso di C# con Hive e Pig, vedere [Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="57fb5-181">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="57fb5-182">Per informazioni sull'uso di C# con Storm in HDInsight tramite, vedere [Sviluppare topologie C# per Apache Storm in HDInsight tramite gli strumenti Hadoop per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="57fb5-182">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>