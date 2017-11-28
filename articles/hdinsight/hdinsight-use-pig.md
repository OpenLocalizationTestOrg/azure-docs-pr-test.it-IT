---
title: aaaUse Hadoop Pig in HDInsight | Documenti Microsoft
description: Informazioni su come toouse Pig con Hadoop in HDInsight.
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
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="22ed4-103">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="22ed4-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="22ed4-104">Informazioni su come toouse [Pig Apache](http://pig.apache.org/) con HDInsight...</span><span class="sxs-lookup"><span data-stu-id="22ed4-104">Learn how toouse [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="22ed4-105">Pig è una piattaforma che consente la creazione di programmi per Hadoop usando un linguaggio procedurale denominato *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="22ed4-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="22ed4-106">Pig è un tooJava alternativo per la creazione di *MapReduce* soluzioni e è incluso in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22ed4-106">Pig is an alternative tooJava for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="22ed4-107">Utilizzare hello hello toodiscover tabella vari modi Pig può essere utilizzato con HDInsight seguenti:</span><span class="sxs-lookup"><span data-stu-id="22ed4-107">Use hello following table toodiscover hello various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="22ed4-108">**Usare questo** se si desidera...</span><span class="sxs-lookup"><span data-stu-id="22ed4-108">**Use this** if you want...</span></span> | <span data-ttu-id="22ed4-109">...una shell **interattiva**</span><span class="sxs-lookup"><span data-stu-id="22ed4-109">...an **interactive** shell</span></span> | <span data-ttu-id="22ed4-110">...elaborazione**batch**</span><span class="sxs-lookup"><span data-stu-id="22ed4-110">...**batch** processing</span></span> | <span data-ttu-id="22ed4-111">...con questo **sistema operativo cluster**</span><span class="sxs-lookup"><span data-stu-id="22ed4-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="22ed4-112">...da questo **sistema operativo client**</span><span class="sxs-lookup"><span data-stu-id="22ed4-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="22ed4-113">SSH</span><span class="sxs-lookup"><span data-stu-id="22ed4-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="22ed4-114">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-114">✔</span></span> |<span data-ttu-id="22ed4-115">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-115">✔</span></span> |<span data-ttu-id="22ed4-116">Linux</span><span class="sxs-lookup"><span data-stu-id="22ed4-116">Linux</span></span> |<span data-ttu-id="22ed4-117">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="22ed4-118">API REST</span><span class="sxs-lookup"><span data-stu-id="22ed4-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="22ed4-119">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-119">✔</span></span> |<span data-ttu-id="22ed4-120">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-120">Linux or Windows</span></span> |<span data-ttu-id="22ed4-121">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="22ed4-122">.NET SDK per Hadoop</span><span class="sxs-lookup"><span data-stu-id="22ed4-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="22ed4-123">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-123">✔</span></span> |<span data-ttu-id="22ed4-124">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-124">Linux or Windows</span></span> |<span data-ttu-id="22ed4-125">Windows (per ora)</span><span class="sxs-lookup"><span data-stu-id="22ed4-125">Windows (for now)</span></span> |
| [<span data-ttu-id="22ed4-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="22ed4-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="22ed4-127">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-127">✔</span></span> |<span data-ttu-id="22ed4-128">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-128">Linux or Windows</span></span> |<span data-ttu-id="22ed4-129">Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-129">Windows</span></span> |
| <span data-ttu-id="22ed4-130">[Desktop remoto](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="22ed4-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="22ed4-131">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-131">✔</span></span> |<span data-ttu-id="22ed4-132">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-132">✔</span></span> |<span data-ttu-id="22ed4-133">Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-133">Windows</span></span> |<span data-ttu-id="22ed4-134">Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="22ed4-135">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="22ed4-135">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="22ed4-136">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="22ed4-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="22ed4-137"><a id="why"></a>Perché usare Pig</span><span class="sxs-lookup"><span data-stu-id="22ed4-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="22ed4-138">Una delle sfide hello l'elaborazione dei dati tramite il Framework MapReduce in Hadoop implementa la logica di elaborazione usando solo una mappa e una funzione di riduzione.</span><span class="sxs-lookup"><span data-stu-id="22ed4-138">One of hello challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="22ed4-139">Per un'elaborazione complessa, è spesso hanno toobreak l'elaborazione in più operazioni MapReduce che vengono concatenati risultato hello desiderato tooachieve.</span><span class="sxs-lookup"><span data-stu-id="22ed4-139">For complex processing, you often have toobreak processing into multiple MapReduce operations that are chained together tooachieve hello desired result.</span></span>

<span data-ttu-id="22ed4-140">Pig consente l'elaborazione come una serie di trasformazioni che hello flussi di dati tramite l'output di hello desiderato tooproduce toodefine.</span><span class="sxs-lookup"><span data-stu-id="22ed4-140">Pig allows you toodefine processing as a series of transformations that hello data flows through tooproduce hello desired output.</span></span>

<span data-ttu-id="22ed4-141">Pig latino Hello consente si toodescribe hello flusso di dati da un input non elaborato, tramite una o più trasformazioni, tooproduce output di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="22ed4-141">hello Pig Latin language allows you toodescribe hello data flow from raw input, through one or more transformations, tooproduce hello desired output.</span></span> <span data-ttu-id="22ed4-142">I programmi in Pig Latin seguono questo modello generale:</span><span class="sxs-lookup"><span data-stu-id="22ed4-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="22ed4-143">**Carico**: leggere dati toobe modificato dal file system di hello</span><span class="sxs-lookup"><span data-stu-id="22ed4-143">**Load**: Read data toobe manipulated from hello file system</span></span>

* <span data-ttu-id="22ed4-144">**Trasformare**: modificare dati hello</span><span class="sxs-lookup"><span data-stu-id="22ed4-144">**Transform**: Manipulate hello data</span></span>

* <span data-ttu-id="22ed4-145">**Eseguire il dump o archiviare**: schermata toohello dati di Output o se archiviarlo per l'elaborazione</span><span class="sxs-lookup"><span data-stu-id="22ed4-145">**Dump or store**: Output data toohello screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="22ed4-146">Funzioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="22ed4-146">User-defined functions</span></span>

<span data-ttu-id="22ed4-147">Latino Pig supporta anche le funzioni definite dall'utente (UDF), che consente di tooinvoke i componenti esterni che implementano la logica di difficile toomodel in latino Pig.</span><span class="sxs-lookup"><span data-stu-id="22ed4-147">Pig Latin also supports user-defined functions (UDF), which allows you tooinvoke external components that implement logic that is difficult toomodel in Pig Latin.</span></span>

<span data-ttu-id="22ed4-148">Per altre informazioni su Pig Latin, vedere il [manuale di riferimento di Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) e il [manuale di riferimento di Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="22ed4-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="22ed4-149">Per un esempio di utilizzo di funzioni definite dall'utente con Pig, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="22ed4-149">For an example of using UDFs with Pig, see hello following documents:</span></span>

* <span data-ttu-id="22ed4-150">[Usare DataFu con Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu è una raccolta di utili funzioni definite dall'utente gestite mediante Apache</span><span class="sxs-lookup"><span data-stu-id="22ed4-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="22ed4-151">Usare Python con Pig e Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="22ed4-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="22ed4-152">Usare C# con Hive e Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="22ed4-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="22ed4-153"><a id="data"></a>Dati di esempio</span><span class="sxs-lookup"><span data-stu-id="22ed4-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="22ed4-154">HDInsight fornisce vari set di dati esempio, che vengono archiviati in hello `/example/data` e `/HdiSamples` directory.</span><span class="sxs-lookup"><span data-stu-id="22ed4-154">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="22ed4-155">Queste directory sono in spazio di archiviazione di hello predefinito per il cluster.</span><span class="sxs-lookup"><span data-stu-id="22ed4-155">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="22ed4-156">esempio Pig Hello in questo documento usa hello *log4j* file `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="22ed4-156">hello Pig example in this document uses hello *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="22ed4-157">Ogni log nel file hello è costituito da una riga di campi che contiene un `[LOG LEVEL]` campo tooshow hello hello tipo e il livello di gravità, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="22ed4-157">Each log inside hello file consists of a line of fields that contains a `[LOG LEVEL]` field tooshow hello type and hello severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="22ed4-158">Nell'esempio precedente hello, il livello di registrazione di hello è errore.</span><span class="sxs-lookup"><span data-stu-id="22ed4-158">In hello previous example, hello log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="22ed4-159">È anche possibile generare un file log4j utilizzando hello [Log4j Apache](http://en.wikipedia.org/wiki/Log4j) strumento di registrazione e quindi caricare il blob tooyour file.</span><span class="sxs-lookup"><span data-stu-id="22ed4-159">You can also generate a log4j file by using hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file tooyour blob.</span></span> <span data-ttu-id="22ed4-160">Vedere [tooHDInsight caricare dati](hdinsight-upload-data.md) per le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="22ed4-160">See [Upload Data tooHDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="22ed4-161">Per altre informazioni sul modo in cui HDInsight usa l'archiviazione BLOB di Azure, vedere [Usare l'archiviazione BLOB di Azure con HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="22ed4-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="22ed4-162"><a id="job"></a>Processo di esempio</span><span class="sxs-lookup"><span data-stu-id="22ed4-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="22ed4-163">il processo Pig latino seguente Hello carica hello `sample.log` file dall'archiviazione di hello predefinito per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22ed4-163">hello following Pig Latin job loads hello `sample.log` file from hello default storage for your HDInsight cluster.</span></span> <span data-ttu-id="22ed4-164">Quindi esegue una serie di trasformazioni che produce un numero di procedura molte volte ogni dati di input di livello hello durante l'esecuzione di log.</span><span class="sxs-lookup"><span data-stu-id="22ed4-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in hello input data.</span></span> <span data-ttu-id="22ed4-165">i risultati di Hello vengono scritti tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="22ed4-165">hello results are written tooSTDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="22ed4-166">Hello immagine seguente mostra un riepilogo delle quali ogni trasformazione toohello dati.</span><span class="sxs-lookup"><span data-stu-id="22ed4-166">hello following image shows a summary of what each transformation does toohello data.</span></span>

![Rappresentazione grafica di trasformazioni hello][image-hdi-pig-data-transformation]

## <span data-ttu-id="22ed4-168"><a id="run"></a>Esegui processo Pig latino hello</span><span class="sxs-lookup"><span data-stu-id="22ed4-168"><a id="run"></a>Run hello Pig Latin job</span></span>

<span data-ttu-id="22ed4-169">HDInsight è in grado di eseguire processi Pig Latin in vari modi.</span><span class="sxs-lookup"><span data-stu-id="22ed4-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="22ed4-170">Utilizzare hello seguente toodecide tabella quale metodo si adatta alle proprie esigenze, quindi seguire il collegamento hello per una procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="22ed4-170">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="22ed4-171">**Usare questo** se si desidera...</span><span class="sxs-lookup"><span data-stu-id="22ed4-171">**Use this** if you want...</span></span> | <span data-ttu-id="22ed4-172">...una shell **interattiva**</span><span class="sxs-lookup"><span data-stu-id="22ed4-172">...an **interactive** shell</span></span> | <span data-ttu-id="22ed4-173">...elaborazione**batch**</span><span class="sxs-lookup"><span data-stu-id="22ed4-173">...**batch** processing</span></span> | <span data-ttu-id="22ed4-174">...con questo **sistema operativo cluster**</span><span class="sxs-lookup"><span data-stu-id="22ed4-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="22ed4-175">...da questo **client**</span><span class="sxs-lookup"><span data-stu-id="22ed4-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="22ed4-176">SSH</span><span class="sxs-lookup"><span data-stu-id="22ed4-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="22ed4-177">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-177">✔</span></span> |<span data-ttu-id="22ed4-178">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-178">✔</span></span> |<span data-ttu-id="22ed4-179">Linux</span><span class="sxs-lookup"><span data-stu-id="22ed4-179">Linux</span></span> |<span data-ttu-id="22ed4-180">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="22ed4-181">Curl</span><span class="sxs-lookup"><span data-stu-id="22ed4-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="22ed4-182">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-182">✔</span></span> |<span data-ttu-id="22ed4-183">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-183">Linux or Windows</span></span> |<span data-ttu-id="22ed4-184">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="22ed4-185">.NET SDK per Hadoop</span><span class="sxs-lookup"><span data-stu-id="22ed4-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="22ed4-186">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-186">✔</span></span> |<span data-ttu-id="22ed4-187">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-187">Linux or Windows</span></span> |<span data-ttu-id="22ed4-188">Windows (per ora)</span><span class="sxs-lookup"><span data-stu-id="22ed4-188">Windows (for now)</span></span> |
| [<span data-ttu-id="22ed4-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="22ed4-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="22ed4-190">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-190">✔</span></span> |<span data-ttu-id="22ed4-191">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-191">Linux or Windows</span></span> |<span data-ttu-id="22ed4-192">Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-192">Windows</span></span> |
| <span data-ttu-id="22ed4-193">[Desktop remoto](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="22ed4-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="22ed4-194">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-194">✔</span></span> |<span data-ttu-id="22ed4-195">✔</span><span class="sxs-lookup"><span data-stu-id="22ed4-195">✔</span></span> |<span data-ttu-id="22ed4-196">Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-196">Windows</span></span> |<span data-ttu-id="22ed4-197">Windows</span><span class="sxs-lookup"><span data-stu-id="22ed4-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="22ed4-198">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="22ed4-198">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="22ed4-199">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="22ed4-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="22ed4-200">Pig e SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="22ed4-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="22ed4-201">È possibile utilizzare SQL Server Integration Services (SSIS) toorun un processo Pig.</span><span class="sxs-lookup"><span data-stu-id="22ed4-201">You can use SQL Server Integration Services (SSIS) toorun a Pig job.</span></span> <span data-ttu-id="22ed4-202">Hello Azure Feature Pack per SSIS fornisce hello seguenti dei componenti che funzionano con i processi Pig in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22ed4-202">hello Azure Feature Pack for SSIS provides hello following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="22ed4-203">[Attività di Pig di Azure HDInsight][pigtask]</span><span class="sxs-lookup"><span data-stu-id="22ed4-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="22ed4-204">[Gestione connessione della sottoscrizione di Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="22ed4-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="22ed4-205">Altre informazioni su hello Azure Feature Pack per SSIS [qui][ssispack].</span><span class="sxs-lookup"><span data-stu-id="22ed4-205">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="22ed4-206"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22ed4-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="22ed4-207">Ora che si è appreso come toouse Pig con HDInsight, utilizzare hello seguendo i collegamenti tooexplore toowork altri modi con Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22ed4-207">Now that you have learned how toouse Pig with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="22ed4-208">[Caricare dati tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="22ed4-208">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="22ed4-209">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="22ed4-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="22ed4-210">Usare Sqoop con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="22ed4-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="22ed4-211">Usare Oozie con HDInsight</span><span class="sxs-lookup"><span data-stu-id="22ed4-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="22ed4-212">[Usare processi MapReduce con HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="22ed4-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
