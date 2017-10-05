---
title: Usare Pig di Hadoop in HDInsight | Microsoft Docs
description: Informazioni su come usare Pig con Hadoop in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 474f901ffdaf1ed372ace19076ef723b8b10cb9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="acbe2-103">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="acbe2-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="acbe2-104">Informazioni su come usare [Apache Pig](http://pig.apache.org/) con HDInsight...</span><span class="sxs-lookup"><span data-stu-id="acbe2-104">Learn how to use [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="acbe2-105">Pig è una piattaforma che consente la creazione di programmi per Hadoop usando un linguaggio procedurale denominato *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="acbe2-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="acbe2-106">Pig è un'alternativa a Java per la creazione di soluzioni *MapReduce* ed è incluso in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="acbe2-106">Pig is an alternative to Java for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="acbe2-107">Usare la tabella seguente per individuare i vari modi in cui Pig può essere usato con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="acbe2-107">Use the following table to discover the various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="acbe2-108">**Usare questo** se si desidera...</span><span class="sxs-lookup"><span data-stu-id="acbe2-108">**Use this** if you want...</span></span> | <span data-ttu-id="acbe2-109">...una shell **interattiva**</span><span class="sxs-lookup"><span data-stu-id="acbe2-109">...an **interactive** shell</span></span> | <span data-ttu-id="acbe2-110">...elaborazione**batch**</span><span class="sxs-lookup"><span data-stu-id="acbe2-110">...**batch** processing</span></span> | <span data-ttu-id="acbe2-111">...con questo **sistema operativo cluster**</span><span class="sxs-lookup"><span data-stu-id="acbe2-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="acbe2-112">...da questo **sistema operativo client**</span><span class="sxs-lookup"><span data-stu-id="acbe2-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="acbe2-113">SSH</span><span class="sxs-lookup"><span data-stu-id="acbe2-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="acbe2-114">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-114">✔</span></span> |<span data-ttu-id="acbe2-115">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-115">✔</span></span> |<span data-ttu-id="acbe2-116">Linux</span><span class="sxs-lookup"><span data-stu-id="acbe2-116">Linux</span></span> |<span data-ttu-id="acbe2-117">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="acbe2-118">API REST</span><span class="sxs-lookup"><span data-stu-id="acbe2-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="acbe2-119">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-119">✔</span></span> |<span data-ttu-id="acbe2-120">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-120">Linux or Windows</span></span> |<span data-ttu-id="acbe2-121">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="acbe2-122">.NET SDK per Hadoop</span><span class="sxs-lookup"><span data-stu-id="acbe2-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="acbe2-123">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-123">✔</span></span> |<span data-ttu-id="acbe2-124">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-124">Linux or Windows</span></span> |<span data-ttu-id="acbe2-125">Windows (per ora)</span><span class="sxs-lookup"><span data-stu-id="acbe2-125">Windows (for now)</span></span> |
| [<span data-ttu-id="acbe2-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="acbe2-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="acbe2-127">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-127">✔</span></span> |<span data-ttu-id="acbe2-128">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-128">Linux or Windows</span></span> |<span data-ttu-id="acbe2-129">Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-129">Windows</span></span> |
| <span data-ttu-id="acbe2-130">[Desktop remoto](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="acbe2-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="acbe2-131">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-131">✔</span></span> |<span data-ttu-id="acbe2-132">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-132">✔</span></span> |<span data-ttu-id="acbe2-133">Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-133">Windows</span></span> |<span data-ttu-id="acbe2-134">Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="acbe2-135">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="acbe2-135">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="acbe2-136">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="acbe2-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="acbe2-137"><a id="why"></a>Perché usare Pig</span><span class="sxs-lookup"><span data-stu-id="acbe2-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="acbe2-138">Quando si elaborano dati usando MapReduce in Hadoop, uno dei problemi principali è riuscire a implementare la logica di elaborazione usando solo una mappa e una funzione di riduzione.</span><span class="sxs-lookup"><span data-stu-id="acbe2-138">One of the challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="acbe2-139">In caso di esigenze di elaborazione complesse, è spesso necessario interrompere l'elaborazione in più operazioni di MapReduce concatenate insieme per ottenere il risultato desiderato.</span><span class="sxs-lookup"><span data-stu-id="acbe2-139">For complex processing, you often have to break processing into multiple MapReduce operations that are chained together to achieve the desired result.</span></span>

<span data-ttu-id="acbe2-140">Pig consente di definire l'elaborazione come una serie di trasformazioni a cui vengono sottoposti i dati fino a raggiungere l'output desiderato.</span><span class="sxs-lookup"><span data-stu-id="acbe2-140">Pig allows you to define processing as a series of transformations that the data flows through to produce the desired output.</span></span>

<span data-ttu-id="acbe2-141">Il linguaggio Pig Latin consente di descrivere il flusso dati dall'input non elaborato fino all'output desiderato, attraverso una o più trasformazioni.</span><span class="sxs-lookup"><span data-stu-id="acbe2-141">The Pig Latin language allows you to describe the data flow from raw input, through one or more transformations, to produce the desired output.</span></span> <span data-ttu-id="acbe2-142">I programmi in Pig Latin seguono questo modello generale:</span><span class="sxs-lookup"><span data-stu-id="acbe2-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="acbe2-143">**Load**: lettura dei dati da manipolare dal file system</span><span class="sxs-lookup"><span data-stu-id="acbe2-143">**Load**: Read data to be manipulated from the file system</span></span>

* <span data-ttu-id="acbe2-144">**Transform**: manipolazione dei dati</span><span class="sxs-lookup"><span data-stu-id="acbe2-144">**Transform**: Manipulate the data</span></span>

* <span data-ttu-id="acbe2-145">**Dump or store**: output dei dati sullo schermo o archiviazione per l'elaborazione</span><span class="sxs-lookup"><span data-stu-id="acbe2-145">**Dump or store**: Output data to the screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="acbe2-146">Funzioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="acbe2-146">User-defined functions</span></span>

<span data-ttu-id="acbe2-147">Pig Latin supporta anche funzioni definite dall'utente (UDF), che consentono di richiamare componenti esterni in grado di implementare logica difficile da modellare in Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="acbe2-147">Pig Latin also supports user-defined functions (UDF), which allows you to invoke external components that implement logic that is difficult to model in Pig Latin.</span></span>

<span data-ttu-id="acbe2-148">Per altre informazioni su Pig Latin, vedere il [manuale di riferimento di Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) e il [manuale di riferimento di Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="acbe2-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="acbe2-149">Per un esempio sull'uso di funzioni definite dall'utente con Pig, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="acbe2-149">For an example of using UDFs with Pig, see the following documents:</span></span>

* <span data-ttu-id="acbe2-150">[Usare DataFu con Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu è una raccolta di utili funzioni definite dall'utente gestite mediante Apache</span><span class="sxs-lookup"><span data-stu-id="acbe2-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="acbe2-151">Usare Python con Pig e Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="acbe2-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="acbe2-152">Usare C# con Hive e Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="acbe2-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="acbe2-153"><a id="data"></a>Dati di esempio</span><span class="sxs-lookup"><span data-stu-id="acbe2-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="acbe2-154">HDInsight offre diversi set di dati di esempio, archiviati nelle directory `/example/data` e `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="acbe2-154">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="acbe2-155">Queste directory si trovano nella risorsa di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="acbe2-155">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="acbe2-156">L'esempio di Pig in questo documento usa il file *log4j* da `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="acbe2-156">The Pig example in this document uses the *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="acbe2-157">Ogni log all'interno del file è costituito da una riga di campi che contiene un campo `[LOG LEVEL]` per visualizzare il tipo e la gravità. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="acbe2-157">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="acbe2-158">Nell'esempio precedente, il livello log è ERROR.</span><span class="sxs-lookup"><span data-stu-id="acbe2-158">In the previous example, the log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="acbe2-159">È anche possibile generare un file log4j usando lo strumento di registrazione [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) e quindi caricandolo nel BLOB.</span><span class="sxs-lookup"><span data-stu-id="acbe2-159">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to your blob.</span></span> <span data-ttu-id="acbe2-160">Per istruzioni, vedere [Caricamento di dati in HDInsight](hdinsight-upload-data.md) .</span><span class="sxs-lookup"><span data-stu-id="acbe2-160">See [Upload Data to HDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="acbe2-161">Per altre informazioni sul modo in cui HDInsight usa l'archiviazione BLOB di Azure, vedere [Usare l'archiviazione BLOB di Azure con HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="acbe2-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="acbe2-162"><a id="job"></a>Processo di esempio</span><span class="sxs-lookup"><span data-stu-id="acbe2-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="acbe2-163">Il processo Pig Latin seguente carica il file `sample.log` dalla risorsa di archiviazione predefinita per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="acbe2-163">The following Pig Latin job loads the `sample.log` file from the default storage for your HDInsight cluster.</span></span> <span data-ttu-id="acbe2-164">Esegue quindi una serie di trasformazioni che generano un conteggio delle occorrenze di ciascun livello di log presente nei dati di input.</span><span class="sxs-lookup"><span data-stu-id="acbe2-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in the input data.</span></span> <span data-ttu-id="acbe2-165">I risultati vengono scritti in STDOUT.</span><span class="sxs-lookup"><span data-stu-id="acbe2-165">The results are written to STDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="acbe2-166">L'immagine seguente illustra un riepilogo degli effetti di ogni trasformazione sui dati.</span><span class="sxs-lookup"><span data-stu-id="acbe2-166">The following image shows a summary of what each transformation does to the data.</span></span>

![Rappresentazione grafica delle trasformazioni][image-hdi-pig-data-transformation]

## <span data-ttu-id="acbe2-168"><a id="run"></a>Eseguire il processo Pig Latin</span><span class="sxs-lookup"><span data-stu-id="acbe2-168"><a id="run"></a>Run the Pig Latin job</span></span>

<span data-ttu-id="acbe2-169">HDInsight è in grado di eseguire processi Pig Latin in vari modi.</span><span class="sxs-lookup"><span data-stu-id="acbe2-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="acbe2-170">Usare la tabella seguente per decidere il metodo più adatto alle proprie esigenze, quindi fare clic sul collegamento per visualizzare una procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="acbe2-170">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="acbe2-171">**Usare questo** se si desidera...</span><span class="sxs-lookup"><span data-stu-id="acbe2-171">**Use this** if you want...</span></span> | <span data-ttu-id="acbe2-172">...una shell **interattiva**</span><span class="sxs-lookup"><span data-stu-id="acbe2-172">...an **interactive** shell</span></span> | <span data-ttu-id="acbe2-173">...elaborazione**batch**</span><span class="sxs-lookup"><span data-stu-id="acbe2-173">...**batch** processing</span></span> | <span data-ttu-id="acbe2-174">...con questo **sistema operativo cluster**</span><span class="sxs-lookup"><span data-stu-id="acbe2-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="acbe2-175">...da questo **client**</span><span class="sxs-lookup"><span data-stu-id="acbe2-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="acbe2-176">SSH</span><span class="sxs-lookup"><span data-stu-id="acbe2-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="acbe2-177">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-177">✔</span></span> |<span data-ttu-id="acbe2-178">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-178">✔</span></span> |<span data-ttu-id="acbe2-179">Linux</span><span class="sxs-lookup"><span data-stu-id="acbe2-179">Linux</span></span> |<span data-ttu-id="acbe2-180">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="acbe2-181">Curl</span><span class="sxs-lookup"><span data-stu-id="acbe2-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="acbe2-182">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-182">✔</span></span> |<span data-ttu-id="acbe2-183">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-183">Linux or Windows</span></span> |<span data-ttu-id="acbe2-184">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="acbe2-185">.NET SDK per Hadoop</span><span class="sxs-lookup"><span data-stu-id="acbe2-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="acbe2-186">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-186">✔</span></span> |<span data-ttu-id="acbe2-187">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-187">Linux or Windows</span></span> |<span data-ttu-id="acbe2-188">Windows (per ora)</span><span class="sxs-lookup"><span data-stu-id="acbe2-188">Windows (for now)</span></span> |
| [<span data-ttu-id="acbe2-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="acbe2-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="acbe2-190">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-190">✔</span></span> |<span data-ttu-id="acbe2-191">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-191">Linux or Windows</span></span> |<span data-ttu-id="acbe2-192">Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-192">Windows</span></span> |
| <span data-ttu-id="acbe2-193">[Desktop remoto](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="acbe2-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="acbe2-194">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-194">✔</span></span> |<span data-ttu-id="acbe2-195">✔</span><span class="sxs-lookup"><span data-stu-id="acbe2-195">✔</span></span> |<span data-ttu-id="acbe2-196">Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-196">Windows</span></span> |<span data-ttu-id="acbe2-197">Windows</span><span class="sxs-lookup"><span data-stu-id="acbe2-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="acbe2-198">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="acbe2-198">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="acbe2-199">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="acbe2-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="acbe2-200">Pig e SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="acbe2-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="acbe2-201">È possibile usare SQL Server Integration Services (SSIS) per eseguire un processo Pig.</span><span class="sxs-lookup"><span data-stu-id="acbe2-201">You can use SQL Server Integration Services (SSIS) to run a Pig job.</span></span> <span data-ttu-id="acbe2-202">Il Feature Pack di Azure per SSIS fornisce i seguenti componenti che funzionano con i processi Pig in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="acbe2-202">The Azure Feature Pack for SSIS provides the following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="acbe2-203">[Attività di Pig di Azure HDInsight][pigtask]</span><span class="sxs-lookup"><span data-stu-id="acbe2-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="acbe2-204">[Gestione connessione della sottoscrizione di Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="acbe2-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="acbe2-205">Altre informazioni sul Feature Pack di Azure per SSIS sono disponibili [qui][ssispack].</span><span class="sxs-lookup"><span data-stu-id="acbe2-205">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="acbe2-206"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="acbe2-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="acbe2-207">Dopo avere appreso come usare Pig con HDInsight, vedere i collegamenti seguenti per scoprire altri modi di usare Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="acbe2-207">Now that you have learned how to use Pig with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="acbe2-208">[Caricare dati in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="acbe2-208">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="acbe2-209">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="acbe2-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="acbe2-210">Usare Sqoop con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="acbe2-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="acbe2-211">Usare Oozie con HDInsight</span><span class="sxs-lookup"><span data-stu-id="acbe2-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="acbe2-212">[Usare processi MapReduce con HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="acbe2-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
