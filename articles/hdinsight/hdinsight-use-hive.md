---
title: Cosa sono Apache Hive e HiveQL - Azure HDInsight | Microsoft Docs
description: "Apache Hive è un sistema di data warehouse per Hadoop. È possibile eseguire query sui dati archiviati in Hive tramite HiveQL, che è simile a Transact-SQL. Questo documento riporta informazioni su come usare Hive e HiveQL con Azure HDInsight."
keywords: "hiveql, cos'è hive, hadoop hiveql, come usare hive, informazioni su hive, cos'è hive"
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
ms.openlocfilehash: 6b3ee17141f773bec07cf40e0b6d63363e9b5164
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="94a01-106">Cosa sono Apache Hive e HiveQL in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="94a01-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="94a01-107">[Apache Hive](http://hive.apache.org/) è un sistema di data warehouse per Hadoop.</span><span class="sxs-lookup"><span data-stu-id="94a01-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="94a01-108">Hive consente di eseguire attività di riepilogo, query e analisi dei dati.</span><span class="sxs-lookup"><span data-stu-id="94a01-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="94a01-109">Le query di Hive sono scritte in HiveQL, linguaggio di query simile a SQL.</span><span class="sxs-lookup"><span data-stu-id="94a01-109">Hive queries are written in HiveQL, which is a query language similar to SQL.</span></span>

<span data-ttu-id="94a01-110">Hive consente di proiettare la struttura su dati principalmente non strutturati.</span><span class="sxs-lookup"><span data-stu-id="94a01-110">Hive allows you to project structure on largely unstructured data.</span></span> <span data-ttu-id="94a01-111">Dopo aver definito la struttura, è possibile usare HiveQL per eseguire una query sui dati anche senza alcuna conoscenza di Java o MapReduce.</span><span class="sxs-lookup"><span data-stu-id="94a01-111">After you define the structure, you can use HiveQL to query the data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="94a01-112">HDInsight offre diversi tipi di cluster ottimizzati per carichi di lavoro specifici.</span><span class="sxs-lookup"><span data-stu-id="94a01-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="94a01-113">I tipi di cluster usati più di frequente per le query Hive sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="94a01-113">The following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="94a01-114">__Interactive Hive__: un cluster Hadoop che offre la funzionalità [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) per migliorare i tempi di risposta per le query interattive.</span><span class="sxs-lookup"><span data-stu-id="94a01-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality to improve response times for interactive queries.</span></span> <span data-ttu-id="94a01-115">Per altre informazioni, vedere il documento su come [iniziare a usare Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md).</span><span class="sxs-lookup"><span data-stu-id="94a01-115">For more information, see the [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="94a01-116">__Hadoop__: un cluster Hadoop che è ottimizzato per carichi di lavoro di elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="94a01-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="94a01-117">Per altre informazioni, vedere il documento su come [iniziare a usare Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="94a01-117">For more information, see the [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="94a01-118">__Spark__: Apache Spark ha una funzionalità integrata per l'utilizzo di Hive.</span><span class="sxs-lookup"><span data-stu-id="94a01-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="94a01-119">Per altre informazioni, vedere il documento su come [iniziare a usare Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="94a01-119">For more information, see the [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="94a01-120">__HBase__: HiveQL può essere usato per eseguire query sui dati archiviati in HBase.</span><span class="sxs-lookup"><span data-stu-id="94a01-120">__HBase__: HiveQL can be used to query data stored in HBase.</span></span> <span data-ttu-id="94a01-121">Per altre informazioni, vedere il documento su come [iniziare a usare HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="94a01-121">For more information, see the [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-to-use-hive"></a><span data-ttu-id="94a01-122">Come usare Hive</span><span class="sxs-lookup"><span data-stu-id="94a01-122">How to use Hive</span></span>

<span data-ttu-id="94a01-123">Consultare la tabella seguente per informazioni su come usare Hive con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="94a01-123">Use the following table to discover how to use Hive with HDInsight:</span></span>

| <span data-ttu-id="94a01-124">**Usare questo metodo** se si vuole...</span><span class="sxs-lookup"><span data-stu-id="94a01-124">**Use this method** if you want...</span></span> | <span data-ttu-id="94a01-125">...una shell **interattiva**</span><span class="sxs-lookup"><span data-stu-id="94a01-125">...an **interactive** shell</span></span> | <span data-ttu-id="94a01-126">...elaborazione**batch**</span><span class="sxs-lookup"><span data-stu-id="94a01-126">...**batch** processing</span></span> | <span data-ttu-id="94a01-127">...con questo **sistema operativo cluster**</span><span class="sxs-lookup"><span data-stu-id="94a01-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="94a01-128">...da questo **sistema operativo client**</span><span class="sxs-lookup"><span data-stu-id="94a01-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="94a01-129">Vista di Hive</span><span class="sxs-lookup"><span data-stu-id="94a01-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="94a01-130">✔</span><span class="sxs-lookup"><span data-stu-id="94a01-130">✔</span></span> |<span data-ttu-id="94a01-131">✔</span><span class="sxs-lookup"><span data-stu-id="94a01-131">✔</span></span> |<span data-ttu-id="94a01-132">Linux</span><span class="sxs-lookup"><span data-stu-id="94a01-132">Linux</span></span> |<span data-ttu-id="94a01-133">Qualsiasi versione (basata su browser)</span><span class="sxs-lookup"><span data-stu-id="94a01-133">Any (browser based)</span></span> |
| [<span data-ttu-id="94a01-134">Client Beeline</span><span class="sxs-lookup"><span data-stu-id="94a01-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="94a01-135">✔</span><span class="sxs-lookup"><span data-stu-id="94a01-135">✔</span></span> |<span data-ttu-id="94a01-136">✔</span><span class="sxs-lookup"><span data-stu-id="94a01-136">✔</span></span> |<span data-ttu-id="94a01-137">Linux</span><span class="sxs-lookup"><span data-stu-id="94a01-137">Linux</span></span> |<span data-ttu-id="94a01-138">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="94a01-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="94a01-139">API REST</span><span class="sxs-lookup"><span data-stu-id="94a01-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="94a01-140">✔</span><span class="sxs-lookup"><span data-stu-id="94a01-140">✔</span></span> |<span data-ttu-id="94a01-141">Linux o Windows*</span><span class="sxs-lookup"><span data-stu-id="94a01-141">Linux or Windows*</span></span> |<span data-ttu-id="94a01-142">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="94a01-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="94a01-143">HDInsight Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="94a01-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="94a01-144">✔</span><span class="sxs-lookup"><span data-stu-id="94a01-144">✔</span></span> |<span data-ttu-id="94a01-145">Linux o Windows*</span><span class="sxs-lookup"><span data-stu-id="94a01-145">Linux or Windows*</span></span> |<span data-ttu-id="94a01-146">Windows</span><span class="sxs-lookup"><span data-stu-id="94a01-146">Windows</span></span> |
| [<span data-ttu-id="94a01-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="94a01-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="94a01-148">✔</span><span class="sxs-lookup"><span data-stu-id="94a01-148">✔</span></span> |<span data-ttu-id="94a01-149">Linux o Windows*</span><span class="sxs-lookup"><span data-stu-id="94a01-149">Linux or Windows*</span></span> |<span data-ttu-id="94a01-150">Windows</span><span class="sxs-lookup"><span data-stu-id="94a01-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="94a01-151">\* Linux è l'unico sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="94a01-151">\* Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="94a01-152">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="94a01-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="94a01-153">Se si usa un cluster HDInsight basato su Windows, è possibile usare la [console Query](hdinsight-hadoop-use-hive-query-console.md) dal browser o [Desktop remoto](hdinsight-hadoop-use-hive-remote-desktop.md) per eseguire query Hive.</span><span class="sxs-lookup"><span data-stu-id="94a01-153">If you are using a Windows-based HDInsight cluster, you can use the [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) to run Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="94a01-154">Informazioni di riferimento sul linguaggio HiveQL</span><span class="sxs-lookup"><span data-stu-id="94a01-154">HiveQL language reference</span></span>

<span data-ttu-id="94a01-155">Informazioni di riferimento sul linguaggio HiveQL sono disponibili nel [manuale del linguaggio (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="94a01-155">HiveQL language reference is available in the [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="94a01-156">Hive e la struttura dei dati</span><span class="sxs-lookup"><span data-stu-id="94a01-156">Hive and data structure</span></span>

<span data-ttu-id="94a01-157">Hive è in grado di usare dati strutturati e semistrutturati.</span><span class="sxs-lookup"><span data-stu-id="94a01-157">Hive understands how to work with structured and semi-structured data.</span></span> <span data-ttu-id="94a01-158">Ad esempio, file di testo in cui i campi sono delimitati da caratteri specifici.</span><span class="sxs-lookup"><span data-stu-id="94a01-158">For example, text files where the fields are delimited by specific characters.</span></span> <span data-ttu-id="94a01-159">L'istruzione HiveQL seguente crea una tabella di dati delimitati da spazi:</span><span class="sxs-lookup"><span data-stu-id="94a01-159">The following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="94a01-160">Hive supporta inoltre **serializzatori/deserializzatori** personalizzati per dati complessi o strutturati in modo irregolare.</span><span class="sxs-lookup"><span data-stu-id="94a01-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="94a01-161">Per altre informazioni, vedere l'articolo su [come usare un serializzatore/deserializzatore JSON personalizzato con HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="94a01-161">For more information, see the [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="94a01-162">Per altre informazioni sui formati di file supportati da Hive, vedere il [manuale del linguaggio (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="94a01-162">For more information on file formats supported by Hive, see the [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="94a01-163">Confronto tra le tabelle interne ed esterne di Hive</span><span class="sxs-lookup"><span data-stu-id="94a01-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="94a01-164">Con Hive è possibile creare due tipi di tabelle:</span><span class="sxs-lookup"><span data-stu-id="94a01-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="94a01-165">__Interna__: i dati vengono archiviati nel data warehouse di Hive.</span><span class="sxs-lookup"><span data-stu-id="94a01-165">__Internal__: Data is stored in the Hive data warehouse.</span></span> <span data-ttu-id="94a01-166">Il data warehouse si trova in `/hive/warehouse/` nella risorsa di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="94a01-166">The data warehouse is located at `/hive/warehouse/` on the default storage for the cluster.</span></span>

    <span data-ttu-id="94a01-167">Usare tabelle interne quando:</span><span class="sxs-lookup"><span data-stu-id="94a01-167">Use internal tables when:</span></span>

    * <span data-ttu-id="94a01-168">I dati sono temporanei.</span><span class="sxs-lookup"><span data-stu-id="94a01-168">Data is temporary.</span></span>
    * <span data-ttu-id="94a01-169">Si desidera che Hive gestisca il ciclo di vita della tabella e dei dati.</span><span class="sxs-lookup"><span data-stu-id="94a01-169">You want Hive to manage the lifecycle of the table and data.</span></span>

* <span data-ttu-id="94a01-170">__Interna__: i dati vengono archiviati all'esterno del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="94a01-170">__External__: Data is stored outside the data warehouse.</span></span> <span data-ttu-id="94a01-171">I dati possono essere archiviati in tutte le risorse di archiviazione accessibili dal cluster.</span><span class="sxs-lookup"><span data-stu-id="94a01-171">The data can be stored on any storage accessible by the cluster.</span></span>

    <span data-ttu-id="94a01-172">Usare tabelle esterne quando:</span><span class="sxs-lookup"><span data-stu-id="94a01-172">Use external tables when:</span></span>

    * <span data-ttu-id="94a01-173">I dati vengono usati anche all'esterno di Hive.</span><span class="sxs-lookup"><span data-stu-id="94a01-173">The data is also used outside of Hive.</span></span> <span data-ttu-id="94a01-174">Ad esempio, i file di dati vengono aggiornati da un altro processo (che non blocca i file).</span><span class="sxs-lookup"><span data-stu-id="94a01-174">For example, the data files are updated by another process (that does not lock the files.)</span></span>
    * <span data-ttu-id="94a01-175">I dati devono rimanere nel percorso sottostante, anche dopo l'eliminazione della tabella.</span><span class="sxs-lookup"><span data-stu-id="94a01-175">Data needs to remain in the underlying location, even after dropping the table.</span></span>
    * <span data-ttu-id="94a01-176">È necessario un percorso personalizzato, ad esempio un account di archiviazione non predefinito.</span><span class="sxs-lookup"><span data-stu-id="94a01-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="94a01-177">Un programma diverso da Hive gestisce il formato dei dati, il percorso e così via.</span><span class="sxs-lookup"><span data-stu-id="94a01-177">A program other than hive manages the data format, location, etc.</span></span>

<span data-ttu-id="94a01-178">Per altre informazioni, vedere il post di blog [Hive Internal and External Tables Intro][cindygross-hive-tables] (Introduzione alle tabelle interne ed esterne di Hive).</span><span class="sxs-lookup"><span data-stu-id="94a01-178">For more information, see the [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="94a01-179">Funzioni definite dall'utente (UDF)</span><span class="sxs-lookup"><span data-stu-id="94a01-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="94a01-180">Hive può anche essere esteso tramite **funzioni definite dall'utente (UDF)**,</span><span class="sxs-lookup"><span data-stu-id="94a01-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="94a01-181">che consentono di implementare funzionalità o logica non facilmente modellate in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="94a01-181">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="94a01-182">Per un esempio sull'uso di funzioni definite dall'utente con Hive, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="94a01-182">For an example of using UDFs with Hive, see the following documents:</span></span>

* [<span data-ttu-id="94a01-183">Usare una funzione Java definita dall'utente con Hive</span><span class="sxs-lookup"><span data-stu-id="94a01-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="94a01-184">Usare una funzione Python definita dall'utente con Hive e Pig</span><span class="sxs-lookup"><span data-stu-id="94a01-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="94a01-185">Usare una funzione C# definita dall'utente con Hive e Pig</span><span class="sxs-lookup"><span data-stu-id="94a01-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="94a01-186">Come aggiungere una funzione Hive personalizzata definita dall'utente in HDInsight</span><span class="sxs-lookup"><span data-stu-id="94a01-186">How to add a custom Hive user-defined function to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="94a01-187">Esempio di funzione Hive personalizzata definita dall'utente per convertire i formati di data/ora in timestamp Hive</span><span class="sxs-lookup"><span data-stu-id="94a01-187">An example Hive user-defined function to convert date/time formats to Hive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="94a01-188"><a id="data"></a>Dati di esempio</span><span class="sxs-lookup"><span data-stu-id="94a01-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="94a01-189">Hive in HDInsight include una tabella interna denominata `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="94a01-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="94a01-190">HDInsight offre inoltre set di dati di esempio che possono essere usati con Hive.</span><span class="sxs-lookup"><span data-stu-id="94a01-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="94a01-191">Questi set di dati sono archiviati nelle directory `/example/data` e `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="94a01-191">These data sets are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="94a01-192">Queste directory si trovano nella risorsa di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="94a01-192">These directories exist in the default storage for your cluster.</span></span>

## <span data-ttu-id="94a01-193"><a id="job"></a>Query Hive di esempio</span><span class="sxs-lookup"><span data-stu-id="94a01-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="94a01-194">Le seguenti istruzioni di HiveQL creano colonne nel file `/example/data/sample.log`:</span><span class="sxs-lookup"><span data-stu-id="94a01-194">The following HiveQL statements project columns onto the `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="94a01-195">Nell'esempio precedente, le istruzioni HiveQL eseguono le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="94a01-195">In the previous example, the HiveQL statements perform the following actions:</span></span>

* <span data-ttu-id="94a01-196">`set hive.execution.engine=tez;`: configura il motore di esecuzione per l'uso di Tez.</span><span class="sxs-lookup"><span data-stu-id="94a01-196">`set hive.execution.engine=tez;`: Sets the execution engine to use Tez.</span></span> <span data-ttu-id="94a01-197">L'uso di Tez invece di MapReduce offre un aumento delle prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="94a01-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="94a01-198">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span><span class="sxs-lookup"><span data-stu-id="94a01-198">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="94a01-199">Questa istruzione è obbligatoria solo quando si usa un cluster HDInsight basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="94a01-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="94a01-200">Tez è il motore di esecuzione predefinito per HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="94a01-200">Tez is the default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="94a01-201">`DROP TABLE`: se la tabella esiste già, eliminarla.</span><span class="sxs-lookup"><span data-stu-id="94a01-201">`DROP TABLE`: If the table already exists, delete it.</span></span>

* <span data-ttu-id="94a01-202">`CREATE EXTERNAL TABLE`: crea una nuova tabella **esterna** in Hive.</span><span class="sxs-lookup"><span data-stu-id="94a01-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="94a01-203">Le tabelle esterne archiviano solo la definizione della tabella in Hive.</span><span class="sxs-lookup"><span data-stu-id="94a01-203">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="94a01-204">I dati rimangono nel percorso e nel formato originale.</span><span class="sxs-lookup"><span data-stu-id="94a01-204">The data is left in the original location and in the original format.</span></span>

* <span data-ttu-id="94a01-205">`ROW FORMAT`: indica a Hive il modo in cui sono formattati i dati.</span><span class="sxs-lookup"><span data-stu-id="94a01-205">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="94a01-206">In questo caso, i campi in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="94a01-206">In this case, the fields in each log are separated by a space.</span></span>

* <span data-ttu-id="94a01-207">`STORED AS TEXTFILE LOCATION`: indica a Hive dove sono archiviati i dati (la directory `example/data`) e che sono archiviati come testo.</span><span class="sxs-lookup"><span data-stu-id="94a01-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="94a01-208">I dati possono essere contenuti in un file o distribuiti tra più file all'interno della directory.</span><span class="sxs-lookup"><span data-stu-id="94a01-208">The data can be in one file or spread across multiple files within the directory.</span></span>

* <span data-ttu-id="94a01-209">`SELECT`: seleziona un conteggio di tutte le righe in cui la colonna **t4** contiene il valore **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="94a01-209">`SELECT`: Selects a count of all rows where the column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="94a01-210">L'istruzione restituisce un valore pari a **3**, poiché sono presenti tre righe contenenti questo valore.</span><span class="sxs-lookup"><span data-stu-id="94a01-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="94a01-211">`INPUT__FILE__NAME LIKE '%.log'`: Hive tenta di applicare lo schema a tutti i file della directory.</span><span class="sxs-lookup"><span data-stu-id="94a01-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="94a01-212">In questo caso la directory contiene file che non corrispondono allo schema.</span><span class="sxs-lookup"><span data-stu-id="94a01-212">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="94a01-213">Per evitare dati errati nei risultati, questa istruzione indica a Hive che devono essere restituiti dati solo da file che terminano con .log.</span><span class="sxs-lookup"><span data-stu-id="94a01-213">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="94a01-214">Usa le tabelle esterne se si prevede che i dati sottostanti verranno aggiornati da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="94a01-214">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="94a01-215">Ad esempio, un processo di caricamento dati automatizzato o un'operazione MapReduce.</span><span class="sxs-lookup"><span data-stu-id="94a01-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="94a01-216">L'eliminazione di una tabella esterna **non** comporta anche l'eliminazione dei dati. Viene eliminata solo la definizione della tabella.</span><span class="sxs-lookup"><span data-stu-id="94a01-216">Dropping an external table does **not** delete the data, it only deletes the table definition.</span></span>

<span data-ttu-id="94a01-217">Per creare una tabella **interno** anziché esterna, usare il codice HiveQL seguente:</span><span class="sxs-lookup"><span data-stu-id="94a01-217">To create an **internal** table instead of external, use the following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="94a01-218">Di seguito sono elencate le istruzioni che eseguono queste azioni:</span><span class="sxs-lookup"><span data-stu-id="94a01-218">These statements perform the following actions:</span></span>

* <span data-ttu-id="94a01-219">`CREATE TABLE IF NOT EXISTS`: se la tabella non esiste, crearla.</span><span class="sxs-lookup"><span data-stu-id="94a01-219">`CREATE TABLE IF NOT EXISTS`: If the table does not exist, create it.</span></span> <span data-ttu-id="94a01-220">Poiché non viene usata la parola chiave **EXTERNAL**, questa istruzione crea una tabella interna.</span><span class="sxs-lookup"><span data-stu-id="94a01-220">Because the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="94a01-221">La tabella viene archiviata nel data warehouse di Hive e gestita completamente da Hive.</span><span class="sxs-lookup"><span data-stu-id="94a01-221">The table is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="94a01-222">`STORED AS ORC`: archivia i dati nel formato ORC, Optimized Row Columnar.</span><span class="sxs-lookup"><span data-stu-id="94a01-222">`STORED AS ORC`: Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="94a01-223">ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.</span><span class="sxs-lookup"><span data-stu-id="94a01-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="94a01-224">`INSERT OVERWRITE ... SELECT`: seleziona dalla tabella**log4jLogs** le righe contenenti **[ERROR]**, quindi inserisce i dati nella tabella **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="94a01-224">`INSERT OVERWRITE ... SELECT`: Selects rows from the **log4jLogs** table that contains **[ERROR]**, and then inserts the data into the **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="94a01-225">A differenza delle tabelle esterne, se si elimina una tabella interna vengono eliminati anche i dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="94a01-225">Unlike external tables, dropping an internal table also deletes the underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="94a01-226">Ottimizzare le prestazioni delle query di Hive</span><span class="sxs-lookup"><span data-stu-id="94a01-226">Improve Hive query performance</span></span>

### <span data-ttu-id="94a01-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="94a01-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="94a01-228">[Apache Tez](http://tez.apache.org) è un framework che consente di eseguire applicazioni come Hive, che richiedono un uso elevato di dati, in modo molto più efficiente e scalabile.</span><span class="sxs-lookup"><span data-stu-id="94a01-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, to run much more efficiently at scale.</span></span> <span data-ttu-id="94a01-229">Tez è abilitata come impostazione predefinita per i cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="94a01-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="94a01-230">Tez è attualmente disattivata per impostazione predefinita per i cluster HDInsight basati su Windows e deve essere abilitata.</span><span class="sxs-lookup"><span data-stu-id="94a01-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="94a01-231">Per poter usufruire dei vantaggi di Tez, è necessario impostare il valore seguente per una query Hive:</span><span class="sxs-lookup"><span data-stu-id="94a01-231">To take advantage of Tez, the following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="94a01-232">Tez è il motore predefinito per i cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="94a01-232">Tez is the default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="94a01-233">La [documentazione sulla progettazione di Hive su Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contiene le informazioni dettagliate sulle scelte di implementazione e l'ottimizzazione delle configurazioni.</span><span class="sxs-lookup"><span data-stu-id="94a01-233">The [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about the implementation choices and tuning configurations.</span></span>

<span data-ttu-id="94a01-234">Per facilitare il debug di processi eseguiti mediante Tez, HDInsight fornisce le interfacce utente Web seguenti che consentono di visualizzare i dettagli dei processi Tez:</span><span class="sxs-lookup"><span data-stu-id="94a01-234">To aid in debugging jobs ran using Tez, HDInsight provides the following web UIs that allow you to view details of Tez jobs:</span></span>

* [<span data-ttu-id="94a01-235">Usare la vista Ambari Tez in HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="94a01-235">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="94a01-236">Usare l'interfaccia utente di Tez in HDInsight basato su Windows</span><span class="sxs-lookup"><span data-stu-id="94a01-236">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="94a01-237">Low Latency Analytical Processing (LLAP)</span><span class="sxs-lookup"><span data-stu-id="94a01-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="94a01-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (o Live Long and Process) è una nuova funzionalità di Hive 2.0 che consente di mettere in cache le query in memoria.</span><span class="sxs-lookup"><span data-stu-id="94a01-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="94a01-239">LLAP rende molto più veloci le query Hive, in alcuni casi fino a [26 volte più veloci rispetto a Hive 1.x](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="94a01-239">LLAP makes Hive queries much faster, up to [26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="94a01-240">HDInsight offre LLAP nel tipo di cluster Interactive Hive.</span><span class="sxs-lookup"><span data-stu-id="94a01-240">HDInsight provides LLAP in the Interactive Hive cluster type.</span></span> <span data-ttu-id="94a01-241">Per altre informazioni, vedere il documento su come [iniziare a usare Interactive Hive](hdinsight-hadoop-use-interactive-hive.md).</span><span class="sxs-lookup"><span data-stu-id="94a01-241">For more information, see the [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="94a01-242">Processi di Hive e SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="94a01-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="94a01-243">È possibile usare SQL Server Integration Services (SSIS) per eseguire un processo Hive.</span><span class="sxs-lookup"><span data-stu-id="94a01-243">You can use SQL Server Integration Services (SSIS) to run a Hive job.</span></span> <span data-ttu-id="94a01-244">Il Feature Pack di Azure per SSIS fornisce i seguenti componenti che funzionano con i processi Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="94a01-244">The Azure Feature Pack for SSIS provides the following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="94a01-245">[Attività di Hive di Azure HDInsight][hivetask]</span><span class="sxs-lookup"><span data-stu-id="94a01-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="94a01-246">[Gestione connessione della sottoscrizione di Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="94a01-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="94a01-247">Altre informazioni sul Feature Pack di Azure per SSIS sono disponibili [qui][ssispack].</span><span class="sxs-lookup"><span data-stu-id="94a01-247">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="94a01-248"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94a01-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="94a01-249">Dopo avere appreso che cos'è Hive e come si usa con Hadoop in HDInsight, vedere i collegamenti seguenti per scoprire altri modi di usare Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="94a01-249">Now that you've learned what Hive is and how to use it with Hadoop in HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="94a01-250">[Caricare dati in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="94a01-250">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="94a01-251">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="94a01-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="94a01-252">[Usare processi MapReduce con HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="94a01-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
