---
title: Eseguire query interattive in un cluster Azure HDInsight Spark | Microsoft Docs
description: Guida introduttiva di HDInsight Spark per la creazione di un cluster Apache Spark in HDInsight.
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
ms.openlocfilehash: ada1c3d1482c68834dbbf5eabbd045a7e0c01f9f
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="50689-104">Eseguire query interattive in un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="50689-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="50689-105">In questo articolo si userà un notebook di Jupyter per eseguire query SQL Spark interattive su un cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="50689-105">In this article, you use a Jupyter notebook to run interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="50689-106">Il notebook di Jupyter è un'applicazione basata su browser che consente di estendere al Web l'esperienza interattiva basata su console.</span><span class="sxs-lookup"><span data-stu-id="50689-106">Jupyter notebook is a browser-based application that extends the console-based interactive experience to the Web.</span></span> <span data-ttu-id="50689-107">Per altre informazioni, vedere [The Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html) (Il notebook di Jupyter).</span><span class="sxs-lookup"><span data-stu-id="50689-107">For more information, see [The Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="50689-108">In questa esercitazione si userà il kernel **PySpark** nel notebook di Jupyter per eseguire una query SQL Spark interattiva.</span><span class="sxs-lookup"><span data-stu-id="50689-108">For this tutorial, you use the **PySpark** kernel in the Jupyter notebook to run an interactive Spark SQL query.</span></span> <span data-ttu-id="50689-109">I notebook di Jupyter nei cluster HDInsight supportano anche due altri kernel: **PySpark3** e **Spark**.</span><span class="sxs-lookup"><span data-stu-id="50689-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="50689-110">Per altre informazioni sui kernel e i vantaggi offerti dall'uso di **PySpark**, vedere [Usare i kernel per Jupyter Notebook con cluster Apache Spark in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="50689-110">For more information about the kernels, and the benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50689-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="50689-111">Prerequisites</span></span>

* <span data-ttu-id="50689-112">**Cluster Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="50689-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="50689-113">Per istruzioni, vedere [Creare un cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="50689-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-to-run-interactive-queries"></a><span data-ttu-id="50689-114">Creare un notebook di Jupyter per eseguire query interattive</span><span class="sxs-lookup"><span data-stu-id="50689-114">Create a Jupyter notebook to run interactive queries</span></span>

<span data-ttu-id="50689-115">Per eseguire le query si useranno i dati di esempio disponibili per impostazione predefinita nella risorsa di archiviazione associata al cluster.</span><span class="sxs-lookup"><span data-stu-id="50689-115">To run queries, we use sample data that is by default available in the storage associated with the cluster.</span></span> <span data-ttu-id="50689-116">È necessario, tuttavia, caricare prima i dati in Spark come un dataframe.</span><span class="sxs-lookup"><span data-stu-id="50689-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="50689-117">Solo a questo punto sarà possibile eseguire query sul dataframe usando il notebook di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="50689-117">Once you have the dataframe, you can run queries on it using the Jupyter notebook.</span></span> <span data-ttu-id="50689-118">In questa sezione si analizzerà come:</span><span class="sxs-lookup"><span data-stu-id="50689-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="50689-119">Registrare un set di dati di esempio come un dataframe di Spark.</span><span class="sxs-lookup"><span data-stu-id="50689-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="50689-120">Eseguire query sul dataframe.</span><span class="sxs-lookup"><span data-stu-id="50689-120">Run queries on the dataframe.</span></span>

1. <span data-ttu-id="50689-121">Aprire il [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="50689-121">Open the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="50689-122">Se si è scelto di aggiungere il cluster al dashboard, fare clic sul riquadro del cluster nel dashboard per avviare il relativo pannello.</span><span class="sxs-lookup"><span data-stu-id="50689-122">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="50689-123">Se il cluster non è stato aggiunto al dashboard, nel riquadro sinistro fare clic su **Cluster HDInsight** e quindi sul cluster creato.</span><span class="sxs-lookup"><span data-stu-id="50689-123">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="50689-124">In **Collegamenti rapidi** fare clic su **Dashboard cluster** e quindi su **Notebook di Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="50689-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="50689-125">Se richiesto, immettere le credenziali per il cluster.</span><span class="sxs-lookup"><span data-stu-id="50689-125">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="50689-126">![Aprire Jupyter Notebook per eseguire la query interattiva Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Aprire Jupyter Notebook per eseguire la query interattiva Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="50689-126">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="50689-127">È anche possibile accedere all'istanza di Jupyter Notebook per il cluster aprendo l'URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="50689-127">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="50689-128">Sostituire **CLUSTERNAME** con il nome del cluster:</span><span class="sxs-lookup"><span data-stu-id="50689-128">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="50689-129">Creare un notebook.</span><span class="sxs-lookup"><span data-stu-id="50689-129">Create a notebook.</span></span> <span data-ttu-id="50689-130">Fare clic su **Nuovo** e quindi su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="50689-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="50689-131">![Creare un'istanza di Jupyter Notebook per eseguire la query interattiva Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Creare un'istanza di Jupyter Notebook per eseguire la query interattiva Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="50689-131">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="50689-132">Un nuovo notebook verrà creato e aperto con il nome Untitled (Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="50689-132">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="50689-133">Fare clic sul nome del notebook nella parte superiore e, se si vuole, immettere un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="50689-133">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="50689-134">![Specificare un nome per l'istanza di Jupyter Notebook dalla quale eseguire la query interattiva Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Specificare un nome per l'istanza di Jupyter Notebook dalla quale eseguire la query interattiva Spark")</span><span class="sxs-lookup"><span data-stu-id="50689-134">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5. <span data-ttu-id="50689-135">Incollare il codice seguente in una cella vuota e quindi premere **MAIUSC + INVIO** per eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="50689-135">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="50689-136">Il codice importa i tipi necessari per questo scenario:</span><span class="sxs-lookup"><span data-stu-id="50689-136">The code imports the types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="50689-137">Poiché il notebook è stato creato tramite il kernel PySpark, non è necessario creare contesti in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="50689-137">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="50689-138">I contesti Spark e Hive vengono creati automaticamente quando si esegue la prima cella di codice.</span><span class="sxs-lookup"><span data-stu-id="50689-138">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span>

    <span data-ttu-id="50689-139">![Stato della query interattiva Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Stato della query interattiva Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="50689-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="50689-140">Ogni volta che si esegue una query interattiva in Jupyter, il titolo della finestra del Web browser visualizza lo stato **(Occupato)** accanto al titolo del notebook.</span><span class="sxs-lookup"><span data-stu-id="50689-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="50689-141">È anche visibile un cerchio pieno accanto al testo **PySpark** nell'angolo in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="50689-141">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="50689-142">Al termine del processo viene visualizzato un cerchio vuoto.</span><span class="sxs-lookup"><span data-stu-id="50689-142">After the job is completed, it changes to a hollow circle.</span></span>

6. <span data-ttu-id="50689-143">Prima di caricare i dati in un cluster Spark, è possibile visualizzarne di seguito uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="50689-143">Before you load the data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="50689-144">I dati di esempio usati in questa esercitazione sono disponibili come file CSV in tutti i cluster HDInsight Spark all'indirizzo **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="50689-144">The sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="50689-145">I dati acquisiscono le variazioni di temperatura di un edificio.</span><span class="sxs-lookup"><span data-stu-id="50689-145">The data captures the temperature variations of a building.</span></span> <span data-ttu-id="50689-146">Di seguito sono riportate le prime righe di dati.</span><span class="sxs-lookup"><span data-stu-id="50689-146">Here are the first few rows of the data.</span></span>

    <span data-ttu-id="50689-147">![Snapshot di dati per query SQL Spark interattive](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot di dati per query SQL Spark interattive")</span><span class="sxs-lookup"><span data-stu-id="50689-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="50689-148">Creare un dataframe e una tabella temporanea (**hvac**) eseguendo il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="50689-148">Create a dataframe and a temporary table (**hvac**) by running the following code.</span></span> <span data-ttu-id="50689-149">Ai fini di questa esercitazione, nella tabella temporanea verrà creato un numero inferiore di colonne rispetto alle colonne relative ai dati CSV non elaborati.</span><span class="sxs-lookup"><span data-stu-id="50689-149">For this tutorial, we do not create all the columns in the temporary table as compared to the columns in the raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse the data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer the schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="50689-150">Dopo aver creato la tabella, eseguire una query interattiva sui dati usando il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="50689-150">Once the table is created, run interactive query on the data, use the following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="50689-151">Dato che si usa un kernel PySpark, è ora possibile eseguire direttamente una query SQL interattiva sulla tabella temporanea **hvac** creata usando il comando Magic `%%sql`.</span><span class="sxs-lookup"><span data-stu-id="50689-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on the temporary table **hvac** that you created by using the `%%sql` magic.</span></span> <span data-ttu-id="50689-152">Per altre informazioni sul comando Magic `%%sql` e sugli altri comandi Magic disponibili con il kernel PySpark, vedere [Kernel disponibili per i notebook di Jupyter con cluster Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="50689-152">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="50689-153">L'output tabulare seguente viene visualizzato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="50689-153">The following tabular output is displayed by default.</span></span>

     <span data-ttu-id="50689-154">![Tabella di output dei risultati della query interattiva Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabella di output dei risultati della query interattiva Spark")</span><span class="sxs-lookup"><span data-stu-id="50689-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="50689-155">È anche possibile visualizzare i risultati in altri formati.</span><span class="sxs-lookup"><span data-stu-id="50689-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="50689-156">Ad esempio, un grafico ad area per lo stesso output apparirebbe come segue.</span><span class="sxs-lookup"><span data-stu-id="50689-156">For example, an area graph for the same output would look like the following.</span></span>

    <span data-ttu-id="50689-157">![Grafico ad area dei risultati della query interattiva Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Grafico ad area dei risultati della query interattiva Spark")</span><span class="sxs-lookup"><span data-stu-id="50689-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="50689-158">Al termine dell'esecuzione dell'applicazione, arrestare il notebook per rilasciare le risorse del cluster.</span><span class="sxs-lookup"><span data-stu-id="50689-158">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="50689-159">A tale scopo, dal menu **File** del notebook fare clic su **Close and Halt** (Chiudi e interrompi).</span><span class="sxs-lookup"><span data-stu-id="50689-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="50689-160">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="50689-160">Next step</span></span>

<span data-ttu-id="50689-161">In questo articolo è stata illustrata la procedura per eseguire query interattive in Spark usando il notebook di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="50689-161">In this article you learned how to run interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="50689-162">Passare all’articolo successivo per scoprire come eseguire lo spostamento forzato dei dati registrati in Spark in uno strumento di analisi BI come Power BI o Tableau.</span><span class="sxs-lookup"><span data-stu-id="50689-162">Advance to the next article to see how the data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="50689-163">Spark BI usando gli strumenti di visualizzazione di dati con Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="50689-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




