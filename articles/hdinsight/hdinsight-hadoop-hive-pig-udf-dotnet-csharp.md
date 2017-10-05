---
title: Usare C# con Hive e Pig in Hadoop in HDInsight - Azure | Microsoft Docs
description: Informazioni su come usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 58e7af47be71c3e0389e5fb4641e124eb648494e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="d0b5e-103">Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0b5e-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="d0b5e-104">Informazioni su come usare le funzioni definite dall'utente C# con Apache Hive e Pig in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-104">Learn how to use C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0b5e-105">I passaggi descritti in questo documento funzionano con i cluster HDInsight basati su Linux e su Windows.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-105">The steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d0b5e-106">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d0b5e-107">Per altre informazioni, vedere [Componenti e versioni di Hadoop disponibili in HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="d0b5e-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="d0b5e-108">Sia Hive sia Pig sono in grado di passare i dati alle applicazioni esterne per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-108">Both Hive and Pig can pass data to external applications for processing.</span></span> <span data-ttu-id="d0b5e-109">Questo processo è noto come _streaming_.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-109">This process is known as _streaming_.</span></span> <span data-ttu-id="d0b5e-110">Quando si usa un'applicazione .NET, i dati vengono passati all'applicazione su STDIN e l'applicazione restituisce i risultati in STDOUT.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-110">When using a .NET applciation, the data is passed to the application on STDIN, and the application returns the results on STDOUT.</span></span> <span data-ttu-id="d0b5e-111">Per leggere e scrivere da STDIN e STDOUT, è possibile usare `Console.ReadLine()` e `Console.WriteLine()` da un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-111">To read and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0b5e-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d0b5e-112">Prerequisites</span></span>

* <span data-ttu-id="d0b5e-113">Una familiarità nello scrivere e nel compilare il codice C# destinato a .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="d0b5e-114">Usare qualsiasi IDE desiderato.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-114">Use whatever IDE you want.</span></span> <span data-ttu-id="d0b5e-115">Si consigliano [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 o [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="d0b5e-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="d0b5e-116">Nella procedura di questo documento viene usato Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-116">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="d0b5e-117">Un modo per caricare i file con estensione exe nel cluster ed eseguire i processi Pig e Hive.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-117">A way to upload .exe files to the cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="d0b5e-118">Si consigliano gli strumenti Data Lake per Visual Studio, Azure PowerShell e l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-118">We recommend the Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="d0b5e-119">La procedura in questo documento usa gli strumenti Data Lake per Visual Studio per caricare i file ed eseguire l'esempio di query Hive.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-119">The steps in this document use the Data Lake Tools for Visual Studio to upload the files and run the example Hive query.</span></span>

    <span data-ttu-id="d0b5e-120">Per informazioni su altri modi per eseguire query Hive e processi Pig, vedere i seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="d0b5e-120">For information on other ways to run Hive queries and Pig jobs, see the following documents:</span></span>

    * [<span data-ttu-id="d0b5e-121">Usare Apache Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0b5e-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="d0b5e-122">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0b5e-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="d0b5e-123">Un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="d0b5e-124">Per altre informazioni sulla creazione di un cluster, vedere [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="d0b5e-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="d0b5e-125">.NET su HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0b5e-125">.NET on HDInsight</span></span>

* <span data-ttu-id="d0b5e-126">Cluster __HDInsight basati su Linux__ che usano [Mono (https://mono-project.com)](https://mono-project.com) per eseguire le applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="d0b5e-127">La versione mono 4.2.1 è inclusa nella versione 3.5 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="d0b5e-128">Per altre informazioni sulla compatibilità Mono con le versioni di .NET Framework, vedere il documento relativo alla [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="d0b5e-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="d0b5e-129">Per usare una versione specifica di Mono, vedere il documento [Install or update Mono](hdinsight-hadoop-install-mono.md) (Installare o aggiornare Mono).</span><span class="sxs-lookup"><span data-stu-id="d0b5e-129">To use a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="d0b5e-130">I cluster di __HDInsight basato su Windows__ usano Microsoft .NET Common Language Runtime per eseguire le applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-130">__Windows-based HDInsight__ clusters use the Microsoft .NET CLR to run .NET applications.</span></span>

<span data-ttu-id="d0b5e-131">Per altre informazioni sulla versione del framework .NET e di Mono compresa nelle versioni di HDInsight, vedere [Componenti e versioni di Hadoop disponibili in HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="d0b5e-131">For more information on the version of the .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-the-c-projects"></a><span data-ttu-id="d0b5e-132">Creare il progetto C\#</span><span class="sxs-lookup"><span data-stu-id="d0b5e-132">Create the C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="d0b5e-133">UDF di Hive</span><span class="sxs-lookup"><span data-stu-id="d0b5e-133">Hive UDF</span></span>

1. <span data-ttu-id="d0b5e-134">Aprire Visual Studio e creare una soluzione.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="d0b5e-135">Come tipo di progetto selezionare **App console (.NET Framework)** e assegnare al nuovo progetto il nome **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-135">For the project type, select **Console App (.NET Framework)**, and name the new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d0b5e-136">Selezionare __.NET Framework 4.5__ se si usa un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d0b5e-137">Per altre informazioni sulla compatibilità Mono con le versioni di .NET Framework, vedere il documento relativo alla [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="d0b5e-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="d0b5e-138">Sostituire il contenuto del file **Program.cs** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d0b5e-138">Replace the contents of **Program.cs** with the following:</span></span>

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse the string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data to stdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for the given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array to hex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. <span data-ttu-id="d0b5e-139">Compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-139">Build the project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="d0b5e-140">UDF di Pig</span><span class="sxs-lookup"><span data-stu-id="d0b5e-140">Pig UDF</span></span>

1. <span data-ttu-id="d0b5e-141">Aprire Visual Studio e creare una soluzione.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="d0b5e-142">Come tipo di progetto selezionare **Applicazione console** e assegnare al nuovo progetto il nome **PigUDF**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-142">For the project type, select **Console Application**, and name the new project **PigUDF**.</span></span>

2. <span data-ttu-id="d0b5e-143">Sostituire il contenuto del file **Program.cs** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d0b5e-143">Replace the contents of the **Program.cs** file with the following code:</span></span>

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim the error info off the beginning and add a note to the end of the line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split the fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    <span data-ttu-id="d0b5e-144">Questa applicazione analizza le righe inviate da Pig e riformatta quelle che iniziano con `java.lang.Exception`.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-144">This application parses the lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="d0b5e-145">Salvare **Program.cs**e quindi compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-145">Save **Program.cs**, and then build the project.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="d0b5e-146">Caricare nella risorsa di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d0b5e-146">Upload to storage</span></span>

1. <span data-ttu-id="d0b5e-147">In Visual Studio aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="d0b5e-148">Espandere **Azure** e quindi **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="d0b5e-149">Se richiesto, immettere le credenziali della sottoscrizione di Azure, quindi fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="d0b5e-150">Espandere il cluster HDInsight in cui si desidera distribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-150">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="d0b5e-151">Viene elencata una voce con il testo __(Account di archiviazione predefinito)__.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-151">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![Esplora server con account di archiviazione per il cluster](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="d0b5e-153">Se è possibile espandere questa voce, si usa un __Account di archiviazione di Azure__ come risorsa di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="d0b5e-154">Per visualizzare i file nel percorso di archiviazione predefinito per il cluster, espandere la voce e quindi fare doppio clic su __(Contenitore predefinito)__.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-154">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="d0b5e-155">Se non è possibile espandere questa voce, si usa un __Azure Data Lake Store__ come risorsa di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="d0b5e-156">Per visualizzare i file nel percorso di archiviazione predefinito per il cluster, fare doppio clic sulla voce __(Account di archiviazione predefinito)__.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-156">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="d0b5e-157">Per caricare i file con estensione .exe, usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d0b5e-157">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="d0b5e-158">Se si usa un __Account di Archiviazione di Azure__, fare clic sull'icona per il caricamento, quindi passare alla cartella **bin\debug** per il progetto **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-158">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **HiveCSharp** project.</span></span> <span data-ttu-id="d0b5e-159">Selezionare infine il file **HiveCSharp.exe** e fare clic su **Ok**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-159">Finally, select the **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![icona relativa al caricamento](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="d0b5e-161">Se si usa __Azure Data Lake Store__, fare doppio clic su un'area vuota nell'elenco di file e quindi selezionare __Carica__.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-161">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="d0b5e-162">Selezionare infine il file **HiveCSharp.exe** e fare clic su **Apri**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-162">Finally, select the **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="d0b5e-163">Una volta terminato il caricamento di __HiveCSharp.exe__, ripetere il processo di caricamento per il file __PigUDF.exe__.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-163">Once the __HiveCSharp.exe__ upload has finished, repeat the upload process for the __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="d0b5e-164">Eseguire una query Hive</span><span class="sxs-lookup"><span data-stu-id="d0b5e-164">Run a Hive query</span></span>

1. <span data-ttu-id="d0b5e-165">In Visual Studio aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="d0b5e-166">Espandere **Azure** e quindi **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="d0b5e-167">Fare clic con il pulsante destro del mouse sul cluster in cui è stata distribuita l'applicazione **HiveCSharp**, quindi selezionare **Scrivi una query Hive**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-167">Right-click the cluster that you deployed the **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="d0b5e-168">Per la query Hive usare il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="d0b5e-168">Use the following text for the Hive query:</span></span>

    ```hiveql
    -- Uncomment the following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment the following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="d0b5e-169">Rimuovere il commento dell'istruzione `add file` che corrisponde al tipo di archiviazione predefinita usata per il cluster.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-169">Uncomment the `add file` statement that matches the type of default storage used for your cluster.</span></span>

    <span data-ttu-id="d0b5e-170">Questa query seleziona i campi `clientid`, `devicemake` e `devicemodel` da `hivesampletable` e li passa all'applicazione HiveCSharp.exe.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-170">This query selects the `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes the fields to the HiveCSharp.exe application.</span></span> <span data-ttu-id="d0b5e-171">La query si aspetta che l'applicazione restituisca tre campi, che vengono archiviati come `clientid`, `phoneLabel` e `phoneHash`.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-171">The query expects the application to return three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="d0b5e-172">La query prevede anche di trovare HiveCSharp.exe nella radice del contenitore di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-172">The query also expects to find HiveCSharp.exe in the root of the default storage container.</span></span>

5. <span data-ttu-id="d0b5e-173">Fare clic su **Invia** per inviare il processo al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-173">Click **Submit** to submit the job to the HDInsight cluster.</span></span> <span data-ttu-id="d0b5e-174">Viene visualizzata la finestra **Hive Job Summary** (Riepilogo processo Hive).</span><span class="sxs-lookup"><span data-stu-id="d0b5e-174">The **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="d0b5e-175">Fare clic su **Aggiorna** per aggiornare il riepilogo fino all'impostazione del valore **Stato processo** su **Completato**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-175">Click **Refresh** to refresh the summary until **Job Status** changes to **Completed**.</span></span> <span data-ttu-id="d0b5e-176">Per visualizzare l'output del processo, fare clic su **Output processo**.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-176">To view the job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="d0b5e-177">Eseguire un processo Pig</span><span class="sxs-lookup"><span data-stu-id="d0b5e-177">Run a Pig job</span></span>

1. <span data-ttu-id="d0b5e-178">Per connettersi al cluster HDInsight, usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d0b5e-178">Use one of the following methods to connect to your HDInsight cluster:</span></span>

    * <span data-ttu-id="d0b5e-179">Se si usa un cluster HDInsight __basato su Linux__, usare SSH.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="d0b5e-180">Ad esempio, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="d0b5e-181">Per altre informazioni, vedere [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="d0b5e-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="d0b5e-182">Se viene usato un cluster HDInsight __basato su Windows__, [Connettersi a cluster con RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="d0b5e-182">If you are using a __Windows-based__ HDInsight cluster, [Connect to the cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="d0b5e-183">Usare uno dei comandi seguenti per avviare la riga di comando di Pig:</span><span class="sxs-lookup"><span data-stu-id="d0b5e-183">Use one the following command to start the Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="d0b5e-184">Se si usa un cluster basato su Windows, usare invece i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d0b5e-184">If you are using a Windows-based cluster, use the following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="d0b5e-185">Viene visualizzato un prompt `grunt>`.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="d0b5e-186">Immettere il codice seguente per eseguire un processo Pig che usa l'applicazione .NET Framework:</span><span class="sxs-lookup"><span data-stu-id="d0b5e-186">Enter the following to run a Pig job that uses the .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="d0b5e-187">L'istruzione `DEFINE` crea un alias di `streamer` per le applicazioni pigudf.exe e `CACHE` lo carica dalla risorsa di archiviazione per il cluster.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-187">The `DEFINE` statement creates an alias of `streamer` for the pigudf.exe applications, and `CACHE` loads it from default storage for the cluster.</span></span> <span data-ttu-id="d0b5e-188">In seguito, `streamer` viene usato con l'operatore `STREAM` per elaborare le singole righe contenute in LOG e restituire i dati sotto forma di serie di colonne.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-188">Later, `streamer` is used with the `STREAM` operator to process the single lines contained in LOG and return the data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d0b5e-189">Il nome dell'applicazione usato per lo streaming deve essere racchiuso tra caratteri \` (carattere di apice inverso) quando associato ad alias e da ' (virgoletta singola) se usato con `SHIP\`.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-189">The application name that is used for streaming must be surrounded by the \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="d0b5e-190">Dopo l'immissione dell'ultima riga il processo dovrebbe essere avviato.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-190">After entering the last line, the job should start.</span></span> <span data-ttu-id="d0b5e-191">L'output restituito è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="d0b5e-191">It returns output similar to the following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="d0b5e-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0b5e-192">Next steps</span></span>

<span data-ttu-id="d0b5e-193">In questo documento è stato illustrato come usare un'applicazione .NET Framework da Hive e Pig in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0b5e-193">In this document, you have learned how to use a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="d0b5e-194">Per altre informazioni su come usare Python con Hive e Pig, vedere [Usare Python con Hive e Pig in HDInsight](hdinsight-python.md).</span><span class="sxs-lookup"><span data-stu-id="d0b5e-194">If you would like to learn how to use Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="d0b5e-195">Per altre modalità d'uso di Pig e Hive e per informazioni su come usare MapReduce, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d0b5e-195">For other ways to use Pig and Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="d0b5e-196">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0b5e-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d0b5e-197">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0b5e-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d0b5e-198">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0b5e-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
