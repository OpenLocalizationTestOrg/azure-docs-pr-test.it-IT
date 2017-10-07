---
title: aaaUse MapReduce e Curl con Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come tooremotely eseguire i processi MapReduce con Hadoop in HDInsight mediante Curl.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="c7d4d-103">Esecuzione di processi MapReduce con Hadoop in HDInsight tramite REST</span><span class="sxs-lookup"><span data-stu-id="c7d4d-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="c7d4d-104">Informazioni su come toouse hello API REST WebHCat toorun MapReduce i processi in un Hadoop nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-104">Learn how toouse hello WebHCat REST API toorun MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="c7d4d-105">CURL è toodemonstrate usato come è possibile interagire con HDInsight con i processi MapReduce toorun le richieste HTTP non elaborati.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="c7d4d-106">Se si ha già familiarità con i server basati su Linux, Hadoop, ma sono tooHDInsight nuovo, vedere hello [è necessario tooknow su basati su Linux, Hadoop in HDInsight](hdinsight-hadoop-linux-information.md) documento.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-106">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see hello [What you need tooknow about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="c7d4d-107"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c7d4d-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="c7d4d-108">Un cluster Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7d4d-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="c7d4d-109">Curl</span><span class="sxs-lookup"><span data-stu-id="c7d4d-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="c7d4d-110">jq</span><span class="sxs-lookup"><span data-stu-id="c7d4d-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="c7d4d-111"><a id="curl"></a>Eseguire processi MapReduce mediante Curl</span><span class="sxs-lookup"><span data-stu-id="c7d4d-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="c7d4d-112">Quando si utilizza Curl o qualsiasi altra comunicazione REST con WebHCat, è necessario autenticare le richieste di hello, fornendo la password e nome utente dell'amministratore del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-112">When you use Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="c7d4d-113">È necessario utilizzare il nome del cluster hello come parte dell'URI utilizzato toosend hello richieste toohello server hello.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-113">You must use hello cluster name as part of hello URI that is used toosend hello requests toohello server.</span></span>
>
> <span data-ttu-id="c7d4d-114">Per i comandi hello in questa sezione, sostituire **USERNAME** cluster toohello tooauthenticate utente hello e **PASSWORD** con password hello per account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-114">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="c7d4d-115">Sostituire **CLUSTERNAME** con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-115">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="c7d4d-116">Hello API REST vengono protetti tramite [l'autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="c7d4d-116">hello REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="c7d4d-117">È consigliabile eseguire sempre le richieste utilizzando HTTPS tooensure che le credenziali vengono inviate in modo sicuro toohello server.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-117">You should always make requests by using HTTPS tooensure that your credentials are securely sent toohello server.</span></span>


1. <span data-ttu-id="c7d4d-118">Dalla riga di comando, utilizzare hello dopo che è possibile connettersi a cluster di HDInsight tooyour tooverify di comando:</span><span class="sxs-lookup"><span data-stu-id="c7d4d-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="c7d4d-119">Si dovrebbe ricevere un toohello simile di risposta JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="c7d4d-119">You should receive a response similar toohello following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="c7d4d-120">i parametri di Hello utilizzati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7d4d-120">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="c7d4d-121">**-u**: indica il nome di utente hello e la password utilizzati richiesta hello tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="c7d4d-121">**-u**: Indicates hello user name and password used tooauthenticate hello request</span></span>
   * <span data-ttu-id="c7d4d-122">**-G**: indica che questa operazione è una richiesta GET</span><span class="sxs-lookup"><span data-stu-id="c7d4d-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="c7d4d-123">Hello inizio hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, hello uguale per tutte le richieste.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-123">hello beginning of hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span>

2. <span data-ttu-id="c7d4d-124">un processo MapReduce, toosubmit utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c7d4d-124">toosubmit a MapReduce job, use hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="c7d4d-125">fine Hello di hello URI (mapreduce/jar) indica WebHCat che questa richiesta viene avviato un processo MapReduce da una classe in un file jar.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-125">hello end of hello URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="c7d4d-126">i parametri di Hello utilizzati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7d4d-126">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="c7d4d-127">**-d**: `-G` non viene utilizzato, in modo richiesta hello predefinite metodo POST toohello.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-127">**-d**: `-G` is not used, so hello request defaults toohello POST method.</span></span> <span data-ttu-id="c7d4d-128">`-d`Specifica i valori dei dati hello vengono inviati con richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-128">`-d` specifies hello data values that are sent with hello request.</span></span>
    * <span data-ttu-id="c7d4d-129">**User.Name**: hello utente che esegue il comando hello</span><span class="sxs-lookup"><span data-stu-id="c7d4d-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="c7d4d-130">**file JAR**: è stato eseguito il percorso di hello del file jar hello contenente toobe di classe</span><span class="sxs-lookup"><span data-stu-id="c7d4d-130">**jar**: hello location of hello jar file that contains class toobe ran</span></span>
    * <span data-ttu-id="c7d4d-131">**classe**: hello classe che contiene la logica MapReduce hello</span><span class="sxs-lookup"><span data-stu-id="c7d4d-131">**class**: hello class that contains hello MapReduce logic</span></span>
    * <span data-ttu-id="c7d4d-132">**arg**: hello argomenti toobe passato toohello il processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-132">**arg**: hello arguments toobe passed toohello MapReduce job.</span></span> <span data-ttu-id="c7d4d-133">In questo caso, hello input directory hello e di file di testo che vengono usate per l'output di hello</span><span class="sxs-lookup"><span data-stu-id="c7d4d-133">In this case, hello input text file and hello directory that are used for hello output</span></span>

     <span data-ttu-id="c7d4d-134">Questo comando deve restituire un ID di processo che può essere utilizzato toocheck hello stato del processo di hello:</span><span class="sxs-lookup"><span data-stu-id="c7d4d-134">This command should return a job ID that can be used toocheck hello status of hello job:</span></span>

       <span data-ttu-id="c7d4d-135">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="c7d4d-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="c7d4d-136">stato di hello toocheck del processo di hello, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c7d4d-136">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="c7d4d-137">Sostituire hello **JOBID** con valore hello restituito nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-137">Replace hello **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="c7d4d-138">Ad esempio, se hello restituirà valore `{"id":"job_1415651640909_0026"}`, quindi hello JOBID sarebbe `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-138">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then hello JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="c7d4d-139">Se il processo di hello è stato completato, lo stato di hello restituito è `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-139">If hello job is complete, hello state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c7d4d-140">Questa richiesta Curl restituisce un documento JSON con informazioni sul processo hello.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-140">This Curl request returns a JSON document with information about hello job.</span></span> <span data-ttu-id="c7d4d-141">Viene utilizzato Jq tooretrieve hello solo valore di stato.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-141">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="c7d4d-142">Quando hello cambiato lo stato del processo di hello troppo`SUCCEEDED`, è possibile recuperare i risultati di hello del processo di hello dall'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-142">When hello state of hello job has changed too`SUCCEEDED`, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="c7d4d-143">Hello `statusdir` parametro che viene passata con query hello contiene il percorso di hello hello del file di output.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-143">hello `statusdir` parameter that is passed with hello query contains hello location of hello output file.</span></span> <span data-ttu-id="c7d4d-144">In questo esempio, è il percorso di hello `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-144">In this example, hello location is `/example/curl`.</span></span> <span data-ttu-id="c7d4d-145">Questo indirizzo archivia l'output di hello del processo di hello in spazio di archiviazione di hello cluster predefinito in `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-145">This address stores hello output of hello job in hello clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="c7d4d-146">È possibile elencare e scaricare questi file tramite hello [CLI di Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c7d4d-146">You can list and download these files by using hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="c7d4d-147">Per ulteriori informazioni sull'uso di BLOB da hello CLI di Azure, vedere hello [Using hello Azure CLI 2.0 con l'archiviazione di Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs) documento.</span><span class="sxs-lookup"><span data-stu-id="c7d4d-147">For more information on working with blobs from hello Azure CLI, see hello [Using hello Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="c7d4d-148"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c7d4d-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="c7d4d-149">Per informazioni generali sui processi MapReduce in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c7d4d-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="c7d4d-150">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7d4d-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="c7d4d-151">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c7d4d-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="c7d4d-152">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7d4d-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c7d4d-153">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7d4d-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="c7d4d-154">Per ulteriori informazioni sull'interfaccia REST hello utilizzato in questo articolo, vedere hello [WebHCat riferimento](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="c7d4d-154">For more information about hello REST interface that is used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>
