---
title: Usare MapReduce e Curl con Hadoop in HDInsight - Azure | Microsoft Docs
description: "Informazioni su come eseguire in modalità remota processi MapReduce con Hadoop in HDInsight mediante Curl."
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
ms.openlocfilehash: 8238bb829df95dcb8c99c0b7fff53c627a56f47c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="3169c-103">Esecuzione di processi MapReduce con Hadoop in HDInsight tramite REST</span><span class="sxs-lookup"><span data-stu-id="3169c-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="3169c-104">Informazioni su come usare l'API REST WebHCat per l'esecuzione di processi MapReduce in un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3169c-104">Learn how to use the WebHCat REST API to run MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="3169c-105">Curl viene usato per illustrare come sia possibile interagire con HDInsight usando richieste HTTP non elaborate per eseguire processi MapReduce.</span><span class="sxs-lookup"><span data-stu-id="3169c-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="3169c-106">Se si ha già familiarità con l'uso di server Hadoop basati su Linux, ma non si ha esperienza con HDInsight, vedere il documento [Informazioni utili su Hadoop basato su Linux in HDInsight](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="3169c-106">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see the [What you need to know about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="3169c-107"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3169c-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="3169c-108">Un cluster Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3169c-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="3169c-109">Curl</span><span class="sxs-lookup"><span data-stu-id="3169c-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="3169c-110">jq</span><span class="sxs-lookup"><span data-stu-id="3169c-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="3169c-111"><a id="curl"></a>Eseguire processi MapReduce mediante Curl</span><span class="sxs-lookup"><span data-stu-id="3169c-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="3169c-112">Quando si usa Curl o qualsiasi altra forma di comunicazione REST con WebHCat, è necessario autenticare le richieste fornendo il nome utente e la password da amministratore del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3169c-112">When you use Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="3169c-113">È necessario specificare il nome del cluster come parte dell'URI usato per inviare le richieste al server.</span><span class="sxs-lookup"><span data-stu-id="3169c-113">You must use the cluster name as part of the URI that is used to send the requests to the server.</span></span>
>
> <span data-ttu-id="3169c-114">Per i comandi riportati in questa sezione, sostituire **USERNAME** con l'utente da autenticare nel cluster e **PASSWORD** con la password dell'account utente.</span><span class="sxs-lookup"><span data-stu-id="3169c-114">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="3169c-115">Sostituire **CLUSTERNAME** con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="3169c-115">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="3169c-116">L'API REST viene protetta tramite l' [autenticazione dell'accesso di base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="3169c-116">The REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="3169c-117">È necessario effettuare sempre le richieste usando il protocollo HTTPS per essere certi che le credenziali vengano inviate in modo sicuro al server.</span><span class="sxs-lookup"><span data-stu-id="3169c-117">You should always make requests by using HTTPS to ensure that your credentials are securely sent to the server.</span></span>


1. <span data-ttu-id="3169c-118">Da una riga di comando usare il comando seguente per verificare che sia possibile connettersi al cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3169c-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="3169c-119">Dovrebbe essere visualizzato un messaggio simile al JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="3169c-119">You should receive a response similar to the following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="3169c-120">I parametri usati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="3169c-120">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="3169c-121">**-u**: il nome utente e la password usati per autenticare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="3169c-121">**-u**: Indicates the user name and password used to authenticate the request</span></span>
   * <span data-ttu-id="3169c-122">**-G**: indica che questa operazione è una richiesta GET</span><span class="sxs-lookup"><span data-stu-id="3169c-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="3169c-123">L'inizio dell'URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, sarà uguale per tutte le richieste.</span><span class="sxs-lookup"><span data-stu-id="3169c-123">The beginning of the URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span>

2. <span data-ttu-id="3169c-124">Per inviare un processo MapReduce, usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="3169c-124">To submit a MapReduce job, use the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="3169c-125">La fine dell'URI (/mapreduce/jar) indica a WebHCat che la richiesta avvia un processo MapReduce da una classe in un file con estensione jar.</span><span class="sxs-lookup"><span data-stu-id="3169c-125">The end of the URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="3169c-126">I parametri usati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="3169c-126">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="3169c-127">**-d**: `-G` non viene usato, quindi la richiesta userà il metodo POST per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="3169c-127">**-d**: `-G` is not used, so the request defaults to the POST method.</span></span> <span data-ttu-id="3169c-128">`-d` specifica i valori di dati che vengono inviati con la richiesta.</span><span class="sxs-lookup"><span data-stu-id="3169c-128">`-d` specifies the data values that are sent with the request.</span></span>
    * <span data-ttu-id="3169c-129">**user.name**: l'utente che esegue il comando.</span><span class="sxs-lookup"><span data-stu-id="3169c-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="3169c-130">**jar**: il percorso del file con estensione jar che contiene la classe da eseguire.</span><span class="sxs-lookup"><span data-stu-id="3169c-130">**jar**: The location of the jar file that contains class to be ran</span></span>
    * <span data-ttu-id="3169c-131">**class**: la classe che contiene la logica MapReduce.</span><span class="sxs-lookup"><span data-stu-id="3169c-131">**class**: The class that contains the MapReduce logic</span></span>
    * <span data-ttu-id="3169c-132">**arg**: gli argomenti da passare al processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="3169c-132">**arg**: The arguments to be passed to the MapReduce job.</span></span> <span data-ttu-id="3169c-133">In questo caso, il file di testo di input e la directory usata per l'output</span><span class="sxs-lookup"><span data-stu-id="3169c-133">In this case, the input text file and the directory that are used for the output</span></span>

     <span data-ttu-id="3169c-134">Questo comando dovrebbe restituire un ID processo utilizzabile per verificare lo stato del processo:</span><span class="sxs-lookup"><span data-stu-id="3169c-134">This command should return a job ID that can be used to check the status of the job:</span></span>

       <span data-ttu-id="3169c-135">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="3169c-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="3169c-136">Per verificare lo stato del processo, usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="3169c-136">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="3169c-137">Sostituire **JOBID** con il valore restituito nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="3169c-137">Replace the **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="3169c-138">Ad esempio, se il valore restituito è `{"id":"job_1415651640909_0026"}`, JOBID sarà `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="3169c-138">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then the JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="3169c-139">Se il processo è stato completato, lo stato restituito è `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="3169c-139">If the job is complete, the state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3169c-140">Questa richiesta curl restituisce un documento JSON con informazioni sul processo.</span><span class="sxs-lookup"><span data-stu-id="3169c-140">This Curl request returns a JSON document with information about the job.</span></span> <span data-ttu-id="3169c-141">Jq viene usato per recuperare solo il valore di stato.</span><span class="sxs-lookup"><span data-stu-id="3169c-141">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="3169c-142">Dopo che lo stato del processo risulta essere `SUCCEEDED`, è possibile recuperare i risultati del processo dall'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="3169c-142">When the state of the job has changed to `SUCCEEDED`, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="3169c-143">Il parametro `statusdir` passato con la query contiene il percorso del file di output.</span><span class="sxs-lookup"><span data-stu-id="3169c-143">The `statusdir` parameter that is passed with the query contains the location of the output file.</span></span> <span data-ttu-id="3169c-144">In questo esempio la località è `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="3169c-144">In this example, the location is `/example/curl`.</span></span> <span data-ttu-id="3169c-145">Questo indirizzo archivia l'output del processo nella risorsa di archiviazione predefinita dei cluster in `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="3169c-145">This address stores the output of the job in the clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="3169c-146">È possibile elencare e scaricare questi file usando l' [Interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3169c-146">You can list and download these files by using the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="3169c-147">Per altre informazioni sull'uso dei BLOB dalla riga di comando di Azure, vedere il documento [Uso dell'Interfaccia della riga di comando di Azure 2.0 con Archiviazione di Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs).</span><span class="sxs-lookup"><span data-stu-id="3169c-147">For more information on working with blobs from the Azure CLI, see the [Using the Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="3169c-148"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3169c-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="3169c-149">Per informazioni generali sui processi MapReduce in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3169c-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="3169c-150">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3169c-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="3169c-151">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3169c-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="3169c-152">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3169c-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="3169c-153">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3169c-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="3169c-154">Per altre informazioni sull'interfaccia REST usata in questo articolo, vedere le [informazioni di riferimento su WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="3169c-154">For more information about the REST interface that is used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>