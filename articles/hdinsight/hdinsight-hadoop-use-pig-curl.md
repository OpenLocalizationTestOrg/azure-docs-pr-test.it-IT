---
title: Usare Pig di Hadoop con REST in HDInsight - Azure | Microsoft Docs
description: Informazioni su come usare REST per eseguire processi Pig Latin in un cluster Hadoop in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a86864a779b0de1c6d5669cfbba0f3e1a27f1ff1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="b6b0f-103">Eseguire processi Pig con Hadoop in HDInsight tramite REST</span><span class="sxs-lookup"><span data-stu-id="b6b0f-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="b6b0f-104">Informazioni su come eseguire processi Pig Latin inviando richieste REST a un cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-104">Learn how to run Pig Latin jobs by making REST requests to an Azure HDInsight cluster.</span></span> <span data-ttu-id="b6b0f-105">Per illustrare come poter interagire con HDInsight usando l'API REST WebHCat, viene usato Curl.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-105">Curl is used to demonstrate how you can interact with HDInsight using the WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="b6b0f-106">Se si ha già familiarità con l'uso di server Hadoop basati su Linux ma non si è esperti di HDInsight, vedere [Informazioni sull'uso di HDInsight in Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="b6b0f-106">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="b6b0f-107"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b6b0f-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="b6b0f-108">Un cluster Azure HDInsight (Hadoop in HDInsight) (basato su Linux o basato su Windows)</span><span class="sxs-lookup"><span data-stu-id="b6b0f-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b6b0f-109">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b6b0f-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b6b0f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="b6b0f-111">Curl</span><span class="sxs-lookup"><span data-stu-id="b6b0f-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="b6b0f-112">jq</span><span class="sxs-lookup"><span data-stu-id="b6b0f-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="b6b0f-113"><a id="curl"></a>Eseguire processi Pig mediante Curl</span><span class="sxs-lookup"><span data-stu-id="b6b0f-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="b6b0f-114">L'API REST viene protetta tramite l' [autenticazione dell'accesso di base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="b6b0f-114">The REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="b6b0f-115">Per essere certi che le credenziali vengano inviate al server in modo sicuro, eseguire sempre le richieste usando il protocollo Secure HTTP (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="b6b0f-115">Always make requests by using Secure HTTP (HTTPS) to ensure that your credentials are securely sent to the server.</span></span>
>
> <span data-ttu-id="b6b0f-116">Quando si usano i comandi riportati in questa sezione, sostituire `USERNAME` con l'utente da autenticare nel cluster e `PASSWORD` con la password dell'account utente.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-116">When using the commands in this section, replace `USERNAME` with the user to authenticate to the cluster, and replace `PASSWORD` with the password for the user account.</span></span> <span data-ttu-id="b6b0f-117">Sostituire `CLUSTERNAME` con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-117">Replace `CLUSTERNAME` with the name of your cluster.</span></span>
>


1. <span data-ttu-id="b6b0f-118">Da una riga di comando usare il comando seguente per verificare che sia possibile connettersi al cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b6b0f-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="b6b0f-119">Dovrebbe essere visualizzata la risposta JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="b6b0f-119">You should receive the following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="b6b0f-120">I parametri usati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6b0f-120">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="b6b0f-121">**-u**: il nome utente e la password usati per autenticare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-121">**-u**: The user name and password used to authenticate the request</span></span>
    * <span data-ttu-id="b6b0f-122">**-G**: indica che è una richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="b6b0f-123">L'inizio dell'URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, sarà uguale per tutte le richieste.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-123">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="b6b0f-124">Il percorso, **/status**, indica che la richiesta deve restituire lo stato di WebHCat, noto anche come Templeton, per il server.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-124">The path, **/status**, indicates that the request is to return the status of WebHCat (also known as Templeton) for the server.</span></span>

2. <span data-ttu-id="b6b0f-125">Usare il seguente codice per inviare un processo Pig Latin al cluster:</span><span class="sxs-lookup"><span data-stu-id="b6b0f-125">Use the following code to submit a Pig Latin job to the cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="b6b0f-126">I parametri usati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6b0f-126">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="b6b0f-127">**-d**: dato che `-G` non viene usato, la richiesta userà il metodo POST per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-127">**-d**: Because `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="b6b0f-128">`-d` specifica i valori di dati che vengono inviati con la richiesta.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-128">`-d` specifies the data values that are sent with the request.</span></span>

    * <span data-ttu-id="b6b0f-129">**user.name**: l'utente che esegue il comando.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="b6b0f-130">**execute**: le istruzioni Pig Latin da eseguire.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-130">**execute**: The Pig Latin statements to execute</span></span>
    * <span data-ttu-id="b6b0f-131">**statusdir**: la directory in cui è scritto lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-131">**statusdir**: The directory that the status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6b0f-132">Si noti che gli spazi tra le istruzioni Pig Latin vengono sostituiti dal carattere `+` se è in uso Curl.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-132">Notice that the spaces in Pig Latin statements are replaced by the `+` character when used with Curl.</span></span>

    <span data-ttu-id="b6b0f-133">Questo comando dovrebbe restituire un ID processo utilizzabile per verificare lo stato del processo, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b6b0f-133">This command should return a job ID that can be used to check the status of the job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="b6b0f-134">Per verificare lo stato del processo, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b6b0f-134">To check the status of the job, use the following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="b6b0f-135">Sostituire `JOBID` con il valore restituito nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-135">Replace `JOBID` with the value returned in the previous step.</span></span> <span data-ttu-id="b6b0f-136">Se, ad esempio, il valore restituito è `{"id":"job_1415651640909_0026"}`, `JOBID` sarà `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-136">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="b6b0f-137">Se il processo è stato completato, lo stato è **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-137">If the job has finished, the state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6b0f-138">Questa richiesta Curl restituisce un documento JSON (JavaScript Object Notation) con informazioni sul processo e jq viene usato per recuperare il valore di stato.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job, and jq is used to retrieve only the state value.</span></span>

## <span data-ttu-id="b6b0f-139"><a id="results"></a>Visualizzare risultati</span><span class="sxs-lookup"><span data-stu-id="b6b0f-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="b6b0f-140">Quando lo stato del processo viene modificato in **SUCCEEDED**, è possibile recuperare i risultati del processo.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-140">When the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job.</span></span> <span data-ttu-id="b6b0f-141">Il parametro `statusdir` passato con la query contiene il percorso del file di output; in questo caso `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="b6b0f-142">HDInsight usa l'archiviazione di Azure o Azure Data Lake Store come archivio dati predefinito.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-142">HDInsight can use either Azure Storage or Azure Data Lake Store as the default data store.</span></span> <span data-ttu-id="b6b0f-143">In base all'archivio usato, sono disponibili vari modi per ottenere i dati.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-143">There are various ways to get at the data depending on which one you use.</span></span> <span data-ttu-id="b6b0f-144">Per altre informazioni, vedere la sezione relativa all'archiviazione del documento [Informazioni sull'uso di HDInsight in Linux](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="b6b0f-144">For more information, see the storage section of the [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="b6b0f-145"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b6b0f-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="b6b0f-146">Come illustrato in questo documento, è possibile usare una richiesta HTTP non elaborata per eseguire, monitorare e visualizzare i risultati dei processi Pig nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b6b0f-146">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="b6b0f-147">Per altre informazioni sull'interfaccia REST usata in questo articolo, vedere le [informazioni di riferimento su WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="b6b0f-147">For more information about the REST interface used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="b6b0f-148"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6b0f-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="b6b0f-149">Per informazioni generali su Pig in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b6b0f-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="b6b0f-150">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6b0f-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="b6b0f-151">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b6b0f-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="b6b0f-152">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6b0f-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b6b0f-153">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6b0f-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
