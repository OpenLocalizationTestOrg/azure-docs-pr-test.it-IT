---
title: aaaUse Hadoop Pig con Desktop remoto in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse hello Pig comando toorun latino Pig le istruzioni da un cluster di Hadoop basato su Windows tooa connessione Desktop remoto in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="19e04-103">Eseguire processi Pig da una connessione Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="19e04-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="19e04-104">Questo documento fornisce una procedura dettagliata per l'utilizzo di istruzioni hello Pig comando toorun latino Pig da un cluster di HDInsight basati su Windows tooa connessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="19e04-104">This document provides a walkthrough for using hello Pig command toorun Pig Latin statements from a Remote Desktop connection tooa Windows-based HDInsight cluster.</span></span> <span data-ttu-id="19e04-105">Alfabeto latino Pig consente toocreate MapReduce applicazioni descrivendo le trasformazioni dei dati, anziché eseguire il mapping e ridurre le funzioni.</span><span class="sxs-lookup"><span data-stu-id="19e04-105">Pig Latin allows you toocreate MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19e04-106">Desktop remoto è disponibile solo nei cluster HDInsight che usa Windows come sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="19e04-106">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="19e04-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="19e04-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="19e04-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="19e04-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="19e04-109">Per HDInsight 3.4 o successiva, vedere [usare Pig con HDInsight e SSH](hdinsight-hadoop-use-pig-ssh.md) per informazioni sull'esecuzione di Pig in modo interattivo i processi direttamente nel hello cluster da una riga di comando.</span><span class="sxs-lookup"><span data-stu-id="19e04-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="19e04-110"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="19e04-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="19e04-111">passaggi di hello toocomplete in questo articolo, sarà necessario seguente hello.</span><span class="sxs-lookup"><span data-stu-id="19e04-111">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="19e04-112">Un cluster HDInsight (Hadoop in HDInsight) basato su Windows</span><span class="sxs-lookup"><span data-stu-id="19e04-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="19e04-113">Un computer client che esegue Windows 10, Windows 8 o Windows 7</span><span class="sxs-lookup"><span data-stu-id="19e04-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="19e04-114"><a id="connect"></a>Connettersi con Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="19e04-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="19e04-115">Abilitare Desktop remoto per il cluster HDInsight hello e quindi connettersi tooit seguendo le istruzioni di hello in [connettersi tooHDInsight cluster tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="19e04-115">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="19e04-116"><a id="pig"></a>Comando Pig hello</span><span class="sxs-lookup"><span data-stu-id="19e04-116"><a id="pig"></a>Use hello Pig command</span></span>
1. <span data-ttu-id="19e04-117">Dopo aver creato una connessione Desktop remoto, avviare hello **della riga di comando Hadoop** utilizzando icona hello sul desktop di hello.</span><span class="sxs-lookup"><span data-stu-id="19e04-117">After you have a Remote Desktop connection, start hello **Hadoop Command Line** by using hello icon on hello desktop.</span></span>
2. <span data-ttu-id="19e04-118">Utilizzare hello toostart hello Pig comando seguente:</span><span class="sxs-lookup"><span data-stu-id="19e04-118">Use hello following toostart hello Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="19e04-119">Verrà visualizzato un prompt dei comandi `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="19e04-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="19e04-120">Immettere l'istruzione hello:</span><span class="sxs-lookup"><span data-stu-id="19e04-120">Enter hello following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="19e04-121">Il comando Carica contenuto hello del file sample.log hello in file log hello.</span><span class="sxs-lookup"><span data-stu-id="19e04-121">This command loads hello contents of hello sample.log file into hello LOGS file.</span></span> <span data-ttu-id="19e04-122">È possibile visualizzare il contenuto di hello del file hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="19e04-122">You can view hello contents of hello file by using hello following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="19e04-123">Trasformare i dati di hello applicando un livello di registrazione di hello solo tooextract di espressione regolare di ogni record:</span><span class="sxs-lookup"><span data-stu-id="19e04-123">Transform hello data by applying a regular expression tooextract only hello logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="19e04-124">È possibile utilizzare **DUMP** dati hello tooview dopo la trasformazione hello.</span><span class="sxs-lookup"><span data-stu-id="19e04-124">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="19e04-125">In questo caso, `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="19e04-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="19e04-126">Continuare l'applicazione di trasformazioni utilizzando hello seguendo le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="19e04-126">Continue applying transformations by using hello following statements.</span></span> <span data-ttu-id="19e04-127">Utilizzare `DUMP` risultato hello tooview della trasformazione hello dopo ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="19e04-127">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="19e04-128">Istruzione</span><span class="sxs-lookup"><span data-stu-id="19e04-128">Statement</span></span></th><th><span data-ttu-id="19e04-129">Risultato</span><span class="sxs-lookup"><span data-stu-id="19e04-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="19e04-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="19e04-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="19e04-131">Rimuove le righe che contengono un valore null per il livello di registrazione hello e archivia i risultati di hello in FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="19e04-131">Removes rows that contain a null value for hello log level and stores hello results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="19e04-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="19e04-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="19e04-133">Hello di gruppi di righe dal livello di registrazione e archivia i risultati di hello in GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="19e04-133">Groups hello rows by log level and stores hello results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="19e04-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="19e04-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="19e04-135">Crea un nuovo set di dati che contiene ciascun valore univoco del livello di registrazione e il numero di occorrenze.</span><span class="sxs-lookup"><span data-stu-id="19e04-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="19e04-136">I risultati vengono memorizzati in FREQUENCIES</span><span class="sxs-lookup"><span data-stu-id="19e04-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="19e04-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="19e04-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="19e04-138">Ordina i livelli di registrazione hello conteggio (decrescente) e archivia nel risultato</span><span class="sxs-lookup"><span data-stu-id="19e04-138">Orders hello log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="19e04-139">
6.È inoltre possibile salvare i risultati di hello di una trasformazione utilizzando hello `STORE` istruzione.</span><span class="sxs-lookup"><span data-stu-id="19e04-139">
6. You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="19e04-140">Ad esempio, hello comando seguente salva hello `RESULT` toohello **/example/data/pigout** directory nel contenitore di archiviazione hello predefinito per il cluster:</span><span class="sxs-lookup"><span data-stu-id="19e04-140">For example, hello following command saves hello `RESULT` toohello **/example/data/pigout** directory in hello default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="19e04-141">dati Hello viene archiviati nella directory specificata di hello in file denominati **parte nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="19e04-141">hello data is stored in hello specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="19e04-142">Se esiste già una directory di hello, si riceverà un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="19e04-142">If hello directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="19e04-143">hello tooexit grunt prompt dei comandi, immettere l'istruzione hello.</span><span class="sxs-lookup"><span data-stu-id="19e04-143">tooexit hello grunt prompt, enter hello following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="19e04-144">File batch di Pig Latin</span><span class="sxs-lookup"><span data-stu-id="19e04-144">Pig Latin batch files</span></span>
<span data-ttu-id="19e04-145">Inoltre, è possibile utilizzare hello Pig comando toorun latino Pig contenuta in un file.</span><span class="sxs-lookup"><span data-stu-id="19e04-145">You can also use hello Pig command toorun Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="19e04-146">Dopo la chiusura prompt grunt hello, aprire **blocco note** e creare un nuovo file denominato **pigbatch.pig** in hello **PIG_HOME %** directory.</span><span class="sxs-lookup"><span data-stu-id="19e04-146">After exiting hello grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in hello **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="19e04-147">Tipo o a seguito di hello Incolla righe in hello **pigbatch.pig** file e quindi salvarlo:</span><span class="sxs-lookup"><span data-stu-id="19e04-147">Type or paste hello following lines into hello **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="19e04-148">Hello utilizzare seguente hello toorun **pigbatch.pig** file utilizzando il comando di pig hello.</span><span class="sxs-lookup"><span data-stu-id="19e04-148">Use hello following toorun hello **pigbatch.pig** file using hello pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="19e04-149">Al termine del processo batch hello, verrà visualizzato dopo l'output, che deve essere hello stesso come quando si utilizza hello `DUMP RESULT;` nei passaggi precedenti hello:</span><span class="sxs-lookup"><span data-stu-id="19e04-149">When hello batch job completes, you should see hello following output, which should be hello same as when you used `DUMP RESULT;` in hello previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="19e04-150"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="19e04-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="19e04-151">Come si può notare, hello comando Pig consente toointeractively consentono di eseguire operazioni di MapReduce o eseguire processi latino Pig archiviate in un file batch.</span><span class="sxs-lookup"><span data-stu-id="19e04-151">As you can see, hello Pig command allows you toointeractively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="19e04-152"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="19e04-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="19e04-153">Per informazioni generali su Pig in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="19e04-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="19e04-154">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="19e04-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="19e04-155">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="19e04-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="19e04-156">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="19e04-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="19e04-157">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="19e04-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
