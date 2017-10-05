---
title: Usare Pig di Hadoop con SSH in un cluster HDInsight - Azure | Microsoft Docs
description: Informazioni su come connettersi a un cluster Hadoop basato su Linux con SSH e quindi usare il comando Pig per eseguire istruzioni Pig Latin in modo interattivo o come processo batch.
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
ms.openlocfilehash: e4c893ef4bfa573dd9fbc9c9b0ae296720769842
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-the-pig-command-ssh"></a><span data-ttu-id="46fd5-103">Eseguire processi Pig in un cluster basato su Linux con il comando Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="46fd5-103">Run Pig jobs on a Linux-based cluster with the Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="46fd5-104">Informazioni su come eseguire in modo interattivo i processi Pig da una connessione SSH al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="46fd5-104">Learn how to interactively run Pig jobs from an SSH connection to your HDInsight cluster.</span></span> <span data-ttu-id="46fd5-105">Il linguaggio di programmazione Pig Latin consente di descrivere le trasformazioni applicate ai dati di input per produrre l'output desiderato.</span><span class="sxs-lookup"><span data-stu-id="46fd5-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46fd5-106">I passaggi descritti in questo documento richiedono un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="46fd5-106">The steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="46fd5-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="46fd5-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="46fd5-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="46fd5-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="46fd5-109"><a id="ssh"></a>Connettersi con SSH</span><span class="sxs-lookup"><span data-stu-id="46fd5-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="46fd5-110">Connettersi al cluster HDInsight usando SSH.</span><span class="sxs-lookup"><span data-stu-id="46fd5-110">Use SSH to connect to your HDInsight cluster.</span></span> <span data-ttu-id="46fd5-111">L'esempio seguente si connette a un cluster denominato **myhdinsight** come account denominato **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="46fd5-111">The following example connects to a cluster named **myhdinsight** as the account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="46fd5-112">**Se è stata fornita una chiave del certificato per l'autenticazione SSH** durante la creazione del cluster HDInsight, potrebbe essere necessario specificare il percorso della chiave privata nel sistema client.</span><span class="sxs-lookup"><span data-stu-id="46fd5-112">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="46fd5-113">**Se è stata specificata una password per l'autenticazione SSH** durante la creazione del cluster HDInsight, fornire la password quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="46fd5-113">**If you provided a password for SSH authentication** when you created the HDInsight cluster, provide the password when prompted.</span></span>

<span data-ttu-id="46fd5-114">Per altre informazioni sull'uso di SSH con HDInsight, vedere l'articolo [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="46fd5-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="46fd5-115"><a id="pig"></a>Usare il comando Pig</span><span class="sxs-lookup"><span data-stu-id="46fd5-115"><a id="pig"></a>Use the Pig command</span></span>

1. <span data-ttu-id="46fd5-116">Una volta connessi, avviare l'interfaccia della riga di comando di Pig (CLI) tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="46fd5-116">Once connected, start the Pig command-line interface (CLI) by using the following command:</span></span>

        pig

    <span data-ttu-id="46fd5-117">Dopo qualche istante verrà visualizzato un prompt dei comandi `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="46fd5-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="46fd5-118">Immettere la seguente istruzione:</span><span class="sxs-lookup"><span data-stu-id="46fd5-118">Enter the following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="46fd5-119">Questo comando carica i contenuti del file sample. log in LOGS.</span><span class="sxs-lookup"><span data-stu-id="46fd5-119">This command loads the contents of the sample.log file into LOGS.</span></span> <span data-ttu-id="46fd5-120">È possibile visualizzare i contenuti del file usando l'istruzione seguente:</span><span class="sxs-lookup"><span data-stu-id="46fd5-120">You can view the contents of the file by using the following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="46fd5-121">Successivamente, trasformare i dati applicando un'espressione regolare per estrarre solo il livello di registrazione da ogni record usando l'istruzione seguente:</span><span class="sxs-lookup"><span data-stu-id="46fd5-121">Next, transform the data by applying a regular expression to extract only the logging level from each record by using the following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="46fd5-122">È possibile usare **DUMP** per visualizzare i dati dopo la trasformazione.</span><span class="sxs-lookup"><span data-stu-id="46fd5-122">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="46fd5-123">In questo caso, usare `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="46fd5-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="46fd5-124">Continuare ad applicare le trasformazioni usando le istruzioni presenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="46fd5-124">Continue applying transformations by using the statements in the following table:</span></span>

    | <span data-ttu-id="46fd5-125">Istruzione Pig Latin</span><span class="sxs-lookup"><span data-stu-id="46fd5-125">Pig Latin statement</span></span> | <span data-ttu-id="46fd5-126">Funzionamento dell'istruzione</span><span class="sxs-lookup"><span data-stu-id="46fd5-126">What the statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="46fd5-127">Rimuove le righe che contengono un valore null per il livello di registrazione e memorizza i risultati in `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="46fd5-127">Removes rows that contain a null value for the log level and stores the results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="46fd5-128">Raggruppa le righe in base al livello di registrazione e memorizza i risultati in `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="46fd5-128">Groups the rows by log level and stores the results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="46fd5-129">Crea un set di dati che contiene ciascun valore univoco del livello di registrazione e il numero di occorrenze.</span><span class="sxs-lookup"><span data-stu-id="46fd5-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="46fd5-130">Il set di dati viene archiviato in `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="46fd5-130">The data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="46fd5-131">Ordina i livelli di registrazione in base al numero (decrescente) e memorizza i risultati in `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="46fd5-131">Orders the log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="46fd5-132">Usare `DUMP` per visualizzare il risultato della trasformazione dopo ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="46fd5-132">Use `DUMP` to view the result of the transformation after each step.</span></span>

5. <span data-ttu-id="46fd5-133">È anche possibile salvare i risultati di una trasformazione usando l'istruzione `STORE` .</span><span class="sxs-lookup"><span data-stu-id="46fd5-133">You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="46fd5-134">Ad esempio, la seguente istruzione salva l'`RESULT` nella directory `/example/data/pigout` nella risorsa di archiviazione predefinita per il cluster:</span><span class="sxs-lookup"><span data-stu-id="46fd5-134">For example, the following statement saves the `RESULT` to the `/example/data/pigout` directory on the default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="46fd5-135">I dati vengono memorizzati nella directory specificata nei file denominati `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="46fd5-135">The data is stored in the specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="46fd5-136">Se la directory esiste già, si riceve un errore.</span><span class="sxs-lookup"><span data-stu-id="46fd5-136">If the directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="46fd5-137">Per uscire dal prompt grunt, immettere la seguente istruzione:</span><span class="sxs-lookup"><span data-stu-id="46fd5-137">To exit the grunt prompt, enter the following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="46fd5-138">File batch di Pig Latin</span><span class="sxs-lookup"><span data-stu-id="46fd5-138">Pig Latin batch files</span></span>

<span data-ttu-id="46fd5-139">È inoltre possibile usare il comando Pig per eseguire processi Pig Latin contenuti in un file.</span><span class="sxs-lookup"><span data-stu-id="46fd5-139">You can also use the Pig command to run Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="46fd5-140">Dopo aver chiuso il prompt grunt, usare il seguente comando per indirizzare STDIN in un file denominato `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="46fd5-140">After exiting the grunt prompt, use the following command to pipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="46fd5-141">Questo file viene creato nella home directory per l'account utente SSH.</span><span class="sxs-lookup"><span data-stu-id="46fd5-141">This file is created in the home directory for the SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="46fd5-142">Digitare o incollare le righe seguenti e quindi premere CTRL+D al termine.</span><span class="sxs-lookup"><span data-stu-id="46fd5-142">Type or paste the following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="46fd5-143">Usare l'istruzione seguente per eseguire il file `pigbatch.pig` tramite il comando Pig.</span><span class="sxs-lookup"><span data-stu-id="46fd5-143">Use the following command to run the `pigbatch.pig` file by using the Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="46fd5-144">Al termine dell'esecuzione del processo batch, verrà visualizzato il seguente output:</span><span class="sxs-lookup"><span data-stu-id="46fd5-144">Once the batch job finishes, you see the following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="46fd5-145"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46fd5-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="46fd5-146">Per informazioni generali su sull'uso di Pig con HDInsight, vedere il documento seguente:</span><span class="sxs-lookup"><span data-stu-id="46fd5-146">For general information on Pig in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="46fd5-147">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="46fd5-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="46fd5-148">Per altre informazioni su come usare Hadoop con HDInsight, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="46fd5-148">For more information on other ways to work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="46fd5-149">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="46fd5-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="46fd5-150">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="46fd5-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
