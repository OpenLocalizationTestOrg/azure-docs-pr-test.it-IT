---
title: aaaMapReduce e Desktop remoto con Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse Desktop remoto tooconnect tooHadoop HDInsight e l'esecuzione dei processi di MapReduce.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="5371c-103">Uso di MapReduce con Hadoop in HDInsight con Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="5371c-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="5371c-104">In questo articolo verrà informazioni su come tooconnect tooa Hadoop in HDInsight cluster tramite Desktop remoto e quindi eseguire i processi MapReduce utilizzando i comandi di Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="5371c-104">In this article, you will learn how tooconnect tooa Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using hello Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5371c-105">Desktop re,moto è disponibile solo nei cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="5371c-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="5371c-106">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="5371c-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5371c-107">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5371c-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="5371c-108">Per HDInsight 3.4 o successiva, vedere [utilizzare MapReduce con SSH](hdinsight-hadoop-use-mapreduce-ssh.md) per informazioni sulla connessione cluster HDInsight toohello e in esecuzione processi di MapReduce.</span><span class="sxs-lookup"><span data-stu-id="5371c-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting toohello HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="5371c-109"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5371c-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="5371c-110">passaggi di hello toocomplete in questo articolo, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="5371c-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="5371c-111">Un cluster HDInsight (Hadoop in HDInsight) basato su Windows</span><span class="sxs-lookup"><span data-stu-id="5371c-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="5371c-112">Un computer client che esegue Windows 10, Windows 8 o Windows 7</span><span class="sxs-lookup"><span data-stu-id="5371c-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="5371c-113"><a id="connect"></a>Connettersi con Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="5371c-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="5371c-114">Abilitare Desktop remoto per il cluster HDInsight hello e quindi connettersi tooit seguendo le istruzioni di hello in [connettersi tooHDInsight cluster tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="5371c-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="5371c-115"><a id="hadoop"></a>Utilizzare il comando di Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="5371c-115"><a id="hadoop"></a>Use hello Hadoop command</span></span>
<span data-ttu-id="5371c-116">Quando si è connessi toohello desktop per il cluster HDInsight hello, utilizzare hello seguendo i passaggi toorun un processo MapReduce tramite il comando di Hadoop hello:</span><span class="sxs-lookup"><span data-stu-id="5371c-116">When you are connected toohello desktop for hello HDInsight cluster, use hello following steps toorun a MapReduce job by using hello Hadoop command:</span></span>

1. <span data-ttu-id="5371c-117">Dal desktop di HDInsight hello, avviare hello **della riga di comando Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="5371c-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span> <span data-ttu-id="5371c-118">Si apre un nuovo prompt in hello **c:\apps\dist\hadoop-&lt;numero di versione >** directory.</span><span class="sxs-lookup"><span data-stu-id="5371c-118">This opens a new command prompt in hello **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5371c-119">numero di versione di Hello cambia in caso di aggiornamento Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5371c-119">hello version number changes as Hadoop is updated.</span></span> <span data-ttu-id="5371c-120">Hello **HADOOP_HOME** variabile di ambiente può essere il percorso di hello toofind utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5371c-120">hello **HADOOP_HOME** environment variable can be used toofind hello path.</span></span> <span data-ttu-id="5371c-121">Ad esempio, `cd %HADOOP_HOME%` modifiche directory toohello directory Hadoop, senza la necessità di un numero di versione di hello tooknow.</span><span class="sxs-lookup"><span data-stu-id="5371c-121">For example, `cd %HADOOP_HOME%` changes directories toohello Hadoop directory, without requiring you tooknow hello version number.</span></span>
   >
   >
2. <span data-ttu-id="5371c-122">hello toouse **Hadoop** toorun un processo MapReduce di esempio di comando, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5371c-122">toouse hello **Hadoop** command toorun an example MapReduce job, use hello following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="5371c-123">Verrà avviata hello **wordcount** (classe), contenute in hello **hadoop-mapreduce-examples.jar** file nella directory corrente hello.</span><span class="sxs-lookup"><span data-stu-id="5371c-123">This starts hello **wordcount** class, which is contained in hello **hadoop-mapreduce-examples.jar** file in hello current directory.</span></span> <span data-ttu-id="5371c-124">Usa come input, hello **wasb://example/data/gutenberg/davinci.txt** documento e l'output è memorizzato nel: **wasb: / / / esempio/data/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="5371c-124">As input, it uses hello **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5371c-125">Per ulteriori informazioni su questi dati di esempio MapReduce hello e di processo, vedere <a href="hdinsight-use-mapreduce.md">utilizzare MapReduce di HDInsight Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="5371c-125">for more information about this MapReduce job and hello example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="5371c-126">processo Hello genera dettagli come l'elaborazione e restituisce toohello informazioni simili che seguono. una volta completato il processo di hello:</span><span class="sxs-lookup"><span data-stu-id="5371c-126">hello job emits details as it is processed, and it returns information similar toohello following when hello job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="5371c-127">Una volta completato il processo di hello, utilizzare hello i seguenti file di comando toolist hello output è archiviati in **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="5371c-127">When hello job is complete, use hello following command toolist hello output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="5371c-128">In questo modo, vengono visualizzati due file: **_SUCCESS** e **part-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="5371c-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="5371c-129">Hello **parte-r-00000** file contiene l'output di hello per questo processo.</span><span class="sxs-lookup"><span data-stu-id="5371c-129">hello **part-r-00000** file contains hello output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5371c-130">Alcuni processi MapReduce possono dividere risultati hello in più **parte-r-# # #** file.</span><span class="sxs-lookup"><span data-stu-id="5371c-130">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="5371c-131">In questo caso, utilizzare hello # # # suffisso ordine hello tooindicate dei file hello.</span><span class="sxs-lookup"><span data-stu-id="5371c-131">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>
   >
   >
5. <span data-ttu-id="5371c-132">l'output di hello tooview, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5371c-132">tooview hello output, use hello following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="5371c-133">Consente di visualizzare un elenco di parole hello contenuti in hello **wasb://example/data/gutenberg/davinci.txt** file, con numero di hello di volte in cui ogni parola si è verificato.</span><span class="sxs-lookup"><span data-stu-id="5371c-133">This displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file, along with hello number of times each word occured.</span></span> <span data-ttu-id="5371c-134">Hello Ecco un esempio di dati hello che saranno contenuti nel file hello:</span><span class="sxs-lookup"><span data-stu-id="5371c-134">hello following is an example of hello data that will be contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="5371c-135"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5371c-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="5371c-136">Come si può notare, hello Hadoop comando fornisce toorun un modo semplice i processi MapReduce in un cluster HDInsight e visualizzazione output di hello processo.</span><span class="sxs-lookup"><span data-stu-id="5371c-136">As you can see, hello Hadoop command provides an easy way toorun MapReduce jobs on an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="5371c-137"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5371c-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="5371c-138">Per informazioni generali sui processi MapReduce in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5371c-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="5371c-139">Usare MapReduce in HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="5371c-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="5371c-140">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5371c-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="5371c-141">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5371c-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5371c-142">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5371c-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
