---
title: aaaMapReduce e la connessione SSH con Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come i processi toouse SSH toorun MapReduce con Hadoop in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="11088-103">Usare MapReduce con Hadoop in HDInsight con SSH</span><span class="sxs-lookup"><span data-stu-id="11088-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="11088-104">Informazioni su come i processi MapReduce toosubmit un tooHDInsight connessione Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="11088-104">Learn how toosubmit MapReduce jobs from a Secure Shell (SSH) connection tooHDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="11088-105">Se si ha già familiarità con basati su Linux, Hadoop server, ma si sono tooHDInsight nuovo, vedere [suggerimenti basati su Linux HDInsight](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="11088-105">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="11088-106"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="11088-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="11088-107">Un cluster HDInsight (Hadoop in HDInsight) basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="11088-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="11088-108">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="11088-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="11088-109">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="11088-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="11088-110">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="11088-110">An SSH client.</span></span> <span data-ttu-id="11088-111">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="11088-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="11088-112"><a id="ssh"></a>Connettersi con SSH</span><span class="sxs-lookup"><span data-stu-id="11088-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="11088-113">Connettere il cluster toohello tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="11088-113">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="11088-114">Ad esempio, hello comando seguente si connette tooa cluster denominato **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="11088-114">For example, hello following command connects tooa cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="11088-115">**Se si utilizza una chiave del certificato per l'autenticazione SSH**, potrebbe essere necessario percorso hello toospecify della chiave privata hello nel sistema client, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="11088-115">**If you use a certificate key for SSH authentication**, you may need toospecify hello location of hello private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="11088-116">**Se si utilizza una password per l'autenticazione SSH**, è necessario tooprovide password hello, quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="11088-116">**If you use a password for SSH authentication**, you need tooprovide hello password when prompted.</span></span>

<span data-ttu-id="11088-117">Per altre informazioni sull'uso di SSH con HDInsight, vedere l'articolo [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="11088-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="11088-118"><a id="hadoop"></a>Usare i comandi Hadoop</span><span class="sxs-lookup"><span data-stu-id="11088-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="11088-119">Dopo avere connesso toohello cluster HDInsight, toostart un processo MapReduce il comando che segue hello di utilizzo:</span><span class="sxs-lookup"><span data-stu-id="11088-119">After you are connected toohello HDInsight cluster, use hello following command toostart a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="11088-120">Questo comando Avvia hello `wordcount` (classe), contenute in hello `hadoop-mapreduce-examples.jar` file.</span><span class="sxs-lookup"><span data-stu-id="11088-120">This command starts hello `wordcount` class, which is contained in hello `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="11088-121">Usa hello `/example/data/gutenberg/davinci.txt` documento come input e output viene memorizzato in `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="11088-121">It uses hello `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="11088-122">Per ulteriori informazioni su questi dati di esempio MapReduce hello e di processo, vedere [utilizzare MapReduce in Hadoop in HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="11088-122">For more information about this MapReduce job and hello example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="11088-123">processo Hello genera dettagli come elabora e restituisce informazioni toohello simile seguente testo al termine il processo di hello:</span><span class="sxs-lookup"><span data-stu-id="11088-123">hello job emits details as it processes, and it returns information similar toohello following text when hello job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="11088-124">Al termine del processo di hello, utilizzare i seguenti file di output di comando toolist hello hello:</span><span class="sxs-lookup"><span data-stu-id="11088-124">When hello job completes, use hello following command toolist hello output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="11088-125">Con questo comando vengono visualizzati due file: `_SUCCESS` e `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="11088-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="11088-126">Hello `part-r-00000` file contiene l'output di hello per questo processo.</span><span class="sxs-lookup"><span data-stu-id="11088-126">hello `part-r-00000` file contains hello output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="11088-127">Alcuni processi MapReduce possono dividere risultati hello in più **parte-r-# # #** file.</span><span class="sxs-lookup"><span data-stu-id="11088-127">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="11088-128">In questo caso, utilizzare hello # # # suffisso ordine hello tooindicate dei file hello.</span><span class="sxs-lookup"><span data-stu-id="11088-128">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>

4. <span data-ttu-id="11088-129">l'output di hello tooview, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="11088-129">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="11088-130">Questo comando Visualizza un elenco di parole hello contenuti in hello **wasb://example/data/gutenberg/davinci.txt** file e hello il numero di volte in cui ogni parola si è verificato.</span><span class="sxs-lookup"><span data-stu-id="11088-130">This command displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file and hello number of times each word occurred.</span></span> <span data-ttu-id="11088-131">Hello testo riportato di seguito è riportato un esempio di hello i dati contenuti nel file hello:</span><span class="sxs-lookup"><span data-stu-id="11088-131">hello following text is an example of hello data that is contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="11088-132"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="11088-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="11088-133">Come si può notare, i comandi di Hadoop forniscono toorun un modo semplice i processi MapReduce in un cluster HDInsight e visualizzazione output di hello processo.</span><span class="sxs-lookup"><span data-stu-id="11088-133">As you can see, Hadoop commands provide an easy way toorun MapReduce jobs in an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="11088-134"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="11088-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="11088-135">Per informazioni generali sui processi MapReduce in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="11088-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="11088-136">Usare MapReduce in HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="11088-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="11088-137">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="11088-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="11088-138">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="11088-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="11088-139">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="11088-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
