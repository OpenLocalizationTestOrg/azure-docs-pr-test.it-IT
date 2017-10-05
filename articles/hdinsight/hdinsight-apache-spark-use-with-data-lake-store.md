---
title: Usare Apache Spark per analizzare i dati in Azure Data Lake Store | Microsoft Docs
description: Eseguire processi Spark per analizzare i dati archiviati in Azure Data Lake Store
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 66f115c4f348ccaeb8855568ba1ad50faa442173
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-hdinsight-spark-cluster-to-analyze-data-in-data-lake-store"></a><span data-ttu-id="881c0-103">Usare il cluster HDInsight Spark per analizzare i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="881c0-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>

<span data-ttu-id="881c0-104">In questa esercitazione si usa un notebook Jupyter disponibile con i cluster HDInsight Spark per eseguire un processo che legge i dati da un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="881c0-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="881c0-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="881c0-105">Prerequisites</span></span>

* <span data-ttu-id="881c0-106">Account di Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="881c0-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="881c0-107">Seguire le istruzioni fornite in [Introduzione ad Archivio Azure Data Lake tramite il portale di Azure](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="881c0-107">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="881c0-108">Cluster Azure HDInsight Spark con Data Lake Store come risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="881c0-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="881c0-109">Seguire le istruzioni disponibili in [Creare un cluster HDInsight con Data Lake Store tramite il portale di Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="881c0-109">Follow the instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-the-data"></a><span data-ttu-id="881c0-110">Preparare i dati</span><span class="sxs-lookup"><span data-stu-id="881c0-110">Prepare the data</span></span>

> [!NOTE]
> <span data-ttu-id="881c0-111">Non è necessario eseguire questo passaggio se è stato creato il cluster HDInsight con Data Lake Store come spazio di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="881c0-111">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="881c0-112">I processi di creazione del cluster aggiunge alcuni dati di esempio nell'account di Data Lake Store specificato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="881c0-112">The cluster creation processes adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span></span> <span data-ttu-id="881c0-113">Passare alla sezione [Usare il cluster e HDInsight Spark con Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="881c0-113">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="881c0-114">Se è stato creato un cluster HDInsight con Data Lake Store come risorsa di archiviazione aggiuntiva e un BLOB di Archiviazione di Azure come risorsa di archiviazione predefinita, è necessario copiare prima di tutto alcuni dati di esempio nell'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="881c0-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span></span> <span data-ttu-id="881c0-115">È possibile usare i dati di esempio dal BLOB di Archiviazione di Azure associati al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="881c0-115">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span></span> <span data-ttu-id="881c0-116">Per farlo, è possibile usare lo [strumento ADLCopy](http://aka.ms/downloadadlcopy) .</span><span class="sxs-lookup"><span data-stu-id="881c0-116">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span></span> <span data-ttu-id="881c0-117">Scaricare e installare lo strumento dal collegamento.</span><span class="sxs-lookup"><span data-stu-id="881c0-117">Download and install the tool from the link.</span></span>

1. <span data-ttu-id="881c0-118">Aprire un prompt dei comandi e passare alla directory in cui è installato AdlCopy, in genere `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="881c0-118">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="881c0-119">Eseguire il comando seguente per copiare un BLOB specifico dal contenitore di origine a un'istanza di Archivio Data Lake:</span><span class="sxs-lookup"><span data-stu-id="881c0-119">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="881c0-120">Copiare il file di dati di esempio **HVAC.csv** disponibile nel percorso **/HdiSamples/HdiSamples/SensorSampleData/hvac/** nell'account Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="881c0-120">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span></span> <span data-ttu-id="881c0-121">Il frammento di codice dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="881c0-121">The code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="881c0-122">Assicurarsi che nel nome del file e nel percorso le maiuscole siano corrette.</span><span class="sxs-lookup"><span data-stu-id="881c0-122">Make sure you the file and path names are in the proper case.</span></span>
   >
   >
3. <span data-ttu-id="881c0-123">Verrà richiesto di immettere le credenziali per la sottoscrizione di Azure in cui si trova l'account Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="881c0-123">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="881c0-124">L'output visualizzato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="881c0-124">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="881c0-125">Il file di dati (**HVAC.csv**) sarà copiato in una cartella denominata **/hvac** nell'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="881c0-125">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="881c0-126">Usare un cluster HDInsight Spark con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="881c0-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="881c0-127">Dalla Schermata iniziale del [portale di Azure](https://portal.azure.com/)fare clic sul riquadro del cluster Spark (se è stato aggiunto sulla Schermata iniziale).</span><span class="sxs-lookup"><span data-stu-id="881c0-127">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="881c0-128">È anche possibile passare al cluster da **Esplora tutto** > **Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="881c0-128">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="881c0-129">Dal pannello del cluster Spark fare clic su **Collegamenti rapidi** e dal pannello **Dashboard cluster** fare clic su **Notebook di Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="881c0-129">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="881c0-130">Se richiesto, immettere le credenziali per il cluster.</span><span class="sxs-lookup"><span data-stu-id="881c0-130">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="881c0-131">È anche possibile raggiungere il notebook di Jupyter per il cluster aprendo l'URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="881c0-131">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="881c0-132">Sostituire **CLUSTERNAME** con il nome del cluster:</span><span class="sxs-lookup"><span data-stu-id="881c0-132">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="881c0-133">Creare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="881c0-133">Create a new notebook.</span></span> <span data-ttu-id="881c0-134">Fare clic su **Nuovo** e quindi su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="881c0-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="881c0-135">![Creare un nuovo notebook Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Creare un nuovo notebook Jupyter")</span><span class="sxs-lookup"><span data-stu-id="881c0-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="881c0-136">Poiché il notebook è stato creato tramite il kernel PySpark, non è necessario creare contesti in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="881c0-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="881c0-137">I contesti Spark e Hive vengono creati automaticamente quando si esegue la prima cella di codice.</span><span class="sxs-lookup"><span data-stu-id="881c0-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="881c0-138">È possibile iniziare con l'importazione dei tipi necessari per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="881c0-138">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="881c0-139">A tale scopo incollare il frammento di codice seguente in una cella e premere **MAIUSC+INVIO**.</span><span class="sxs-lookup"><span data-stu-id="881c0-139">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="881c0-140">Ogni volta che viene eseguito un processo in Jupyter, il titolo della finestra del Web browser visualizzerà lo stato **(Occupato)** accanto al titolo del notebook.</span><span class="sxs-lookup"><span data-stu-id="881c0-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="881c0-141">È anche visibile un cerchio pieno accanto al testo **PySpark** nell'angolo in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="881c0-141">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="881c0-142">Dopo il completamento del processo, viene visualizzato un cerchio vuoto.</span><span class="sxs-lookup"><span data-stu-id="881c0-142">After the job is completed, this will change to a hollow circle.</span></span>

     <span data-ttu-id="881c0-143">![Stato di un processo del notebook Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Stato di un processo del notebook Jupyter")</span><span class="sxs-lookup"><span data-stu-id="881c0-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="881c0-144">Caricare i dati di esempio in una tabella temporanea mediante il file **HVAC.csv** che è stato copiato nell'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="881c0-144">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span></span> <span data-ttu-id="881c0-145">È possibile accedere ai dati dell'account di Archivio Data Lake mediante il seguente modello di URL.</span><span class="sxs-lookup"><span data-stu-id="881c0-145">You can access the data in the Data Lake Store account using the following URL pattern.</span></span>

    * <span data-ttu-id="881c0-146">Se è presente un Data Lake Store come risorsa di archiviazione predefinita, il file HVAC.csv sarà disponibile in un percorso analogo all'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="881c0-146">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="881c0-147">In alternativa, è possibile anche usare un formato abbreviato, ad esempio il seguente:</span><span class="sxs-lookup"><span data-stu-id="881c0-147">Or, you could also use a shortened format such as the following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="881c0-148">Se è presente un Data Lake Store come risorsa di archiviazione aggiuntiva, il file HVAC.csv sarà disponibile nel percorso in cui è stato copiato, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="881c0-148">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="881c0-149">In una cella vuota incollare l'esempio di codice seguente, sostituire **MYDATALAKESTORE** con il nome dell'account Data Lake Store e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="881c0-149">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="881c0-150">Questo esempio di codice registra i dati in una tabella temporanea denominata **hvac**.</span><span class="sxs-lookup"><span data-stu-id="881c0-150">This code example registers the data into a temporary table called **hvac**.</span></span>

            # Load the data. The path below assumes Data Lake Store is default storage for the Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create the schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse the data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register the data fram as a table to run queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="881c0-151">Dato che si usa un kernel PySpark, è ora possibile eseguire direttamente una query SQL sulla tabella temporanea **hvac** appena creata usando il comando Magic `%%sql`.</span><span class="sxs-lookup"><span data-stu-id="881c0-151">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span></span> <span data-ttu-id="881c0-152">Per altre informazioni sul magic `%%sql` e sugli altri magic disponibili con il kernel PySpark, vedere [Kernel disponibili per i notebook di Jupyter con cluster Spark in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="881c0-152">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="881c0-153">Una volta che il processo viene completato correttamente, per impostazione predefinita viene visualizzato l'output tabulare seguente.</span><span class="sxs-lookup"><span data-stu-id="881c0-153">Once the job is completed successfully, the following tabular output is displayed by default.</span></span>

      <span data-ttu-id="881c0-154">![Tabella di output dei risultati della query](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Tabella di output dei risultati della query")</span><span class="sxs-lookup"><span data-stu-id="881c0-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="881c0-155">È anche possibile visualizzare i risultati in altri formati.</span><span class="sxs-lookup"><span data-stu-id="881c0-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="881c0-156">Ad esempio, un grafico ad area per lo stesso output apparirebbe come segue.</span><span class="sxs-lookup"><span data-stu-id="881c0-156">For example, an area graph for the same output would look like the following.</span></span>

     <span data-ttu-id="881c0-157">![Grafico ad area dei risultati della query](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Grafico ad area dei risultati della query")</span><span class="sxs-lookup"><span data-stu-id="881c0-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="881c0-158">Al termine dell'esecuzione dell'applicazione, è necessario arrestare il notebook per rilasciare le risorse.</span><span class="sxs-lookup"><span data-stu-id="881c0-158">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="881c0-159">A tale scopo, dal menu **File** del notebook fare clic su **Close and Halt** (Chiudi e interrompi).</span><span class="sxs-lookup"><span data-stu-id="881c0-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="881c0-160">Questa operazione consente di arrestare e chiudere il notebook.</span><span class="sxs-lookup"><span data-stu-id="881c0-160">This will shutdown and close the notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="881c0-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="881c0-161">Next steps</span></span>

* [<span data-ttu-id="881c0-162">Creare un'applicazione Scala autonoma da eseguire nel cluster Apache Spark in HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="881c0-162">Create a standalone Scala application to run on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="881c0-163">Usare gli strumenti HDInsight nel Toolkit di Azure per IntelliJ per creare applicazioni Spark per il cluster HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="881c0-163">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="881c0-164">Usare gli strumenti HDInsight nel Toolkit di Azure per Eclipse per creare applicazioni Spark per il cluster HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="881c0-164">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
