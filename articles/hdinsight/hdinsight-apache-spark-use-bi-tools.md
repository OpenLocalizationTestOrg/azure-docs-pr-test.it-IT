---
title: Spark BI usando gli strumenti di visualizzazione di dati in Azure HDInsight | Microsoft Docs
description: Usare gli strumenti di visualizzazione di dati per l'analisi con Apache Spark BI nei cluster HDInsight
keywords: apache spark bi, spark bi, visualizzazione dei dati spark, spark business intelligence
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 49dd161049ac442081fe6d26cf8bd3a56a2e0687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a><span data-ttu-id="6cb0a-104">Apache Spark BI usando gli strumenti di visualizzazione di dati con Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6cb0a-104">Apache Spark BI using data visualization tools with Azure HDInsight</span></span>

<span data-ttu-id="6cb0a-105">Informazioni su come usare gli strumenti di visualizzazione dei dati, come Power BI e Tableau per analizzare un set di dati di esempio non elaborati usando Apache Spark BI nei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-105">Learn how to use data visualization tools such as Power BI and Tableau to analyze a raw sample data set using Apache Spark BI on HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="6cb0a-106">La connettività con gli strumenti di business intelligence descritta in questo articolo non è supportata su Spark 2.1 in Azure HDInsight 3.6 Preview.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="6cb0a-107">Solo le versioni 1.6 e 2.0 di Spark (HDInsight 3.4 e 3.5 rispettivamente) sono supportate.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="6cb0a-108">Questa esercitazione è disponibile anche come notebook di Jupyter in un cluster Spark HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-108">This tutorial is also available as a Jupyter notebook on an HDInsight Spark cluster.</span></span> <span data-ttu-id="6cb0a-109">L'esperienza offerta dal notebook consente di eseguire i frammenti di codice Python dal notebook stesso.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-109">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="6cb0a-110">Per eseguire l'esercitazione da un notebook, creare un cluster Spark, avviare un notebook di Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`) e quindi eseguire il notebook **Use BI tools with Apache Spark on HDInsight.ipynb** nella cartella **Python**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-110">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under the **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cb0a-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6cb0a-111">Prerequisites</span></span>

* <span data-ttu-id="6cb0a-112">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="6cb0a-113">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="6cb0a-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <span data-ttu-id="6cb0a-114"><a name="hivetable"></a>Preparare i dati per la visualizzazione dei dati di Spark</span><span class="sxs-lookup"><span data-stu-id="6cb0a-114"><a name="hivetable"></a>Prepare data for Spark data visualization</span></span>

<span data-ttu-id="6cb0a-115">In questa sezione viene usato il notebook di [Jupyter](https://jupyter.org) da un cluster Spark in HDInsight per eseguire i processi che elaborano i dati di esempio non elaborati e li salvano come tabella.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-115">In this section, we use the [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster to run jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="6cb0a-116">I dati di esempio sono un file con estensione csv (hvac.csv) disponibile in tutti i cluster per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-116">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span> <span data-ttu-id="6cb0a-117">Dopo avere salvato i dati come tabella, nella sezione successiva vengono usati gli strumenti di business intelligence per connettersi alla tabella ed eseguire visualizzazioni di dati.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-117">Once your data is saved as a table, in the next section we use BI tools to connect to the table and perform data visualizations.</span></span>

> [!NOTE]
> <span data-ttu-id="6cb0a-118">Se si eseguono i passaggi descritti in questo articolo dopo aver completato le istruzioni in [Eseguire query interattive in un cluster HDInsight Spark](hdinsight-apache-spark-load-data-run-query.md), è possibile procedere al passaggio 8 riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-118">If you are performing the steps in this article after completing the instructions in [Run interactive queries on an HDInsight Spark cluster](hdinsight-apache-spark-load-data-run-query.md), you can skip to Step 8 below.</span></span>
>

1. <span data-ttu-id="6cb0a-119">Dalla Schermata iniziale del [portale di Azure](https://portal.azure.com/) fare clic sul riquadro del cluster Spark, se è stato aggiunto sulla Schermata iniziale.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="6cb0a-120">È anche possibile passare al cluster da **Esplora tutto** > **Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="6cb0a-121">Nel pannello del cluster Spark fare clic su **Dashboard cluster** e quindi su **Notebook di Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="6cb0a-122">Se richiesto, immettere le credenziali per il cluster.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6cb0a-123">È anche possibile raggiungere il notebook di Jupyter per il cluster aprendo l'URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="6cb0a-124">Sostituire **CLUSTERNAME** con il nome del cluster:</span><span class="sxs-lookup"><span data-stu-id="6cb0a-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="6cb0a-125">Creare un notebook.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-125">Create a notebook.</span></span> <span data-ttu-id="6cb0a-126">Fare clic su **Nuovo** e quindi su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="6cb0a-127">![Creare un notebook di Jupyter per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Creare un notebook di Jupyter per Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-127">![Create a Jupyter notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Create a Jupyter notebook for Apache Spark BI")</span></span>

4. <span data-ttu-id="6cb0a-128">Un nuovo notebook verrà creato e aperto con il nome Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="6cb0a-129">Fare clic sul nome del notebook nella parte superiore e immettere un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="6cb0a-130">![Specificare un nome per il notebook per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Specificare un nome per il notebook per Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-130">![Provide a name for the notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Provide a name for the notebook for Apache Spark BI")</span></span>

5. <span data-ttu-id="6cb0a-131">Poiché il notebook è stato creato tramite il kernel PySpark, non è necessario creare contesti in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="6cb0a-132">I contesti Spark e Hive vengono creati automaticamente quando si esegue la prima cella di codice.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-132">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="6cb0a-133">È possibile iniziare con l'importazione dei tipi necessari per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-133">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="6cb0a-134">A tale scopo, posizionare il cursore nella cella e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-134">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="6cb0a-135">Caricare i dati di esempio in una tabella temporanea.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-135">Load sample data into a temporary table.</span></span> <span data-ttu-id="6cb0a-136">Quando si crea un cluster Spark in HDInsight, il file di dati di esempio **hvac.csv** viene copiato nell'account di archiviazione associato in **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-136">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="6cb0a-137">In una cella vuota incollare il frammento di codice seguente e premere **MAIUSC+INVIO**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-137">In an empty cell, paste the following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="6cb0a-138">Questo frammento di codice consente di registrare i dati in una tabella denominata **hvac**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-138">This snippet registers the data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. <span data-ttu-id="6cb0a-139">Verificare che la tabella è stata creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-139">Verify that the table was successfully created.</span></span> <span data-ttu-id="6cb0a-140">È possibile usare il comando speciale `%%sql` per eseguire direttamente query Hive.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-140">You can use the `%%sql` magic to run Hive queries directly.</span></span> <span data-ttu-id="6cb0a-141">Per altre informazioni sul magic `%%sql` e sugli altri magic disponibili con il kernel PySpark, vedere [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="6cb0a-141">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="6cb0a-142">Viene visualizzato un output come il seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb0a-142">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="6cb0a-143">Solo le tabelle in cui il valore sotto la colonna **isTemporary** è false sono tabelle hive che vengono archiviate in metastore ed è possibile accedervi con strumenti di business intelligence.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-143">Only the tables that have false under the **isTemporary** column are hive tables that are stored in the metastore and can be accessed from the BI tools.</span></span> <span data-ttu-id="6cb0a-144">In questa esercitazione si esegue la connessione alla tabella **hvac** creata.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-144">In this tutorial, we connect to the **hvac** table we created.</span></span>

8. <span data-ttu-id="6cb0a-145">Verificare che la tabella contiene i dati desiderati.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-145">Verify that the table contains the intended data.</span></span> <span data-ttu-id="6cb0a-146">In una cella vuota del notebook copiare il frammento di codice seguente e premere **MAIUSC+INVIO**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-146">In an empty cell in the notebook, copy the following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="6cb0a-147">Arrestare il notebook per rilasciare le risorse.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-147">Shut down the notebook to release the resources.</span></span> <span data-ttu-id="6cb0a-148">A tale scopo, dal menu **File** del notebook fare clic su **Close and Halt** (Chiudi e interrompi).</span><span class="sxs-lookup"><span data-stu-id="6cb0a-148">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <span data-ttu-id="6cb0a-149"><a name="powerbi"></a>Usare Power BI per la visualizzazione dei dati di Spark</span><span class="sxs-lookup"><span data-stu-id="6cb0a-149"><a name="powerbi"></a>Use Power BI for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="6cb0a-150">Questa sezione è applicabile solo a Spark 1.6 in HDInsight 3.4 e Spark 2.0 in HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-150">This section is applicable only for Spark 1.6 on HDInsight 3.4 and Spark 2.0 on HDInsight 3.5.</span></span>
>
>

<span data-ttu-id="6cb0a-151">Dopo aver salvato i dati come una tabella, è possibile usare Power BI per connettersi ai dati e visualizzarli per creare rapporti, dashboard e così via.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-151">Once you have saved the data as a table, you can use Power BI to connect to the data and visualize it to create reports, dashboards, etc.</span></span>

1. <span data-ttu-id="6cb0a-152">Accertarsi di avere accesso a Power BI.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-152">Make sure you have access to Power BI.</span></span> <span data-ttu-id="6cb0a-153">È possibile ottenere una sottoscrizione di anteprima gratuita di Power BI da [http://www.powerbi.com/](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="6cb0a-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="6cb0a-154">Accedere a [Power BI](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="6cb0a-154">Sign in to [Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="6cb0a-155">Nella parte inferiore del riquadro di sinistra fare clic su **Recupera dati**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-155">From the bottom of the left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="6cb0a-156">Nella pagina **Recupera dati** sotto **Connettersi ai dati o importarli** per **Database** fare clic su **Recupera**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-156">On the **Get Data** page, under **Import or Connect to Data**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="6cb0a-157">![Ottenere i dati in Power BI per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Ottenere i dati in Power BI per Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-157">![Get data into Power BI for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI for Apache Spark BI")</span></span>

5. <span data-ttu-id="6cb0a-158">Nella schermata successiva fare clic su **Spark in Azure HDInsight** e quindi su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-158">On the next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="6cb0a-159">Quando richiesto, immettere l'URL del cluster (`mysparkcluster.azurehdinsight.net`) e le credenziali per connettersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-159">When prompted, enter the cluster URL (`mysparkcluster.azurehdinsight.net`) and the credentials to connect to the cluster.</span></span>

    <span data-ttu-id="6cb0a-160">![Connettersi ad Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connettersi ad Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-160">![Connect to Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connect to Apache Spark BI")</span></span>

    <span data-ttu-id="6cb0a-161">Dopo aver stabilito la connessione, Power BI avvia l'importazione di dati dal cluster Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-161">After the connection is established, Power BI starts importing data from the Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="6cb0a-162">Power BI importa i dati e aggiunge un set di dati **Spark** nell'intestazione **Set di dati**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-162">Power BI imports the data and adds a **Spark** dataset under the **Datasets** heading.</span></span> <span data-ttu-id="6cb0a-163">Fare clic sul set di dati per aprire un nuovo foglio di lavoro per la visualizzazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-163">Click the data set to open a new worksheet to visualize the data.</span></span> <span data-ttu-id="6cb0a-164">È inoltre possibile salvare il foglio di lavoro come report.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-164">You can also save the worksheet as a report.</span></span> <span data-ttu-id="6cb0a-165">A tale scopo, scegliere **Salva** dal menu **File**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-165">To save a worksheet, from the **File** menu, click **Save**.</span></span>

    <span data-ttu-id="6cb0a-166">![Riquadro di Apache Spark BI nel dashboard di Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Riquadro di Apache Spark BI nel dashboard di Power BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-166">![Apache Spark BI tile on Power BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="6cb0a-167">Si noti che nell'elenco **Campi** sulla destra è presente la tabella **hvac** creata prima.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-167">Notice that the **Fields** list on the right lists the **hvac** table you created earlier.</span></span> <span data-ttu-id="6cb0a-168">Espandere la tabella per visualizzare i campi della tabella, come definito in precedenza nel notebook.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-168">Expand the table to see the fields in the table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="6cb0a-169">![Elencare le tabelle nel dashboard di Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Elencare le tabelle nel dashboard di Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-169">![List tables on Apache Spark BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "List tables on Apache Spark BI dashboard")</span></span>

8. <span data-ttu-id="6cb0a-170">Creare una visualizzazione per mostrare la variazione tra temperatura di destinazione e temperatura effettiva per ogni edificio.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-170">Build a visualization to show the variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="6cb0a-171">Per visualizzare i dati, selezionare **Grafico ad aree** indicato in rosso.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-171">To visualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="6cb0a-172">Per definire l'asse, trascinare e rilasciare il campo **BuildingID** nei campi **Asse** e **ActualTemp**/**TargetTemp** in **Valore**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-172">To define the axis, drag-and-drop the **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="6cb0a-173">![Creare le visualizzazioni di dati usando Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Creare le visualizzazioni di dati usando Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-173">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

9. <span data-ttu-id="6cb0a-174">Per impostazione predefinita, la visualizzazione mostra la somma di **ActualTemp** e **TargetTemp**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-174">By default the visualization shows the sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="6cb0a-175">Per entrambi i campi, dall'elenco a discesa selezionare **Media** per ottenere una media della temperature effettiva e di destinazione per entrambe le compilazioni.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-175">For both the fields, from the drop-down, select **Average** to get an average of actual and target temperatures for both buildings.</span></span>

    <span data-ttu-id="6cb0a-176">![Creare le visualizzazioni di dati usando Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Creare le visualizzazioni di dati usando Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-176">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

10. <span data-ttu-id="6cb0a-177">La visualizzazione dei dati deve essere simile a quella nello screenshot.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-177">Your data visualization should be similar to the one in the screenshot.</span></span> <span data-ttu-id="6cb0a-178">Spostare il cursore sopra la visualizzazione per ottenere suggerimenti con i dati rilevanti.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-178">Move your cursor over the visualization to get tool tips with relevant data.</span></span>

    <span data-ttu-id="6cb0a-179">![Creare le visualizzazioni di dati usando Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Creare le visualizzazioni di dati usando Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-179">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

11. <span data-ttu-id="6cb0a-180">Fare clic su **Salva** nel menu principale e specificare un nome per il report.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-180">Click **Save** from the top menu and provide a report name.</span></span> <span data-ttu-id="6cb0a-181">È inoltre possibile aggiungere l'oggetto visivo.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-181">You can also pin the visual.</span></span> <span data-ttu-id="6cb0a-182">Quando si aggiunge una visualizzazione, viene archiviata nel dashboard consentendo di tenere traccia dell'ultimo valore in modo immediato.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-182">When you pin a visualization, it is stored on your dashboard so you can track the latest value at a glance.</span></span>

   <span data-ttu-id="6cb0a-183">È possibile aggiungere tutte le visualizzazioni per lo stesso set di dati e aggiungerle al dashboard per uno snapshot dei dati.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-183">You can add as many visualizations as you want for the same dataset and pin them to the dashboard for a snapshot of your data.</span></span> <span data-ttu-id="6cb0a-184">Inoltre, i cluster Spark in HDInsight sono direttamente connessi a Power BI.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-184">Also, Spark clusters on HDInsight are connected to Power BI with direct connect.</span></span> <span data-ttu-id="6cb0a-185">Ciò assicura che i dati di Power BI siano sempre aggiornati dal cluster e non è quindi necessario pianificare gli aggiornamenti per il set di dati.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-185">This ensures that Power BI always has the most up-to-date data from your cluster so you do not need to schedule refreshes for the dataset.</span></span>

## <span data-ttu-id="6cb0a-186"><a name="tableau"></a>Usare Tableau Desktop per la visualizzazione dei dati Spark</span><span class="sxs-lookup"><span data-stu-id="6cb0a-186"><a name="tableau"></a>Use Tableau Desktop for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="6cb0a-187">Questa sezione è applicabile solo per i cluster Spark 1.5.2 creati in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="6cb0a-188">Installare [Tableau Desktop](http://www.tableau.com/products/desktop) nel computer in cui si sta eseguendo questa esercitazione di Apache Spark BI.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on the computer where you are running this Apache Spark BI tutorial.</span></span>

2. <span data-ttu-id="6cb0a-189">Assicurarsi che nel computer sia installato un driver ODBC di Microsoft Spark.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="6cb0a-190">È possibile installare il driver da [qui](http://go.microsoft.com/fwlink/?LinkId=616229).</span><span class="sxs-lookup"><span data-stu-id="6cb0a-190">You can install the driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="6cb0a-191">Avviare Tableau Desktop.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="6cb0a-192">Nel riquadro di sinistra, nell'elenco dei server a cui connettersi, fare clic su **Spark SQL**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-192">In the left pane, from the list of server to connect to, click **Spark SQL**.</span></span> <span data-ttu-id="6cb0a-193">Se Spark SQL non è presente per impostazione predefinita nel riquadro sinistro, è possibile trovarlo facendo clic su **More Servers**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-193">If Spark SQL is not listed by default in the left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="6cb0a-194">Nella finestra di dialogo della connessione a Spark SQL, specificare i valori come illustrato nello screenshot e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-194">In the Spark SQL connection dialog box, provide the values as shown in the screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="6cb0a-195">![Connettersi a un cluster per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connettersi a un cluster per Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-195">![Connect to a cluster for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect to a cluster for Apache Spark BI")</span></span>

    <span data-ttu-id="6cb0a-196">L'elenco a discesa di autenticazione indica **Microsoft Azure HDInsight Service** come opzione solo se nel computer è installato il [driver ODBC di Microsoft Spark](http://go.microsoft.com/fwlink/?LinkId=616229) .</span><span class="sxs-lookup"><span data-stu-id="6cb0a-196">The authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed the [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on the computer.</span></span>
3. <span data-ttu-id="6cb0a-197">Nella schermata successiva fare clic sull'icona **Find** (Trova) dal menu a discesa **Schema** e quindi su **default** (predefinito).</span><span class="sxs-lookup"><span data-stu-id="6cb0a-197">On the next screen, from the **Schema** drop-down, click the **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="6cb0a-198">![Trovare lo schema per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Trovare lo schema per Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-198">![Find schema for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")</span></span>
4. <span data-ttu-id="6cb0a-199">Per il campo **Table** (Tabella) fare di nuovo clic sull'icona **Find** (Trova) per elencare tutte le tabelle Hive disponibili nel cluster.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-199">For the **Table** field, click the **Find** icon again to list all the Hive tables available in the cluster.</span></span> <span data-ttu-id="6cb0a-200">Verrà visualizzata la tabella **hvac** creata in precedenza tramite il notebook.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-200">You should see the **hvac** table you created earlier using the notebook.</span></span>

    <span data-ttu-id="6cb0a-201">![Trovare la tabella per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Trovare la tabella per Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-201">![Find table for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")</span></span>
5. <span data-ttu-id="6cb0a-202">Trascinare e rilasciare la tabella nella casella superiore a destra.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-202">Drag and drop the table to the top box on the right.</span></span> <span data-ttu-id="6cb0a-203">Tableau importa i dati e lo schema viene visualizzato come evidenziato dalla casella rossa.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-203">Tableau imports the data and displays the schema as highlighted by the red box.</span></span>

    <span data-ttu-id="6cb0a-204">![Aggiungere tabelle a Tableau per Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Aggiungere tabelle a Tableau per Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-204">![Add tables to Tableau for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables to Tableau for Apache Spark BI")</span></span>
6. <span data-ttu-id="6cb0a-205">Fare clic sulla scheda **Sheet1** nella parte inferiore sinistra.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-205">Click the **Sheet1** tab at the bottom left.</span></span> <span data-ttu-id="6cb0a-206">Apportare una visualizzazione che mostra la temperatura effettiva e di destinazione media per tutti gli edifici e per ogni data.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-206">Make a visualization that shows the average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="6cb0a-207">Trascinare **Date** (Data) e **Building ID** (ID compilazione) su **Columns** (Colonne) e **Actual Temp**/**Target Temp** (Temp effettiva/Temp di destinazione) su **Rows** (Righe).</span><span class="sxs-lookup"><span data-stu-id="6cb0a-207">Drag **Date** and **Building ID** to **Columns** and **Actual Temp**/**Target Temp** to **Rows**.</span></span> <span data-ttu-id="6cb0a-208">In **Marks** (Marcatori) selezionare **Area** per usare una mappa di area per la visualizzazione dei dati Spark.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-208">Under **Marks**, select **Area** to use an area map for Spark data visualization.</span></span>

     <span data-ttu-id="6cb0a-209">![Aggiungere campi per la visualizzazione dei dati Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Aggiungere campi per la visualizzazione dei dati Spark")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-209">![Add fields for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")</span></span>
7. <span data-ttu-id="6cb0a-210">Per impostazione predefinita, i campi di temperatura vengono visualizzati come funzione di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-210">By default, the temperature fields are shown as aggregate.</span></span> <span data-ttu-id="6cb0a-211">Se si vuole visualizzare la media delle temperature invece, è possibile farlo dall'elenco a discesa, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-211">If you want to show the average temperatures instead, you can do so from the drop-down, as shown below.</span></span>

    <span data-ttu-id="6cb0a-212">![Eseguire la media della temperatura per la visualizzazione dei dati Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Eseguire la media della temperatura per la visualizzazione dei dati Spark")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-212">![Take average of temperature for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")</span></span>

8. <span data-ttu-id="6cb0a-213">È anche possibile super-imporre una mappa di temperatura rispetto a un'altra per farsi un'idea migliore della differenza tra le temperature effettive e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-213">You can also super-impose one temperature map over the other to get a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="6cb0a-214">Spostare il puntatore del mouse nell'angolo del grafico ad aree inferiore fino a visualizzare la forma evidenziata in un cerchio rosso.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-214">Move the mouse to the corner of the lower area map till you see the handle shape highlighted in a red circle.</span></span> <span data-ttu-id="6cb0a-215">Trascinare il grafico sull'altro grafico nella parte superiore e rilasciare il mouse quando viene visualizzata la forma evidenziata in un rettangolo rosso.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-215">Drag the map to the other map on the top and release the mouse when you see the shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="6cb0a-216">![Unire mappe per la visualizzazione dei dati Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Unire mappe per la visualizzazione dei dati Spark")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-216">![Merge maps for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")</span></span>

     <span data-ttu-id="6cb0a-217">La visualizzazione dei dati dovrebbe cambiare come mostrato nello screenshot:</span><span class="sxs-lookup"><span data-stu-id="6cb0a-217">Your data visualization should change as shown in the screenshot:</span></span>

    <span data-ttu-id="6cb0a-218">![Output di Tableau per la visualizzazione dei dati Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Output di Tableau per la visualizzazione dei dati Spark")</span><span class="sxs-lookup"><span data-stu-id="6cb0a-218">![Tableau output for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")</span></span>
9. <span data-ttu-id="6cb0a-219">Fare clic su **Save** per salvare il foglio di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-219">Click **Save** to save the worksheet.</span></span> <span data-ttu-id="6cb0a-220">È possibile creare dashboard e aggiungervi uno o più fogli.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-220">You can create dashboards and add one or more sheets to it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cb0a-221">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6cb0a-221">Next steps</span></span>

<span data-ttu-id="6cb0a-222">Finora è stato descritto come creare un cluster, frame di dati Spark per i dati query e quindi accedere ai dati dagli strumenti di BI.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-222">So far you learned how to create a cluster, create Spark data frames to query data, and then access that data from BI tools.</span></span> <span data-ttu-id="6cb0a-223">È ora possibile esaminare le istruzioni su come gestire le risorse del cluster ed eseguire il debug dei processi in esecuzione in un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="6cb0a-223">You can now look at instructions on how to manage the cluster resources and debug jobs that are running in an HDInsight Spark cluster.</span></span>

* [<span data-ttu-id="6cb0a-224">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6cb0a-224">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="6cb0a-225">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6cb0a-225">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

