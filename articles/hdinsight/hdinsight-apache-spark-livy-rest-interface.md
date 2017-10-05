---
title: Usare Livy Spark per inviare processi al cluster Spark in Azure HDInsight | Microsoft Docs
description: "Informazioni su come usare l'API REST di Apache Spark per inviare i processi in modalità remota a un cluster Azure HDInsight."
keywords: apache spark rest api,livy spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: e1a28d69bbf40ea3134a7899a0d2fe70e5fc9e71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-apache-spark-rest-api-to-submit-remote-jobs-to-an-hdinsight-spark-cluster"></a><span data-ttu-id="18df8-104">Usare l'API REST di Apache Spark per inviare i processi remoti a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="18df8-104">Use Apache Spark REST API to submit remote jobs to an HDInsight Spark cluster</span></span>

<span data-ttu-id="18df8-105">Informazioni su come usare Livy, l'API REST di Apache Spark per inviare processi remoti a un cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="18df8-105">Learn how to use Livy, the Apache Spark REST API, which is used to submit remote jobs to an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="18df8-106">Per informazioni dettagliate, vedere [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="18df8-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="18df8-107">È possibile usare Livy per l'esecuzione interattiva di shell Spark o per inviare processi batch da eseguire su Spark.</span><span class="sxs-lookup"><span data-stu-id="18df8-107">You can use Livy to run interactive Spark shells or submit batch jobs to be run on Spark.</span></span> <span data-ttu-id="18df8-108">Questo articolo parla dell'uso di Livy per inviare processi batch.</span><span class="sxs-lookup"><span data-stu-id="18df8-108">This article talks about using Livy to submit batch jobs.</span></span> <span data-ttu-id="18df8-109">I frammenti di codice in questo articolo usano cURL per eseguire chiamate API REST all'endpoint Livy Spark.</span><span class="sxs-lookup"><span data-stu-id="18df8-109">The snippets in this article use cURL to make REST API calls to the Livy Spark endpoint.</span></span>

<span data-ttu-id="18df8-110">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="18df8-110">**Prerequisites:**</span></span>

* <span data-ttu-id="18df8-111">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18df8-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="18df8-112">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="18df8-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="18df8-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="18df8-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="18df8-114">Questo articolo usa cURL per illustrare come effettuare chiamate API REST con un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="18df8-114">This article uses cURL to demonstrate how to make REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="18df8-115">Inviare un processo batch Livy Spark</span><span class="sxs-lookup"><span data-stu-id="18df8-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="18df8-116">Prima di inviare un processo batch, è necessario caricare il file con estensione jar dell'applicazione nell'archivio del cluster associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="18df8-116">Before you submit a batch job, you must upload the application jar on the cluster storage associated with the cluster.</span></span> <span data-ttu-id="18df8-117">A tale scopo è possibile usare [**AzCopy**](../storage/common/storage-use-azcopy.md), un'utilità della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="18df8-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, to do so.</span></span> <span data-ttu-id="18df8-118">Sono disponibili molti altri client da usare per caricare i dati.</span><span class="sxs-lookup"><span data-stu-id="18df8-118">There are various other clients you can use to upload data.</span></span> <span data-ttu-id="18df8-119">Altre informazioni in merito sono disponibili in [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="18df8-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path to application jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="18df8-120">**Esempi**:</span><span class="sxs-lookup"><span data-stu-id="18df8-120">**Examples**:</span></span>

* <span data-ttu-id="18df8-121">Se il file con estensione jar si trova nell'archivio del cluster (WASB)</span><span class="sxs-lookup"><span data-stu-id="18df8-121">If the jar file is on the cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="18df8-122">Se si vuole trasferire il nome del file con estensione JAR e il nome della classe come parte di un file di input, in questo esempio input.txt</span><span class="sxs-lookup"><span data-stu-id="18df8-122">If you want to pass the jar filename and the classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-the-cluster"></a><span data-ttu-id="18df8-123">Ottenere informazioni sui batch Livy Spark in esecuzione nel cluster</span><span class="sxs-lookup"><span data-stu-id="18df8-123">Get information on Livy Spark batches running on the cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="18df8-124">**Esempi**:</span><span class="sxs-lookup"><span data-stu-id="18df8-124">**Examples**:</span></span>

* <span data-ttu-id="18df8-125">Per recuperare tutti i batch Livy Spark in esecuzione nel cluster:</span><span class="sxs-lookup"><span data-stu-id="18df8-125">If you want to retrieve all the Livy Spark batches running on the cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="18df8-126">Se si vuole recuperare un batch specifico con un determinato ID batch</span><span class="sxs-lookup"><span data-stu-id="18df8-126">If you want to retrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="18df8-127">Eliminare un processo batch Livy Spark</span><span class="sxs-lookup"><span data-stu-id="18df8-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="18df8-128">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="18df8-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="18df8-129">Livy Spark e disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="18df8-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="18df8-130">Livy fornisce disponibilità elevata per i processi Spark in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="18df8-130">Livy provides high-availability for Spark jobs running on the cluster.</span></span> <span data-ttu-id="18df8-131">Ecco alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="18df8-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="18df8-132">Se il servizio Livy diventa inattivo dopo l'invio di un processo in modalità remota a un cluster Spark, il processo rimane in esecuzione in background.</span><span class="sxs-lookup"><span data-stu-id="18df8-132">If the Livy service goes down after you have submitted a job remotely to a Spark cluster, the job continues to run in the background.</span></span> <span data-ttu-id="18df8-133">Quando Livy ritorna attivo, ripristina lo stato del processo e crea un report.</span><span class="sxs-lookup"><span data-stu-id="18df8-133">When Livy is back up, it restores the status of the job and reports it back.</span></span>
* <span data-ttu-id="18df8-134">I notebook di Jupyter per HDInsight sono basati su Livy in back-end.</span><span class="sxs-lookup"><span data-stu-id="18df8-134">Jupyter notebooks for HDInsight are powered by Livy in the backend.</span></span> <span data-ttu-id="18df8-135">Se un notebook è in esecuzione in un processo Spark e il servizio Livy viene riavviato, il notebook continuerà a eseguire le celle del codice.</span><span class="sxs-lookup"><span data-stu-id="18df8-135">If a notebook is running a Spark job and the Livy service gets restarted, the notebook continues to run the code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="18df8-136">Mostra un esempio</span><span class="sxs-lookup"><span data-stu-id="18df8-136">Show me an example</span></span>
<span data-ttu-id="18df8-137">Questa sezione esamina alcuni esempi di come usare Livy Spark per inviare un processo batch, monitorare il progresso del processo e quindi eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="18df8-137">In this section, we look at examples to use Livy Spark to submit batch job, monitor the progress of the job, and then delete it.</span></span> <span data-ttu-id="18df8-138">L'applicazione usata in questo esempio è quella sviluppata nell'articolo [Creare un'applicazione Scala autonoma da eseguire nel cluster HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="18df8-138">The application we use in this example is the one developed in the article [Create a standalone Scala application and to run on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="18df8-139">Questa procedura presuppone che:</span><span class="sxs-lookup"><span data-stu-id="18df8-139">The steps here assume that:</span></span>

* <span data-ttu-id="18df8-140">Il file con estensione jar dell'applicazione è già stato copiato nell'account di archiviazione associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="18df8-140">You have already copied over the application jar to the storage account associated with the cluster.</span></span>
* <span data-ttu-id="18df8-141">CuRL è installato nel computer in cui si sta provando a eseguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="18df8-141">You have CuRL installed on the computer where you are trying these steps.</span></span>

<span data-ttu-id="18df8-142">Eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="18df8-142">Perform the following steps:</span></span>

1. <span data-ttu-id="18df8-143">Verificare prima che Livy Spark sia in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="18df8-143">Let us first verify that Livy Spark is running on the cluster.</span></span> <span data-ttu-id="18df8-144">È possibile eseguire questa operazione ottenendo un elenco di batch in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="18df8-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="18df8-145">Se è la prima volta che si esegue un processo usando Livy, il risultato restituito dovrebbe essere zero.</span><span class="sxs-lookup"><span data-stu-id="18df8-145">If you are running a job using Livy for the first time, the output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="18df8-146">L'output dovrebbe essere simile al seguente frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="18df8-146">You should get an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="18df8-147">Si noti che l'ultima riga nell'output corrisponde a **total:0**, che indica che non sono presenti batch in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="18df8-147">Notice how the last line in the output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="18df8-148">Inviare ora un processo batch.</span><span class="sxs-lookup"><span data-stu-id="18df8-148">Let us now submit a batch job.</span></span> <span data-ttu-id="18df8-149">Il frammento di codice seguente usa un file di input (input.txt) per trasferire il nome del file con estensione JAR e il nome della classe come parametri.</span><span class="sxs-lookup"><span data-stu-id="18df8-149">The following snippet uses an input file (input.txt) to pass the jar name and the class name as parameters.</span></span> <span data-ttu-id="18df8-150">L'uso di un file di input è l'approccio consigliato se si eseguono questi passaggi da un computer Windows.</span><span class="sxs-lookup"><span data-stu-id="18df8-150">If you are running these steps from a Windows computer, using an input file is the recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="18df8-151">I parametri nel file **input.txt** sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="18df8-151">The parameters in the file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="18df8-152">L'output visualizzato dovrebbe essere simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="18df8-152">You should see an output similar to the  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="18df8-153">Si noti che l'ultima riga dell'output indica **state:starting**.</span><span class="sxs-lookup"><span data-stu-id="18df8-153">Notice how the last line of the output says **state:starting**.</span></span> <span data-ttu-id="18df8-154">Indica anche **id:0**.</span><span class="sxs-lookup"><span data-stu-id="18df8-154">It also says, **id:0**.</span></span> <span data-ttu-id="18df8-155">**0** è l'ID del batch.</span><span class="sxs-lookup"><span data-stu-id="18df8-155">Here, **0** is the batch ID.</span></span>

3. <span data-ttu-id="18df8-156">È ora possibile recuperare lo stato di questo batch specifico usando l'ID del batch.</span><span class="sxs-lookup"><span data-stu-id="18df8-156">You can now retrieve the status of this specific batch using the batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="18df8-157">L'output visualizzato dovrebbe essere simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="18df8-157">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="18df8-158">L'output ora indica **state:success**, il che suggerisce che il processo è stato completato.</span><span class="sxs-lookup"><span data-stu-id="18df8-158">The output now shows **state:success**, which suggests that the job was successfully completed.</span></span>

4. <span data-ttu-id="18df8-159">Se si vuole, è ora possibile eliminare il batch.</span><span class="sxs-lookup"><span data-stu-id="18df8-159">If you want, you can now delete the batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="18df8-160">L'output visualizzato dovrebbe essere simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="18df8-160">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="18df8-161">L'ultima riga dell'output indica che il batch è stato correttamente eliminato.</span><span class="sxs-lookup"><span data-stu-id="18df8-161">The last line of the output shows that the batch was successfully deleted.</span></span> <span data-ttu-id="18df8-162">Anche l'eliminazione di un processo, mentre è in esecuzione, termina il processo.</span><span class="sxs-lookup"><span data-stu-id="18df8-162">Deleting a job, while it is running, also kills the job.</span></span> <span data-ttu-id="18df8-163">Se si elimina un processo completato correttamente o non correttamente, le informazioni sul processo vengono eliminate completamente.</span><span class="sxs-lookup"><span data-stu-id="18df8-163">If you delete a job that has completed, successfully or otherwise, it deletes the job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="18df8-164">Uso di Livy Spark nei cluster HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="18df8-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="18df8-165">Un cluster HDInsight 3.5, per impostazione predefinita, disabilita l'uso di percorsi di file locali per accedere ai file di dati di esempio o a file JAR.</span><span class="sxs-lookup"><span data-stu-id="18df8-165">HDInsight 3.5 cluster, by default, disables use of local file paths to access sample data files or jars.</span></span> <span data-ttu-id="18df8-166">Si consiglia di usare invece il percorso `wasb://` per accedere a file JAR o a file di dati di esempio dal cluster.</span><span class="sxs-lookup"><span data-stu-id="18df8-166">We encourage you to use the `wasb://` path instead to access jars or sample data files from the cluster.</span></span> <span data-ttu-id="18df8-167">Se si vuole usare un percorso locale, è necessario aggiornare di conseguenza la configurazione di Ambari.</span><span class="sxs-lookup"><span data-stu-id="18df8-167">If you do want to use local path, you must update the Ambari configuration accordingly.</span></span> <span data-ttu-id="18df8-168">A tale scopo, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="18df8-168">To do so:</span></span>

1. <span data-ttu-id="18df8-169">Passare al portale di Ambari per il cluster.</span><span class="sxs-lookup"><span data-stu-id="18df8-169">Go to the Ambari portal for the cluster.</span></span> <span data-ttu-id="18df8-170">L'interfaccia utente Web di Ambari è disponibile nel cluster HDInsight all'indirizzo https://**NOMECLUSTER**.azurehdidnsight.net, dove NOMECLUSTER è il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="18df8-170">The Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is the name of your cluster.</span></span>

2. <span data-ttu-id="18df8-171">Nel riquadro di spostamento sinistro fare clic su **Livy** e quindi su **Configs** (Configurazioni).</span><span class="sxs-lookup"><span data-stu-id="18df8-171">From the left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="18df8-172">In **livy-default** aggiungere il nome della proprietà `livy.file.local-dir-whitelist` e impostarne il valore su **"/"**, per consentire l'accesso completo al file system.</span><span class="sxs-lookup"><span data-stu-id="18df8-172">Under **livy-default** add the property name `livy.file.local-dir-whitelist` and set it's value to **"/"** if you want to allow full access to file system.</span></span> <span data-ttu-id="18df8-173">Se si vuole consentire l'accesso solo a una directory specifica, specificare il percorso di tale directory come valore.</span><span class="sxs-lookup"><span data-stu-id="18df8-173">If you want to allow access only to a specific directory, provide the path to that directory as the value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="18df8-174">Invio di processi Livy per un cluster all'interno di una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="18df8-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="18df8-175">Se ci si connette a un cluster HDInsight Spark all'interno di una rete virtuale di Azure, è possibile connettersi direttamente a Livy nel cluster.</span><span class="sxs-lookup"><span data-stu-id="18df8-175">If you connect to an HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect to Livy on the cluster.</span></span> <span data-ttu-id="18df8-176">In tal caso, l'URL per l'endpoint di Livy è `http://<IP address of the headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="18df8-176">In such a case, the URL for Livy endpoint is `http://<IP address of the headnode>:8998/batches`.</span></span> <span data-ttu-id="18df8-177">In questo caso, **8998** è la porta su cui viene eseguito Livy sul nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="18df8-177">Here, **8998** is the port on which Livy runs on the cluster headnode.</span></span> <span data-ttu-id="18df8-178">Per altre informazioni sull'accesso ai servizi sulle porte non pubbliche, vedere [Porte usate dai servizi Hadoop su HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="18df8-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="18df8-179">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="18df8-179">Troubleshooting</span></span>

<span data-ttu-id="18df8-180">Di seguito sono illustrati alcuni problemi riscontrabili durante l'uso di Livy per l'invio di processi remoti ai cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="18df8-180">Here are some issues that you might run into while using Livy for remote job submission to Spark clusters.</span></span>

### <a name="using-an-external-jar-from-the-additional-storage-is-not-supported"></a><span data-ttu-id="18df8-181">L'uso di un file jar esterno dalla risorsa di archiviazione aggiuntiva non è supportato.</span><span class="sxs-lookup"><span data-stu-id="18df8-181">Using an external jar from the additional storage is not supported</span></span>

<span data-ttu-id="18df8-182">**Problema:** se il processo Livy Spark fa riferimento a un file con estensione JAR esterno dall'account di archiviazione associata al cluster, il processo avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="18df8-182">**Problem:** If your Livy Spark job references an external jar from the additional storage account associated with the cluster, the job fails.</span></span>

<span data-ttu-id="18df8-183">**Soluzione:** verificare che il file jar che si vuole usare sia disponibile nella risorsa di archiviazione associata al cluster HDInsight predefinito.</span><span class="sxs-lookup"><span data-stu-id="18df8-183">**Resolution:** Make sure that the jar you want to use is available in the default storage associated with the HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="18df8-184">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="18df8-184">Next step</span></span>

* [<span data-ttu-id="18df8-185">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="18df8-185">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="18df8-186">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="18df8-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

