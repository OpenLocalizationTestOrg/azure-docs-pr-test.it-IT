---
title: Chiamare i programmi Spark da Azure Data Factory | Microsoft Docs
description: "È possibile chiamare i programmi Spark da una data factory di Azure usando l'attività MapReduce."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 57894bbdd9208f8c32eb65e29f04e2ae723780ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="f1ac4-103">Chiamare i programmi Spark dalle pipeline Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f1ac4-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="f1ac4-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="f1ac4-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="f1ac4-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="f1ac4-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="f1ac4-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="f1ac4-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="f1ac4-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="f1ac4-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="f1ac4-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="f1ac4-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="f1ac4-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f1ac4-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="f1ac4-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f1ac4-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="f1ac4-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="f1ac4-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="f1ac4-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f1ac4-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="f1ac4-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="f1ac4-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="f1ac4-114">Introduzione</span><span class="sxs-lookup"><span data-stu-id="f1ac4-114">Introduction</span></span>
<span data-ttu-id="f1ac4-115">L'attività Spark è una delle [attività di trasformazione dei dati](data-factory-data-transformation-activities.md) supportate da Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-115">Spark Activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="f1ac4-116">Questa attività esegue il programma Spark specificato nel cluster Apache Spark in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-116">This activity runs the specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="f1ac4-117">L'attività Spark non supporta i cluster Spark HDInsight che usano Azure Data Lake Store come risorsa di archiviazione primaria.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="f1ac4-118">L'attività Spark supporta solo cluster Spark HDInsight esistenti (personalizzati).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="f1ac4-119">Non supporta un servizio collegato HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="f1ac4-120">Procedura dettagliata: creare una pipeline con attività Spark</span><span class="sxs-lookup"><span data-stu-id="f1ac4-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="f1ac4-121">Di seguito viene illustrata la procedura usata in generale per creare una pipeline di Data Factory con un'attività Spark.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-121">Here are the typical steps to create a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="f1ac4-122">Creare una data factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-122">Create a data factory.</span></span>
2. <span data-ttu-id="f1ac4-123">Creare un servizio collegato Archiviazione di Azure per collegare l'archiviazione di Azure associata al cluster Spark HDInsight alla data factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-123">Create an Azure Storage linked service to link your Azure storage that is associated with your HDInsight Spark cluster to the data factory.</span></span>     
2. <span data-ttu-id="f1ac4-124">Creare un servizio collegato HDInsight di Azure per collegare il cluster Apache Spark in HDInsight di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-124">Create an Azure HDInsight linked service to link your Apache Spark cluster in Azure HDInsight to the data factory.</span></span>
3. <span data-ttu-id="f1ac4-125">Creare un set di dati che faccia riferimento al servizio collegato di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-125">Create a dataset that refers to the Azure Storage linked service.</span></span> <span data-ttu-id="f1ac4-126">Attualmente, è necessario specificare un set di dati di output per un'attività anche se non viene prodotto alcun output.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="f1ac4-127">Creare una pipeline con l'attività Spark che faccia riferimento al servizio collegato HDInsight creato al passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-127">Create a pipeline with Spark activity that refers to the HDInsight linked service created in #2.</span></span> <span data-ttu-id="f1ac4-128">L'attività è configurata con il set di dati creato nel passaggio precedente come un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-128">The activity is configured with the dataset you created in the previous step as an output dataset.</span></span> <span data-ttu-id="f1ac4-129">Il set di dati di output è ciò su cui si basa la pianificazione (oraria, giornaliera e così via).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-129">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="f1ac4-130">Pertanto, è necessario specificare il set di dati di output anche se l'attività non ha prodotto alcun output.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-130">Therefore, you must specify the output dataset even though the activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f1ac4-131">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f1ac4-131">Prerequisites</span></span>
1. <span data-ttu-id="f1ac4-132">Creare un **account di Archiviazione di Azure generico** seguendo le istruzioni della procedura dettagliata: [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-132">Create a **general-purpose Azure Storage Account** by following instructions in the walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="f1ac4-133">Creare un **cluster Apache Spark in HDInsight di Azure** seguendo le istruzioni riportate nell'esercitazione: [Creare il cluster Apache Spark in HDInsight di Azure](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in the tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="f1ac4-134">Associare l'account di archiviazione di Azure creato al passaggio 1 con questo cluster.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-134">Associate the Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="f1ac4-135">Scaricare e leggere il file di script python **test.py**, disponibile all'indirizzo: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-135">Download and review the python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="f1ac4-136">Caricare **test.py** nella cartella **pyFiles** nel contenitore **adfspark** nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-136">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="f1ac4-137">Creare la cartella e il contenitore, se non esistono.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-137">Create the container and the folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="f1ac4-138">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="f1ac4-138">Create data factory</span></span>
<span data-ttu-id="f1ac4-139">In questo passaggio iniziale viene creata la data factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-139">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="f1ac4-140">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f1ac4-141">Fare clic su **NUOVO** nel menu a sinistra e quindi su **Dati e analisi** e **Data factory**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-141">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="f1ac4-142">Nel pannello **Nuova data factory** immettere **SparkDF** come nome.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-142">In the **New data factory** blade, enter **SparkDF** for the Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f1ac4-143">Il nome della data factory di Azure deve essere **univoco a livello globale**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-143">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="f1ac4-144">Se viene visualizzato l'errore **Il nome "SparkDF" per la data factory non è disponibile**,</span><span class="sxs-lookup"><span data-stu-id="f1ac4-144">If you see the error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="f1ac4-145">cambiare il nome della data factory, ad esempio nomeutenteSparkDFdate, e provare di nuovo a crearla.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-145">Change the name of the data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="f1ac4-146">Per informazioni sulle regole di denominazione per gli elementi di Data Factory, vedere l'argomento [Azure Data Factory - Regole di denominazione](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="f1ac4-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="f1ac4-147">Selezionare la **sottoscrizione di Azure** in cui creare la data factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-147">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="f1ac4-148">Selezionare un **gruppo di risorse** di Azure esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="f1ac4-149">Selezionare l'opzione **Aggiungi al dashboard**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-149">Select **Pin to dashboard** option.</span></span>  
6. <span data-ttu-id="f1ac4-150">Fare clic su **Crea** nel pannello **Nuova data factory**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-150">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f1ac4-151">Per creare istanze di data factory, è necessario essere membri del ruolo [Collaboratore Data factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) a livello di sottoscrizione/gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-151">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
7. <span data-ttu-id="f1ac4-152">Nel **dashboard** del portale di Azure verrà visualizzata la data factory in fase di creazione:</span><span class="sxs-lookup"><span data-stu-id="f1ac4-152">You see the data factory being created in the **dashboard** of the Azure portal as follows:</span></span>   
8. <span data-ttu-id="f1ac4-153">Dopo la creazione della data factory, viene visualizzata la pagina corrispondente con elencato il contenuto della data factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-153">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span> <span data-ttu-id="f1ac4-154">Se non è possibile visualizzare la pagina della data factory, fare clic sul rispettivo riquadro nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-154">If you do not see the data factory page, click the tile for your data factory on the dashboard.</span></span>

    ![Pannello Data factory](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="f1ac4-156">Creazione di servizi collegati</span><span class="sxs-lookup"><span data-stu-id="f1ac4-156">Create linked services</span></span>
<span data-ttu-id="f1ac4-157">In questo passaggio si creano due servizi collegati, uno per collegare il cluster Spark alla data factory e l'altro per collegare l'archiviazione di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-157">In this step, you create two linked services, one to link your Spark cluster to your data factory, and the other to link your Azure storage to your data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="f1ac4-158">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f1ac4-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="f1ac4-159">In questo passaggio l'account di archiviazione di Azure viene collegato alla data factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-159">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="f1ac4-160">Un set di dati creato in un passaggio successivo di questa procedura dettagliata si riferisce a questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-160">A dataset you create in a step later in this walkthrough refers to this linked service.</span></span> <span data-ttu-id="f1ac4-161">Anche il servizio collegato HDInsight definito nel passaggio successivo fa riferimento a questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-161">The HDInsight linked service that you define in the next step refers to this linked service too.</span></span>  

1. <span data-ttu-id="f1ac4-162">Fare clic su **Creare e distribuire** nel pannello **Data Factory** per la data factory interessata.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-162">Click **Author and deploy** on the **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="f1ac4-163">Verrà visualizzato l'editor di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-163">You should see the Data Factory Editor.</span></span>
2. <span data-ttu-id="f1ac4-164">Fare clic su **Nuovo archivio dati** e scegliere **Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nuovo archivio dati - Archiviazione di Azure - Menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="f1ac4-166">Nell'editor verrà visualizzato lo **script JSON** per la creazione di un servizio collegato Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-166">You should see the **JSON script** for creating an Azure Storage linked service in the editor.</span></span>

   ![Servizio collegato Archiviazione di Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="f1ac4-168">Sostituire **account name** e **account key** con il nome e la chiave di accesso dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-168">Replace **account name** and **account key** with the name and access key of your Azure storage account.</span></span> <span data-ttu-id="f1ac4-169">Per informazioni su come ottenere la chiave di accesso alle risorse di archiviazione, vedere le informazioni su come visualizzare, copiare e rigenerare le chiavi di accesso alle risorse di archiviazione in [Gestire l'account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-169">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="f1ac4-170">Per distribuire il servizio collegato, fare clic su **Distribuisci** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-170">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="f1ac4-171">Al termine della distribuzione del servizio collegato, la finestra **Bozza-1** verrà nascosta e nella visualizzazione albero a sinistra verrà visualizzato **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-171">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="f1ac4-172">Creare un servizio collegato HDInsight</span><span class="sxs-lookup"><span data-stu-id="f1ac4-172">Create HDInsight linked service</span></span>
<span data-ttu-id="f1ac4-173">In questo passaggio si crea un servizio collegato HDInsight di Azure per collegare il cluster Spark HDInsight alla data factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-173">In this step, you create Azure HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span></span> <span data-ttu-id="f1ac4-174">In questo esempio il cluster HDInsight viene usato per eseguire il programma Spark specificato nell'attività Spark della pipeline.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-174">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span></span>  

1. <span data-ttu-id="f1ac4-175">Fare clic su **... Altro** sulla barra degli strumenti, scegliere **Nuovo calcolo** e quindi fare clic su **Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-175">Click **... More** on the toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Creare un servizio collegato HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="f1ac4-177">Copiare e incollare il frammento di codice seguente nella finestra **Bozza-1** .</span><span class="sxs-lookup"><span data-stu-id="f1ac4-177">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="f1ac4-178">Nell'editor JSON editor seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f1ac4-178">In the JSON editor, do the following steps:</span></span>
    1. <span data-ttu-id="f1ac4-179">Specificare l'**URI** per il cluster Spark HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-179">Specify the **URI** for the HDInsight Spark cluster.</span></span> <span data-ttu-id="f1ac4-180">Ad esempio: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="f1ac4-181">Specificare il nome dell'**utente** che ha accesso al cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-181">Specify the name of the **user** who has access to the Spark cluster.</span></span>
    3. <span data-ttu-id="f1ac4-182">Specificare la **password** per l'utente.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-182">Specify the **password** for user.</span></span>
    4. <span data-ttu-id="f1ac4-183">Specificare il **servizio collegato Archiviazione di Azure** associato al cluster Spark HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-183">Specify the **Azure Storage linked service** that is associated with the HDInsight Spark cluster.</span></span> <span data-ttu-id="f1ac4-184">Nell'esempio è: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - <span data-ttu-id="f1ac4-185">L'attività Spark non supporta i cluster Spark HDInsight che usano Azure Data Lake Store come risorsa di archiviazione primaria.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="f1ac4-186">L'attività Spark supporta solo cluster Spark HDInsight esistenti (personalizzati).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="f1ac4-187">Non supporta un servizio collegato HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="f1ac4-188">Per informazioni dettagliate sul servizio collegato HDInsight, vedere [Servizio collegato HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about the HDInsight linked service.</span></span>
3.  <span data-ttu-id="f1ac4-189">Per distribuire il servizio collegato, fare clic su **Distribuisci** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-189">To deploy the linked service, click **Deploy** on the command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="f1ac4-190">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="f1ac4-190">Create output dataset</span></span>
<span data-ttu-id="f1ac4-191">Il set di dati di output è ciò su cui si basa la pianificazione (oraria, giornaliera e così via).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-191">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="f1ac4-192">Pertanto è necessario specificare il set di dati di output per l'attività Spark nella pipeline, anche se l'attività non produce alcun output.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-192">Therefore, you must specify an output dataset for the spark activity in the pipeline even though the activity does not really produce any output.</span></span> <span data-ttu-id="f1ac4-193">La specifica di un set di dati di input per l'attività è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-193">Specifying an input dataset for the activity is optional.</span></span>

1. <span data-ttu-id="f1ac4-194">Nell'**editor di Data Factory** fare clic su **... Altro** sulla barra dei comandi e quindi fare clic su **Nuovo set di dati** e selezionare **Archivio BLOB di Azure**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-194">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="f1ac4-195">Copiare e incollare il frammento di codice seguente nella finestra Bozza-1.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-195">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="f1ac4-196">Il frammento JSON definisce un set di dati denominato **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-196">The JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="f1ac4-197">Specificare anche che i risultati devono essere archiviati nel contenitore BLOB denominato **adfspark** e nella cartella denominata **pyFiles/output**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-197">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span></span> <span data-ttu-id="f1ac4-198">Come accennato in precedenza, questo set di dati è un set di dati fittizio.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="f1ac4-199">Il programma Spark in questo esempio non produce alcun output.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-199">The Spark program in this example does not produce any output.</span></span> <span data-ttu-id="f1ac4-200">La sezione **availability** specifica che il set di dati di output viene prodotto su base giornaliera.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-200">The **availability** section specifies that the output dataset is produced daily.</span></span>  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="f1ac4-201">Per distribuire il set di dati, fare clic su **Distribuisci** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-201">To deploy the dataset, click **Deploy** on the command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="f1ac4-202">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="f1ac4-202">Create pipeline</span></span>
<span data-ttu-id="f1ac4-203">In questo passaggio viene creata una pipeline con un'**attività HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="f1ac4-204">In questo momento la pianificazione è basata sul set di dati di output, quindi è necessario creare un set di dati di output anche se l'attività non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-204">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="f1ac4-205">Se l'attività non richiede input, è possibile ignorare la creazione del set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-205">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="f1ac4-206">Pertanto in questo esempio non viene specificato alcun set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="f1ac4-207">Nell'**editor di Data Factory** fare clic su **... Altro** sulla barra dei comandi e quindi fare clic su **Nuova pipeline**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-207">In the **Data Factory Editor**, click **… More** on the command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="f1ac4-208">Sostituire lo script nella finestra Bozza-1 con lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="f1ac4-208">Replace the script in the Draft-1 window with the following script:</span></span>

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    <span data-ttu-id="f1ac4-209">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="f1ac4-209">Note the following points:</span></span>
    - <span data-ttu-id="f1ac4-210">La proprietà **type** è impostata su **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-210">The **type** property is set to **HDInsightSpark**.</span></span>
    - <span data-ttu-id="f1ac4-211">Il **rootPath** è impostato su **adfspark\\pyFiles**, dove adfspark è il contenitore BLOB di Azure e pyFiles è la cartella di file nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-211">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="f1ac4-212">In questo esempio, l'archivio BLOB di Azure è quello associato al cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-212">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="f1ac4-213">È possibile caricare il file in un archivio di Azure diverso.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-213">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="f1ac4-214">In tal caso, creare un servizio collegato Archiviazione di Azure per collegare l'account di archiviazione alla data factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-214">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="f1ac4-215">Quindi, specificare il nome del servizio collegato come valore per la proprietà **sparkJobLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-215">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="f1ac4-216">Vedere [Proprietà dell'attività Spark](#spark-activity-properties) per informazioni dettagliate su questa e altre proprietà supportate dall'attività Spark.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>  
    - <span data-ttu-id="f1ac4-217">La proprietà **entryFilePath** è impostata su **test.py**, ovvero il file python.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-217">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span>
    - <span data-ttu-id="f1ac4-218">La proprietà **getDebugInfo** è impostata su **Sempre**, a indicare che i file di log vengono sempre generati (con esito positivo o negativo).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-218">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="f1ac4-219">Non è consigliabile impostare questa proprietà su `Always` in un ambiente di produzione, a meno che non si stia tentando di risolvere un problema.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-219">We recommend that you do not set this property to `Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="f1ac4-220">La sezione **outputs** presenta un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-220">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="f1ac4-221">Anche se il programma Spark non genera alcun output, è necessario specificare un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-221">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="f1ac4-222">Il set di dati di output è ciò su cui si basa la pianificazione della pipeline (oraria, giornaliera e così via).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-222">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="f1ac4-223">Per informazioni dettagliate sulle proprietà supportate dall'attività Spark, vedere la sezione [Proprietà dell'attività Spark](#spark-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-223">For details about the properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="f1ac4-224">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-224">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="f1ac4-225">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="f1ac4-225">Monitor pipeline</span></span>
1. <span data-ttu-id="f1ac4-226">Fare clic su **X** per chiudere i pannelli dell'editor di Data Factory e tornare al pannello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-226">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory home page.</span></span> <span data-ttu-id="f1ac4-227">Fare clic su **Monitoraggio e gestione** per avviare l'applicazione di monitoraggio in un'altra scheda.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-227">Click **Monitor and Manage** to launch the monitoring application in another tab.</span></span>

    ![Riquadro Monitoraggio e gestione](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="f1ac4-229">Modificare il filtro **Ora di inizio** in alto su **2/1/2017** e fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-229">Change the **Start time** filter at the top to **2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="f1ac4-230">Verrà visualizzata una sola finestra di attività, in quanto tra l'ora di inizio (2017-02-01) e l'ora di fine (2017-02-02) della pipeline c'è un solo giorno.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-230">You should see only one activity window as there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span></span> <span data-ttu-id="f1ac4-231">Verificare che lo stato della sezione dati sia **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-231">Confirm that the data slice is in **ready** state.</span></span>

    ![Monitorare la pipeline](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="f1ac4-233">Selezionare la **finestra attività** per visualizzare i dettagli sull'esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-233">Select the **activity window** to see details about the activity run.</span></span> <span data-ttu-id="f1ac4-234">Se si verifica un errore, i dettagli sono visualizzati nel riquadro di destra.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-234">If there is an error, you see details about it in the right pane.</span></span>

### <a name="verify-the-results"></a><span data-ttu-id="f1ac4-235">Verificare i risultati</span><span class="sxs-lookup"><span data-stu-id="f1ac4-235">Verify the results</span></span>

1. <span data-ttu-id="f1ac4-236">Avviare **Jupyter Notebook** per il cluster Spark HDInsight accedendo a: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="f1ac4-237">È possibile anche avviare il dashboard del cluster per il cluster Spark HDInsight e quindi avviare **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="f1ac4-238">Fare clic su **Nuovo** -> **PySpark** per avviare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-238">Click **New** -> **PySpark** to start a new notebook.</span></span>

    ![Nuovo notebook Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="f1ac4-240">Eseguire il comando seguente copiando e incollando il testo e premendo **MAIUSC + INVIO** alla fine della seconda istruzione.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-240">Run the following command by copy/pasting the text and pressing **SHIFT + ENTER** at the end of the second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="f1ac4-241">Verificare che i dati della tabella hvac siano visibili:</span><span class="sxs-lookup"><span data-stu-id="f1ac4-241">Confirm that you see the data from the hvac table:</span></span>  

    ![Risultati della query Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="f1ac4-243">Per informazioni dettagliate, vedere la sezione [Eseguire una query SQL Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="f1ac4-244">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="f1ac4-244">Troubleshooting</span></span>
<span data-ttu-id="f1ac4-245">Poiché **getDebugInfo** è impostato su **Sempre**, è possibile vedere una sottocartella **log** nella cartella **pyFiles** nel contenitore BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-245">Since you set **getDebugInfo** to **Always**, you see a **log** subfolder in the **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="f1ac4-246">Il file di log nella cartella di registro offre dettagli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-246">The log file in the log folder provides additional details.</span></span> <span data-ttu-id="f1ac4-247">Tale file è particolarmente utile quando si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="f1ac4-248">In un ambiente di produzione può risultare utile impostarlo su **Errore**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-248">In a production environment, you may want to set it to **Failure**.</span></span>

<span data-ttu-id="f1ac4-249">Per la risoluzione del problema, eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f1ac4-249">For further troubleshooting, do the following steps:</span></span>


1. <span data-ttu-id="f1ac4-250">Accedere a `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-250">Navigate to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Applicazione interfaccia utente di Yarn](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="f1ac4-252">Fare clic su **Log** per uno dei tentativi di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-252">Click **Logs** for one of the run attempts.</span></span>

    ![Pagina Applicazione](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="f1ac4-254">Nella pagina del log dovrebbero essere visualizzate informazioni aggiuntive sull'errore.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-254">You should see additional error information in the log page.</span></span>

    ![Errore log](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="f1ac4-256">Le sezioni seguenti contengono informazioni sulle entità di Data Factory e sull'uso del cluster Apache Spark e dell'attività di Spark nella data factory.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-256">The following sections provide information about Data Factory entities to use Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="f1ac4-257">Proprietà dell'attività Spark</span><span class="sxs-lookup"><span data-stu-id="f1ac4-257">Spark activity properties</span></span>
<span data-ttu-id="f1ac4-258">Di seguito è riportata la definizione JSON di esempio di una pipeline con attività Spark:</span><span class="sxs-lookup"><span data-stu-id="f1ac4-258">Here is the sample JSON definition of a pipeline with Spark Activity:</span></span>    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes the Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="f1ac4-259">La tabella seguente fornisce le descrizioni delle proprietà JSON usate nella definizione JSON:</span><span class="sxs-lookup"><span data-stu-id="f1ac4-259">The following table describes the JSON properties used in the JSON definition:</span></span>

| <span data-ttu-id="f1ac4-260">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f1ac4-260">Property</span></span> | <span data-ttu-id="f1ac4-261">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f1ac4-261">Description</span></span> | <span data-ttu-id="f1ac4-262">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="f1ac4-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="f1ac4-263">name</span><span class="sxs-lookup"><span data-stu-id="f1ac4-263">name</span></span> | <span data-ttu-id="f1ac4-264">Nome dell'attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-264">Name of the activity in the pipeline.</span></span> | <span data-ttu-id="f1ac4-265">Sì</span><span class="sxs-lookup"><span data-stu-id="f1ac4-265">Yes</span></span> |
| <span data-ttu-id="f1ac4-266">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f1ac4-266">description</span></span> | <span data-ttu-id="f1ac4-267">Testo che descrive l'attività.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-267">Text describing what the activity does.</span></span> | <span data-ttu-id="f1ac4-268">No</span><span class="sxs-lookup"><span data-stu-id="f1ac4-268">No</span></span> |
| <span data-ttu-id="f1ac4-269">type</span><span class="sxs-lookup"><span data-stu-id="f1ac4-269">type</span></span> | <span data-ttu-id="f1ac4-270">Questa proprietà deve essere impostata su HDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-270">This property must be set to HDInsightSpark.</span></span> | <span data-ttu-id="f1ac4-271">Sì</span><span class="sxs-lookup"><span data-stu-id="f1ac4-271">Yes</span></span> |
| <span data-ttu-id="f1ac4-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f1ac4-272">linkedServiceName</span></span> | <span data-ttu-id="f1ac4-273">Riferimento a un servizio collegato HDInsight in cui viene eseguito il programma Spark.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-273">Name of the HDInsight linked service on which the Spark program runs.</span></span> | <span data-ttu-id="f1ac4-274">Sì</span><span class="sxs-lookup"><span data-stu-id="f1ac4-274">Yes</span></span> |
| <span data-ttu-id="f1ac4-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="f1ac4-275">rootPath</span></span> | <span data-ttu-id="f1ac4-276">Contenitore BLOB di Azure e cartella che contiene il file Spark.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-276">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="f1ac4-277">Il nome del file distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-277">The file name is case-sensitive.</span></span> | <span data-ttu-id="f1ac4-278">Sì</span><span class="sxs-lookup"><span data-stu-id="f1ac4-278">Yes</span></span> |
| <span data-ttu-id="f1ac4-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="f1ac4-279">entryFilePath</span></span> | <span data-ttu-id="f1ac4-280">Percorso relativo alla cartella radice del pacchetto/codice Spark.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-280">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="f1ac4-281">Sì</span><span class="sxs-lookup"><span data-stu-id="f1ac4-281">Yes</span></span> |
| <span data-ttu-id="f1ac4-282">className</span><span class="sxs-lookup"><span data-stu-id="f1ac4-282">className</span></span> | <span data-ttu-id="f1ac4-283">Classe principale Java/Spark dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f1ac4-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="f1ac4-284">No</span><span class="sxs-lookup"><span data-stu-id="f1ac4-284">No</span></span> |
| <span data-ttu-id="f1ac4-285">arguments</span><span class="sxs-lookup"><span data-stu-id="f1ac4-285">arguments</span></span> | <span data-ttu-id="f1ac4-286">Elenco di argomenti della riga di comando del programma Spark.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-286">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="f1ac4-287">No</span><span class="sxs-lookup"><span data-stu-id="f1ac4-287">No</span></span> |
| <span data-ttu-id="f1ac4-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="f1ac4-288">proxyUser</span></span> | <span data-ttu-id="f1ac4-289">Account utente da rappresentare per eseguire il programma Spark</span><span class="sxs-lookup"><span data-stu-id="f1ac4-289">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="f1ac4-290">No</span><span class="sxs-lookup"><span data-stu-id="f1ac4-290">No</span></span> |
| <span data-ttu-id="f1ac4-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="f1ac4-291">sparkConfig</span></span> | <span data-ttu-id="f1ac4-292">Specificare i valori delle proprietà di configurazione di Spark elencati nell'argomento: [Configurazione di SparK: proprietà dell'applicazione](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="f1ac4-292">Specify values for Spark configuration properties listed in the topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="f1ac4-293">No</span><span class="sxs-lookup"><span data-stu-id="f1ac4-293">No</span></span> |
| <span data-ttu-id="f1ac4-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="f1ac4-294">getDebugInfo</span></span> | <span data-ttu-id="f1ac4-295">Specifica quando i file di log di Spark vengono copiati nell'archiviazione di Azure usata dal cluster HDInsight (o) specificata da sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-295">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="f1ac4-296">Valori consentiti: None, Always o Failure.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="f1ac4-297">Valore predefinito: None.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-297">Default value: None.</span></span> | <span data-ttu-id="f1ac4-298">No</span><span class="sxs-lookup"><span data-stu-id="f1ac4-298">No</span></span> |
| <span data-ttu-id="f1ac4-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="f1ac4-299">sparkJobLinkedService</span></span> | <span data-ttu-id="f1ac4-300">Il servizio collegato di archiviazione di Azure che contiene il file di processo, le dipendenze e i log di Spark.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-300">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="f1ac4-301">Se non si specifica un valore per questa proprietà, viene usato lo spazio di archiviazione associato al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-301">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="f1ac4-302">No</span><span class="sxs-lookup"><span data-stu-id="f1ac4-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="f1ac4-303">Struttura di cartelle</span><span class="sxs-lookup"><span data-stu-id="f1ac4-303">Folder structure</span></span>
<span data-ttu-id="f1ac4-304">L'attività Spark non supporta uno script inline come invece fanno le attività Pig e Hive.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-304">The Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="f1ac4-305">I processi Spark sono anche più estendibili dei processi Pig/Hive.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="f1ac4-306">Per i processi Spark è possibile offrire più dipendenze, ad esempio pacchetti jar (posizionati in CLASSPATH di java), file python (posizionati in PYTHONPATH) e qualsiasi altro file.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="f1ac4-307">Creare la struttura seguente di cartelle nell'archivio BLOB di Azure a cui fa riferimento il servizio collegato HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-307">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span></span> <span data-ttu-id="f1ac4-308">Caricare i file dipendenti nelle sottocartelle appropriate all'interno della cartella radice rappresentata da **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-308">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="f1ac4-309">Ad esempio, caricare i file python nella sottocartella pyFiles e i file jar nella sottocartella jars della cartella radice.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-309">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span></span> <span data-ttu-id="f1ac4-310">In fase di esecuzione, il servizio Data Factory prevede la struttura di cartelle seguente nell'archivio BLOB di Azure:</span><span class="sxs-lookup"><span data-stu-id="f1ac4-310">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span></span>     

| <span data-ttu-id="f1ac4-311">Path</span><span class="sxs-lookup"><span data-stu-id="f1ac4-311">Path</span></span> | <span data-ttu-id="f1ac4-312">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f1ac4-312">Description</span></span> | <span data-ttu-id="f1ac4-313">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="f1ac4-313">Required</span></span> | <span data-ttu-id="f1ac4-314">Tipo</span><span class="sxs-lookup"><span data-stu-id="f1ac4-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="f1ac4-315">.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-315">.</span></span> | <span data-ttu-id="f1ac4-316">Percorso radice del processo Spark nel servizio collegato di archiviazione</span><span class="sxs-lookup"><span data-stu-id="f1ac4-316">The root path of the Spark job in the storage linked service</span></span>  | <span data-ttu-id="f1ac4-317">Sì</span><span class="sxs-lookup"><span data-stu-id="f1ac4-317">Yes</span></span> | <span data-ttu-id="f1ac4-318">Cartella</span><span class="sxs-lookup"><span data-stu-id="f1ac4-318">Folder</span></span> |
| <span data-ttu-id="f1ac4-319">&lt;definito dall'utente &gt;</span><span class="sxs-lookup"><span data-stu-id="f1ac4-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="f1ac4-320">Percorso che punta al file di ingresso del processo Spark</span><span class="sxs-lookup"><span data-stu-id="f1ac4-320">The path pointing to the entry file of the Spark job</span></span> | <span data-ttu-id="f1ac4-321">Sì</span><span class="sxs-lookup"><span data-stu-id="f1ac4-321">Yes</span></span> | <span data-ttu-id="f1ac4-322">File</span><span class="sxs-lookup"><span data-stu-id="f1ac4-322">File</span></span> |
| <span data-ttu-id="f1ac4-323">./jars</span><span class="sxs-lookup"><span data-stu-id="f1ac4-323">./jars</span></span> | <span data-ttu-id="f1ac4-324">Tutti i file in questa cartella vengono caricati e inseriti nel classpath java del cluster</span><span class="sxs-lookup"><span data-stu-id="f1ac4-324">All files under this folder are uploaded and placed on the java classpath of the cluster</span></span> | <span data-ttu-id="f1ac4-325">No</span><span class="sxs-lookup"><span data-stu-id="f1ac4-325">No</span></span> | <span data-ttu-id="f1ac4-326">Cartella</span><span class="sxs-lookup"><span data-stu-id="f1ac4-326">Folder</span></span> |
| <span data-ttu-id="f1ac4-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="f1ac4-327">./pyFiles</span></span> | <span data-ttu-id="f1ac4-328">Tutti i file in questa cartella vengono caricati e inseriti nel PYTHONPATH del cluster</span><span class="sxs-lookup"><span data-stu-id="f1ac4-328">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span></span> | <span data-ttu-id="f1ac4-329">No</span><span class="sxs-lookup"><span data-stu-id="f1ac4-329">No</span></span> | <span data-ttu-id="f1ac4-330">Cartella</span><span class="sxs-lookup"><span data-stu-id="f1ac4-330">Folder</span></span> |
| <span data-ttu-id="f1ac4-331">./files</span><span class="sxs-lookup"><span data-stu-id="f1ac4-331">./files</span></span> | <span data-ttu-id="f1ac4-332">Tutti i file in questa cartella vengono caricati e inseriti nella directory di lavoro executor</span><span class="sxs-lookup"><span data-stu-id="f1ac4-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="f1ac4-333">No</span><span class="sxs-lookup"><span data-stu-id="f1ac4-333">No</span></span> | <span data-ttu-id="f1ac4-334">Cartella</span><span class="sxs-lookup"><span data-stu-id="f1ac4-334">Folder</span></span> |
| <span data-ttu-id="f1ac4-335">./archives</span><span class="sxs-lookup"><span data-stu-id="f1ac4-335">./archives</span></span> | <span data-ttu-id="f1ac4-336">Tutti i file in questa cartella sono decompressi</span><span class="sxs-lookup"><span data-stu-id="f1ac4-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="f1ac4-337">No</span><span class="sxs-lookup"><span data-stu-id="f1ac4-337">No</span></span> | <span data-ttu-id="f1ac4-338">Cartella</span><span class="sxs-lookup"><span data-stu-id="f1ac4-338">Folder</span></span> |
| <span data-ttu-id="f1ac4-339">./logs</span><span class="sxs-lookup"><span data-stu-id="f1ac4-339">./logs</span></span> | <span data-ttu-id="f1ac4-340">Cartella in cui sono archiviati i log del cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-340">The folder where logs from the Spark cluster are stored.</span></span>| <span data-ttu-id="f1ac4-341">No</span><span class="sxs-lookup"><span data-stu-id="f1ac4-341">No</span></span> | <span data-ttu-id="f1ac4-342">Cartella</span><span class="sxs-lookup"><span data-stu-id="f1ac4-342">Folder</span></span> |

<span data-ttu-id="f1ac4-343">Di seguito è riportato un esempio per una risorsa di archiviazione che contiene due file di processo Spark nell'archivio BLOB di Azure a cui fa riferimento il servizio collegato HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1ac4-343">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span></span>

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
