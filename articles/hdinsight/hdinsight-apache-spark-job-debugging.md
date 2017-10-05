---
title: Eseguire il debug di processi Apache Spark in esecuzione in Azure HDInsight | Microsoft Docs
description: Usare l'interfaccia utente di YARN, l'interfaccia utente di Spark e il server della cronologia di Spark per tenere traccia ed eseguire il debug di processi in esecuzione in un cluster Spark in Azure HDInsight
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
ms.openlocfilehash: bf66757cc9439a969c9f28abc0b95055ff697c3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="b4d13-103">Eseguire il debug di processi Apache Spark in esecuzione in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4d13-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="b4d13-104">Questo articolo illustra come tenere traccia ed eseguire il debug di processi Spark in esecuzione nei cluster HDInsight tramite l'interfaccia utente di YARN, l'interfaccia utente di Spark e il server di cronologia Spark.</span><span class="sxs-lookup"><span data-stu-id="b4d13-104">In this article you will learn how to track and debug Spark jobs running on HDInsight clusters using the YARN UI, Spark UI, and the Spark History Server.</span></span> <span data-ttu-id="b4d13-105">Per questo articolo,si avvierà un processo Spark usando un notebook disponibile nel cluster Spark, **Machine Learning: analisi predittiva dei dati del controllo degli alimenti tramite MLlib**.</span><span class="sxs-lookup"><span data-stu-id="b4d13-105">For this article, we will start a Spark job using a notebook available with the Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="b4d13-106">È possibile usare la procedura seguente per tenere traccia di un'applicazione inviata usando anche qualsiasi altro approccio, ad esempio, **spark-submit**.</span><span class="sxs-lookup"><span data-stu-id="b4d13-106">You can use the steps below to track an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4d13-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b4d13-107">Prerequisites</span></span>
<span data-ttu-id="b4d13-108">È necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b4d13-108">You must have the following:</span></span>

* <span data-ttu-id="b4d13-109">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d13-109">An Azure subscription.</span></span> <span data-ttu-id="b4d13-110">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b4d13-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b4d13-111">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b4d13-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b4d13-112">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b4d13-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="b4d13-113">Si sarà già avviato il notebook **[Machine Learning: analisi predittiva dei dati del controllo degli alimenti tramite MLlib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="b4d13-113">You should have started running the notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="b4d13-114">Per istruzioni su come eseguire questo notebook, seguire il collegamento.</span><span class="sxs-lookup"><span data-stu-id="b4d13-114">For instructions on how to run this notebook, follow the link.</span></span>  

## <a name="track-an-application-in-the-yarn-ui"></a><span data-ttu-id="b4d13-115">Tenere traccia di un'applicazione nell'interfaccia utente di YARN</span><span class="sxs-lookup"><span data-stu-id="b4d13-115">Track an application in the YARN UI</span></span>
1. <span data-ttu-id="b4d13-116">Avviare l'interfaccia utente di YARN</span><span class="sxs-lookup"><span data-stu-id="b4d13-116">Launch the YARN UI.</span></span> <span data-ttu-id="b4d13-117">Nel pannello del cluster fare clic su **Dashboard cluster** e quindi su **YARN**.</span><span class="sxs-lookup"><span data-stu-id="b4d13-117">From the cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Avviare l'interfaccia utente di YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="b4d13-119">In alternativa, è anche possibile avviare l'interfaccia utente di YARN dall'interfaccia utente di Ambari.</span><span class="sxs-lookup"><span data-stu-id="b4d13-119">Alternatively, you can also launch the YARN UI from the Ambari UI.</span></span> <span data-ttu-id="b4d13-120">Per avviare l'interfaccia utente di Ambari, nel pannello del cluster fare clic su **Dashboard cluster** e quindi su **Dashboard cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b4d13-120">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="b4d13-121">Nell'interfaccia utente di Ambari fare clic su **YARN**, su **Collegamenti rapidi**, sulla funzionalità di gestione risorse attiva e quindi fare clic su **ResourceManager UI**.</span><span class="sxs-lookup"><span data-stu-id="b4d13-121">From the Ambari UI, click **YARN**, click **Quick Links**, click the active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="b4d13-122">Poiché il processo Spark è stato avviato con Jupyter Notebook, il nome dell'applicazione è **remotesparkmagics**. Si tratta del nome per tutte le applicazioni avviate dai notebook.</span><span class="sxs-lookup"><span data-stu-id="b4d13-122">Because you started the Spark job using Jupyter notebooks, the application has the name **remotesparkmagics** (this is the name for all applications that are started from the notebooks).</span></span> <span data-ttu-id="b4d13-123">Per ottenere altre informazioni sul processo, fare clic sull'ID dell'applicazione relativo al nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b4d13-123">Click the application ID against the application name to get more information about the job.</span></span> <span data-ttu-id="b4d13-124">Verrà avviata la visualizzazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b4d13-124">This launches the application view.</span></span>
   
    ![Trovare un ID applicazione di Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="b4d13-126">Per le applicazioni avviate da Jupyter Notebook lo stato è sempre **IN ESECUZIONE** fino a quando non si esce dal notebook.</span><span class="sxs-lookup"><span data-stu-id="b4d13-126">For such applications that are launched from the Jupyter notebooks, the status is always **RUNNING** until you exit the notebook.</span></span>
3. <span data-ttu-id="b4d13-127">Nella visualizzazione dell'applicazione è possibile eseguire il drill-down per trovare i contenitori associati all'applicazione e i log (stdout o stderr).</span><span class="sxs-lookup"><span data-stu-id="b4d13-127">From the application view, you can drill down further to find out the containers associated with the application and the logs (stdout/stderr).</span></span> <span data-ttu-id="b4d13-128">È anche possibile avviare l'interfaccia utente di Spark facendo clic sul collegamento corrispondente all' **URL di verifica**, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b4d13-128">You can also launch the Spark UI by clicking the linking corresponding to the **Tracking URL**, as shown below.</span></span> 
   
    ![Scaricare i log del contenitore](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a><span data-ttu-id="b4d13-130">Tenere traccia di un'applicazione nell'interfaccia utente di Spark</span><span class="sxs-lookup"><span data-stu-id="b4d13-130">Track an application in the Spark UI</span></span>
<span data-ttu-id="b4d13-131">Nell'interfaccia utente di Spark è possibile eseguire il drill-down dei processi Spark generati dall'applicazione avviata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b4d13-131">In the Spark UI, you can drill down into the Spark jobs that are spawned by the application you started earlier.</span></span>

1. <span data-ttu-id="b4d13-132">Per avviare l'interfaccia utente di Spark, nella visualizzazione dell'applicazione, fare clic sul collegamento relativo a **URL di verifica**, come illustrato nella schermata precedente.</span><span class="sxs-lookup"><span data-stu-id="b4d13-132">To launch the Spark UI, from the application view, click the link against the **Tracking URL**, as shown in the screen capture above.</span></span> <span data-ttu-id="b4d13-133">È possibile visualizzare tutti i processi Spark avviati dall'applicazione in esecuzione in Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="b4d13-133">You can see all the Spark jobs that are launched by the application running in the Jupyter notebook.</span></span>
   
    ![Visualizzare processi Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="b4d13-135">Fare clic sulla scheda **Executors** per visualizzare le informazioni di elaborazione e archiviazione per ogni executor.</span><span class="sxs-lookup"><span data-stu-id="b4d13-135">Click the **Executors** tab to see processing and storage information for each executor.</span></span> <span data-ttu-id="b4d13-136">È anche possibile recuperare lo stack di chiamate facendo clic sul collegamento **Thread Dump** .</span><span class="sxs-lookup"><span data-stu-id="b4d13-136">You can also retrieve the call stack by clicking on the **Thread Dump** link.</span></span>
   
    ![Visualizzare gli executor Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="b4d13-138">Fare clic sulla scheda **Stages** per visualizzare le fasi associate all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b4d13-138">Click the **Stages** tab to see the stages associated with the application.</span></span>
   
    ![Visualizzare le fasi di Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="b4d13-140">Ogni fase può avere più attività per cui è possibile visualizzare le statistiche di esecuzione, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b4d13-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Visualizzare le fasi di Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="b4d13-142">Nella pagina dei dettagli relativi alle fasi è possibile avviare la visualizzazione DAG.</span><span class="sxs-lookup"><span data-stu-id="b4d13-142">From the stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="b4d13-143">Espandere il collegamento **DAG Visualization** nella parte superiore della pagina, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b4d13-143">Expand the **DAG Visualization** link at the top of the page, as shown below.</span></span>
   
    ![Mostrare la visualizzazione DAG delle fasi di Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="b4d13-145">DAG o Direct Aclyic Graph rappresenta le diverse fasi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b4d13-145">DAG or Direct Aclyic Graph represents the different stages in the application.</span></span> <span data-ttu-id="b4d13-146">Ogni casella blu nel grafico rappresenta un'operazione Spark richiamata dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b4d13-146">Each blue box in the graph represents a Spark operation invoked from the application.</span></span>
5. <span data-ttu-id="b4d13-147">Nella pagina dei dettagli relativi alle fasi è anche possibile avviare la visualizzazione della sequenza temporale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b4d13-147">From the stage details page, you can also launch the application timeline view.</span></span> <span data-ttu-id="b4d13-148">Espandere il collegamento **Event Timeline** nella parte superiore della pagina, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b4d13-148">Expand the **Event Timeline** link at the top of the page, as shown below.</span></span>
   
    ![Visualizzare e la sequenza temporale di eventi delle fasi di Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="b4d13-150">Verranno visualizzati gli eventi di Spark sotto forma di sequenza temporale.</span><span class="sxs-lookup"><span data-stu-id="b4d13-150">This displays the Spark events in the form of a timeline.</span></span> <span data-ttu-id="b4d13-151">La visualizzazione della sequenza temporale è disponibile in tre livelli, tra processi, all'interno di un processo e all'interno di una fase.</span><span class="sxs-lookup"><span data-stu-id="b4d13-151">The timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="b4d13-152">L'immagine precedente mostra la visualizzazione della sequenza temporale per una determinata fase.</span><span class="sxs-lookup"><span data-stu-id="b4d13-152">The image above captures the timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b4d13-153">Se si seleziona la casella di controllo **Enable zooming** , è possibile scorrere a sinistra e destra nella visualizzazione della sequenza temporale.</span><span class="sxs-lookup"><span data-stu-id="b4d13-153">If you select the **Enable zooming** check box, you can scroll left and right across the timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="b4d13-154">Altre schede nell'interfaccia utente di Spark forniscono anche informazioni utili sull'istanza di Spark.</span><span class="sxs-lookup"><span data-stu-id="b4d13-154">Other tabs in the Spark UI provide useful information about the Spark instance as well.</span></span>
   
   * <span data-ttu-id="b4d13-155">Scheda Storage: se l'applicazione crea oggetti RDD, è possibile trovare informazioni corrispondenti in questa scheda.</span><span class="sxs-lookup"><span data-stu-id="b4d13-155">Storage tab - If your application creates an RDDs, you can find information about those in the Storage tab.</span></span>
   * <span data-ttu-id="b4d13-156">Scheda Environment: questa scheda fornisce molte informazioni utili sull'istanza di Spark, ad esempio</span><span class="sxs-lookup"><span data-stu-id="b4d13-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as the</span></span> 
     * <span data-ttu-id="b4d13-157">Versione di Scala</span><span class="sxs-lookup"><span data-stu-id="b4d13-157">Scala version</span></span>
     * <span data-ttu-id="b4d13-158">Directory dei log eventi associata al cluster</span><span class="sxs-lookup"><span data-stu-id="b4d13-158">Event log directory associated with the cluster</span></span>
     * <span data-ttu-id="b4d13-159">Numero di core executor per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="b4d13-159">Number of executor cores for the application</span></span>
     * <span data-ttu-id="b4d13-160">e così via.</span><span class="sxs-lookup"><span data-stu-id="b4d13-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a><span data-ttu-id="b4d13-161">Trovare informazioni sui processi completati tramite Server cronologia Spark</span><span class="sxs-lookup"><span data-stu-id="b4d13-161">Find information about completed jobs using the Spark History Server</span></span>
<span data-ttu-id="b4d13-162">Una volta completato un processo, le informazioni corrispondenti vengono salvate in modo permanente nel Server cronologia Spark.</span><span class="sxs-lookup"><span data-stu-id="b4d13-162">Once a job is completed, the information about the job is persisted in the Spark History Server.</span></span>

1. <span data-ttu-id="b4d13-163">Per avviare il Server cronologia Spark, nel pannello del cluster fare clic su **Dashboard cluster** e quindi su **Server cronologia Spark**.</span><span class="sxs-lookup"><span data-stu-id="b4d13-163">To launch the Spark History Server, from the cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Avviare Server cronologia Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="b4d13-165">In alternativa, è anche possibile avviare l'interfaccia utente del Server cronologia Spark dall'interfaccia utente di Ambari.</span><span class="sxs-lookup"><span data-stu-id="b4d13-165">Alternatively, you can also launch the Spark History Server UI from the Ambari UI.</span></span> <span data-ttu-id="b4d13-166">Per avviare l'interfaccia utente di Ambari, nel pannello del cluster fare clic su **Dashboard cluster** e quindi su **Dashboard cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b4d13-166">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="b4d13-167">Nell'interfaccia utente di Ambari fare clic su **Spark**, fare clic su **Collegamenti rapidi** e quindi sull'interfaccia utente di **Server cronologia Spark**.</span><span class="sxs-lookup"><span data-stu-id="b4d13-167">From the Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="b4d13-168">Saranno elencate tutte le applicazioni completate.</span><span class="sxs-lookup"><span data-stu-id="b4d13-168">You will see all the completed applications listed.</span></span> <span data-ttu-id="b4d13-169">Fare clic su un ID applicazione per eseguire il drill-down di un'applicazione per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="b4d13-169">Click an application ID to drill down into an application for more info.</span></span>
   
    ![Avviare Server cronologia Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="b4d13-171">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b4d13-171">See also</span></span>
*  [<span data-ttu-id="b4d13-172">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4d13-172">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="b4d13-173">Per gli analisti dei dati</span><span class="sxs-lookup"><span data-stu-id="b4d13-173">For data analysts</span></span>

* [<span data-ttu-id="b4d13-174">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="b4d13-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b4d13-175">Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="b4d13-175">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b4d13-176">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4d13-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="b4d13-177">Application Insight telemetry data analysis using Spark in HDInsight (Analisi dei dati di telemetria di Application Insights con Spark in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b4d13-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="b4d13-178">Usare Caffe in Azure HDInsight Spark per l'apprendimento avanzato distribuito</span><span class="sxs-lookup"><span data-stu-id="b4d13-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="b4d13-179">Per gli sviluppatori di Spark</span><span class="sxs-lookup"><span data-stu-id="b4d13-179">For Spark developers</span></span>

* [<span data-ttu-id="b4d13-180">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="b4d13-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b4d13-181">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="b4d13-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="b4d13-182">Usare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark in Scala</span><span class="sxs-lookup"><span data-stu-id="b4d13-182">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b4d13-183">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="b4d13-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b4d13-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Usare il plug-in Strumenti HDInsight per IntelliJ IDEA per eseguire il debug di applicazioni Spark in remoto)</span><span class="sxs-lookup"><span data-stu-id="b4d13-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b4d13-185">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4d13-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b4d13-186">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4d13-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b4d13-187">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="b4d13-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b4d13-188">Installare Jupyter Notebook nel computer e connetterlo a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b4d13-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


