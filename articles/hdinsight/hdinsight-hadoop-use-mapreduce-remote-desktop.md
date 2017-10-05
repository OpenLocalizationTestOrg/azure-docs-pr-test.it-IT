---
title: MapReduce e Remote Desktop con Hadoop in HDInsight - Azure | Microsoft Docs
description: Informazioni su come usare Desktop remoto per connettersi a Hadoop in HDInsight ed eseguire processi MapReduce.
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
ms.openlocfilehash: b56674857b013f9bb3d4dd4b6e97b34e0a97b1b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="4915d-103">Uso di MapReduce con Hadoop in HDInsight con Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="4915d-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="4915d-104">In questo articolo si apprenderà come connettersi a un cluster Hadoop in HDInsight usando Desktop remoto e quindi eseguire processi MapReduce usando il comando Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4915d-104">In this article, you will learn how to connect to a Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using the Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4915d-105">Desktop re,moto è disponibile solo nei cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="4915d-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="4915d-106">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="4915d-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4915d-107">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4915d-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="4915d-108">Per HDInsight 3.4 o versione successiva, vedere [Usare MapReduce con SSH](hdinsight-hadoop-use-mapreduce-ssh.md) per informazioni sulla connessione al cluster HDInsight e l'esecuzione di processi MapReduce.</span><span class="sxs-lookup"><span data-stu-id="4915d-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting to the HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="4915d-109"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4915d-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="4915d-110">Per seguire la procedura descritta in questo articolo, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="4915d-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="4915d-111">Un cluster HDInsight (Hadoop in HDInsight) basato su Windows</span><span class="sxs-lookup"><span data-stu-id="4915d-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="4915d-112">Un computer client che esegue Windows 10, Windows 8 o Windows 7</span><span class="sxs-lookup"><span data-stu-id="4915d-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="4915d-113"><a id="connect"></a>Connettersi con Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="4915d-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="4915d-114">Abilitare Desktop remoto per il cluster HDInsight e quindi connettersi seguendo le istruzioni disponibili in [Connettersi a cluster HDInsight tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="4915d-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="4915d-115"><a id="hadoop"></a>Usare il comando Hadoop</span><span class="sxs-lookup"><span data-stu-id="4915d-115"><a id="hadoop"></a>Use the Hadoop command</span></span>
<span data-ttu-id="4915d-116">Una volta connessi al desktop per il cluster HDInsight, seguire questa procedura per eseguire un processo MapReduce usando il comando Hadoop:</span><span class="sxs-lookup"><span data-stu-id="4915d-116">When you are connected to the desktop for the HDInsight cluster, use the following steps to run a MapReduce job by using the Hadoop command:</span></span>

1. <span data-ttu-id="4915d-117">Dal desktop di HDInsight avviare la **riga di comando di Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="4915d-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span> <span data-ttu-id="4915d-118">Viene aperta una finestra del prompt dei comandi nella directory **c:\apps\dist\hadoop-&lt;numero versione>**.</span><span class="sxs-lookup"><span data-stu-id="4915d-118">This opens a new command prompt in the **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4915d-119">Quando Hadoop viene aggiornato, il numero di versione viene modificato.</span><span class="sxs-lookup"><span data-stu-id="4915d-119">The version number changes as Hadoop is updated.</span></span> <span data-ttu-id="4915d-120">La variabile di ambiente **HADOOP_HOME** può essere usata per trovare il percorso.</span><span class="sxs-lookup"><span data-stu-id="4915d-120">The **HADOOP_HOME** environment variable can be used to find the path.</span></span> <span data-ttu-id="4915d-121">Ad esempio, `cd %HADOOP_HOME%` modifica le directory nella directory di Hadoop, senza richiedere il nome della versione.</span><span class="sxs-lookup"><span data-stu-id="4915d-121">For example, `cd %HADOOP_HOME%` changes directories to the Hadoop directory, without requiring you to know the version number.</span></span>
   >
   >
2. <span data-ttu-id="4915d-122">Per usare il comando **Hadoop** per l'esecuzione di un processo MapReduce di esempio, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4915d-122">To use the **Hadoop** command to run an example MapReduce job, use the following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="4915d-123">Viene avviata la classe **wordcount**, contenuta nel file **hadoop-mapreduce-examples.jar** nella directory corrente.</span><span class="sxs-lookup"><span data-stu-id="4915d-123">This starts the **wordcount** class, which is contained in the **hadoop-mapreduce-examples.jar** file in the current directory.</span></span> <span data-ttu-id="4915d-124">Come input viene usato il documento **wasb://example/data/gutenberg/davinci.txt** e l'output viene archiviato in: **wasb:///example/data/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="4915d-124">As input, it uses the **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4915d-125">Per altre informazioni su questo processo MapReduce e per dati di esempio, vedere <a href="hdinsight-use-mapreduce.md">Usare MapReduce in Hadoop in HDInsight</a>.</span><span class="sxs-lookup"><span data-stu-id="4915d-125">for more information about this MapReduce job and the example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="4915d-126">Il processo genera dettagli durante l'elaborazione e al completamento restituisce informazioni simili alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="4915d-126">The job emits details as it is processed, and it returns information similar to the following when the job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="4915d-127">Al termine del processo, usare il comando seguente per elencare i file di output archiviati in **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="4915d-127">When the job is complete, use the following command to list the output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="4915d-128">In questo modo, vengono visualizzati due file: **_SUCCESS** e **part-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="4915d-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="4915d-129">Il file **part-r-00000** contiene l'output del processo.</span><span class="sxs-lookup"><span data-stu-id="4915d-129">The **part-r-00000** file contains the output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4915d-130">Alcuni processi MapReduce possono dividere i risultati in più file **part-r-#####** .</span><span class="sxs-lookup"><span data-stu-id="4915d-130">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="4915d-131">In questo caso, usare il suffisso ##### per indicare l'ordine dei file.</span><span class="sxs-lookup"><span data-stu-id="4915d-131">If so, use the ##### suffix to indicate the order of the files.</span></span>
   >
   >
5. <span data-ttu-id="4915d-132">Per visualizzare l'output, usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="4915d-132">To view the output, use the following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="4915d-133">Viene visualizzato un elenco di parole contenute nel file **wasb://example/data/gutenberg/davinci.txt** con il numero di occorrenze di ogni parola.</span><span class="sxs-lookup"><span data-stu-id="4915d-133">This displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file, along with the number of times each word occured.</span></span> <span data-ttu-id="4915d-134">Di seguito è riportato un esempio di dati contenuti nel file:</span><span class="sxs-lookup"><span data-stu-id="4915d-134">The following is an example of the data that will be contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="4915d-135"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="4915d-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="4915d-136">Come è possibile notare, il comando Hadoop fornisce un modo semplice per eseguire processi MapReduce in un cluster HDInsight e visualizzare l'output del processo.</span><span class="sxs-lookup"><span data-stu-id="4915d-136">As you can see, the Hadoop command provides an easy way to run MapReduce jobs on an HDInsight cluster and then view the job output.</span></span>

## <span data-ttu-id="4915d-137"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4915d-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="4915d-138">Per informazioni generali sui processi MapReduce in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4915d-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="4915d-139">Usare MapReduce in HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="4915d-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="4915d-140">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4915d-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="4915d-141">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4915d-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="4915d-142">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4915d-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
