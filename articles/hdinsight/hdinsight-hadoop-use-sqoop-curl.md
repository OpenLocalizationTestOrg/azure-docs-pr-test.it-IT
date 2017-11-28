---
title: aaaUse Hadoop Sqoop in HDInsight - Azure latino | Documenti Microsoft
description: Informazioni su come tooremotely inviare Sqoop processi tooHDInsight utilizzando Curl.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="5de3f-103">Esecuzione di processi Sqoop con Hadoop in HDInsight mediante Curl</span><span class="sxs-lookup"><span data-stu-id="5de3f-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="5de3f-104">Informazioni su come cluster di toouse Curl toorun Sqoop processi in un Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5de3f-104">Learn how toouse Curl toorun Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="5de3f-105">CURL è toodemonstrate usato come è possibile interagire con HDInsight con toorun di richieste HTTP non elaborato, monitoraggio e recuperare risultati di hello dei processi Sqoop.</span><span class="sxs-lookup"><span data-stu-id="5de3f-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun, monitor, and retrieve hello results of Sqoop jobs.</span></span> <span data-ttu-id="5de3f-106">Questo procedimento funziona tramite hello API REST WebHCat (precedentemente noto come Templeton) fornita da cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5de3f-106">This works by using hello WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5de3f-107">Se si ha già familiarità con i server basati su Linux, Hadoop, ma sono tooHDInsight nuovo, vedere [informazioni sull'uso di HDInsight su Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="5de3f-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5de3f-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5de3f-108">Prerequisites</span></span>
<span data-ttu-id="5de3f-109">passaggi di hello toocomplete in questo articolo, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="5de3f-109">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="5de3f-110">Un cluster Hadoop in HDInsight (basato su Linux o su Windows)</span><span class="sxs-lookup"><span data-stu-id="5de3f-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="5de3f-111">Curl</span><span class="sxs-lookup"><span data-stu-id="5de3f-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="5de3f-112">jq</span><span class="sxs-lookup"><span data-stu-id="5de3f-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="5de3f-113">Inviare processi Sqoop mediante Azure Curl</span><span class="sxs-lookup"><span data-stu-id="5de3f-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="5de3f-114">Quando si utilizza Curl o qualsiasi altra comunicazione REST con WebHCat, è necessario autenticare le richieste di hello specificando nome utente hello e la password per l'amministratore del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5de3f-114">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="5de3f-115">È inoltre necessario utilizzare il nome del cluster hello come parte di hello Uniform Resource Identifier (URI) utilizzato toosend hello richieste toohello server.</span><span class="sxs-lookup"><span data-stu-id="5de3f-115">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server.</span></span>
> 
> <span data-ttu-id="5de3f-116">Per i comandi hello in questa sezione, sostituire **USERNAME** con hello utente tooauthenticate toohello cluster e sostituire **PASSWORD** con password hello per account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="5de3f-116">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="5de3f-117">Sostituire **CLUSTERNAME** con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="5de3f-117">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
> 
> <span data-ttu-id="5de3f-118">Hello API REST è protetto tramite [l'autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="5de3f-118">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="5de3f-119">È consigliabile eseguire sempre le richieste tramite HTTPS (Secure HTTP) toohelp assicurarsi che le credenziali vengono inviate in modo sicuro toohello server.</span><span class="sxs-lookup"><span data-stu-id="5de3f-119">You should always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>
> 
> 

1. <span data-ttu-id="5de3f-120">Dalla riga di comando, utilizzare hello dopo che è possibile connettersi a cluster di HDInsight tooyour tooverify di comando:</span><span class="sxs-lookup"><span data-stu-id="5de3f-120">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="5de3f-121">Verrà visualizzato di seguito toohello simile risposta:</span><span class="sxs-lookup"><span data-stu-id="5de3f-121">You should receive a response similar toohello following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="5de3f-122">i parametri di Hello utilizzati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="5de3f-122">hello parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="5de3f-123">**-u** -nome utente hello e la password utilizzati richiesta hello tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="5de3f-123">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="5de3f-124">**-G** : indica che si tratta di una richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="5de3f-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="5de3f-125">Hello inizio hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, sarà hello uguale per tutte le richieste.</span><span class="sxs-lookup"><span data-stu-id="5de3f-125">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be hello same for all requests.</span></span> <span data-ttu-id="5de3f-126">percorso di Hello, **/status**, indica che la richiesta hello è tooreturn stato WebHCat (noto anche come Templeton) per il server di hello.</span><span class="sxs-lookup"><span data-stu-id="5de3f-126">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> 
2. <span data-ttu-id="5de3f-127">Utilizzare hello toosubmit un processo sqoop seguenti:</span><span class="sxs-lookup"><span data-stu-id="5de3f-127">Use hello following toosubmit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="5de3f-128">i parametri di Hello utilizzati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="5de3f-128">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="5de3f-129">**-d** - dal `-G` non viene utilizzato, richiesta hello predefinite metodo POST toohello.</span><span class="sxs-lookup"><span data-stu-id="5de3f-129">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="5de3f-130">`-d`Specifica i valori dei dati hello vengono inviati con richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="5de3f-130">`-d` specifies hello data values that are sent with hello request.</span></span>

        * <span data-ttu-id="5de3f-131">**User.Name** -utente hello che esegue il comando hello.</span><span class="sxs-lookup"><span data-stu-id="5de3f-131">**user.name** - hello user that is running hello command.</span></span>

        * <span data-ttu-id="5de3f-132">**comando** -hello tooexecute comando Sqoop.</span><span class="sxs-lookup"><span data-stu-id="5de3f-132">**command** - hello Sqoop command tooexecute.</span></span>

        * <span data-ttu-id="5de3f-133">**statusdir** -directory hello hello stato per il processo verrà scritto.</span><span class="sxs-lookup"><span data-stu-id="5de3f-133">**statusdir** - hello directory that hello status for this job will be written to.</span></span>

    <span data-ttu-id="5de3f-134">Questo comando deve restituire un ID di processo che può essere utilizzato toocheck hello stato del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="5de3f-134">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="5de3f-135">stato di hello toocheck del processo di hello, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5de3f-135">toocheck hello status of hello job, use hello following command.</span></span> <span data-ttu-id="5de3f-136">Sostituire **JOBID** con valore hello restituito nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="5de3f-136">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="5de3f-137">Ad esempio, se hello restituirà valore `{"id":"job_1415651640909_0026"}`, quindi **JOBID** sarebbe `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="5de3f-137">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="5de3f-138">Se il completamento del processo di hello, sarà stato hello **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="5de3f-138">If hello job has finished, hello state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5de3f-139">Questa richiesta Curl restituisce un documento di JavaScript Object Notation (JSON) con informazioni sul processo hello; viene utilizzato jq tooretrieve hello solo valore di stato.</span><span class="sxs-lookup"><span data-stu-id="5de3f-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job; jq is used tooretrieve only hello state value.</span></span>
   > 
   > 
2. <span data-ttu-id="5de3f-140">Dopo aver cambiato troppo hello lo stato del processo di hello**SUCCEEDED**, è possibile recuperare i risultati di hello del processo di hello dall'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="5de3f-140">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="5de3f-141">Hello `statusdir` parametro passato con query hello contiene percorso hello hello del file di output; in questo caso, **wasb: / / / esempio/curl**.</span><span class="sxs-lookup"><span data-stu-id="5de3f-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="5de3f-142">Questo indirizzo archivia l'output di hello del processo di hello in hello **esempio/curl** directory nel contenitore di archiviazione predefinito hello utilizzato dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5de3f-142">This address stores hello output of hello job in hello **example/curl** directory on hello default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="5de3f-143">È possibile elencare e scaricare questi file tramite hello [CLI di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5de3f-143">You can list and download these files by using hello [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="5de3f-144">Ad esempio, file toolist **esempio/curl**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5de3f-144">For example, toolist files in **example/curl**, use hello following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="5de3f-145">toodownload un file, usare nomi hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="5de3f-145">toodownload a file, use hello following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="5de3f-146">È necessario specificare nome account di archiviazione hello che contiene il blob di hello utilizzando hello `-a` e `-k` parametri o set hello **AZURE\_archiviazione\_ACCOUNT** e **AZURE\_archiviazione\_accesso\_chiave** le variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="5de3f-146">You must either specify hello storage account name that contains hello blob by using hello `-a` and `-k` parameters, or set hello **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="5de3f-147">Vedere <a href="hdinsight-upload-data.md" target="_blank" per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="5de3f-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="5de3f-148">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="5de3f-148">Limitations</span></span>
* <span data-ttu-id="5de3f-149">Eseguire l'esportazione bulk - HDInsight basati su Linux con, hello Sqoop connettore utilizzato tooexport dati tooMicrosoft SQL Server o Database SQL di Azure attualmente non supporta inserimenti bulk.</span><span class="sxs-lookup"><span data-stu-id="5de3f-149">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="5de3f-150">Divisione in batch - con HDInsight basati su Linux, quando si utilizza hello `-batch` passare quando l'esecuzione di inserimenti, Sqoop eseguirà più inserimenti anziché l'invio in batch le operazioni di inserimento hello.</span><span class="sxs-lookup"><span data-stu-id="5de3f-150">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="5de3f-151">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5de3f-151">Summary</span></span>
<span data-ttu-id="5de3f-152">Come illustrato in questo documento, è possibile utilizzare un toorun di richiesta HTTP non elaborato, monitoraggio e visualizzare i risultati dei processi Sqoop hello il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5de3f-152">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="5de3f-153">Per ulteriori informazioni sull'interfaccia REST hello usata in questo articolo, vedere hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Guida API REST Sqoop</a>.</span><span class="sxs-lookup"><span data-stu-id="5de3f-153">For more information on hello REST interface used in this article, see hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5de3f-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5de3f-154">Next steps</span></span>
<span data-ttu-id="5de3f-155">Per informazioni generali su Hive con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5de3f-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="5de3f-156">Usare Sqoop con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5de3f-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="5de3f-157">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5de3f-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="5de3f-158">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5de3f-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5de3f-159">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5de3f-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5de3f-160">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5de3f-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


