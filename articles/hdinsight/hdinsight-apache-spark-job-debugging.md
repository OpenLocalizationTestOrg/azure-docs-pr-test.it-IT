---
title: aaaDebug Apache Spark processi in esecuzione in Azure HDInsight | Documenti Microsoft
description: Utilizzo dell'interfaccia utente YARN, interfaccia utente di Spark e la cronologia di Spark server tootrack ed eseguire il debug dei processi in esecuzione in un cluster Spark in HDInsight di Azure
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="eacd0-103">Eseguire il debug di processi Apache Spark in esecuzione in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="eacd0-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="eacd0-104">In questo articolo si apprenderà come tootrack e debug nascita processi in esecuzione nel cluster di HDInsight con hello dell'interfaccia utente YARN, interfaccia utente di Spark e hello Spark cronologia Server.</span><span class="sxs-lookup"><span data-stu-id="eacd0-104">In this article you will learn how tootrack and debug Spark jobs running on HDInsight clusters using hello YARN UI, Spark UI, and hello Spark History Server.</span></span> <span data-ttu-id="eacd0-105">Per questo articolo, si inizierà un processo di Spark utilizzando un notebook disponibile con i cluster di Spark hello, **Machine learning: analisi predittiva su dati di ispezione di cibo utilizzando MLLib**.</span><span class="sxs-lookup"><span data-stu-id="eacd0-105">For this article, we will start a Spark job using a notebook available with hello Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="eacd0-106">È possibile utilizzare passaggi hello di sotto di un'applicazione che è stato inviato utilizzando qualsiasi altro approccio, ad esempio, tootrack **spark-submit**.</span><span class="sxs-lookup"><span data-stu-id="eacd0-106">You can use hello steps below tootrack an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eacd0-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eacd0-107">Prerequisites</span></span>
<span data-ttu-id="eacd0-108">È necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="eacd0-108">You must have hello following:</span></span>

* <span data-ttu-id="eacd0-109">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eacd0-109">An Azure subscription.</span></span> <span data-ttu-id="eacd0-110">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="eacd0-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="eacd0-111">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eacd0-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="eacd0-112">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="eacd0-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="eacd0-113">È consigliabile esecuzione è stata avviata notebook hello, ** [Machine learning: analisi predittiva su dati di ispezione di cibo utilizzando MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="eacd0-113">You should have started running hello notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="eacd0-114">Per istruzioni su come toorun il blocco, seguire hello collegamento.</span><span class="sxs-lookup"><span data-stu-id="eacd0-114">For instructions on how toorun this notebook, follow hello link.</span></span>  

## <a name="track-an-application-in-hello-yarn-ui"></a><span data-ttu-id="eacd0-115">Tenere traccia di un'applicazione hello YARN UI</span><span class="sxs-lookup"><span data-stu-id="eacd0-115">Track an application in hello YARN UI</span></span>
1. <span data-ttu-id="eacd0-116">Avvio dell'interfaccia utente YARN hello.</span><span class="sxs-lookup"><span data-stu-id="eacd0-116">Launch hello YARN UI.</span></span> <span data-ttu-id="eacd0-117">Dal Pannello di hello cluster, fare clic su **Dashboard Cluster**, quindi fare clic su **YARN**.</span><span class="sxs-lookup"><span data-stu-id="eacd0-117">From hello cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Avviare l'interfaccia utente di YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="eacd0-119">In alternativa, è possibile avviare hello dell'interfaccia utente YARN da hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="eacd0-119">Alternatively, you can also launch hello YARN UI from hello Ambari UI.</span></span> <span data-ttu-id="eacd0-120">Fare clic su toolaunch hello Ambari UI, dal pannello cluster hello **Dashboard del Cluster**e quindi fare clic su **Dashboard del Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="eacd0-120">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="eacd0-121">Hello Ambari UI, fare clic su **YARN**, fare clic su **collegamenti rapidi**, fare clic su Gestione risorse attivo hello e quindi fare clic su **ResourceManager UI**.</span><span class="sxs-lookup"><span data-stu-id="eacd0-121">From hello Ambari UI, click **YARN**, click **Quick Links**, click hello active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="eacd0-122">Poiché è stato avviato il processo di Spark hello notebook Jupyter, un'applicazione hello ha nome hello **remotesparkmagics** (questo è il nome di hello per tutte le applicazioni che vengono avviati da notebook hello).</span><span class="sxs-lookup"><span data-stu-id="eacd0-122">Because you started hello Spark job using Jupyter notebooks, hello application has hello name **remotesparkmagics** (this is hello name for all applications that are started from hello notebooks).</span></span> <span data-ttu-id="eacd0-123">Fare clic su ID applicazione hello contro hello applicazione nome tooget ulteriori informazioni sul processo hello.</span><span class="sxs-lookup"><span data-stu-id="eacd0-123">Click hello application ID against hello application name tooget more information about hello job.</span></span> <span data-ttu-id="eacd0-124">Verrà avviata la visualizzazione di applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="eacd0-124">This launches hello application view.</span></span>
   
    ![Trovare un ID applicazione di Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="eacd0-126">Per le applicazioni avviate dal notebook Jupyter hello, è sempre stato hello **esecuzione** fino a quando non si esce da notebook hello.</span><span class="sxs-lookup"><span data-stu-id="eacd0-126">For such applications that are launched from hello Jupyter notebooks, hello status is always **RUNNING** until you exit hello notebook.</span></span>
3. <span data-ttu-id="eacd0-127">Dalla visualizzazione applicazione hello, è possibile visualizzare ulteriormente toofind i contenitori di hello associata a un'applicazione hello e registri di hello (stdout/stderr).</span><span class="sxs-lookup"><span data-stu-id="eacd0-127">From hello application view, you can drill down further toofind out hello containers associated with hello application and hello logs (stdout/stderr).</span></span> <span data-ttu-id="eacd0-128">È anche possibile avviare l'interfaccia utente di Spark hello facendo clic sul collegamento corrispondente toohello hello **rilevamento URL**, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="eacd0-128">You can also launch hello Spark UI by clicking hello linking corresponding toohello **Tracking URL**, as shown below.</span></span> 
   
    ![Scaricare i log del contenitore](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a><span data-ttu-id="eacd0-130">Tenere traccia di un'applicazione hello Spark UI</span><span class="sxs-lookup"><span data-stu-id="eacd0-130">Track an application in hello Spark UI</span></span>
<span data-ttu-id="eacd0-131">Nell'interfaccia utente di Spark hello, è possibile scorrere verso il basso processi Spark hello generati dall'applicazione hello che è stato avviato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="eacd0-131">In hello Spark UI, you can drill down into hello Spark jobs that are spawned by hello application you started earlier.</span></span>

1. <span data-ttu-id="eacd0-132">toolaunch hello Spark UI, dalla visualizzazione applicazione hello, fare clic su collegamento hello contro hello **rilevamento URL**, come illustrato nella cattura di schermata hello precedente.</span><span class="sxs-lookup"><span data-stu-id="eacd0-132">toolaunch hello Spark UI, from hello application view, click hello link against hello **Tracking URL**, as shown in hello screen capture above.</span></span> <span data-ttu-id="eacd0-133">È possibile visualizzare tutti i processi di Spark hello avviati da un'applicazione hello in esecuzione in server Jupyter notebook di hello.</span><span class="sxs-lookup"><span data-stu-id="eacd0-133">You can see all hello Spark jobs that are launched by hello application running in hello Jupyter notebook.</span></span>
   
    ![Visualizzare processi Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="eacd0-135">Fare clic su hello **executor** toosee informazioni di elaborazione e archiviazione per ogni esecutore della scheda.</span><span class="sxs-lookup"><span data-stu-id="eacd0-135">Click hello **Executors** tab toosee processing and storage information for each executor.</span></span> <span data-ttu-id="eacd0-136">È inoltre possibile recuperare nello stack di chiamate hello facendo clic su hello **Thread Dump** collegamento.</span><span class="sxs-lookup"><span data-stu-id="eacd0-136">You can also retrieve hello call stack by clicking on hello **Thread Dump** link.</span></span>
   
    ![Visualizzare gli executor Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="eacd0-138">Fare clic su hello **fasi** scheda fasi hello toosee associate a un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="eacd0-138">Click hello **Stages** tab toosee hello stages associated with hello application.</span></span>
   
    ![Visualizzare le fasi di Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="eacd0-140">Ogni fase può avere più attività per cui è possibile visualizzare le statistiche di esecuzione, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="eacd0-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Visualizzare le fasi di Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="eacd0-142">Dalla pagina dei dettagli di hello fase, è possibile avviare visualizzazione DAG.</span><span class="sxs-lookup"><span data-stu-id="eacd0-142">From hello stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="eacd0-143">Espandere hello **visualizzazione DAG** collegamento nella parte superiore di hello della pagina di hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="eacd0-143">Expand hello **DAG Visualization** link at hello top of hello page, as shown below.</span></span>
   
    ![Mostrare la visualizzazione DAG delle fasi di Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="eacd0-145">DAG o diretta Aclyic grafico rappresenta hello nelle diverse fasi applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="eacd0-145">DAG or Direct Aclyic Graph represents hello different stages in hello application.</span></span> <span data-ttu-id="eacd0-146">Ogni casella blu nel grafico hello rappresenta un'operazione di Spark richiamata da un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="eacd0-146">Each blue box in hello graph represents a Spark operation invoked from hello application.</span></span>
5. <span data-ttu-id="eacd0-147">Dalla pagina dei dettagli di hello fase, è possibile avviare visualizzazione della cronologia di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="eacd0-147">From hello stage details page, you can also launch hello application timeline view.</span></span> <span data-ttu-id="eacd0-148">Espandere hello **evento Timeline** collegamento nella parte superiore di hello della pagina di hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="eacd0-148">Expand hello **Event Timeline** link at hello top of hello page, as shown below.</span></span>
   
    ![Visualizzare e la sequenza temporale di eventi delle fasi di Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="eacd0-150">Consente di visualizzare gli eventi di Spark hello forma hello di una sequenza temporale.</span><span class="sxs-lookup"><span data-stu-id="eacd0-150">This displays hello Spark events in hello form of a timeline.</span></span> <span data-ttu-id="eacd0-151">visualizzazione cronologia Hello è disponibile a tre livelli, tra i processi, all'interno di un processo e all'interno di una fase.</span><span class="sxs-lookup"><span data-stu-id="eacd0-151">hello timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="eacd0-152">immagine di Hello precedente acquisisce visualizzazione cronologia hello per una determinata fase.</span><span class="sxs-lookup"><span data-stu-id="eacd0-152">hello image above captures hello timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="eacd0-153">Se si seleziona hello **Abilita zoom** casella di controllo, è possibile scorrere a sinistra e destra in visualizzazione cronologia hello.</span><span class="sxs-lookup"><span data-stu-id="eacd0-153">If you select hello **Enable zooming** check box, you can scroll left and right across hello timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="eacd0-154">Altre schede nell'interfaccia utente di Spark hello forniscono informazioni utili sull'istanza di Spark hello anche.</span><span class="sxs-lookup"><span data-stu-id="eacd0-154">Other tabs in hello Spark UI provide useful information about hello Spark instance as well.</span></span>
   
   * <span data-ttu-id="eacd0-155">Scheda archiviazione - se l'applicazione crea un RDDs, è possibile trovare informazioni su quelli nella scheda archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="eacd0-155">Storage tab - If your application creates an RDDs, you can find information about those in hello Storage tab.</span></span>
   * <span data-ttu-id="eacd0-156">Scheda ambiente - questa scheda vengono fornite numerose informazioni utili sull'istanza, ad esempio hello Spark</span><span class="sxs-lookup"><span data-stu-id="eacd0-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as hello</span></span> 
     * <span data-ttu-id="eacd0-157">Versione di Scala</span><span class="sxs-lookup"><span data-stu-id="eacd0-157">Scala version</span></span>
     * <span data-ttu-id="eacd0-158">Directory log di eventi associato hello cluster</span><span class="sxs-lookup"><span data-stu-id="eacd0-158">Event log directory associated with hello cluster</span></span>
     * <span data-ttu-id="eacd0-159">Numero di core esecutore per un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="eacd0-159">Number of executor cores for hello application</span></span>
     * <span data-ttu-id="eacd0-160">e così via.</span><span class="sxs-lookup"><span data-stu-id="eacd0-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a><span data-ttu-id="eacd0-161">Trovare informazioni sui processi completati utilizzando hello Spark cronologia Server</span><span class="sxs-lookup"><span data-stu-id="eacd0-161">Find information about completed jobs using hello Spark History Server</span></span>
<span data-ttu-id="eacd0-162">Al termine di un processo, informazioni di hello processo hello sono persistente nel hello Spark cronologia Server.</span><span class="sxs-lookup"><span data-stu-id="eacd0-162">Once a job is completed, hello information about hello job is persisted in hello Spark History Server.</span></span>

1. <span data-ttu-id="eacd0-163">Fare clic su toolaunch hello Spark cronologia Server, dal Pannello di cluster hello, **Dashboard del Cluster**, quindi fare clic su **Spark cronologia Server**.</span><span class="sxs-lookup"><span data-stu-id="eacd0-163">toolaunch hello Spark History Server, from hello cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Avviare Server cronologia Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="eacd0-165">In alternativa, è anche possibile avviare hello interfaccia utente del Server Spark cronologia da hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="eacd0-165">Alternatively, you can also launch hello Spark History Server UI from hello Ambari UI.</span></span> <span data-ttu-id="eacd0-166">Fare clic su toolaunch hello Ambari UI, dal pannello cluster hello **Dashboard del Cluster**e quindi fare clic su **Dashboard del Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="eacd0-166">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="eacd0-167">Hello Ambari UI, fare clic su **Spark**, fare clic su **collegamenti rapidi**, quindi fare clic su **interfaccia utente del Server Spark cronologia**.</span><span class="sxs-lookup"><span data-stu-id="eacd0-167">From hello Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="eacd0-168">Si noterà che tutte le applicazioni elencate hello completata.</span><span class="sxs-lookup"><span data-stu-id="eacd0-168">You will see all hello completed applications listed.</span></span> <span data-ttu-id="eacd0-169">Fare clic su un toodrill ID applicazione verso il basso in un'applicazione per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="eacd0-169">Click an application ID toodrill down into an application for more info.</span></span>
   
    ![Avviare Server cronologia Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="eacd0-171">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="eacd0-171">See also</span></span>
*  [<span data-ttu-id="eacd0-172">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="eacd0-172">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="eacd0-173">Per gli analisti dei dati</span><span class="sxs-lookup"><span data-stu-id="eacd0-173">For data analysts</span></span>

* [<span data-ttu-id="eacd0-174">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="eacd0-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="eacd0-175">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="eacd0-175">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="eacd0-176">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="eacd0-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="eacd0-177">Application Insight telemetry data analysis using Spark in HDInsight (Analisi dei dati di telemetria di Application Insights con Spark in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="eacd0-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="eacd0-178">Usare Caffe in Azure HDInsight Spark per l'apprendimento avanzato distribuito</span><span class="sxs-lookup"><span data-stu-id="eacd0-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="eacd0-179">Per gli sviluppatori di Spark</span><span class="sxs-lookup"><span data-stu-id="eacd0-179">For Spark developers</span></span>

* [<span data-ttu-id="eacd0-180">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="eacd0-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="eacd0-181">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="eacd0-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="eacd0-182">Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="eacd0-182">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="eacd0-183">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="eacd0-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="eacd0-184">Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota</span><span class="sxs-lookup"><span data-stu-id="eacd0-184">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="eacd0-185">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="eacd0-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="eacd0-186">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="eacd0-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="eacd0-187">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="eacd0-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="eacd0-188">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="eacd0-188">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


