---
title: Usare Pig di Hadoop con Desktop remoto in HDInsight - Azure | Microsoft Docs
description: Informazioni su come usare il comando Pig per l'esecuzione di istruzioni Pig Latin da una connessione Desktop remoto a un cluster Hadoop basato su Windows in HDInsight.
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
ms.openlocfilehash: 5e8d4fbd8afc54c8bbc1a9a71c66d7022a7d5986
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="292d9-103">Eseguire processi Pig da una connessione Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="292d9-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="292d9-104">Questo documento fornisce una procedura dettagliata dell'uso del comando Pig per l'esecuzione di istruzioni Pig Latin da una connessione Desktop remoto a un cluster HDInsight basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="292d9-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="292d9-105">Pig Latin consente di creare applicazioni MapReduce descrivendo le trasformazioni di dati, anziché eseguendo il mapping e la riduzione delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="292d9-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="292d9-106">Desktop remoto è disponibile solo nei cluster HDInsight che usano Windows come sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="292d9-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="292d9-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="292d9-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="292d9-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="292d9-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="292d9-109">Per HDInsight 3.4 o versione successiva, vedere [Usare Pig con HDInsight e SSH](hdinsight-hadoop-use-pig-ssh.md) per informazioni sull'esecuzione interattiva di processi Pig sul cluster dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="292d9-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="292d9-110"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="292d9-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="292d9-111">Per seguire la procedura descritta in questo articolo, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="292d9-111">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="292d9-112">Un cluster HDInsight (Hadoop in HDInsight) basato su Windows</span><span class="sxs-lookup"><span data-stu-id="292d9-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="292d9-113">Un computer client che esegue Windows 10, Windows 8 o Windows 7</span><span class="sxs-lookup"><span data-stu-id="292d9-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="292d9-114"><a id="connect"></a>Connettersi con Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="292d9-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="292d9-115">Abilitare Desktop remoto per il cluster HDInsight e quindi connettersi seguendo le istruzioni disponibili in [Connettersi a cluster HDInsight tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="292d9-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="292d9-116"><a id="pig"></a>Usare il comando Pig</span><span class="sxs-lookup"><span data-stu-id="292d9-116"><a id="pig"></a>Use the Pig command</span></span>
1. <span data-ttu-id="292d9-117">Dopo avere stabilito una connessione Desktop remoto, avviare la **riga di comando di Hadoop** usando l'icona sul desktop.</span><span class="sxs-lookup"><span data-stu-id="292d9-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span></span>
2. <span data-ttu-id="292d9-118">Usare il codice seguente per avviare il comando Pig:</span><span class="sxs-lookup"><span data-stu-id="292d9-118">Use the following to start the Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="292d9-119">Verrà visualizzato un prompt dei comandi `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="292d9-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="292d9-120">Immettere la seguente istruzione:</span><span class="sxs-lookup"><span data-stu-id="292d9-120">Enter the following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="292d9-121">Questo comando carica i contenuti del file sample.log nel file LOGS.</span><span class="sxs-lookup"><span data-stu-id="292d9-121">This command loads the contents of the sample.log file into the LOGS file.</span></span> <span data-ttu-id="292d9-122">È possibile visualizzare i contenuti del file usando il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="292d9-122">You can view the contents of the file by using the following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="292d9-123">Trasformare i dati applicando un'espressione regolare per estrarre solo il livello di registrazione da ciascun record:</span><span class="sxs-lookup"><span data-stu-id="292d9-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="292d9-124">È possibile usare **DUMP** per visualizzare i dati dopo la trasformazione.</span><span class="sxs-lookup"><span data-stu-id="292d9-124">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="292d9-125">In questo caso, `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="292d9-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="292d9-126">Continuare ad applicare le trasformazioni usando le seguenti istruzioni.</span><span class="sxs-lookup"><span data-stu-id="292d9-126">Continue applying transformations by using the following statements.</span></span> <span data-ttu-id="292d9-127">Usare `DUMP` per visualizzare il risultato della trasformazione dopo ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="292d9-127">Use `DUMP` to view the result of the transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="292d9-128">Istruzione</span><span class="sxs-lookup"><span data-stu-id="292d9-128">Statement</span></span></th><th><span data-ttu-id="292d9-129">Risultato</span><span class="sxs-lookup"><span data-stu-id="292d9-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="292d9-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="292d9-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="292d9-131">Rimuove le righe che contengono un valore null per il livello di registrazione e memorizza i risultati in FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="292d9-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="292d9-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="292d9-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="292d9-133">Raggruppa le righe in base al livello di registrazione e memorizza i risultati in GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="292d9-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="292d9-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="292d9-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="292d9-135">Crea un nuovo set di dati che contiene ciascun valore univoco del livello di registrazione e il numero di occorrenze.</span><span class="sxs-lookup"><span data-stu-id="292d9-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="292d9-136">I risultati vengono memorizzati in FREQUENCIES</span><span class="sxs-lookup"><span data-stu-id="292d9-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="292d9-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="292d9-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="292d9-138">Ordina i livelli di registrazione in base al numero (decrescente) e memorizza i risultati in RESULT</span><span class="sxs-lookup"><span data-stu-id="292d9-138">Orders the log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="292d9-139">
6. È anche possibile salvare i risultati di una trasformazione usando `STORE` l'istruzione.</span><span class="sxs-lookup"><span data-stu-id="292d9-139">
6. You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="292d9-140">Ad esempio, il seguente comando salva il valore `RESULT` nella directory **/example/data/pigout** nel contenitore di archiviazione predefinito per il cluster:</span><span class="sxs-lookup"><span data-stu-id="292d9-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="292d9-141">I dati vengono memorizzati nella directory specificata nei file denominati **part-nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="292d9-141">The data is stored in the specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="292d9-142">Se la directory esiste già, si riceverà un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="292d9-142">If the directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="292d9-143">Per uscire dal prompt grunt, immettere la seguente istruzione.</span><span class="sxs-lookup"><span data-stu-id="292d9-143">To exit the grunt prompt, enter the following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="292d9-144">File batch di Pig Latin</span><span class="sxs-lookup"><span data-stu-id="292d9-144">Pig Latin batch files</span></span>
<span data-ttu-id="292d9-145">È inoltre possibile usare il comando Pig per eseguire processi Pig Latin contenuti in un file.</span><span class="sxs-lookup"><span data-stu-id="292d9-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="292d9-146">Dopo aver chiuso il prompt grunt, aprire il **Blocco note** e creare un nuovo file denominato **pigbatch.pig** nella directory **%PIG_HOME%**.</span><span class="sxs-lookup"><span data-stu-id="292d9-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="292d9-147">Digitare o incollare le seguenti righe nel file **pigbatch.pig** e quindi salvarlo:</span><span class="sxs-lookup"><span data-stu-id="292d9-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="292d9-148">Usare quanto segue per eseguire il file **pigbatch.pig** usando il comando pig.</span><span class="sxs-lookup"><span data-stu-id="292d9-148">Use the following to run the **pigbatch.pig** file using the pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="292d9-149">Al termine del processo batch, si otterrà il seguente output, corrispondente a quello ottenuto quando è stato usato `DUMP RESULT;` nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="292d9-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="292d9-150"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="292d9-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="292d9-151">Come si può notare, il comando Pig consente di eseguire in modo interattivo operazioni di MapReduce o di eseguire processi Pig Latin archiviati in un file batch.</span><span class="sxs-lookup"><span data-stu-id="292d9-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="292d9-152"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="292d9-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="292d9-153">Per informazioni generali su Pig in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="292d9-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="292d9-154">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="292d9-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="292d9-155">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="292d9-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="292d9-156">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="292d9-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="292d9-157">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="292d9-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
