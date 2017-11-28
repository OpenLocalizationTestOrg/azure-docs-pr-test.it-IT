---
title: aaaUse Hadoop Pig con SSH in un cluster HDInsight - Azure | Documenti Microsoft
description: Informazioni su come connettersi cluster basati su Linux, Hadoop tooa con SSH, e quindi Usa hello Pig comando toorun latino Pig istruzioni in modo interattivo o come un batch di processo.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a><span data-ttu-id="294b6-103">Eseguire i processi di Pig in un cluster basato su Linux con hello comando Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="294b6-103">Run Pig jobs on a Linux-based cluster with hello Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="294b6-104">Informazioni su come eseguire processi Pig di toointeractively da un cluster di HDInsight tooyour connessione SSH.</span><span class="sxs-lookup"><span data-stu-id="294b6-104">Learn how toointeractively run Pig jobs from an SSH connection tooyour HDInsight cluster.</span></span> <span data-ttu-id="294b6-105">Hello linguaggio di programmazione Pig latino consente trasformazioni toodescribe di output di hello desiderato tooproduce dati applicato toohello di input.</span><span class="sxs-lookup"><span data-stu-id="294b6-105">hello Pig Latin programming language allows you toodescribe transformations that are applied toohello input data tooproduce hello desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="294b6-106">Hello passaggi in questo documento richiedono un cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="294b6-106">hello steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="294b6-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="294b6-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="294b6-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="294b6-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="294b6-109"><a id="ssh"></a>Connettersi con SSH</span><span class="sxs-lookup"><span data-stu-id="294b6-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="294b6-110">Utilizzare cluster di HDInsight tooyour tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="294b6-110">Use SSH tooconnect tooyour HDInsight cluster.</span></span> <span data-ttu-id="294b6-111">esempio Hello collega tooa cluster denominato **myhdinsight** come account hello denominato **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="294b6-111">hello following example connects tooa cluster named **myhdinsight** as hello account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="294b6-112">**Se si fornisce una chiave del certificato per l'autenticazione SSH** al momento della creazione del cluster HDInsight hello, potrebbe essere necessario percorso hello toospecify della chiave privata hello nel sistema client.</span><span class="sxs-lookup"><span data-stu-id="294b6-112">**If you provided a certificate key for SSH authentication** when you created hello HDInsight cluster, you may need toospecify hello location of hello private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="294b6-113">**Se è stata specificata una password per l'autenticazione SSH** al momento della creazione del cluster HDInsight hello, fornire una password, hello quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="294b6-113">**If you provided a password for SSH authentication** when you created hello HDInsight cluster, provide hello password when prompted.</span></span>

<span data-ttu-id="294b6-114">Per altre informazioni sull'uso di SSH con HDInsight, vedere l'articolo [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="294b6-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="294b6-115"><a id="pig"></a>Comando Pig hello</span><span class="sxs-lookup"><span data-stu-id="294b6-115"><a id="pig"></a>Use hello Pig command</span></span>

1. <span data-ttu-id="294b6-116">Una volta connessi, è possibile avviare interfaccia della riga di comando di hello Pig (CLI) utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="294b6-116">Once connected, start hello Pig command-line interface (CLI) by using hello following command:</span></span>

        pig

    <span data-ttu-id="294b6-117">Dopo qualche istante verrà visualizzato un prompt dei comandi `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="294b6-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="294b6-118">Immettere l'istruzione hello:</span><span class="sxs-lookup"><span data-stu-id="294b6-118">Enter hello following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="294b6-119">Il comando Carica contenuto hello del file sample.log hello nei log.</span><span class="sxs-lookup"><span data-stu-id="294b6-119">This command loads hello contents of hello sample.log file into LOGS.</span></span> <span data-ttu-id="294b6-120">È possibile visualizzare il contenuto di hello del file hello utilizzando hello seguente istruzione:</span><span class="sxs-lookup"><span data-stu-id="294b6-120">You can view hello contents of hello file by using hello following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="294b6-121">Trasformare quindi dati hello applicando un livello di registrazione di hello solo tooextract di espressione regolare di ogni record utilizzando hello seguente istruzione:</span><span class="sxs-lookup"><span data-stu-id="294b6-121">Next, transform hello data by applying a regular expression tooextract only hello logging level from each record by using hello following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="294b6-122">È possibile utilizzare **DUMP** dati hello tooview dopo la trasformazione hello.</span><span class="sxs-lookup"><span data-stu-id="294b6-122">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="294b6-123">In questo caso, usare `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="294b6-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="294b6-124">Continuare l'applicazione di trasformazioni utilizzando le istruzioni di hello nei hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="294b6-124">Continue applying transformations by using hello statements in hello following table:</span></span>

    | <span data-ttu-id="294b6-125">Istruzione Pig Latin</span><span class="sxs-lookup"><span data-stu-id="294b6-125">Pig Latin statement</span></span> | <span data-ttu-id="294b6-126">Quale istruzione hello</span><span class="sxs-lookup"><span data-stu-id="294b6-126">What hello statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="294b6-127">Rimuove le righe che contengono un valore null per il livello di registrazione hello e archivia i risultati di hello in `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="294b6-127">Removes rows that contain a null value for hello log level and stores hello results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="294b6-128">Hello di gruppi di righe dal livello di registrazione e archivia i risultati di hello in `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="294b6-128">Groups hello rows by log level and stores hello results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="294b6-129">Crea un set di dati che contiene ciascun valore univoco del livello di registrazione e il numero di occorrenze.</span><span class="sxs-lookup"><span data-stu-id="294b6-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="294b6-130">set di dati Hello viene archiviato in `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="294b6-130">hello data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="294b6-131">Ordina i livelli di registrazione hello in base al conteggio (decrescente) e archivia in `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="294b6-131">Orders hello log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="294b6-132">Utilizzare `DUMP` risultato hello tooview della trasformazione hello dopo ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="294b6-132">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

5. <span data-ttu-id="294b6-133">È inoltre possibile salvare i risultati di hello di una trasformazione utilizzando hello `STORE` istruzione.</span><span class="sxs-lookup"><span data-stu-id="294b6-133">You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="294b6-134">Ad esempio, hello istruzione Salva hello `RESULT` toohello `/example/data/pigout` directory di archiviazione hello predefiniti per il cluster:</span><span class="sxs-lookup"><span data-stu-id="294b6-134">For example, hello following statement saves hello `RESULT` toohello `/example/data/pigout` directory on hello default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="294b6-135">dati Hello viene archiviati nella directory specificata di hello in file denominati `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="294b6-135">hello data is stored in hello specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="294b6-136">Se esiste già una directory di hello, viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="294b6-136">If hello directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="294b6-137">hello tooexit grunt prompt dei comandi, immettere l'istruzione hello:</span><span class="sxs-lookup"><span data-stu-id="294b6-137">tooexit hello grunt prompt, enter hello following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="294b6-138">File batch di Pig Latin</span><span class="sxs-lookup"><span data-stu-id="294b6-138">Pig Latin batch files</span></span>

<span data-ttu-id="294b6-139">È inoltre possibile utilizzare hello Pig comando toorun latino Pig contenuti in un file.</span><span class="sxs-lookup"><span data-stu-id="294b6-139">You can also use hello Pig command toorun Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="294b6-140">Dopo la chiusura prompt grunt hello, seguente hello utilizzare comando toopipe STDIN in un file denominato `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="294b6-140">After exiting hello grunt prompt, use hello following command toopipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="294b6-141">Questo file viene creato nella directory home hello hello account utente SSH.</span><span class="sxs-lookup"><span data-stu-id="294b6-141">This file is created in hello home directory for hello SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="294b6-142">Digitare o incollare hello le righe seguenti e quindi utilizzare Ctrl + D al termine.</span><span class="sxs-lookup"><span data-stu-id="294b6-142">Type or paste hello following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="294b6-143">Comando che segue di hello utilizzare hello toorun `pigbatch.pig` file utilizzando il comando di Pig hello.</span><span class="sxs-lookup"><span data-stu-id="294b6-143">Use hello following command toorun hello `pigbatch.pig` file by using hello Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="294b6-144">Al termine del processo batch hello, vedrai hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="294b6-144">Once hello batch job finishes, you see hello following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="294b6-145"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="294b6-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="294b6-146">Per informazioni generali su Pig in HDInsight, vedere hello seguente documento:</span><span class="sxs-lookup"><span data-stu-id="294b6-146">For general information on Pig in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="294b6-147">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="294b6-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="294b6-148">Per ulteriori informazioni su altri modi di toowork con Hadoop in HDInsight, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="294b6-148">For more information on other ways toowork with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="294b6-149">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="294b6-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="294b6-150">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="294b6-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
