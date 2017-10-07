---
title: "aaaWhat è Apache Hive e HiveQL - HDInsight di Azure | Documenti Microsoft"
description: "Apache Hive è un sistema di data warehouse per Hadoop. È possibile eseguire query di dati archiviati nell'Hive tramite HiveQL, quali simile tooTransact-SQL. In questo documento, informazioni su come toouse Hive e HiveQL con Azure HDInsight."
keywords: "hiveql, novità hive, hiveql hadoop, hive, qual è l'hive di informazioni su come toouse hive,"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="cc8c9-106">Cosa sono Apache Hive e HiveQL in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cc8c9-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="cc8c9-107">[Apache Hive](http://hive.apache.org/) è un sistema di data warehouse per Hadoop.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="cc8c9-108">Hive consente di eseguire attività di riepilogo, query e analisi dei dati.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="cc8c9-109">HiveQL, ovvero un linguaggio di query simili tooSQL sono scritte le query hive.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-109">Hive queries are written in HiveQL, which is a query language similar tooSQL.</span></span>

<span data-ttu-id="cc8c9-110">Hive consente tooproject struttura sui dati in larga misura non strutturati.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-110">Hive allows you tooproject structure on largely unstructured data.</span></span> <span data-ttu-id="cc8c9-111">Dopo aver definito una struttura di hello, è possibile utilizzare dati di hello tooquery HiveQL senza una conoscenza del linguaggio o MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-111">After you define hello structure, you can use HiveQL tooquery hello data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="cc8c9-112">HDInsight offre diversi tipi di cluster ottimizzati per carichi di lavoro specifici.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="cc8c9-113">Hello seguenti tipi di cluster viene spesso usata per le query Hive:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-113">hello following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="cc8c9-114">__Hive interattivo__: Hadoop A cluster che fornisce [bassa latenza Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) funzionalità tooimprove tempi di risposta query interattive.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality tooimprove response times for interactive queries.</span></span> <span data-ttu-id="cc8c9-115">Per ulteriori informazioni, vedere hello [iniziano con interattivo Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-115">For more information, see hello [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="cc8c9-116">__Hadoop__: un cluster Hadoop che è ottimizzato per carichi di lavoro di elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="cc8c9-117">Per ulteriori informazioni, vedere hello [avviare con Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-117">For more information, see hello [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="cc8c9-118">__Spark__: Apache Spark ha una funzionalità integrata per l'utilizzo di Hive.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="cc8c9-119">Per ulteriori informazioni, vedere hello [iniziano con Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-119">For more information, see hello [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="cc8c9-120">__HBase__: HiveQL può essere utilizzato tooquery dati archiviati in HBase.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-120">__HBase__: HiveQL can be used tooquery data stored in HBase.</span></span> <span data-ttu-id="cc8c9-121">Per ulteriori informazioni, vedere hello [iniziano con HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-121">For more information, see hello [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-toouse-hive"></a><span data-ttu-id="cc8c9-122">Come toouse Hive</span><span class="sxs-lookup"><span data-stu-id="cc8c9-122">How toouse Hive</span></span>

<span data-ttu-id="cc8c9-123">Utilizzare hello toodiscover tabella come toouse Hive con HDInsight seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-123">Use hello following table toodiscover how toouse Hive with HDInsight:</span></span>

| <span data-ttu-id="cc8c9-124">**Usare questo metodo** se si vuole...</span><span class="sxs-lookup"><span data-stu-id="cc8c9-124">**Use this method** if you want...</span></span> | <span data-ttu-id="cc8c9-125">...una shell **interattiva**</span><span class="sxs-lookup"><span data-stu-id="cc8c9-125">...an **interactive** shell</span></span> | <span data-ttu-id="cc8c9-126">...elaborazione**batch**</span><span class="sxs-lookup"><span data-stu-id="cc8c9-126">...**batch** processing</span></span> | <span data-ttu-id="cc8c9-127">...con questo **sistema operativo cluster**</span><span class="sxs-lookup"><span data-stu-id="cc8c9-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="cc8c9-128">...da questo **sistema operativo client**</span><span class="sxs-lookup"><span data-stu-id="cc8c9-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="cc8c9-129">Vista di Hive</span><span class="sxs-lookup"><span data-stu-id="cc8c9-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="cc8c9-130">✔</span><span class="sxs-lookup"><span data-stu-id="cc8c9-130">✔</span></span> |<span data-ttu-id="cc8c9-131">✔</span><span class="sxs-lookup"><span data-stu-id="cc8c9-131">✔</span></span> |<span data-ttu-id="cc8c9-132">Linux</span><span class="sxs-lookup"><span data-stu-id="cc8c9-132">Linux</span></span> |<span data-ttu-id="cc8c9-133">Qualsiasi versione (basata su browser)</span><span class="sxs-lookup"><span data-stu-id="cc8c9-133">Any (browser based)</span></span> |
| [<span data-ttu-id="cc8c9-134">Client Beeline</span><span class="sxs-lookup"><span data-stu-id="cc8c9-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="cc8c9-135">✔</span><span class="sxs-lookup"><span data-stu-id="cc8c9-135">✔</span></span> |<span data-ttu-id="cc8c9-136">✔</span><span class="sxs-lookup"><span data-stu-id="cc8c9-136">✔</span></span> |<span data-ttu-id="cc8c9-137">Linux</span><span class="sxs-lookup"><span data-stu-id="cc8c9-137">Linux</span></span> |<span data-ttu-id="cc8c9-138">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="cc8c9-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="cc8c9-139">API REST</span><span class="sxs-lookup"><span data-stu-id="cc8c9-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="cc8c9-140">✔</span><span class="sxs-lookup"><span data-stu-id="cc8c9-140">✔</span></span> |<span data-ttu-id="cc8c9-141">Linux o Windows*</span><span class="sxs-lookup"><span data-stu-id="cc8c9-141">Linux or Windows*</span></span> |<span data-ttu-id="cc8c9-142">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="cc8c9-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="cc8c9-143">HDInsight Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc8c9-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="cc8c9-144">✔</span><span class="sxs-lookup"><span data-stu-id="cc8c9-144">✔</span></span> |<span data-ttu-id="cc8c9-145">Linux o Windows*</span><span class="sxs-lookup"><span data-stu-id="cc8c9-145">Linux or Windows*</span></span> |<span data-ttu-id="cc8c9-146">Windows</span><span class="sxs-lookup"><span data-stu-id="cc8c9-146">Windows</span></span> |
| [<span data-ttu-id="cc8c9-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc8c9-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="cc8c9-148">✔</span><span class="sxs-lookup"><span data-stu-id="cc8c9-148">✔</span></span> |<span data-ttu-id="cc8c9-149">Linux o Windows*</span><span class="sxs-lookup"><span data-stu-id="cc8c9-149">Linux or Windows*</span></span> |<span data-ttu-id="cc8c9-150">Windows</span><span class="sxs-lookup"><span data-stu-id="cc8c9-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="cc8c9-151">\*Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-151">\* Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cc8c9-152">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cc8c9-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="cc8c9-153">Se si utilizza un cluster HDInsight basati su Windows, è possibile utilizzare hello [console Query](hdinsight-hadoop-use-hive-query-console.md) dal browser o [Desktop remoto](hdinsight-hadoop-use-hive-remote-desktop.md) query Hive toorun.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-153">If you are using a Windows-based HDInsight cluster, you can use hello [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="cc8c9-154">Informazioni di riferimento sul linguaggio HiveQL</span><span class="sxs-lookup"><span data-stu-id="cc8c9-154">HiveQL language reference</span></span>

<span data-ttu-id="cc8c9-155">Riferimenti al linguaggio HiveQL è disponibile in hello [manuale di linguaggio (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="cc8c9-155">HiveQL language reference is available in hello [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="cc8c9-156">Hive e la struttura dei dati</span><span class="sxs-lookup"><span data-stu-id="cc8c9-156">Hive and data structure</span></span>

<span data-ttu-id="cc8c9-157">Hive interpreta come toowork con strutturato e dati semistrutturati.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-157">Hive understands how toowork with structured and semi-structured data.</span></span> <span data-ttu-id="cc8c9-158">Ad esempio, file di testo in cui i campi di hello sono delimitati da caratteri specifici.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-158">For example, text files where hello fields are delimited by specific characters.</span></span> <span data-ttu-id="cc8c9-159">Hello HiveQL istruzione crea una tabella dati delimitati da spazi:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-159">hello following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="cc8c9-160">Hive supporta inoltre **serializzatori/deserializzatori** personalizzati per dati complessi o strutturati in modo irregolare.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="cc8c9-161">Per ulteriori informazioni, vedere hello [come toouse un SerDe JSON personalizzato con HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) documento.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-161">For more information, see hello [How toouse a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="cc8c9-162">Per ulteriori informazioni sui formati di file supportati da Hive, vedere hello [manuale di linguaggio (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="cc8c9-162">For more information on file formats supported by Hive, see hello [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="cc8c9-163">Confronto tra le tabelle interne ed esterne di Hive</span><span class="sxs-lookup"><span data-stu-id="cc8c9-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="cc8c9-164">Con Hive è possibile creare due tipi di tabelle:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="cc8c9-165">__Interno__: dati vengono archiviati nel data warehouse di hello Hive.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-165">__Internal__: Data is stored in hello Hive data warehouse.</span></span> <span data-ttu-id="cc8c9-166">Hello del data warehouse si trova in `/hive/warehouse/` in spazio di archiviazione predefinito hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-166">hello data warehouse is located at `/hive/warehouse/` on hello default storage for hello cluster.</span></span>

    <span data-ttu-id="cc8c9-167">Usare tabelle interne quando:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-167">Use internal tables when:</span></span>

    * <span data-ttu-id="cc8c9-168">I dati sono temporanei.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-168">Data is temporary.</span></span>
    * <span data-ttu-id="cc8c9-169">Si desidera ciclo di vita di Hive toomanage hello della tabella di hello e dati.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-169">You want Hive toomanage hello lifecycle of hello table and data.</span></span>

* <span data-ttu-id="cc8c9-170">__Esterno__: dati vengono archiviati all'esterno di data warehouse di hello.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-170">__External__: Data is stored outside hello data warehouse.</span></span> <span data-ttu-id="cc8c9-171">dati Hello possono essere archiviati in tutte le archiviazioni accessibili dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-171">hello data can be stored on any storage accessible by hello cluster.</span></span>

    <span data-ttu-id="cc8c9-172">Usare tabelle esterne quando:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-172">Use external tables when:</span></span>

    * <span data-ttu-id="cc8c9-173">dati Hello viene inoltre utilizzati all'esterno di Hive.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-173">hello data is also used outside of Hive.</span></span> <span data-ttu-id="cc8c9-174">Ad esempio, i file di dati hello vengono aggiornati da un altro processo (che non consente di bloccare file hello.)</span><span class="sxs-lookup"><span data-stu-id="cc8c9-174">For example, hello data files are updated by another process (that does not lock hello files.)</span></span>
    * <span data-ttu-id="cc8c9-175">I dati devono tooremain in hello sottostante posizione, anche dopo l'eliminazione di tabella hello.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-175">Data needs tooremain in hello underlying location, even after dropping hello table.</span></span>
    * <span data-ttu-id="cc8c9-176">È necessario un percorso personalizzato, ad esempio un account di archiviazione non predefinito.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="cc8c9-177">Un programma diverso da hive gestisce il formato di dati di hello, posizione, e così via.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-177">A program other than hive manages hello data format, location, etc.</span></span>

<span data-ttu-id="cc8c9-178">Per ulteriori informazioni, vedere hello [Hive interno e introduzione di tabelle esterno] [ cindygross-hive-tables] post di blog.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-178">For more information, see hello [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="cc8c9-179">Funzioni definite dall'utente (UDF)</span><span class="sxs-lookup"><span data-stu-id="cc8c9-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="cc8c9-180">Hive può anche essere esteso tramite **funzioni definite dall'utente (UDF)**,</span><span class="sxs-lookup"><span data-stu-id="cc8c9-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="cc8c9-181">Una funzione definita dall'utente consente a funzionalità tooimplement o logica che non è facilmente modellata in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-181">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="cc8c9-182">Per un esempio di utilizzo di funzioni definite dall'utente con Hive, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-182">For an example of using UDFs with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="cc8c9-183">Usare una funzione Java definita dall'utente con Hive</span><span class="sxs-lookup"><span data-stu-id="cc8c9-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="cc8c9-184">Usare una funzione Python definita dall'utente con Hive e Pig</span><span class="sxs-lookup"><span data-stu-id="cc8c9-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="cc8c9-185">Usare una funzione C# definita dall'utente con Hive e Pig</span><span class="sxs-lookup"><span data-stu-id="cc8c9-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="cc8c9-186">Funzionamento di tooHDInsight tooadd un Hive personalizzato definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="cc8c9-186">How tooadd a custom Hive user-defined function tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="cc8c9-187">Un'esempio Hive funzione definita dall'utente tooconvert formati data/ora tooHive timestamp</span><span class="sxs-lookup"><span data-stu-id="cc8c9-187">An example Hive user-defined function tooconvert date/time formats tooHive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="cc8c9-188"><a id="data"></a>Dati di esempio</span><span class="sxs-lookup"><span data-stu-id="cc8c9-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="cc8c9-189">Hive in HDInsight include una tabella interna denominata `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="cc8c9-190">HDInsight offre inoltre set di dati di esempio che possono essere usati con Hive.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="cc8c9-191">Questi set di dati vengono archiviati in hello `/example/data` e `/HdiSamples` directory.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-191">These data sets are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="cc8c9-192">Queste directory esistano nel servizio di archiviazione hello predefinito per il cluster.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-192">These directories exist in hello default storage for your cluster.</span></span>

## <span data-ttu-id="cc8c9-193"><a id="job"></a>Query Hive di esempio</span><span class="sxs-lookup"><span data-stu-id="cc8c9-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="cc8c9-194">Hello seguente HiveQL istruzioni progetto colonne hello `/example/data/sample.log` file:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-194">hello following HiveQL statements project columns onto hello `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="cc8c9-195">Nell'esempio precedente hello, le istruzioni HiveQL hello eseguono hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-195">In hello previous example, hello HiveQL statements perform hello following actions:</span></span>

* <span data-ttu-id="cc8c9-196">`set hive.execution.engine=tez;`: Set hello esecuzione motore toouse Tez.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-196">`set hive.execution.engine=tez;`: Sets hello execution engine toouse Tez.</span></span> <span data-ttu-id="cc8c9-197">L'uso di Tez invece di MapReduce offre un aumento delle prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="cc8c9-198">Per ulteriori informazioni su Tez, vedere hello [Tez Apache utilizzo per migliorare le prestazioni](#usetez) sezione.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-198">For more information on Tez, see hello [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cc8c9-199">Questa istruzione è obbligatoria solo quando si usa un cluster HDInsight basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="cc8c9-200">Tez è di tipo motore di esecuzione predefinito hello per HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-200">Tez is hello default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="cc8c9-201">`DROP TABLE`: Se hello tabella esiste già, eliminarla.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-201">`DROP TABLE`: If hello table already exists, delete it.</span></span>

* <span data-ttu-id="cc8c9-202">`CREATE EXTERNAL TABLE`: crea una nuova tabella **esterna** in Hive.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="cc8c9-203">Le tabelle esterne archiviano solo la definizione di tabella hello nell'Hive.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-203">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="cc8c9-204">dati Hello viene lasciati nella posizione originale hello e nel formato originale hello.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-204">hello data is left in hello original location and in hello original format.</span></span>

* <span data-ttu-id="cc8c9-205">`ROW FORMAT`: Indica la formattazione di dati hello Hive.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-205">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="cc8c9-206">In questo caso, i campi di hello in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-206">In this case, hello fields in each log are separated by a space.</span></span>

* <span data-ttu-id="cc8c9-207">`STORED AS TEXTFILE LOCATION`: Indica Hive dove hello memorizzati (hello `example/data` directory) e a cui è archiviato come testo.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="cc8c9-208">è possibile in un file o distribuiti tra più file all'interno di directory hello dati Hello.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-208">hello data can be in one file or spread across multiple files within hello directory.</span></span>

* <span data-ttu-id="cc8c9-209">`SELECT`: Consente di selezionare un conteggio di tutte le righe in cui hello colonna **t4** contiene il valore di hello **[errore]**.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-209">`SELECT`: Selects a count of all rows where hello column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="cc8c9-210">L'istruzione restituisce un valore pari a **3**, poiché sono presenti tre righe contenenti questo valore.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="cc8c9-211">`INPUT__FILE__NAME LIKE '%.log'`-Hive tenta tooapply hello tooall nei file di schema directory hello.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="cc8c9-212">In questo caso, la directory hello contiene file che non corrispondono allo schema di hello.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-212">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="cc8c9-213">tooprevent i dati errati nei risultati di hello, questa istruzione indica di Hive che si dovrebbe restituire solo dati da file che terminano con. log.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-213">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="cc8c9-214">Le tabelle esterne da utilizzare quando si prevede di hello sottostante toobe dati aggiornati da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-214">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="cc8c9-215">Ad esempio, un processo di caricamento dati automatizzato o un'operazione MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="cc8c9-216">Eliminazione di una tabella esterna **non** eliminare i dati di hello, Elimina solo la definizione di tabella hello.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-216">Dropping an external table does **not** delete hello data, it only deletes hello table definition.</span></span>

<span data-ttu-id="cc8c9-217">toocreate un **interno** tabella anziché esterno, usare hello HiveQL seguente:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-217">toocreate an **internal** table instead of external, use hello following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="cc8c9-218">Queste istruzioni consentono di eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-218">These statements perform hello following actions:</span></span>

* <span data-ttu-id="cc8c9-219">`CREATE TABLE IF NOT EXISTS`: Se la tabella hello non esiste, crearla.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-219">`CREATE TABLE IF NOT EXISTS`: If hello table does not exist, create it.</span></span> <span data-ttu-id="cc8c9-220">Poiché hello **esterno** parola chiave non viene utilizzato, l'istruzione seguente crea una tabella interna.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-220">Because hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="cc8c9-221">tabella Hello verrà archiviata nel data warehouse di hello Hive e completamente gestita da Hive.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-221">hello table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="cc8c9-222">`STORED AS ORC`: Archivia dati hello in formato con ottimizzazione per la riga a colonne (ORC).</span><span class="sxs-lookup"><span data-stu-id="cc8c9-222">`STORED AS ORC`: Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="cc8c9-223">ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="cc8c9-224">`INSERT OVERWRITE ... SELECT`: Consente di selezionare le righe da hello **log4jLogs** tabella che contiene **[errore]**, e quindi inserisce hello dati in hello **degli errori** tabella.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-224">`INSERT OVERWRITE ... SELECT`: Selects rows from hello **log4jLogs** table that contains **[ERROR]**, and then inserts hello data into hello **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="cc8c9-225">A differenza delle tabelle esterne, eliminazione di una tabella interna elimina anche i dati sottostanti hello.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-225">Unlike external tables, dropping an internal table also deletes hello underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="cc8c9-226">Ottimizzare le prestazioni delle query di Hive</span><span class="sxs-lookup"><span data-stu-id="cc8c9-226">Improve Hive query performance</span></span>

### <span data-ttu-id="cc8c9-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="cc8c9-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="cc8c9-228">[Apache Tez](http://tez.apache.org) è un framework che consente alle applicazioni con utilizzo intensivo di dati, ad esempio Hive, toorun in modo più efficiente su larga scala.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, toorun much more efficiently at scale.</span></span> <span data-ttu-id="cc8c9-229">Tez è abilitata come impostazione predefinita per i cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="cc8c9-230">Tez è attualmente disattivata per impostazione predefinita per i cluster HDInsight basati su Windows e deve essere abilitata.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="cc8c9-231">per una query Hive, è necessario impostare tootake sfruttare Tez, hello il valore seguente:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-231">tootake advantage of Tez, hello following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="cc8c9-232">Tez è il motore predefinito hello per i cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-232">Tez is hello default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="cc8c9-233">Hello [Hive nei documenti di progettazione Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contiene i dettagli sulle scelte di implementazione hello e le configurazioni di ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-233">hello [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about hello implementation choices and tuning configurations.</span></span>

<span data-ttu-id="cc8c9-234">tooaid eseguire il debug di processi viene eseguito utilizzando Tez, HDInsight fornisce hello segue le interfacce utente web che consentono di tooview dettagli dei processi Tez:</span><span class="sxs-lookup"><span data-stu-id="cc8c9-234">tooaid in debugging jobs ran using Tez, HDInsight provides hello following web UIs that allow you tooview details of Tez jobs:</span></span>

* [<span data-ttu-id="cc8c9-235">Utilizzare hello vista Ambari Tez in HDInsight basati su Linux</span><span class="sxs-lookup"><span data-stu-id="cc8c9-235">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="cc8c9-236">Utilizzare hello Tez UI in HDInsight basati su Windows</span><span class="sxs-lookup"><span data-stu-id="cc8c9-236">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="cc8c9-237">Low Latency Analytical Processing (LLAP)</span><span class="sxs-lookup"><span data-stu-id="cc8c9-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="cc8c9-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (o Live Long and Process) è una nuova funzionalità di Hive 2.0 che consente di mettere in cache le query in memoria.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="cc8c9-239">LLAP rende molto più veloce, le query di Hive troppo[x 26 più velocemente di quanto Hive 1. x in alcuni casi](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="cc8c9-239">LLAP makes Hive queries much faster, up too[26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="cc8c9-240">HDInsight fornisce LLAP hello Hive interattiva di tipo cluster.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-240">HDInsight provides LLAP in hello Interactive Hive cluster type.</span></span> <span data-ttu-id="cc8c9-241">Per ulteriori informazioni, vedere hello [iniziano con Hive interattivo](hdinsight-hadoop-use-interactive-hive.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-241">For more information, see hello [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="cc8c9-242">Processi di Hive e SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="cc8c9-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="cc8c9-243">È possibile utilizzare SQL Server Integration Services (SSIS) toorun un processo Hive.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-243">You can use SQL Server Integration Services (SSIS) toorun a Hive job.</span></span> <span data-ttu-id="cc8c9-244">Hello Azure Feature Pack per SSIS fornisce hello seguenti dei componenti che funzionano con i processi Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-244">hello Azure Feature Pack for SSIS provides hello following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="cc8c9-245">[Attività di Hive di Azure HDInsight][hivetask]</span><span class="sxs-lookup"><span data-stu-id="cc8c9-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="cc8c9-246">[Gestione connessione della sottoscrizione di Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="cc8c9-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="cc8c9-247">Altre informazioni su hello Azure Feature Pack per SSIS [qui][ssispack].</span><span class="sxs-lookup"><span data-stu-id="cc8c9-247">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="cc8c9-248"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cc8c9-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="cc8c9-249">Ora che si è appreso che cos'è Hive e come toouse con Hadoop in HDInsight, utilizzare hello seguendo i collegamenti tooexplore toowork altri modi con Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc8c9-249">Now that you've learned what Hive is and how toouse it with Hadoop in HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="cc8c9-250">[Caricare dati tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="cc8c9-250">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="cc8c9-251">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="cc8c9-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="cc8c9-252">[Usare processi MapReduce con HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="cc8c9-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
