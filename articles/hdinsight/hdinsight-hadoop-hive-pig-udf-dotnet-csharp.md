---
title: aaaUse c# con Hive e Pig in Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse c# definito dall'utente (UDF) di funzioni con Hive e Pig streaming in Azure HDInsight.
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
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="7d0a8-103">Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d0a8-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="7d0a8-104">Informazioni su come toouse c# funzioni definite dall'utente (UDF) con Apache Hive e Pig in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-104">Learn how toouse C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d0a8-105">passaggi di Hello in questo documento di lavoro con i cluster HDInsight basati su Linux sia basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-105">hello steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="7d0a8-106">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7d0a8-107">Per altre informazioni, vedere l'articolo sul [controllo delle versioni del componente di HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="7d0a8-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="7d0a8-108">Entrambi Hive e Pig passare applicazioni tooexternal dati per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-108">Both Hive and Pig can pass data tooexternal applications for processing.</span></span> <span data-ttu-id="7d0a8-109">Questo processo è noto come _streaming_.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-109">This process is known as _streaming_.</span></span> <span data-ttu-id="7d0a8-110">Quando si utilizza un'applicazione .NET, i dati di hello vengono trasferiti toohello applicazione STDIN e un'applicazione hello restituisce i risultati di hello in STDOUT.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-110">When using a .NET applciation, hello data is passed toohello application on STDIN, and hello application returns hello results on STDOUT.</span></span> <span data-ttu-id="7d0a8-111">tooread e scrittura da STDIN e STDOUT, è possibile utilizzare `Console.ReadLine()` e `Console.WriteLine()` da un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-111">tooread and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d0a8-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7d0a8-112">Prerequisites</span></span>

* <span data-ttu-id="7d0a8-113">Una familiarità nello scrivere e nel compilare il codice C# destinato a .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="7d0a8-114">Usare qualsiasi IDE desiderato.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-114">Use whatever IDE you want.</span></span> <span data-ttu-id="7d0a8-115">Si consigliano [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 o [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="7d0a8-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="7d0a8-116">Hello passaggi di questo utilizzo di documento, Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-116">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="7d0a8-117">Un .exe tooupload modo file toohello cluster ed esecuzione di processi Pig e Hive.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-117">A way tooupload .exe files toohello cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="7d0a8-118">È consigliabile hello Data Lake Tools per Visual Studio, Azure PowerShell e CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-118">We recommend hello Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="7d0a8-119">Hello passaggi descritti in questo documento utilizzano gli strumenti di hello Data Lake per i file di Visual Studio tooupload hello ed eseguire query Hive di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-119">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files and run hello example Hive query.</span></span>

    <span data-ttu-id="7d0a8-120">Per informazioni su altre query Hive toorun di modi e processi Pig, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="7d0a8-120">For information on other ways toorun Hive queries and Pig jobs, see hello following documents:</span></span>

    * [<span data-ttu-id="7d0a8-121">Usare Apache Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d0a8-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="7d0a8-122">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d0a8-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="7d0a8-123">Un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="7d0a8-124">Per altre informazioni sulla creazione di un cluster, vedere [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="7d0a8-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="7d0a8-125">.NET su HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d0a8-125">.NET on HDInsight</span></span>

* <span data-ttu-id="7d0a8-126">__HDInsight basati su Linux__ cluster tramite [Mono (https://mono-project.com)](https://mono-project.com) toorun le applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="7d0a8-127">La versione Mono 4.2.1 è inclusa nella versione 3.5 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="7d0a8-128">Per altre informazioni sulla compatibilità Mono con le versioni di .NET Framework, vedere il documento relativo alla [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="7d0a8-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="7d0a8-129">toouse una versione specifica di Mono, vedere hello [installazione o aggiornamento Mono](hdinsight-hadoop-install-mono.md) documento.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-129">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="7d0a8-130">__HDInsight basati su Windows__ cluster utilizzino le applicazioni .NET di hello Microsoft .NET CLR toorun.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-130">__Windows-based HDInsight__ clusters use hello Microsoft .NET CLR toorun .NET applications.</span></span>

<span data-ttu-id="7d0a8-131">Per ulteriori informazioni sulla versione di hello di hello .NET framework e Mono inclusa con le versioni di HDInsight, vedere [versioni dei componenti di HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="7d0a8-131">For more information on hello version of hello .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-hello-c-projects"></a><span data-ttu-id="7d0a8-132">Creare hello C\# progetti</span><span class="sxs-lookup"><span data-stu-id="7d0a8-132">Create hello C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="7d0a8-133">UDF di Hive</span><span class="sxs-lookup"><span data-stu-id="7d0a8-133">Hive UDF</span></span>

1. <span data-ttu-id="7d0a8-134">Aprire Visual Studio e creare una soluzione.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="7d0a8-135">Tipo di progetto hello selezionare **applicazione Console (.NET Framework)**e nome hello nuovo progetto **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-135">For hello project type, select **Console App (.NET Framework)**, and name hello new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7d0a8-136">Selezionare __.NET Framework 4.5__ se si usa un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="7d0a8-137">Per altre informazioni sulla compatibilità Mono con le versioni di .NET Framework, vedere il documento relativo alla [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="7d0a8-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="7d0a8-138">Sostituire il contenuto di hello di **Program.cs** con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="7d0a8-138">Replace hello contents of **Program.cs** with hello following:</span></span>

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
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
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

3. <span data-ttu-id="7d0a8-139">Compilare il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-139">Build hello project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="7d0a8-140">UDF di Pig</span><span class="sxs-lookup"><span data-stu-id="7d0a8-140">Pig UDF</span></span>

1. <span data-ttu-id="7d0a8-141">Aprire Visual Studio e creare una soluzione.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="7d0a8-142">Tipo di progetto hello selezionare **applicazione Console**e nome hello nuovo progetto **PigUDF**.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-142">For hello project type, select **Console Application**, and name hello new project **PigUDF**.</span></span>

2. <span data-ttu-id="7d0a8-143">Sostituire il contenuto di hello di hello **Program.cs** file con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="7d0a8-143">Replace hello contents of hello **Program.cs** file with hello following code:</span></span>

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
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    <span data-ttu-id="7d0a8-144">Questa applicazione analizza linee hello inviate da Pig e riformatta righe che iniziano con `java.lang.Exception`.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-144">This application parses hello lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="7d0a8-145">Salvare **Program.cs**e quindi compilare il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-145">Save **Program.cs**, and then build hello project.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="7d0a8-146">Caricare toostorage</span><span class="sxs-lookup"><span data-stu-id="7d0a8-146">Upload toostorage</span></span>

1. <span data-ttu-id="7d0a8-147">In Visual Studio aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="7d0a8-148">Espandere **Azure** e quindi **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="7d0a8-149">Se richiesto, immettere le credenziali della sottoscrizione di Azure, quindi fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="7d0a8-150">Espandere i cluster HDInsight hello che si desidera toodeploy per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-150">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="7d0a8-151">Una voce con il testo hello __(Account di archiviazione predefinito)__ è elencato.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-151">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Esplora server con l'account di archiviazione hello per cluster hello](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="7d0a8-153">Se questa voce può essere espanso, si utilizza un __Account di archiviazione Azure__ come spazio di archiviazione predefinito per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="7d0a8-154">tooview hello i file di archiviazione predefiniti hello per cluster hello, espandere la voce hello e quindi fare doppio clic su hello __(contenitore predefinito)__.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-154">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="7d0a8-155">Se non è possibile espandere questa voce, si utilizza __archivio Azure Data Lake__ come spazio di archiviazione predefinito hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="7d0a8-156">file di hello tooview in spazio di archiviazione predefinito hello for cluster hello, fare doppio clic su hello __(Account di archiviazione predefinito)__ voce.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-156">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="7d0a8-157">file di .exe tooupload hello, utilizzare uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="7d0a8-157">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="7d0a8-158">Se si utilizza un __Account di archiviazione Azure__, fare clic sull'icona di caricamento hello e quindi selezionare toohello **bin\debug** cartella per hello **HiveCSharp** progetto.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-158">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **HiveCSharp** project.</span></span> <span data-ttu-id="7d0a8-159">Infine, selezionare hello **HiveCSharp.exe** file e fare clic su **Ok**.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-159">Finally, select hello **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![icona relativa al caricamento](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="7d0a8-161">Se si utilizza __archivio Azure Data Lake__, fare doppio clic su un'area vuota nell'elenco di file hello e quindi selezionare __caricare__.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-161">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="7d0a8-162">Infine, selezionare hello **HiveCSharp.exe** file e fare clic su **aprire**.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-162">Finally, select hello **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="7d0a8-163">Una volta hello __HiveCSharp.exe__ ha completato il caricamento, il processo di caricamento hello ripetizione per hello __PigUDF.exe__ file.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-163">Once hello __HiveCSharp.exe__ upload has finished, repeat hello upload process for hello __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="7d0a8-164">Eseguire una query Hive</span><span class="sxs-lookup"><span data-stu-id="7d0a8-164">Run a Hive query</span></span>

1. <span data-ttu-id="7d0a8-165">In Visual Studio aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="7d0a8-166">Espandere **Azure** e quindi **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="7d0a8-167">Cluster hello pulsante destro del mouse che è stato distribuito hello **HiveCSharp** applicazione e quindi selezionare **scrivere una Query Hive**.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-167">Right-click hello cluster that you deployed hello **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="7d0a8-168">Utilizzare hello seguente testo per query Hive hello:</span><span class="sxs-lookup"><span data-stu-id="7d0a8-168">Use hello following text for hello Hive query:</span></span>

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="7d0a8-169">Rimuovere il commento hello `add file` istruzione corrispondente tipo hello spazio di archiviazione predefinito utilizzato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-169">Uncomment hello `add file` statement that matches hello type of default storage used for your cluster.</span></span>

    <span data-ttu-id="7d0a8-170">Questa query Seleziona hello `clientid`, `devicemake`, e `devicemodel` i campi dal `hivesampletable`e passa i campi di hello toohello HiveCSharp.exe applicazione.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-170">This query selects hello `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes hello fields toohello HiveCSharp.exe application.</span></span> <span data-ttu-id="7d0a8-171">query Hello prevede hello tooreturn tre campi dell'applicazione, che vengono archiviati come `clientid`, `phoneLabel`, e `phoneHash`.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-171">hello query expects hello application tooreturn three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="7d0a8-172">query Hello prevede inoltre toofind HiveCSharp.exe nella radice di hello del contenitore di archiviazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-172">hello query also expects toofind HiveCSharp.exe in hello root of hello default storage container.</span></span>

5. <span data-ttu-id="7d0a8-173">Fare clic su **Invia** il cluster HDInsight toohello di toosubmit hello processo.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-173">Click **Submit** toosubmit hello job toohello HDInsight cluster.</span></span> <span data-ttu-id="7d0a8-174">Hello **riepilogo Hive** verrà visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-174">hello **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="7d0a8-175">Fare clic su **aggiornare** toorefresh hello riepilogo finché **lo stato del processo** cambia troppo**completato**.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-175">Click **Refresh** toorefresh hello summary until **Job Status** changes too**Completed**.</span></span> <span data-ttu-id="7d0a8-176">il processo di hello tooview output, fare clic su **Output processo**.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-176">tooview hello job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="7d0a8-177">Eseguire un processo Pig</span><span class="sxs-lookup"><span data-stu-id="7d0a8-177">Run a Pig job</span></span>

1. <span data-ttu-id="7d0a8-178">Utilizzare uno dei seguenti cluster HDInsight di metodi tooconnect tooyour hello:</span><span class="sxs-lookup"><span data-stu-id="7d0a8-178">Use one of hello following methods tooconnect tooyour HDInsight cluster:</span></span>

    * <span data-ttu-id="7d0a8-179">Se si usa un cluster HDInsight __basato su Linux__, usare SSH.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="7d0a8-180">Ad esempio, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="7d0a8-181">Per altre informazioni, vedere [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="7d0a8-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="7d0a8-182">Se si utilizza un __basati su Windows__ cluster HDInsight, [cluster toohello Connetti tramite Desktop remoto](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="7d0a8-182">If you are using a __Windows-based__ HDInsight cluster, [Connect toohello cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="7d0a8-183">Utilizzare una hello riga di comando toostart hello Pig comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7d0a8-183">Use one hello following command toostart hello Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="7d0a8-184">Se si utilizza un cluster basato su Windows, utilizzare hello seguente invece di comandi:</span><span class="sxs-lookup"><span data-stu-id="7d0a8-184">If you are using a Windows-based cluster, use hello following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="7d0a8-185">Viene visualizzato un prompt `grunt>`.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="7d0a8-186">Immettere hello seguente toorun un processo Pig che utilizza un'applicazione hello .NET Framework:</span><span class="sxs-lookup"><span data-stu-id="7d0a8-186">Enter hello following toorun a Pig job that uses hello .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="7d0a8-187">Hello `DEFINE` istruzione crea un alias di `streamer` Applications pigudf.exe hello e `CACHE` caricamento dei dati dall'archivio predefinito per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-187">hello `DEFINE` statement creates an alias of `streamer` for hello pigudf.exe applications, and `CACHE` loads it from default storage for hello cluster.</span></span> <span data-ttu-id="7d0a8-188">In un secondo momento, `streamer` viene utilizzato con hello `STREAM` tooprocess operatore hello singole righe contenute nel LOG e dati hello restituito come una serie di colonne.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-188">Later, `streamer` is used with hello `STREAM` operator tooprocess hello single lines contained in LOG and return hello data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7d0a8-189">nome dell'applicazione Hello è utilizzato per il flusso deve essere racchiuso tra hello \` (apice inverso) carattere quando alias, e ' (virgoletta singola) utilizzato con `SHIP\`.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-189">hello application name that is used for streaming must be surrounded by hello \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="7d0a8-190">Dopo aver immesso l'ultima riga hello, deve iniziare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-190">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="7d0a8-191">Restituisce toohello simili di output il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="7d0a8-191">It returns output similar toohello following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="7d0a8-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d0a8-192">Next steps</span></span>

<span data-ttu-id="7d0a8-193">In questo documento, si è appreso come toouse un'applicazione .NET Framework dall'Hive e Pig in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7d0a8-193">In this document, you have learned how toouse a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="7d0a8-194">Se si desidera vedere toouse Python con Hive e Pig, toolearn [usare Python con Hive e Pig in HDInsight](hdinsight-python.md).</span><span class="sxs-lookup"><span data-stu-id="7d0a8-194">If you would like toolearn how toouse Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="7d0a8-195">Per altri modi toouse Pig e Hive e toolearn sull'utilizzo di MapReduce, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="7d0a8-195">For other ways toouse Pig and Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="7d0a8-196">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d0a8-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7d0a8-197">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d0a8-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7d0a8-198">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d0a8-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
