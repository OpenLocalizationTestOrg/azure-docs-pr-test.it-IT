---
title: aaaRun query interattive in un cluster Azure HDInsight Spark | Documenti Microsoft
description: "Guida introduttiva di HDInsight Spark in modalità di cluster toocreate un Apache Spark in HDInsight."
keywords: guida introduttiva spark,spark interattivo,query interattiva,hdinsight spark,azure spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="151e4-104">Eseguire query interattive in un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="151e4-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="151e4-105">In questo articolo, si utilizza un server Jupyter notebook toorun interattivo Spark query SQL su un cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="151e4-105">In this article, you use a Jupyter notebook toorun interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="151e4-106">Server Jupyter notebook è un'applicazione basata su browser che estende hello esperienza interattiva basata su console toohello Web.</span><span class="sxs-lookup"><span data-stu-id="151e4-106">Jupyter notebook is a browser-based application that extends hello console-based interactive experience toohello Web.</span></span> <span data-ttu-id="151e4-107">Per ulteriori informazioni, vedere [notebook Jupyter hello](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span><span class="sxs-lookup"><span data-stu-id="151e4-107">For more information, see [hello Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="151e4-108">Per questa esercitazione, si userà hello **PySpark** kernel in hello Jupyter notebook toorun una query SQL Spark interattiva.</span><span class="sxs-lookup"><span data-stu-id="151e4-108">For this tutorial, you use hello **PySpark** kernel in hello Jupyter notebook toorun an interactive Spark SQL query.</span></span> <span data-ttu-id="151e4-109">I notebook di Jupyter nei cluster HDInsight supportano anche due altri kernel: **PySpark3** e **Spark**.</span><span class="sxs-lookup"><span data-stu-id="151e4-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="151e4-110">Per ulteriori informazioni su kernel hello e hello vantaggi derivanti dall'utilizzo **PySpark**, vedere [cluster kernel notebook Jupyter utilizzo con Apache Spark in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="151e4-110">For more information about hello kernels, and hello benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="151e4-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="151e4-111">Prerequisites</span></span>

* <span data-ttu-id="151e4-112">**Cluster Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="151e4-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="151e4-113">Per istruzioni, vedere [Creare un cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="151e4-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a><span data-ttu-id="151e4-114">Creare un server Jupyter notebook query interattive toorun</span><span class="sxs-lookup"><span data-stu-id="151e4-114">Create a Jupyter notebook toorun interactive queries</span></span>

<span data-ttu-id="151e4-115">query toorun, utilizziamo i dati di esempio che per impostazione predefinita nel servizio di archiviazione hello associato hello cluster disponibile.</span><span class="sxs-lookup"><span data-stu-id="151e4-115">toorun queries, we use sample data that is by default available in hello storage associated with hello cluster.</span></span> <span data-ttu-id="151e4-116">È necessario, tuttavia, caricare prima i dati in Spark come un dataframe.</span><span class="sxs-lookup"><span data-stu-id="151e4-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="151e4-117">Dopo aver creato hello frame di dati, è possibile eseguire query su di esso utilizzando notebook Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="151e4-117">Once you have hello dataframe, you can run queries on it using hello Jupyter notebook.</span></span> <span data-ttu-id="151e4-118">In questa sezione si analizzerà come:</span><span class="sxs-lookup"><span data-stu-id="151e4-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="151e4-119">Registrare un set di dati di esempio come un dataframe di Spark.</span><span class="sxs-lookup"><span data-stu-id="151e4-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="151e4-120">Eseguire query sul frame di dati hello.</span><span class="sxs-lookup"><span data-stu-id="151e4-120">Run queries on hello dataframe.</span></span>

1. <span data-ttu-id="151e4-121">Aprire hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="151e4-121">Open hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="151e4-122">Se si è scelto di dashboard di toohello toopin hello del cluster, fare clic su riquadro cluster hello dal Pannello di hello dashboard toolaunch hello cluster.</span><span class="sxs-lookup"><span data-stu-id="151e4-122">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="151e4-123">Se si non blocca hello cluster toohello dashboard nel riquadro di sinistra hello, fare clic su **cluster HDInsight**, quindi fare clic su cluster hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="151e4-123">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="151e4-124">In **Collegamenti rapidi** fare clic su **Dashboard cluster** e quindi su **Notebook di Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="151e4-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="151e4-125">Se richiesto, immettere le credenziali di amministratore hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="151e4-125">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="151e4-126">![Aprire Server Jupyter notebook toorun Spark SQL query interattivo](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "aprire Jupyter notebook toorun interattivo Spark nella query SQL")</span><span class="sxs-lookup"><span data-stu-id="151e4-126">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="151e4-127">È inoltre possibile accedere notebook Jupyter hello per il cluster usando hello apertura URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="151e4-127">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="151e4-128">Sostituire **CLUSTERNAME** con nome hello del cluster:</span><span class="sxs-lookup"><span data-stu-id="151e4-128">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="151e4-129">Creare un notebook.</span><span class="sxs-lookup"><span data-stu-id="151e4-129">Create a notebook.</span></span> <span data-ttu-id="151e4-130">Fare clic su **Nuovo** e quindi su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="151e4-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="151e4-131">![Creare una query di Spark SQL interattiva Jupyter notebook toorun](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "creare una query di Spark SQL interattiva Jupyter notebook toorun")</span><span class="sxs-lookup"><span data-stu-id="151e4-131">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="151e4-132">Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="151e4-132">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="151e4-133">Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo, se si desidera.</span><span class="sxs-lookup"><span data-stu-id="151e4-133">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="151e4-134">![Specificare un nome per hello Jupter notebook toorun Spark query interattivo da](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "specificare un nome per hello Jupter notebook toorun Spark query interattivo da")</span><span class="sxs-lookup"><span data-stu-id="151e4-134">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5. <span data-ttu-id="151e4-135">Esempio hello Incolla del codice in una cella vuota e quindi premere **MAIUSC + INVIO** codice hello toorun.</span><span class="sxs-lookup"><span data-stu-id="151e4-135">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="151e4-136">codice Hello Importa i tipi di hello richiesti per questo scenario:</span><span class="sxs-lookup"><span data-stu-id="151e4-136">hello code imports hello types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="151e4-137">Poiché è stato creato un notebook utilizza il kernel PySpark hello, non è necessario toocreate i contesti in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="151e4-137">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="151e4-138">contesti di Spark e Hive Hello vengono automaticamente creati automaticamente quando si esegue prima cella di codice hello.</span><span class="sxs-lookup"><span data-stu-id="151e4-138">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span>

    <span data-ttu-id="151e4-139">![Stato della query interattiva Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Stato della query interattiva Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="151e4-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="151e4-140">Ogni volta che si esegue una query interattiva in Jupyter, il titolo della finestra del browser web viene illustrato un **(occupata)** stato insieme a titolo di hello notebook.</span><span class="sxs-lookup"><span data-stu-id="151e4-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="151e4-141">Viene visualizzato anche un toohello Avanti cerchio pieno **PySpark** testo nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="151e4-141">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="151e4-142">Dopo aver completato il processo di hello, assume la forma cerchio tooa.</span><span class="sxs-lookup"><span data-stu-id="151e4-142">After hello job is completed, it changes tooa hollow circle.</span></span>

6. <span data-ttu-id="151e4-143">Prima di caricare i dati hello in un cluster Spark, vediamo uno snapshot dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="151e4-143">Before you load hello data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="151e4-144">Hello dati di esempio utilizzati in questa esercitazione sono disponibili come file CSV in tutti i cluster di HDInsight Spark **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="151e4-144">hello sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="151e4-145">dati Hello acquisisce le variazioni di temperatura hello di un edificio.</span><span class="sxs-lookup"><span data-stu-id="151e4-145">hello data captures hello temperature variations of a building.</span></span> <span data-ttu-id="151e4-146">Di seguito è hello prime righe di dati hello.</span><span class="sxs-lookup"><span data-stu-id="151e4-146">Here are hello first few rows of hello data.</span></span>

    <span data-ttu-id="151e4-147">![Snapshot di dati per query SQL Spark interattive](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot di dati per query SQL Spark interattive")</span><span class="sxs-lookup"><span data-stu-id="151e4-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="151e4-148">Creare un frame di dati e una tabella temporanea (**impianto**) eseguendo hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="151e4-148">Create a dataframe and a temporary table (**hvac**) by running hello following code.</span></span> <span data-ttu-id="151e4-149">Per questa esercitazione, è non creare tutte le colonne di hello in una tabella temporanea hello come colonne toohello confrontati in dati CSV non elaborati hello.</span><span class="sxs-lookup"><span data-stu-id="151e4-149">For this tutorial, we do not create all hello columns in hello temporary table as compared toohello columns in hello raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="151e4-150">Dopo aver creato una tabella di hello, eseguire query interattivo sui dati hello, utilizzare hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="151e4-150">Once hello table is created, run interactive query on hello data, use hello following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="151e4-151">Perché si sta usando un kernel PySpark, è ora possibile direttamente eseguire una query SQL interattiva per la tabella temporanea hello **impianto** creato utilizzando hello `%%sql` magic.</span><span class="sxs-lookup"><span data-stu-id="151e4-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on hello temporary table **hvac** that you created by using hello `%%sql` magic.</span></span> <span data-ttu-id="151e4-152">Per ulteriori informazioni su hello `%%sql` magic e altri magics disponibili con kernel PySpark hello, vedere [kernel disponibile sui server Jupyter notebook con i cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="151e4-152">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="151e4-153">Hello seguente tabulari output viene visualizzato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="151e4-153">hello following tabular output is displayed by default.</span></span>

     <span data-ttu-id="151e4-154">![Tabella di output dei risultati della query interattiva Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabella di output dei risultati della query interattiva Spark")</span><span class="sxs-lookup"><span data-stu-id="151e4-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="151e4-155">È inoltre possibile visualizzare i risultati hello in anche altre visualizzazioni.</span><span class="sxs-lookup"><span data-stu-id="151e4-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="151e4-156">Ad esempio, un grafico ad area per hello stesso output sarebbe simile al seguente hello.</span><span class="sxs-lookup"><span data-stu-id="151e4-156">For example, an area graph for hello same output would look like hello following.</span></span>

    <span data-ttu-id="151e4-157">![Grafico ad area dei risultati della query interattiva Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Grafico ad area dei risultati della query interattiva Spark")</span><span class="sxs-lookup"><span data-stu-id="151e4-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="151e4-158">Arresto delle risorse cluster di hello notebook toorelease hello al termine dell'esecuzione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="151e4-158">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="151e4-159">toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**.</span><span class="sxs-lookup"><span data-stu-id="151e4-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="151e4-160">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="151e4-160">Next step</span></span>

<span data-ttu-id="151e4-161">In questo articolo si è appreso toorun query interattive in Spark usando server Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="151e4-161">In this article you learned how toorun interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="151e4-162">In uno strumento analitica di Business Intelligence quali Power BI e Tableau di anticipo toohello Avanti articolo toosee come dati di hello che è registrato in Spark possono essere estratti.</span><span class="sxs-lookup"><span data-stu-id="151e4-162">Advance toohello next article toosee how hello data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="151e4-163">Spark BI usando gli strumenti di visualizzazione di dati con Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="151e4-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




