---
title: aaaUse dati tooanalyze Apache Spark in archivio Azure Data Lake | Documenti Microsoft
description: Eseguire i processi di Spark tooanalyze dati archiviati nell'archivio Azure Data Lake
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
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a><span data-ttu-id="5999c-103">Utilizzare i dati di tooanalyze cluster HDInsight Spark in archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="5999c-103">Use HDInsight Spark cluster tooanalyze data in Data Lake Store</span></span>

<span data-ttu-id="5999c-104">In questa esercitazione, si utilizza server Jupyter notebook disponibili con i cluster di HDInsight Spark toorun un processo che legge i dati da un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5999c-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters toorun a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5999c-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5999c-105">Prerequisites</span></span>

* <span data-ttu-id="5999c-106">Account di Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5999c-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="5999c-107">Seguire le istruzioni di hello in [introduzione archivio Azure Data Lake tramite il portale di Azure hello](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5999c-107">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="5999c-108">Cluster Azure HDInsight Spark con Data Lake Store come risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5999c-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="5999c-109">Seguire le istruzioni di hello in [creare un cluster HDInsight con archivio Data Lake tramite il portale di Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5999c-109">Follow hello instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-hello-data"></a><span data-ttu-id="5999c-110">Preparare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="5999c-110">Prepare hello data</span></span>

> [!NOTE]
> <span data-ttu-id="5999c-111">Non è necessario tooperform questo passaggio se è stato creato il cluster di HDInsight hello con archivio Data Lake come spazio di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="5999c-111">You do not need tooperform this step if you have created hello HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="5999c-112">i processi di creazione di cluster Hello aggiunge alcuni dati di esempio nell'account archivio Data Lake hello specificato durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5999c-112">hello cluster creation processes adds some sample data in hello Data Lake Store account that you specify while creating hello cluster.</span></span> <span data-ttu-id="5999c-113">Ignorare la sezione toohello [cluster HDInsight usare Spark con archivio Data Lake](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="5999c-113">Skip toohello section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="5999c-114">Se è stato creato un cluster HDInsight con archivio Data Lake come ulteriore spazio di archiviazione e Blob di archiviazione di Azure come spazio di archiviazione predefinito, è necessario innanzitutto copiare su alcuni toohello di dati di esempio account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5999c-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data toohello Data Lake Store account.</span></span> <span data-ttu-id="5999c-115">È possibile utilizzare i dati di esempio hello hello che BLOB di archiviazione di Azure associata a cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5999c-115">You can use hello sample data from hello Azure Storage Blob associated with hello HDInsight cluster.</span></span> <span data-ttu-id="5999c-116">È possibile utilizzare hello [ADLCopy strumento](http://aka.ms/downloadadlcopy) toodo in modo.</span><span class="sxs-lookup"><span data-stu-id="5999c-116">You can use hello [ADLCopy tool](http://aka.ms/downloadadlcopy) toodo so.</span></span> <span data-ttu-id="5999c-117">Scaricare e installare lo strumento hello dal collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="5999c-117">Download and install hello tool from hello link.</span></span>

1. <span data-ttu-id="5999c-118">Aprire un prompt dei comandi e passare toohello directory in cui AdlCopy è installato, in genere `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="5999c-118">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="5999c-119">Eseguire hello successivo comando toocopy un blob specifico da hello origine contenitore tooa archivio Data Lake:</span><span class="sxs-lookup"><span data-stu-id="5999c-119">Run hello following command toocopy a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="5999c-120">Hello copia **HVAC.csv** del file di dati di esempio in **/HdiSamples/HdiSamples/SensorSampleData/impianto/** toohello account archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5999c-120">Copy hello **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store account.</span></span> <span data-ttu-id="5999c-121">frammento di codice Hello dovrebbe essere simile:</span><span class="sxs-lookup"><span data-stu-id="5999c-121">hello code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="5999c-122">Verificare che si hello file e i nomi di percorso sono in lettere maiuscole iniziali hello.</span><span class="sxs-lookup"><span data-stu-id="5999c-122">Make sure you hello file and path names are in hello proper case.</span></span>
   >
   >
3. <span data-ttu-id="5999c-123">Sarà richiesto tooenter credenziali hello per hello sottoscrizione di Azure in cui si dispone di account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5999c-123">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="5999c-124">Verrà visualizzato un esempio di toohello simile output:</span><span class="sxs-lookup"><span data-stu-id="5999c-124">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="5999c-125">file di dati Hello (**HVAC.csv**) verranno copiati in una cartella **/hvac** in hello account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5999c-125">hello data file (**HVAC.csv**) will be copied under a folder **/hvac** in hello Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="5999c-126">Usare un cluster HDInsight Spark con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5999c-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="5999c-127">Da hello [portale Azure](https://portal.azure.com/), dalla schermata iniziale di hello, fare clic sul riquadro hello per il cluster Spark (se è stato aggiunto, schermata iniziale di toohello).</span><span class="sxs-lookup"><span data-stu-id="5999c-127">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="5999c-128">È inoltre possibile navigare cluster tooyour **Esplora tutto** > **cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5999c-128">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="5999c-129">Dal Pannello di cluster Spark hello, fare clic su **collegamenti rapidi**e quindi da hello **Dashboard Cluster** pannello, fare clic su **server Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="5999c-129">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="5999c-130">Se richiesto, immettere le credenziali di amministratore hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5999c-130">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5999c-131">È anche possibile raggiungere hello server Jupyter Notebook per il cluster usando hello apertura URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="5999c-131">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="5999c-132">Sostituire **CLUSTERNAME** con nome hello del cluster:</span><span class="sxs-lookup"><span data-stu-id="5999c-132">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="5999c-133">Creare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="5999c-133">Create a new notebook.</span></span> <span data-ttu-id="5999c-134">Fare clic su **Nuovo** e quindi su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="5999c-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="5999c-135">![Creare un nuovo notebook Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Creare un nuovo notebook Jupyter")</span><span class="sxs-lookup"><span data-stu-id="5999c-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="5999c-136">Poiché è stato creato un notebook utilizza il kernel PySpark hello, non è necessario toocreate i contesti in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="5999c-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="5999c-137">Quando si esegue prima cella di codice hello contesti di Spark e Hive Hello verranno creati automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="5999c-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="5999c-138">È possibile avviare l'importazione di tipi di hello necessari per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="5999c-138">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="5999c-139">toodo incollare in tal caso, hello seguente frammento di codice in una cella e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="5999c-139">toodo so, paste hello following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="5999c-140">Ogni volta che viene eseguito un processo in Jupyter, verrà visualizzato il titolo della finestra del browser web un **(occupata)** stato insieme a titolo di hello notebook.</span><span class="sxs-lookup"><span data-stu-id="5999c-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="5999c-141">Verrà visualizzato anche un toohello Avanti cerchio pieno **PySpark** testo nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="5999c-141">You will also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="5999c-142">Dopo aver completato il processo di hello, verrà modificato tooa cerchio.</span><span class="sxs-lookup"><span data-stu-id="5999c-142">After hello job is completed, this will change tooa hollow circle.</span></span>

     <span data-ttu-id="5999c-143">![Stato di un processo del notebook Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Stato di un processo del notebook Jupyter")</span><span class="sxs-lookup"><span data-stu-id="5999c-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="5999c-144">Caricare i dati di esempio in una tabella temporanea utilizzando hello **HVAC.csv** file copiato account archivio Data Lake toohello.</span><span class="sxs-lookup"><span data-stu-id="5999c-144">Load sample data into a temporary table using hello **HVAC.csv** file you copied toohello Data Lake Store account.</span></span> <span data-ttu-id="5999c-145">È possibile accedere a dati hello in account archivio Data Lake hello utilizzando hello seguente modello di URL.</span><span class="sxs-lookup"><span data-stu-id="5999c-145">You can access hello data in hello Data Lake Store account using hello following URL pattern.</span></span>

    * <span data-ttu-id="5999c-146">Se si dispone di archivio Data Lake come spazio di archiviazione predefinito, HVAC.csv sarà simile toohello percorso hello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="5999c-146">If you have Data Lake Store as default storage, HVAC.csv will be at hello path similar toohello following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="5999c-147">In alternativa, è anche possibile usare un formato abbreviato come illustrato di seguito hello:</span><span class="sxs-lookup"><span data-stu-id="5999c-147">Or, you could also use a shortened format such as hello following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="5999c-148">Se si dispone di archivio Data Lake come ulteriore spazio di archiviazione, HVAC.csv sarà nel percorso di hello in cui è stato copiato, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5999c-148">If you have Data Lake Store as additional storage, HVAC.csv will be at hello location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="5999c-149">In una cella vuota, hello Incolla esempio di codice seguente sostituire **MYDATALAKESTORE** con il nome dell'account archivio Data Lake e premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="5999c-149">In an empty cell, paste hello following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="5999c-150">Questo esempio di codice registra dati hello in una tabella temporanea denominata **impianto**.</span><span class="sxs-lookup"><span data-stu-id="5999c-150">This code example registers hello data into a temporary table called **hvac**.</span></span>

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="5999c-151">Perché si sta usando un kernel PySpark, è ora possibile direttamente eseguire una query SQL per la tabella temporanea hello **impianto** appena creato utilizzando hello `%%sql` magic.</span><span class="sxs-lookup"><span data-stu-id="5999c-151">Because you are using a PySpark kernel, you can now directly run a SQL query on hello temporary table **hvac** that you just created by using hello `%%sql` magic.</span></span> <span data-ttu-id="5999c-152">Per ulteriori informazioni su hello `%%sql` magic, nonché altri magics disponibili con kernel PySpark hello, vedere [kernel disponibile sui server Jupyter notebook con i cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="5999c-152">For more information about hello `%%sql` magic, as well as other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="5999c-153">Una volta completato il processo di hello, hello seguente tabulari output viene visualizzato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5999c-153">Once hello job is completed successfully, hello following tabular output is displayed by default.</span></span>

      <span data-ttu-id="5999c-154">![Tabella di output dei risultati della query](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Tabella di output dei risultati della query")</span><span class="sxs-lookup"><span data-stu-id="5999c-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="5999c-155">È inoltre possibile visualizzare i risultati hello in anche altre visualizzazioni.</span><span class="sxs-lookup"><span data-stu-id="5999c-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="5999c-156">Ad esempio, un grafico ad area per hello stesso output sarebbe simile al seguente hello.</span><span class="sxs-lookup"><span data-stu-id="5999c-156">For example, an area graph for hello same output would look like hello following.</span></span>

     <span data-ttu-id="5999c-157">![Grafico ad area dei risultati della query](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Grafico ad area dei risultati della query")</span><span class="sxs-lookup"><span data-stu-id="5999c-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="5999c-158">Al termine dell'esecuzione di un'applicazione hello, si consiglia di risorse di arresto hello notebook toorelease hello.</span><span class="sxs-lookup"><span data-stu-id="5999c-158">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="5999c-159">toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**.</span><span class="sxs-lookup"><span data-stu-id="5999c-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="5999c-160">Questo verrà arrestato e notebook hello Chiudi.</span><span class="sxs-lookup"><span data-stu-id="5999c-160">This will shutdown and close hello notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5999c-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5999c-161">Next steps</span></span>

* [<span data-ttu-id="5999c-162">Creare un toorun di applicazione Scala autonomo nel cluster di Apache Spark</span><span class="sxs-lookup"><span data-stu-id="5999c-162">Create a standalone Scala application toorun on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="5999c-163">Utilizzare gli strumenti di HDInsight in Azure Toolkit per le applicazioni per il cluster HDInsight Spark Linux Spark toocreate IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5999c-163">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="5999c-164">Utilizzare gli strumenti di HDInsight in Azure Toolkit per Eclipse toocreate Spark applicazioni cluster HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="5999c-164">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
