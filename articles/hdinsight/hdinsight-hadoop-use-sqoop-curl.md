---
title: Usare Sqoop di Hadoop con Curl in HDInsight - Azure | Microsoft Docs
description: "Informazioni su come inviare in modalità remota processi Sqoop a HDInsight mediante Curl."
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
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="b1812-103">Esecuzione di processi Sqoop con Hadoop in HDInsight mediante Curl</span><span class="sxs-lookup"><span data-stu-id="b1812-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="b1812-104">Informazioni su come usare Curl per l'esecuzione di processi Sqoop in un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1812-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="b1812-105">Curl viene usato per illustrare come è possibile interagire con HDInsight tramite richieste HTTP non elaborate per eseguire, monitorare e recuperare i risultati di processi Sqoop.</span><span class="sxs-lookup"><span data-stu-id="b1812-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span></span> <span data-ttu-id="b1812-106">Ciò avviene mediante l'API REST WebHCat, nota in precedenza come Templeton, fornita dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1812-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b1812-107">Se si ha già familiarità con l'uso di server Hadoop basati su Linux ma non si è esperti di HDInsight, vedere [Informazioni sull'uso di HDInsight in Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="b1812-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b1812-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b1812-108">Prerequisites</span></span>
<span data-ttu-id="b1812-109">Per seguire la procedura descritta in questo articolo, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b1812-109">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="b1812-110">Un cluster Hadoop in HDInsight (basato su Linux o su Windows)</span><span class="sxs-lookup"><span data-stu-id="b1812-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="b1812-111">Curl</span><span class="sxs-lookup"><span data-stu-id="b1812-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="b1812-112">jq</span><span class="sxs-lookup"><span data-stu-id="b1812-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="b1812-113">Inviare processi Sqoop mediante Azure Curl</span><span class="sxs-lookup"><span data-stu-id="b1812-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="b1812-114">Quando si usa Curl o qualsiasi altra forma di comunicazione REST con WebHCat, è necessario autenticare le richieste fornendo il nome utente e la password dell'amministratore cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1812-114">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="b1812-115">È inoltre necessario specificare il nome del cluster come parte dell'URI (Uniform Resource Identifier) usato per inviare le richieste al server.</span><span class="sxs-lookup"><span data-stu-id="b1812-115">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="b1812-116">Per i comandi riportati in questa sezione, sostituire **USERNAME** con l'utente da autenticare nel cluster e **PASSWORD** con la password dell'account utente.</span><span class="sxs-lookup"><span data-stu-id="b1812-116">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="b1812-117">Sostituire **CLUSTERNAME** con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="b1812-117">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="b1812-118">L'API REST viene protetta tramite l' [autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="b1812-118">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="b1812-119">È necessario effettuare sempre le richieste usando il protocollo HTTPS (Secure HTTP) per essere certi che le credenziali vengano inviate in modo sicuro al server.</span><span class="sxs-lookup"><span data-stu-id="b1812-119">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="b1812-120">Da una riga di comando usare il comando seguente per verificare che sia possibile connettersi al cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b1812-120">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="b1812-121">Dovrebbe essere visualizzato un messaggio simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b1812-121">You should receive a response similar to the following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="b1812-122">I parametri usati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1812-122">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="b1812-123">**-u** : il nome utente e la password usati per autenticare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="b1812-123">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="b1812-124">**-G** : indica che si tratta di una richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="b1812-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="b1812-125">L'inizio dell'URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, sarà uguale per tutte le richieste.</span><span class="sxs-lookup"><span data-stu-id="b1812-125">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span></span> <span data-ttu-id="b1812-126">Il percorso, **/status**, indica che la richiesta deve restituire uno stato di WebHCat (noto anche come Templeton) per il server.</span><span class="sxs-lookup"><span data-stu-id="b1812-126">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> 
2. <span data-ttu-id="b1812-127">Usare quanto segue per inviare un processo sqoop:</span><span class="sxs-lookup"><span data-stu-id="b1812-127">Use the following to submit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="b1812-128">I parametri usati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1812-128">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="b1812-129">**-d**: poiché `-G` non viene usato, la richiesta userà il metodo POST per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b1812-129">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="b1812-130">`-d` specifica i valori di dati che vengono inviati con la richiesta.</span><span class="sxs-lookup"><span data-stu-id="b1812-130">`-d` specifies the data values that are sent with the request.</span></span>

        * <span data-ttu-id="b1812-131">**user.name** : l'utente che esegue il comando.</span><span class="sxs-lookup"><span data-stu-id="b1812-131">**user.name** - The user that is running the command.</span></span>

        * <span data-ttu-id="b1812-132">**command** : il comando Sqoop da eseguire.</span><span class="sxs-lookup"><span data-stu-id="b1812-132">**command** - The Sqoop command to execute.</span></span>

        * <span data-ttu-id="b1812-133">**statusdir** : la directory in cui verrà scritto lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="b1812-133">**statusdir** - The directory that the status for this job will be written to.</span></span>

    <span data-ttu-id="b1812-134">Questo comando dovrebbe restituire un ID processo utilizzabile per verificare lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="b1812-134">This command should return a job ID that can be used to check the status of the job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="b1812-135">Per verificare lo stato del processo, usare il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="b1812-135">To check the status of the job, use the following command.</span></span> <span data-ttu-id="b1812-136">Sostituire **JOBID** con il valore restituito nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="b1812-136">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="b1812-137">Se ad esempio il valore restituito è `{"id":"job_1415651640909_0026"}`, **JOBID** sarà `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="b1812-137">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="b1812-138">Se il processo è stato completato, lo stato sarà **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="b1812-138">If the job has finished, the state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b1812-139">Questa richiesta curl restituisce un documento JSON (JavaScript Object Notation) con informazioni sul processo. jq viene usato per recuperare il valore di stato.</span><span class="sxs-lookup"><span data-stu-id="b1812-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span></span>
   > 
   > 
2. <span data-ttu-id="b1812-140">Dopo che lo stato del processo risulta essere **SUCCEEDED**, è possibile recuperare i risultati del processo dall'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1812-140">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="b1812-141">Il parametro `statusdir` passato con la query contiene il percorso del file di output, in questo caso **wasb:///example/curl**.</span><span class="sxs-lookup"><span data-stu-id="b1812-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="b1812-142">Questo indirizzo consente di archiviare l'output del processo nella directory **example/curl** del contenitore di archiviazione predefinito usato dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1812-142">This address stores the output of the job in the **example/curl** directory on the default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="b1812-143">È possibile elencare e scaricare questi file usando l' [Interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b1812-143">You can list and download these files by using the [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="b1812-144">Ad esempio, per elencare i file contenuti in **example/curl**, usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="b1812-144">For example, to list files in **example/curl**, use the following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="b1812-145">Per scaricare un file, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b1812-145">To download a file, use the following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="b1812-146">È necessario specificare il nome dell'account di archiviazione contenente il BLOB usando i parametri `-a` e `-k` oppure impostare le variabili di ambiente **AZURE\_STORAGE\_ACCOUNT** e **AZURE\_STORAGE\_ACCESS\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="b1812-146">You must either specify the storage account name that contains the blob by using the `-a` and `-k` parameters, or set the **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="b1812-147">Vedere <a href="hdinsight-upload-data.md" target="_blank" per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="b1812-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="b1812-148">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="b1812-148">Limitations</span></span>
* <span data-ttu-id="b1812-149">Esportazione di massa: con HDInsight basato su Linux, attualmente il connettore Sqoop, usato per esportare dati in Microsoft SQL Server o nel database SQL di Azure, non supporta inserimenti di massa.</span><span class="sxs-lookup"><span data-stu-id="b1812-149">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="b1812-150">Invio in batch: con HDInsight basato su Linux, quando si usa il comando `-batch` durante gli inserimenti, Sqoop esegue più inserimenti invece di suddividere in batch le operazioni di inserimento.</span><span class="sxs-lookup"><span data-stu-id="b1812-150">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="b1812-151">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b1812-151">Summary</span></span>
<span data-ttu-id="b1812-152">Come illustrato in questo documento, è possibile usare una richiesta HTTP non elaborata per eseguire, monitorare e visualizzare i risultati dei processi Sqoop nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1812-152">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="b1812-153">Per altre informazioni sull'interfaccia REST usata in questo articolo, vedere la <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">guida relativa all'API REST Sqoop</a>.</span><span class="sxs-lookup"><span data-stu-id="b1812-153">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1812-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b1812-154">Next steps</span></span>
<span data-ttu-id="b1812-155">Per informazioni generali su Hive con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b1812-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="b1812-156">Usare Sqoop con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1812-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="b1812-157">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b1812-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="b1812-158">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1812-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b1812-159">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1812-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="b1812-160">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1812-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


