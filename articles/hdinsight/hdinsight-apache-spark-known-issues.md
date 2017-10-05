---
title: Risolvere i problemi del cluster Apache Spark in Azure HDInsight | Microsoft Docs
description: Informazioni sui problemi relativi ai cluster Apache Spark in HDInsight di Azure e come risolverli.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3a493a2c35a6cdd31bb1e4ff66113a8f8d97d4f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="ecc51-103">Problemi noti del cluster Apache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ecc51-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="ecc51-104">Questo documento elenca tutti i problemi noti relativi all'anteprima pubblica di HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="ecc51-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="ecc51-105">Livy perde la sessione interattiva</span><span class="sxs-lookup"><span data-stu-id="ecc51-105">Livy leaks interactive session</span></span>
<span data-ttu-id="ecc51-106">Quando Livy viene riavviato (da Ambari oppure a causa del riavvio della macchina virtuale con nodo head 0) con una sessione interattiva ancora attiva, una sessione di processo interattiva andrà persa.</span><span class="sxs-lookup"><span data-stu-id="ecc51-106">When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="ecc51-107">Per questo motivo, i nuovi processi possono rimanere bloccati in stato Accettato e non possono essere avviati.</span><span class="sxs-lookup"><span data-stu-id="ecc51-107">Because of this, new jobs can stuck in the Accepted state, and cannot be started.</span></span>

<span data-ttu-id="ecc51-108">**Soluzione:**</span><span class="sxs-lookup"><span data-stu-id="ecc51-108">**Mitigation:**</span></span>

<span data-ttu-id="ecc51-109">Seguire questa procedura per risolvere il problema:</span><span class="sxs-lookup"><span data-stu-id="ecc51-109">Use the following procedure to workaround the issue:</span></span>

1. <span data-ttu-id="ecc51-110">Eseguire SSH nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="ecc51-110">Ssh into headnode.</span></span> <span data-ttu-id="ecc51-111">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ecc51-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ecc51-112">Eseguire il comando seguente per trovare gli ID applicazione dei processi interattivi avviati tramite Livy.</span><span class="sxs-lookup"><span data-stu-id="ecc51-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="ecc51-113">I nomi di processo predefiniti corrispondono a Livy se i processi sono stati avviati con una sessione interattiva Livy senza specificare nomi espliciti. Per la sessione Livy avviata dal notebook di Jupyter, il nome del processo verrà avviato con remotesparkmagics_*.</span><span class="sxs-lookup"><span data-stu-id="ecc51-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="ecc51-114">Eseguire il comando seguente per terminare questi processi.</span><span class="sxs-lookup"><span data-stu-id="ecc51-114">Run the following command to kill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="ecc51-115">Verranno avviati nuovi processi.</span><span class="sxs-lookup"><span data-stu-id="ecc51-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="ecc51-116">Il server cronologia Spark non viene avviato</span><span class="sxs-lookup"><span data-stu-id="ecc51-116">Spark History Server not started</span></span>
<span data-ttu-id="ecc51-117">Il server cronologia Spark non viene avviato automaticamente dopo la creazione di un cluster.</span><span class="sxs-lookup"><span data-stu-id="ecc51-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="ecc51-118">**Soluzione:**</span><span class="sxs-lookup"><span data-stu-id="ecc51-118">**Mitigation:**</span></span> 

<span data-ttu-id="ecc51-119">Avviare manualmente il server cronologia da Ambari.</span><span class="sxs-lookup"><span data-stu-id="ecc51-119">Manually start the history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="ecc51-120">Problema di autorizzazioni nella directory log Spark</span><span class="sxs-lookup"><span data-stu-id="ecc51-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="ecc51-121">Quando hdiuser invia un processo con spark-submit, si verifica un errore java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (autorizzazione negata) e il log del driver non viene scritto.</span><span class="sxs-lookup"><span data-stu-id="ecc51-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written.</span></span> 

<span data-ttu-id="ecc51-122">**Soluzione:**</span><span class="sxs-lookup"><span data-stu-id="ecc51-122">**Mitigation:**</span></span>

1. <span data-ttu-id="ecc51-123">Aggiungere hdiuser al gruppo Hadoop.</span><span class="sxs-lookup"><span data-stu-id="ecc51-123">Add hdiuser to the Hadoop group.</span></span> 
2. <span data-ttu-id="ecc51-124">Indicare 777 autorizzazioni in /var/log/spark dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="ecc51-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="ecc51-125">Aggiornare il percorso del log Spark tramite Ambari in modo che corrisponda a una directory con 777 autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="ecc51-125">Update the spark log location using Ambari to be a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="ecc51-126">Eseguire spark-submit come sudo.</span><span class="sxs-lookup"><span data-stu-id="ecc51-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="ecc51-127">Il connettore Spark-Phoenix non è supportato</span><span class="sxs-lookup"><span data-stu-id="ecc51-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="ecc51-128">Attualmente, il connettore Spark-Phoenix non è supportato in un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="ecc51-128">Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="ecc51-129">**Soluzione:**</span><span class="sxs-lookup"><span data-stu-id="ecc51-129">**Mitigation:**</span></span>

<span data-ttu-id="ecc51-130">Usare il connettore Spark-HBase.</span><span class="sxs-lookup"><span data-stu-id="ecc51-130">You must use the Spark-HBase connector instead.</span></span> <span data-ttu-id="ecc51-131">Per istruzioni, vedere [Come usare un connettore Spark-HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="ecc51-131">For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-to-jupyter-notebooks"></a><span data-ttu-id="ecc51-132">Problemi relativi ai notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="ecc51-132">Issues related to Jupyter notebooks</span></span>
<span data-ttu-id="ecc51-133">Seguito alcuni problemi noti relativi ai notebook Jupyter.</span><span class="sxs-lookup"><span data-stu-id="ecc51-133">Following are some known issues related to Jupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="ecc51-134">Notebook con nomi di file contenenti caratteri non ASCII</span><span class="sxs-lookup"><span data-stu-id="ecc51-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="ecc51-135">I notebook Jupyter utilizzabili nei cluster HDInsight Spark non devono contenere nei nomi di file caratteri non ASCII.</span><span class="sxs-lookup"><span data-stu-id="ecc51-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="ecc51-136">Se si tenta di caricare tramite l'interfaccia utente Jupyter un file con un nome di file non ASCII, l'operazione si interromperà senza avvisi. Questo significa che Jupyter non consentirà di caricare il file, ma non genererà un errore visibile.</span><span class="sxs-lookup"><span data-stu-id="ecc51-136">If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="ecc51-137">Errore durante il caricamento di notebook di maggiori dimensioni</span><span class="sxs-lookup"><span data-stu-id="ecc51-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="ecc51-138">Quando si caricano notebook di maggiori dimensioni, potrebbe comparire l'errore **`Error loading notebook`** .</span><span class="sxs-lookup"><span data-stu-id="ecc51-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="ecc51-139">**Soluzione:**</span><span class="sxs-lookup"><span data-stu-id="ecc51-139">**Mitigation:**</span></span>

<span data-ttu-id="ecc51-140">Se viene visualizzato questo errore, non significa che i dati sono danneggiati o persi.</span><span class="sxs-lookup"><span data-stu-id="ecc51-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="ecc51-141">I notebook sono ancora disponibili su disco in `/var/lib/jupyter`ed è possibile usare SSH nel cluster per accedervi.</span><span class="sxs-lookup"><span data-stu-id="ecc51-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span></span> <span data-ttu-id="ecc51-142">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ecc51-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="ecc51-143">Dopo aver effettuato la connessione al cluster usando SSH, è possibile copiare i notebook dal cluster nel computer locale (tramite SCP o WinSCP) come backup per evitare la perdita di dati importanti del notebook.</span><span class="sxs-lookup"><span data-stu-id="ecc51-143">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span></span> <span data-ttu-id="ecc51-144">È quindi possibile usare SSH per il tunneling al nodo head sulla porta 8001 e accedere a Jupyter senza passare attraverso il gateway.</span><span class="sxs-lookup"><span data-stu-id="ecc51-144">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span></span>  <span data-ttu-id="ecc51-145">Qui è possibile cancellare l'output del notebook e salvarlo di nuovo per ridurne le dimensioni.</span><span class="sxs-lookup"><span data-stu-id="ecc51-145">From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.</span></span>

<span data-ttu-id="ecc51-146">Per evitare questo errore in futuro, è necessario seguire alcune procedure consigliate:</span><span class="sxs-lookup"><span data-stu-id="ecc51-146">To prevent this error from happening in the future, you must follow some best practices:</span></span>

* <span data-ttu-id="ecc51-147">È importante mantenere ridotte le dimensioni del notebook.</span><span class="sxs-lookup"><span data-stu-id="ecc51-147">It is important to keep the notebook size small.</span></span> <span data-ttu-id="ecc51-148">L'output dei processi Spark inviato a Jupyter viene salvato in modo permanente nel notebook.</span><span class="sxs-lookup"><span data-stu-id="ecc51-148">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span></span>  <span data-ttu-id="ecc51-149">Con Jupyter in genere è consigliabile evitare di eseguire `.collect()` su RDD o frame di dati di grandi dimensioni. Se si vuole visualizzare il contenuto di un RDD, considerare invece la possibilità di eseguire `.take()` o `.sample()` per evitare la crescita eccessiva dell'output.</span><span class="sxs-lookup"><span data-stu-id="ecc51-149">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="ecc51-150">Quando si salva un notebook, cancellare anche tutte le celle di output per ridurre le dimensioni.</span><span class="sxs-lookup"><span data-stu-id="ecc51-150">Also, when you save a notebook, clear all output cells to reduce the size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="ecc51-151">L'avvio iniziale del notebook richiede più tempo del previsto</span><span class="sxs-lookup"><span data-stu-id="ecc51-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="ecc51-152">La prima istruzione del codice nel notebook di Jupyter tramite il magic Spark potrebbe richiedere più di un minuto.</span><span class="sxs-lookup"><span data-stu-id="ecc51-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="ecc51-153">**Spiegazione:**</span><span class="sxs-lookup"><span data-stu-id="ecc51-153">**Explanation:**</span></span>

<span data-ttu-id="ecc51-154">Ciò accade quando viene eseguita la prima cella di codice.</span><span class="sxs-lookup"><span data-stu-id="ecc51-154">This happens because when the first code cell is run.</span></span> <span data-ttu-id="ecc51-155">In background viene avviata la configurazione della sessione e vengono impostati i contesti Spark, SQL e Hive.</span><span class="sxs-lookup"><span data-stu-id="ecc51-155">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="ecc51-156">La prima istruzione viene eseguita dopo l'impostazione di questi contesti, dando l'impressione che l'esecuzione dell'istruzione impieghi molto tempo.</span><span class="sxs-lookup"><span data-stu-id="ecc51-156">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a><span data-ttu-id="ecc51-157">Timeout del notebook di Jupyter durante la creazione della sessione</span><span class="sxs-lookup"><span data-stu-id="ecc51-157">Jupyter notebook timeout in creating the session</span></span>
<span data-ttu-id="ecc51-158">Quando il cluster Spark esaurisce le risorse, si verificherà il timeout dei kernel Spark e Pyspark nel notebook di Jupyter quando si cerca di creare la sessione.</span><span class="sxs-lookup"><span data-stu-id="ecc51-158">When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session.</span></span> 

<span data-ttu-id="ecc51-159">**Soluzioni:**</span><span class="sxs-lookup"><span data-stu-id="ecc51-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="ecc51-160">Liberare alcune risorse nel cluster Spark nei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ecc51-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="ecc51-161">Arrestando altri notebook Spark selezionando il menu Close and Halt o facendo clic su Shutdown nel notebook.</span><span class="sxs-lookup"><span data-stu-id="ecc51-161">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span></span>
   * <span data-ttu-id="ecc51-162">Arrestando altre applicazioni Spark da YARN.</span><span class="sxs-lookup"><span data-stu-id="ecc51-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="ecc51-163">Riavviare il notebook che si stava cercando di avviare.</span><span class="sxs-lookup"><span data-stu-id="ecc51-163">Restart the notebook you were trying to start up.</span></span> <span data-ttu-id="ecc51-164">Ora dovrebbero essere disponibili risorse sufficienti per creare una sessione.</span><span class="sxs-lookup"><span data-stu-id="ecc51-164">Enough resources should be available for you to create a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="ecc51-165">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ecc51-165">See also</span></span>
* [<span data-ttu-id="ecc51-166">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ecc51-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="ecc51-167">Scenari</span><span class="sxs-lookup"><span data-stu-id="ecc51-167">Scenarios</span></span>
* [<span data-ttu-id="ecc51-168">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ecc51-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="ecc51-169">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="ecc51-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="ecc51-170">Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="ecc51-170">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="ecc51-171">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="ecc51-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="ecc51-172">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ecc51-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="ecc51-173">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="ecc51-173">Create and run applications</span></span>
* [<span data-ttu-id="ecc51-174">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="ecc51-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ecc51-175">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="ecc51-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="ecc51-176">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="ecc51-176">Tools and extensions</span></span>
* [<span data-ttu-id="ecc51-177">Usare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark in Scala</span><span class="sxs-lookup"><span data-stu-id="ecc51-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="ecc51-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Usare il plug-in Strumenti HDInsight per IntelliJ IDEA per eseguire il debug di applicazioni Spark in remoto)</span><span class="sxs-lookup"><span data-stu-id="ecc51-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="ecc51-179">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ecc51-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="ecc51-180">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="ecc51-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="ecc51-181">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="ecc51-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="ecc51-182">Installare Jupyter Notebook nel computer e connetterlo a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="ecc51-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="ecc51-183">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="ecc51-183">Manage resources</span></span>
* [<span data-ttu-id="ecc51-184">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ecc51-184">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="ecc51-185">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ecc51-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

