---
title: cluster aaaTroubleshoot problemi con Apache Spark in HDInsight di Azure | Documenti Microsoft
description: Informazioni sui problemi correlati tooApache i cluster Spark in Azure HDInsight e come toowork intorno quelli.
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
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="4e60e-103">Problemi noti del cluster Apache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e60e-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="4e60e-104">Questo documento tiene traccia di hello tutti i problemi per l'anteprima pubblica di HDInsight Spark hello noti.</span><span class="sxs-lookup"><span data-stu-id="4e60e-104">This document keeps track of all hello known issues for hello HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="4e60e-105">Livy perde la sessione interattiva</span><span class="sxs-lookup"><span data-stu-id="4e60e-105">Livy leaks interactive session</span></span>
<span data-ttu-id="4e60e-106">Quando inserire il riavvio (Ambari o a causa il riavvio del computer virtuale tooheadnode 0) con una sessione interattiva ancora attiva, è possibile che una sessione interattiva andrà perso.</span><span class="sxs-lookup"><span data-stu-id="4e60e-106">When Livy is restarted (from Ambari or due tooheadnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="4e60e-107">Per questo motivo, può essere di nuovo i processi bloccato nello stato accettato hello e non può essere avviato.</span><span class="sxs-lookup"><span data-stu-id="4e60e-107">Because of this, new jobs can stuck in hello Accepted state, and cannot be started.</span></span>

<span data-ttu-id="4e60e-108">**Soluzione:**</span><span class="sxs-lookup"><span data-stu-id="4e60e-108">**Mitigation:**</span></span>

<span data-ttu-id="4e60e-109">Utilizzare hello problema hello tooworkaround di stored procedure seguente:</span><span class="sxs-lookup"><span data-stu-id="4e60e-109">Use hello following procedure tooworkaround hello issue:</span></span>

1. <span data-ttu-id="4e60e-110">Eseguire SSH nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="4e60e-110">Ssh into headnode.</span></span> <span data-ttu-id="4e60e-111">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4e60e-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4e60e-112">Esecuzione hello seguente un'applicazione hello toofind comando ID dei processi interattivi hello avviato tramite inserire il.</span><span class="sxs-lookup"><span data-stu-id="4e60e-112">Run hello following command toofind hello application IDs of hello interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="4e60e-113">Hello nomi di processo predefiniti saranno inserire il se hello processi sono stati avviati con una sessione interattiva di inserire il senza nomi esplicita specificata, per hello sessione avviata dal server Jupyter notebook inserire il nome del processo hello inizierà con remotesparkmagics_ *.</span><span class="sxs-lookup"><span data-stu-id="4e60e-113">hello default job names will be Livy if hello jobs were started with a Livy interactive session with no explicit names specified, For hello Livy session started by Jupyter notebook, hello job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="4e60e-114">Comando che segue hello esecuzione tookill tali processi.</span><span class="sxs-lookup"><span data-stu-id="4e60e-114">Run hello following command tookill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="4e60e-115">Verranno avviati nuovi processi.</span><span class="sxs-lookup"><span data-stu-id="4e60e-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="4e60e-116">Il server cronologia Spark non viene avviato</span><span class="sxs-lookup"><span data-stu-id="4e60e-116">Spark History Server not started</span></span>
<span data-ttu-id="4e60e-117">Il server cronologia Spark non viene avviato automaticamente dopo la creazione di un cluster.</span><span class="sxs-lookup"><span data-stu-id="4e60e-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="4e60e-118">**Soluzione:**</span><span class="sxs-lookup"><span data-stu-id="4e60e-118">**Mitigation:**</span></span> 

<span data-ttu-id="4e60e-119">Avviare manualmente il server di cronologia hello da Ambari.</span><span class="sxs-lookup"><span data-stu-id="4e60e-119">Manually start hello history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="4e60e-120">Problema di autorizzazioni nella directory log Spark</span><span class="sxs-lookup"><span data-stu-id="4e60e-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="4e60e-121">Quando hdiuser invia un processo con spark-submit, si verifica un errore java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (autorizzazione negata) e hello log driver non è stato scritto.</span><span class="sxs-lookup"><span data-stu-id="4e60e-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and hello driver log is not written.</span></span> 

<span data-ttu-id="4e60e-122">**Soluzione:**</span><span class="sxs-lookup"><span data-stu-id="4e60e-122">**Mitigation:**</span></span>

1. <span data-ttu-id="4e60e-123">Aggiungere il gruppo hdiuser toohello Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4e60e-123">Add hdiuser toohello Hadoop group.</span></span> 
2. <span data-ttu-id="4e60e-124">Indicare 777 autorizzazioni in /var/log/spark dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="4e60e-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="4e60e-125">Percorso di log spark hello utilizzando Ambari toobe una directory con 777 autorizzazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="4e60e-125">Update hello spark log location using Ambari toobe a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="4e60e-126">Eseguire spark-submit come sudo.</span><span class="sxs-lookup"><span data-stu-id="4e60e-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="4e60e-127">Il connettore Spark-Phoenix non è supportato</span><span class="sxs-lookup"><span data-stu-id="4e60e-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="4e60e-128">Attualmente, il connettore di Spark Phoenix hello non è supportato con un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="4e60e-128">Currently, hello Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="4e60e-129">**Soluzione:**</span><span class="sxs-lookup"><span data-stu-id="4e60e-129">**Mitigation:**</span></span>

<span data-ttu-id="4e60e-130">È invece necessario utilizzare connettore Spark HBase hello.</span><span class="sxs-lookup"><span data-stu-id="4e60e-130">You must use hello Spark-HBase connector instead.</span></span> <span data-ttu-id="4e60e-131">Per istruzioni, vedere [come connettore Spark HBase toouse](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="4e60e-131">For instructions see [How toouse Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-toojupyter-notebooks"></a><span data-ttu-id="4e60e-132">I problemi relativi a notebook tooJupyter</span><span class="sxs-lookup"><span data-stu-id="4e60e-132">Issues related tooJupyter notebooks</span></span>
<span data-ttu-id="4e60e-133">Di seguito sono i blocchi appunti tooJupyter correlati alcuni problemi noti.</span><span class="sxs-lookup"><span data-stu-id="4e60e-133">Following are some known issues related tooJupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="4e60e-134">Notebook con nomi di file contenenti caratteri non ASCII</span><span class="sxs-lookup"><span data-stu-id="4e60e-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="4e60e-135">I notebook Jupyter utilizzabili nei cluster HDInsight Spark non devono contenere nei nomi di file caratteri non ASCII.</span><span class="sxs-lookup"><span data-stu-id="4e60e-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="4e60e-136">Se si tenta di tooupload un file tramite hello UI Jupyter che ha un nome di file non ASCII, ne verrà eseguito automaticamente (vale a dire Jupyter non consente di caricare file hello, ma non genererà un errore visibile sia).</span><span class="sxs-lookup"><span data-stu-id="4e60e-136">If you try tooupload a file through hello Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload hello file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="4e60e-137">Errore durante il caricamento di notebook di maggiori dimensioni</span><span class="sxs-lookup"><span data-stu-id="4e60e-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="4e60e-138">Quando si caricano notebook di maggiori dimensioni, potrebbe comparire l'errore **`Error loading notebook`** .</span><span class="sxs-lookup"><span data-stu-id="4e60e-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="4e60e-139">**Soluzione:**</span><span class="sxs-lookup"><span data-stu-id="4e60e-139">**Mitigation:**</span></span>

<span data-ttu-id="4e60e-140">Se viene visualizzato questo errore, non significa che i dati sono danneggiati o persi.</span><span class="sxs-lookup"><span data-stu-id="4e60e-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="4e60e-141">I blocchi appunti sono ancora nell'unità disco in `/var/lib/jupyter`, ed è possibile SSH in hello cluster tooaccess li.</span><span class="sxs-lookup"><span data-stu-id="4e60e-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into hello cluster tooaccess them.</span></span> <span data-ttu-id="4e60e-142">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4e60e-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="4e60e-143">Dopo avere connesso il cluster toohello tramite SSH, è possibile copiare i blocchi appunti dal cluster tooyour computer locale (tramite SCP o WinSCP) come una perdita di hello tooprevent backup dei dati importanti nel blocco note hello.</span><span class="sxs-lookup"><span data-stu-id="4e60e-143">Once you have connected toohello cluster using SSH, you can copy your notebooks from your cluster tooyour local machine (using SCP or WinSCP) as a backup tooprevent hello loss of any important data in hello notebook.</span></span> <span data-ttu-id="4e60e-144">È quindi possibile tunnel SSH nel nodo head in porte 8001 tooaccess Jupyter senza passare attraverso il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="4e60e-144">You can then SSH tunnel into your headnode at port 8001 tooaccess Jupyter without going through hello gateway.</span></span>  <span data-ttu-id="4e60e-145">Da qui, è possibile cancellare l'output di hello del blocco note e salvarlo nuovamente la dimensione del blocco per Appunti toominimize hello.</span><span class="sxs-lookup"><span data-stu-id="4e60e-145">From there, you can clear hello output of your notebook and re-save it toominimize hello notebook’s size.</span></span>

<span data-ttu-id="4e60e-146">tooprevent l'errore accada in futuro, è necessario seguire alcune procedure consigliate hello:</span><span class="sxs-lookup"><span data-stu-id="4e60e-146">tooprevent this error from happening in hello future, you must follow some best practices:</span></span>

* <span data-ttu-id="4e60e-147">È importante tookeep dimensioni di blocco per Appunti hello piccole.</span><span class="sxs-lookup"><span data-stu-id="4e60e-147">It is important tookeep hello notebook size small.</span></span> <span data-ttu-id="4e60e-148">Da processi di Spark l'output viene inviato nuovamente tooJupyter è persistente nel blocco note hello.</span><span class="sxs-lookup"><span data-stu-id="4e60e-148">Any output from your Spark jobs that is sent back tooJupyter is persisted in hello notebook.</span></span>  <span data-ttu-id="4e60e-149">È buona norma con Jupyter in tooavoid generale in esecuzione `.collect()` su grandi RDD o frame di dati; in alternativa, se si desidera toopeek contenuto del RDD, si consideri l'esecuzione `.take()` o `.sample()` in modo che l'output non ottiene troppo grande.</span><span class="sxs-lookup"><span data-stu-id="4e60e-149">It is a best practice with Jupyter in general tooavoid running `.collect()` on large RDD’s or dataframes; instead, if you want toopeek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="4e60e-150">Inoltre, quando si salva un notebook, deselezionare tutto l'output dimensioni hello tooreduce di celle.</span><span class="sxs-lookup"><span data-stu-id="4e60e-150">Also, when you save a notebook, clear all output cells tooreduce hello size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="4e60e-151">L'avvio iniziale del notebook richiede più tempo del previsto</span><span class="sxs-lookup"><span data-stu-id="4e60e-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="4e60e-152">La prima istruzione del codice nel notebook di Jupyter tramite il magic Spark potrebbe richiedere più di un minuto.</span><span class="sxs-lookup"><span data-stu-id="4e60e-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="4e60e-153">**Spiegazione:**</span><span class="sxs-lookup"><span data-stu-id="4e60e-153">**Explanation:**</span></span>

<span data-ttu-id="4e60e-154">Ciò accade perché quando si esegue prima cella di codice hello.</span><span class="sxs-lookup"><span data-stu-id="4e60e-154">This happens because when hello first code cell is run.</span></span> <span data-ttu-id="4e60e-155">In background hello verrà avviata la configurazione di sessione e Spark, SQL e contesti di Hive sono impostati.</span><span class="sxs-lookup"><span data-stu-id="4e60e-155">In hello background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="4e60e-156">Dopo aver impostati questi contesti, viene eseguita prima istruzione hello e in questo modo l'impressione di hello che istruzione hello ha richiesto un toocomplete molto tempo.</span><span class="sxs-lookup"><span data-stu-id="4e60e-156">After these contexts are set, hello first statement is run and this gives hello impression that hello statement took a long time toocomplete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a><span data-ttu-id="4e60e-157">Server Jupyter notebook timeout per la creazione della sessione hello</span><span class="sxs-lookup"><span data-stu-id="4e60e-157">Jupyter notebook timeout in creating hello session</span></span>
<span data-ttu-id="4e60e-158">Quando il cluster Spark è esaurito le risorse, hello Spark e Pyspark kernel in notebook Jupyter hello verrà timeout sessione hello toocreate durante il tentativo.</span><span class="sxs-lookup"><span data-stu-id="4e60e-158">When Spark cluster is out of resources, hello Spark and Pyspark kernels in hello Jupyter notebook will timeout trying toocreate hello session.</span></span> 

<span data-ttu-id="4e60e-159">**Soluzioni:**</span><span class="sxs-lookup"><span data-stu-id="4e60e-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="4e60e-160">Liberare alcune risorse nel cluster Spark nei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4e60e-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="4e60e-161">L'arresto di altri blocchi appunti Spark passare toohello chiudere e menu di arresto o facendo clic su arresto in Esplora notebook hello.</span><span class="sxs-lookup"><span data-stu-id="4e60e-161">Stopping other Spark notebooks by going toohello Close and Halt menu or clicking Shutdown in hello notebook explorer.</span></span>
   * <span data-ttu-id="4e60e-162">Arrestando altre applicazioni Spark da YARN.</span><span class="sxs-lookup"><span data-stu-id="4e60e-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="4e60e-163">Riavviare notebook hello che si stava cercando toostart backup.</span><span class="sxs-lookup"><span data-stu-id="4e60e-163">Restart hello notebook you were trying toostart up.</span></span> <span data-ttu-id="4e60e-164">Numero sufficiente di risorse devono essere disponibili per toocreate è ora una sessione.</span><span class="sxs-lookup"><span data-stu-id="4e60e-164">Enough resources should be available for you toocreate a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="4e60e-165">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="4e60e-165">See also</span></span>
* [<span data-ttu-id="4e60e-166">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e60e-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="4e60e-167">Scenari</span><span class="sxs-lookup"><span data-stu-id="4e60e-167">Scenarios</span></span>
* [<span data-ttu-id="4e60e-168">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e60e-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="4e60e-169">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="4e60e-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="4e60e-170">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="4e60e-170">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="4e60e-171">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="4e60e-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="4e60e-172">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e60e-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="4e60e-173">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="4e60e-173">Create and run applications</span></span>
* [<span data-ttu-id="4e60e-174">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="4e60e-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="4e60e-175">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="4e60e-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="4e60e-176">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="4e60e-176">Tools and extensions</span></span>
* [<span data-ttu-id="4e60e-177">Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="4e60e-177">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="4e60e-178">Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota</span><span class="sxs-lookup"><span data-stu-id="4e60e-178">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="4e60e-179">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e60e-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="4e60e-180">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e60e-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="4e60e-181">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="4e60e-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="4e60e-182">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="4e60e-182">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="4e60e-183">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="4e60e-183">Manage resources</span></span>
* [<span data-ttu-id="4e60e-184">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="4e60e-184">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="4e60e-185">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e60e-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

