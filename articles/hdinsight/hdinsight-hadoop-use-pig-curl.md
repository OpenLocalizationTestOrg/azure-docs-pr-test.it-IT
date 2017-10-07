---
title: aaaUse Hadoop Pig in HDInsight - Azure con | Documenti Microsoft
description: Informazioni su come cluster di toouse REST toorun Pig Latin i processi in un Hadoop in HDInsight di Azure.
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
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="63088-103">Eseguire processi Pig con Hadoop in HDInsight tramite REST</span><span class="sxs-lookup"><span data-stu-id="63088-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="63088-104">Informazioni su come toorun latino Pig processi rendendo cluster Azure HDInsight tooan di richieste REST.</span><span class="sxs-lookup"><span data-stu-id="63088-104">Learn how toorun Pig Latin jobs by making REST requests tooan Azure HDInsight cluster.</span></span> <span data-ttu-id="63088-105">CURL è toodemonstrate usato come è possibile interagire con HDInsight mediante l'API REST WebHCat hello.</span><span class="sxs-lookup"><span data-stu-id="63088-105">Curl is used toodemonstrate how you can interact with HDInsight using hello WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="63088-106">Se si ha già familiarità con i server basati su Linux, Hadoop, ma sono tooHDInsight nuovo, vedere [suggerimenti basati su Linux di HDInsight](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="63088-106">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="63088-107"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="63088-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="63088-108">Un cluster Azure HDInsight (Hadoop in HDInsight) (basato su Linux o basato su Windows)</span><span class="sxs-lookup"><span data-stu-id="63088-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="63088-109">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="63088-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="63088-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="63088-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="63088-111">Curl</span><span class="sxs-lookup"><span data-stu-id="63088-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="63088-112">jq</span><span class="sxs-lookup"><span data-stu-id="63088-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="63088-113"><a id="curl"></a>Eseguire processi Pig mediante Curl</span><span class="sxs-lookup"><span data-stu-id="63088-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="63088-114">Hello API REST è protetto tramite [l'autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="63088-114">hello REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="63088-115">Verificare sempre le richieste utilizzando tooensure HTTPS (Secure HTTP) che le credenziali vengono inviate in modo sicuro toohello server.</span><span class="sxs-lookup"><span data-stu-id="63088-115">Always make requests by using Secure HTTP (HTTPS) tooensure that your credentials are securely sent toohello server.</span></span>
>
> <span data-ttu-id="63088-116">Quando si utilizzano i comandi di hello in questa sezione, sostituire `USERNAME` con hello utente tooauthenticate toohello cluster e sostituire `PASSWORD` con password hello per account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="63088-116">When using hello commands in this section, replace `USERNAME` with hello user tooauthenticate toohello cluster, and replace `PASSWORD` with hello password for hello user account.</span></span> <span data-ttu-id="63088-117">Sostituire `CLUSTERNAME` con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="63088-117">Replace `CLUSTERNAME` with hello name of your cluster.</span></span>
>


1. <span data-ttu-id="63088-118">Dalla riga di comando, utilizzare hello dopo che è possibile connettersi a cluster di HDInsight tooyour tooverify di comando:</span><span class="sxs-lookup"><span data-stu-id="63088-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="63088-119">Si dovrebbe ricevere hello risposta JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="63088-119">You should receive hello following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="63088-120">i parametri di Hello utilizzati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="63088-120">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="63088-121">**-u**: nome utente hello e la password utilizzati richiesta hello tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="63088-121">**-u**: hello user name and password used tooauthenticate hello request</span></span>
    * <span data-ttu-id="63088-122">**-G**: indica che è una richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="63088-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="63088-123">Hello inizio hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, hello uguale per tutte le richieste.</span><span class="sxs-lookup"><span data-stu-id="63088-123">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="63088-124">percorso di Hello, **/status**, indica che la richiesta hello stato tooreturn hello di WebHCat (noto anche come Templeton) per il server di hello.</span><span class="sxs-lookup"><span data-stu-id="63088-124">hello path, **/status**, indicates that hello request is tooreturn hello status of WebHCat (also known as Templeton) for hello server.</span></span>

2. <span data-ttu-id="63088-125">Utilizzare hello seguente codice toosubmit un cluster di toohello processo Pig latino:</span><span class="sxs-lookup"><span data-stu-id="63088-125">Use hello following code toosubmit a Pig Latin job toohello cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="63088-126">i parametri di Hello utilizzati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="63088-126">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="63088-127">**-d**: perché `-G` non viene utilizzato, richiesta hello predefinite metodo POST toohello.</span><span class="sxs-lookup"><span data-stu-id="63088-127">**-d**: Because `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="63088-128">`-d`Specifica i valori dei dati hello vengono inviati con richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="63088-128">`-d` specifies hello data values that are sent with hello request.</span></span>

    * <span data-ttu-id="63088-129">**User.Name**: hello utente che esegue il comando hello</span><span class="sxs-lookup"><span data-stu-id="63088-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="63088-130">**eseguire**: hello Pig latino istruzioni tooexecute</span><span class="sxs-lookup"><span data-stu-id="63088-130">**execute**: hello Pig Latin statements tooexecute</span></span>
    * <span data-ttu-id="63088-131">**statusdir**: directory hello hello stato per questo processo viene scritto</span><span class="sxs-lookup"><span data-stu-id="63088-131">**statusdir**: hello directory that hello status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="63088-132">Si noti che gli spazi di hello in latino Pig istruzioni vengono sostituiti da hello `+` carattere se usato con Curl.</span><span class="sxs-lookup"><span data-stu-id="63088-132">Notice that hello spaces in Pig Latin statements are replaced by hello `+` character when used with Curl.</span></span>

    <span data-ttu-id="63088-133">Questo comando deve restituire un ID di processo che può essere utilizzato toocheck hello stato del processo di hello, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="63088-133">This command should return a job ID that can be used toocheck hello status of hello job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="63088-134">stato hello toocheck del processo di hello, utilizzare hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="63088-134">toocheck hello status of hello job, use hello following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="63088-135">Sostituire `JOBID` con valore hello restituito nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="63088-135">Replace `JOBID` with hello value returned in hello previous step.</span></span> <span data-ttu-id="63088-136">Ad esempio, se hello restituirà valore `{"id":"job_1415651640909_0026"}`, quindi `JOBID` è `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="63088-136">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="63088-137">Se ha completato il processo di hello, non è stato hello **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="63088-137">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="63088-138">Questa richiesta Curl restituisce documenti JavaScript Object Notation (JSON) con informazioni sul processo hello e jq è usato tooretrieve hello solo valore di stato.</span><span class="sxs-lookup"><span data-stu-id="63088-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job, and jq is used tooretrieve only hello state value.</span></span>

## <span data-ttu-id="63088-139"><a id="results"></a>Visualizzare risultati</span><span class="sxs-lookup"><span data-stu-id="63088-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="63088-140">Quando hello cambiato lo stato del processo di hello troppo**SUCCEEDED**, è possibile recuperare i risultati di hello di hello processo.</span><span class="sxs-lookup"><span data-stu-id="63088-140">When hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job.</span></span> <span data-ttu-id="63088-141">Hello `statusdir` parametro passato con query hello contiene percorso hello hello del file di output; in questo caso, `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="63088-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="63088-142">HDInsight è possibile utilizzare l'archiviazione di Azure o archivio Azure Data Lake come archivio dati predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="63088-142">HDInsight can use either Azure Storage or Azure Data Lake Store as hello default data store.</span></span> <span data-ttu-id="63088-143">Esistono vari modi tooget dati hello a seconda di quale utilizzare.</span><span class="sxs-lookup"><span data-stu-id="63088-143">There are various ways tooget at hello data depending on which one you use.</span></span> <span data-ttu-id="63088-144">Per ulteriori informazioni, vedere hello archiviazione sezione hello [HDInsight basati su Linux informazioni](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) documento.</span><span class="sxs-lookup"><span data-stu-id="63088-144">For more information, see hello storage section of hello [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="63088-145"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="63088-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="63088-146">Come illustrato in questo documento, è possibile utilizzare un toorun di richiesta HTTP non elaborato, monitoraggio e visualizzare i risultati dei processi Pig hello il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="63088-146">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="63088-147">Per ulteriori informazioni sull'interfaccia REST hello usata in questo articolo, vedere hello [WebHCat riferimento](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="63088-147">For more information about hello REST interface used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="63088-148"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="63088-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="63088-149">Per informazioni generali su Pig in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="63088-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="63088-150">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="63088-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="63088-151">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="63088-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="63088-152">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="63088-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="63088-153">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="63088-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
