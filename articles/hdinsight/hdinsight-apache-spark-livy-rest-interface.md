---
title: cluster aaaUse inserire il Spark toosubmit processi tooSpark in Azure HDInsight | Documenti Microsoft
description: "Informazioni su come toouse API REST di Apache Spark toosubmit Spark i processi in modalità remota cluster Azure HDInsight tooan."
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
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a><span data-ttu-id="34ffa-104">Utilizzare l'API REST di Apache Spark toosubmit processi remoti tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="34ffa-104">Use Apache Spark REST API toosubmit remote jobs tooan HDInsight Spark cluster</span></span>

<span data-ttu-id="34ffa-105">Informazioni su come inserire il, hello Apache Spark l'API REST che è usato toosubmit remoto toouse processi cluster Azure HDInsight Spark tooan.</span><span class="sxs-lookup"><span data-stu-id="34ffa-105">Learn how toouse Livy, hello Apache Spark REST API, which is used toosubmit remote jobs tooan Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="34ffa-106">Per informazioni dettagliate, vedere [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="34ffa-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="34ffa-107">È possibile utilizzare la shell inserire il toorun interattiva Spark o inviare toobe processi batch eseguiti Spark.</span><span class="sxs-lookup"><span data-stu-id="34ffa-107">You can use Livy toorun interactive Spark shells or submit batch jobs toobe run on Spark.</span></span> <span data-ttu-id="34ffa-108">In questo articolo parla mediante processi batch di inserire il toosubmit.</span><span class="sxs-lookup"><span data-stu-id="34ffa-108">This article talks about using Livy toosubmit batch jobs.</span></span> <span data-ttu-id="34ffa-109">frammenti di codice Hello in questo articolo usare cURL toomake endpoint di inserire il Spark toohello chiamate API REST.</span><span class="sxs-lookup"><span data-stu-id="34ffa-109">hello snippets in this article use cURL toomake REST API calls toohello Livy Spark endpoint.</span></span>

<span data-ttu-id="34ffa-110">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="34ffa-110">**Prerequisites:**</span></span>

* <span data-ttu-id="34ffa-111">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="34ffa-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="34ffa-112">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="34ffa-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="34ffa-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="34ffa-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="34ffa-114">In questo articolo Usa toodemonstrate cURL come toomake API REST chiama su un cluster di HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="34ffa-114">This article uses cURL toodemonstrate how toomake REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="34ffa-115">Inviare un processo batch Livy Spark</span><span class="sxs-lookup"><span data-stu-id="34ffa-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="34ffa-116">Prima di inviare un processo batch, è necessario caricare i file jar applicazione hello nell'archiviazione cluster hello associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="34ffa-116">Before you submit a batch job, you must upload hello application jar on hello cluster storage associated with hello cluster.</span></span> <span data-ttu-id="34ffa-117">È possibile utilizzare [ **AzCopy**](../storage/common/storage-use-azcopy.md), un'utilità della riga di comando, toodo in modo.</span><span class="sxs-lookup"><span data-stu-id="34ffa-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, toodo so.</span></span> <span data-ttu-id="34ffa-118">Esistono vari altri client è possibile utilizzare dati tooupload.</span><span class="sxs-lookup"><span data-stu-id="34ffa-118">There are various other clients you can use tooupload data.</span></span> <span data-ttu-id="34ffa-119">Altre informazioni in merito sono disponibili in [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="34ffa-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="34ffa-120">**Esempi**:</span><span class="sxs-lookup"><span data-stu-id="34ffa-120">**Examples**:</span></span>

* <span data-ttu-id="34ffa-121">Se il file jar hello nell'archiviazione cluster hello (WASB)</span><span class="sxs-lookup"><span data-stu-id="34ffa-121">If hello jar file is on hello cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="34ffa-122">Se si desidera toopass hello nome del file jar e hello classname come parte di un file di input (in questo esempio, txt)</span><span class="sxs-lookup"><span data-stu-id="34ffa-122">If you want toopass hello jar filename and hello classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a><span data-ttu-id="34ffa-123">Ottenere informazioni su Spark inserire il batch in esecuzione nel cluster hello</span><span class="sxs-lookup"><span data-stu-id="34ffa-123">Get information on Livy Spark batches running on hello cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="34ffa-124">**Esempi**:</span><span class="sxs-lookup"><span data-stu-id="34ffa-124">**Examples**:</span></span>

* <span data-ttu-id="34ffa-125">Se si desidera che tutti i batch di inserire il Spark hello in esecuzione nel cluster hello tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="34ffa-125">If you want tooretrieve all hello Livy Spark batches running on hello cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="34ffa-126">Se si desidera un batch specifico con un determinato batchId tooretrieve</span><span class="sxs-lookup"><span data-stu-id="34ffa-126">If you want tooretrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="34ffa-127">Eliminare un processo batch Livy Spark</span><span class="sxs-lookup"><span data-stu-id="34ffa-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="34ffa-128">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="34ffa-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="34ffa-129">Livy Spark e disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="34ffa-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="34ffa-130">Inserire il fornisce disponibilità elevata per i processi di Spark in esecuzione nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-130">Livy provides high-availability for Spark jobs running on hello cluster.</span></span> <span data-ttu-id="34ffa-131">Ecco alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="34ffa-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="34ffa-132">Se il servizio di inserire il hello diventa inattivo dopo l'invio di un processo in modalità remota tooa Spark cluster, hello processo continua toorun in background hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-132">If hello Livy service goes down after you have submitted a job remotely tooa Spark cluster, hello job continues toorun in hello background.</span></span> <span data-ttu-id="34ffa-133">Quando inserire il backup, viene ripristinato lo stato di hello del processo hello e dei report di nuovo.</span><span class="sxs-lookup"><span data-stu-id="34ffa-133">When Livy is back up, it restores hello status of hello job and reports it back.</span></span>
* <span data-ttu-id="34ffa-134">Notebook Jupyter per HDInsight sono supportate da inserire il nel back-end hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-134">Jupyter notebooks for HDInsight are powered by Livy in hello backend.</span></span> <span data-ttu-id="34ffa-135">Se un blocco per Appunti è in esecuzione un processo di Spark e hello servizio inserire il Ottiene riavviato, notebook hello continua celle di codice hello toorun.</span><span class="sxs-lookup"><span data-stu-id="34ffa-135">If a notebook is running a Spark job and hello Livy service gets restarted, hello notebook continues toorun hello code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="34ffa-136">Mostra un esempio</span><span class="sxs-lookup"><span data-stu-id="34ffa-136">Show me an example</span></span>
<span data-ttu-id="34ffa-137">In questa sezione è esaminare il processo batch toosubmit di esempi toouse Spark inserire il, monitorare lo stato di avanzamento hello del processo di hello e quindi eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="34ffa-137">In this section, we look at examples toouse Livy Spark toosubmit batch job, monitor hello progress of hello job, and then delete it.</span></span> <span data-ttu-id="34ffa-138">viene usato in questo esempio di applicazione Hello è hello una sviluppate nell'articolo hello [creare un'applicazione Scala autonoma e toorun nel cluster di HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="34ffa-138">hello application we use in this example is hello one developed in hello article [Create a standalone Scala application and toorun on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="34ffa-139">Questa procedura Hello presuppone che:</span><span class="sxs-lookup"><span data-stu-id="34ffa-139">hello steps here assume that:</span></span>

* <span data-ttu-id="34ffa-140">Già stata copiata su hello applicazione jar toohello account di archiviazione associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="34ffa-140">You have already copied over hello application jar toohello storage account associated with hello cluster.</span></span>
* <span data-ttu-id="34ffa-141">È necessario CuRL installato nel computer di hello in cui si sta provando questa procedura.</span><span class="sxs-lookup"><span data-stu-id="34ffa-141">You have CuRL installed on hello computer where you are trying these steps.</span></span>

<span data-ttu-id="34ffa-142">Eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="34ffa-142">Perform hello following steps:</span></span>

1. <span data-ttu-id="34ffa-143">Segnalare il problema verificare innanzitutto che Spark inserire il è in esecuzione nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-143">Let us first verify that Livy Spark is running on hello cluster.</span></span> <span data-ttu-id="34ffa-144">È possibile eseguire questa operazione ottenendo un elenco di batch in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="34ffa-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="34ffa-145">Se si esegue un processo di inserire il hello prima volta, l'output di hello deve restituire zero.</span><span class="sxs-lookup"><span data-stu-id="34ffa-145">If you are running a job using Livy for hello first time, hello output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="34ffa-146">È necessario ottenere un toohello simile output frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="34ffa-146">You should get an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="34ffa-147">Si noti come viene visualizzato hello ultima riga di output di hello **totale: 0**, che non suggerisce nessun batch in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="34ffa-147">Notice how hello last line in hello output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="34ffa-148">Inviare ora un processo batch.</span><span class="sxs-lookup"><span data-stu-id="34ffa-148">Let us now submit a batch job.</span></span> <span data-ttu-id="34ffa-149">Hello frammento di codice seguente viene utilizzato un nome di file di input (txt) toopass hello jar e il nome di classe hello come parametri.</span><span class="sxs-lookup"><span data-stu-id="34ffa-149">hello following snippet uses an input file (input.txt) toopass hello jar name and hello class name as parameters.</span></span> <span data-ttu-id="34ffa-150">Se si eseguono questi passaggi da un computer Windows, utilizzando un file di input è hello approccio consigliato.</span><span class="sxs-lookup"><span data-stu-id="34ffa-150">If you are running these steps from a Windows computer, using an input file is hello recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="34ffa-151">Hello parametri nel file hello **input.txt** sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="34ffa-151">hello parameters in hello file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="34ffa-152">Verrà visualizzato un toohello simile output frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="34ffa-152">You should see an output similar toohello  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="34ffa-153">Si noti come ultima riga di hello dell'output di hello afferma **stato: avvio**.</span><span class="sxs-lookup"><span data-stu-id="34ffa-153">Notice how hello last line of hello output says **state:starting**.</span></span> <span data-ttu-id="34ffa-154">Indica anche **id:0**.</span><span class="sxs-lookup"><span data-stu-id="34ffa-154">It also says, **id:0**.</span></span> <span data-ttu-id="34ffa-155">In questo caso, **0** è hello ID del batch.</span><span class="sxs-lookup"><span data-stu-id="34ffa-155">Here, **0** is hello batch ID.</span></span>

3. <span data-ttu-id="34ffa-156">È ora possibile recuperare lo stato di hello di questo batch specifico utilizzando l'ID del batch hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-156">You can now retrieve hello status of this specific batch using hello batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="34ffa-157">Verrà visualizzato un toohello simile output frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="34ffa-157">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="34ffa-158">output di Hello illustrato **stato: operazione riuscita**, che suggerisce che il processo di hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="34ffa-158">hello output now shows **state:success**, which suggests that hello job was successfully completed.</span></span>

4. <span data-ttu-id="34ffa-159">Se si desidera, è ora possibile eliminare i batch di hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-159">If you want, you can now delete hello batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="34ffa-160">Verrà visualizzato un toohello simile output frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="34ffa-160">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="34ffa-161">Hello l'ultima riga dell'output di hello mostra che batch hello è stata eliminata.</span><span class="sxs-lookup"><span data-stu-id="34ffa-161">hello last line of hello output shows that hello batch was successfully deleted.</span></span> <span data-ttu-id="34ffa-162">Anche l'eliminazione di un processo, mentre è in esecuzione, Termina processo hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-162">Deleting a job, while it is running, also kills hello job.</span></span> <span data-ttu-id="34ffa-163">Se si elimina un processo che è stata completata, completato o in caso contrario, Elimina le informazioni di processo hello completamente.</span><span class="sxs-lookup"><span data-stu-id="34ffa-163">If you delete a job that has completed, successfully or otherwise, it deletes hello job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="34ffa-164">Uso di Livy Spark nei cluster HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="34ffa-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="34ffa-165">Cluster HDInsight 3.5, per impostazione predefinita, disabilita l'utilizzo del file di dati di esempio di file locale percorsi tooaccess o JAR.</span><span class="sxs-lookup"><span data-stu-id="34ffa-165">HDInsight 3.5 cluster, by default, disables use of local file paths tooaccess sample data files or jars.</span></span> <span data-ttu-id="34ffa-166">Si consiglia di hello toouse `wasb://` percorso invece tooaccess JAR o dati di esempio di file dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-166">We encourage you toouse hello `wasb://` path instead tooaccess jars or sample data files from hello cluster.</span></span> <span data-ttu-id="34ffa-167">Se si desidera toouse di percorso locale, è necessario aggiornare di conseguenza configurazione Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-167">If you do want toouse local path, you must update hello Ambari configuration accordingly.</span></span> <span data-ttu-id="34ffa-168">toodo in modo:</span><span class="sxs-lookup"><span data-stu-id="34ffa-168">toodo so:</span></span>

1. <span data-ttu-id="34ffa-169">Passare toohello Ambari portale per i cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-169">Go toohello Ambari portal for hello cluster.</span></span> <span data-ttu-id="34ffa-170">interfaccia utente Web Ambari Hello è disponibile il cluster HDInsight in https://**CLUSTERNAME**. azurehdidnsight.net, dove CLUSTERNAME è il nome di hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="34ffa-170">hello Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is hello name of your cluster.</span></span>

2. <span data-ttu-id="34ffa-171">Hello riquadro di spostamento sinistro, fare clic su **inserire il**, quindi fare clic su **configurazioni**.</span><span class="sxs-lookup"><span data-stu-id="34ffa-171">From hello left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="34ffa-172">In **inserire il predefinito** aggiungere il nome di proprietà hello `livy.file.local-dir-whitelist` e impostarne il valore troppo**"/"** se si desidera tooallow accesso completo toofile sistema.</span><span class="sxs-lookup"><span data-stu-id="34ffa-172">Under **livy-default** add hello property name `livy.file.local-dir-whitelist` and set it's value too**"/"** if you want tooallow full access toofile system.</span></span> <span data-ttu-id="34ffa-173">Se si desidera tooallow accesso tooa solo di directory specifico, fornire directory toothat del percorso di hello come valore hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-173">If you want tooallow access only tooa specific directory, provide hello path toothat directory as hello value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="34ffa-174">Invio di processi Livy per un cluster all'interno di una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="34ffa-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="34ffa-175">Se ci si connette tooan cluster HDInsight Spark da all'interno di una rete virtuale di Azure, è possibile connettersi direttamente tooLivy nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-175">If you connect tooan HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect tooLivy on hello cluster.</span></span> <span data-ttu-id="34ffa-176">In tal caso, hello URL per l'endpoint di inserire il `http://<IP address of hello headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="34ffa-176">In such a case, hello URL for Livy endpoint is `http://<IP address of hello headnode>:8998/batches`.</span></span> <span data-ttu-id="34ffa-177">In questo caso, **8998** hello porta in cui inserire il viene eseguito sul nodo head del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-177">Here, **8998** is hello port on which Livy runs on hello cluster headnode.</span></span> <span data-ttu-id="34ffa-178">Per altre informazioni sull'accesso ai servizi sulle porte non pubbliche, vedere [Porte usate dai servizi Hadoop su HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="34ffa-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="34ffa-179">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="34ffa-179">Troubleshooting</span></span>

<span data-ttu-id="34ffa-180">Ecco alcuni problemi che potrebbero verificarsi durante l'utilizzo di inserire il per i cluster di tooSpark invio processo remoto.</span><span class="sxs-lookup"><span data-stu-id="34ffa-180">Here are some issues that you might run into while using Livy for remote job submission tooSpark clusters.</span></span>

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a><span data-ttu-id="34ffa-181">Utilizzo di un jar esterna dalla memoria aggiuntiva hello non è supportato</span><span class="sxs-lookup"><span data-stu-id="34ffa-181">Using an external jar from hello additional storage is not supported</span></span>

<span data-ttu-id="34ffa-182">**Problema:** se il processo di inserire il Spark fa riferimento a un jar esterno dall'account di archiviazione aggiuntive hello associato hello cluster, il processo di hello non riesce.</span><span class="sxs-lookup"><span data-stu-id="34ffa-182">**Problem:** If your Livy Spark job references an external jar from hello additional storage account associated with hello cluster, hello job fails.</span></span>

<span data-ttu-id="34ffa-183">**Risoluzione:** assicurarsi che si desidera toouse è disponibile in spazio di archiviazione predefinito hello associato al cluster HDInsight hello file jar di hello.</span><span class="sxs-lookup"><span data-stu-id="34ffa-183">**Resolution:** Make sure that hello jar you want toouse is available in hello default storage associated with hello HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="34ffa-184">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="34ffa-184">Next step</span></span>

* [<span data-ttu-id="34ffa-185">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="34ffa-185">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="34ffa-186">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="34ffa-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

