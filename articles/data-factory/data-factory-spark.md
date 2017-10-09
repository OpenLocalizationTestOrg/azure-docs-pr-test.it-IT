---
title: aaaInvoke Spark programmi da Data Factory di Azure | Documenti Microsoft
description: "Informazioni su come i programmi di Spark tooinvoke da una factory di dati di Azure usando hello attività MapReduce."
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
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="2a3c4-103">Chiamare i programmi Spark dalle pipeline Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2a3c4-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="2a3c4-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="2a3c4-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="2a3c4-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="2a3c4-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="2a3c4-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="2a3c4-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="2a3c4-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="2a3c4-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="2a3c4-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="2a3c4-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="2a3c4-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2a3c4-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="2a3c4-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2a3c4-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="2a3c4-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="2a3c4-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="2a3c4-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2a3c4-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="2a3c4-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="2a3c4-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="2a3c4-114">Introduzione</span><span class="sxs-lookup"><span data-stu-id="2a3c4-114">Introduction</span></span>
<span data-ttu-id="2a3c4-115">Attività Spark è uno dei hello [le attività di trasformazione dati](data-factory-data-transformation-activities.md) supportati da Data Factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-115">Spark Activity is one of hello [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="2a3c4-116">Questa attività esegue hello specificato programma Spark sul cluster Apache Spark in HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-116">This activity runs hello specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="2a3c4-117">L'attività Spark non supporta i cluster Spark HDInsight che usano Azure Data Lake Store come risorsa di archiviazione primaria.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="2a3c4-118">L'attività Spark supporta solo cluster Spark HDInsight esistenti (personalizzati).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="2a3c4-119">Non supporta un servizio collegato HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="2a3c4-120">Procedura dettagliata: creare una pipeline con attività Spark</span><span class="sxs-lookup"><span data-stu-id="2a3c4-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="2a3c4-121">Ecco i passaggi tipici di hello toocreate una pipeline di Data Factory con un'attività di Spark.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-121">Here are hello typical steps toocreate a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="2a3c4-122">Creare una data factory.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-122">Create a data factory.</span></span>
2. <span data-ttu-id="2a3c4-123">Creare un toolink di servizio collegato di archiviazione Azure l'archiviazione di Azure associata con la data factory di toohello cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-123">Create an Azure Storage linked service toolink your Azure storage that is associated with your HDInsight Spark cluster toohello data factory.</span></span>     
2. <span data-ttu-id="2a3c4-124">Creare un toolink di servizio collegato di Azure HDInsight cluster Apache Spark in data factory di Azure HDInsight toohello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-124">Create an Azure HDInsight linked service toolink your Apache Spark cluster in Azure HDInsight toohello data factory.</span></span>
3. <span data-ttu-id="2a3c4-125">Creare un set di dati che fa riferimento il servizio di archiviazione di Azure collegati toohello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-125">Create a dataset that refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="2a3c4-126">Attualmente, è necessario specificare un set di dati di output per un'attività anche se non viene prodotto alcun output.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="2a3c4-127">Creare una pipeline con attività Spark che fa riferimento a servizio collegato di HDInsight toohello creato nel #2.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-127">Create a pipeline with Spark activity that refers toohello HDInsight linked service created in #2.</span></span> <span data-ttu-id="2a3c4-128">attività Hello è configurato con dataset hello creato nel passaggio precedente di hello come un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-128">hello activity is configured with hello dataset you created in hello previous step as an output dataset.</span></span> <span data-ttu-id="2a3c4-129">set di dati output hello è quali unità hello pianificazione (oraria, giornaliera, e così via.).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-129">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="2a3c4-130">Pertanto, è necessario specificare il set di dati di hello output anche se l'attività hello non produce un output molto.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-130">Therefore, you must specify hello output dataset even though hello activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2a3c4-131">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2a3c4-131">Prerequisites</span></span>
1. <span data-ttu-id="2a3c4-132">Crea un **generico Account di archiviazione di Azure** seguendo le istruzioni riportate in questa procedura dettagliata hello: [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-132">Create a **general-purpose Azure Storage Account** by following instructions in hello walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="2a3c4-133">Crea un **cluster Apache Spark in Azure HDInsight** seguendo le istruzioni riportate nell'esercitazione hello: [cluster creare Apache Spark in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in hello tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="2a3c4-134">Associare l'account di archiviazione di Azure hello creato nel passaggio &#1; con questo cluster.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-134">Associate hello Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="2a3c4-135">Scaricare ed esaminare i file di script python hello **test.py** disponibile all'indirizzo: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-135">Download and review hello python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="2a3c4-136">Caricare **test.py** toohello **pyFiles** cartella hello **adfspark** contenitore nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-136">Upload **test.py** toohello **pyFiles** folder in hello **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="2a3c4-137">Creare un contenitore di hello e cartella hello se non esistono.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-137">Create hello container and hello folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="2a3c4-138">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="2a3c4-138">Create data factory</span></span>
<span data-ttu-id="2a3c4-139">Iniziamo con la creazione di data factory di hello in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-139">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="2a3c4-140">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2a3c4-141">Fare clic su **NEW** scegliere dal menu a sinistra, hello **dati + Analitica**, fare clic su **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-141">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="2a3c4-142">In hello **nuova data factory** pannello immettere **SparkDF** per hello Name.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-142">In hello **New data factory** blade, enter **SparkDF** for hello Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2a3c4-143">nome Hello di hello Azure data factory deve essere **univoco globale**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-143">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="2a3c4-144">Se viene visualizzato l'errore hello: **"SparkDF" nome della Data factory non è disponibile**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-144">If you see hello error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="2a3c4-145">Modificare il nome di hello della data factory di hello (ad esempio, yournameSparkDFdate e provare a creare di nuovo.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-145">Change hello name of hello data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="2a3c4-146">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="2a3c4-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="2a3c4-147">Seleziona hello **sottoscrizione di Azure** in cui si desidera hello data factory toobe creato.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-147">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="2a3c4-148">Selezionare un **gruppo di risorse** di Azure esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="2a3c4-149">Selezionare **toodashboard Pin** opzione.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-149">Select **Pin toodashboard** option.</span></span>  
6. <span data-ttu-id="2a3c4-150">Fare clic su **crea** su hello **nuova data factory** blade.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-150">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2a3c4-151">le istanze di Data Factory toocreate, è necessario essere un membro di hello [Data Factory collaboratore](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) ruolo a livello di gruppo di risorse di sottoscrizione/hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-151">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
7. <span data-ttu-id="2a3c4-152">Vedrai data factory di hello viene creato nel hello **dashboard** di hello portale di Azure come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2a3c4-152">You see hello data factory being created in hello **dashboard** of hello Azure portal as follows:</span></span>   
8. <span data-ttu-id="2a3c4-153">Dopo aver hello data factory è stata creata correttamente, vedrai hello data factory pagina nella quale viene hello contenuto di data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-153">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span> <span data-ttu-id="2a3c4-154">Se non è possibile visualizzare pagina factory di hello dati, fare clic su riquadro hello per la data factory di dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-154">If you do not see hello data factory page, click hello tile for your data factory on hello dashboard.</span></span>

    ![Pannello Data factory](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="2a3c4-156">Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="2a3c4-156">Create linked services</span></span>
<span data-ttu-id="2a3c4-157">In questo passaggio, creare due servizi collegati, una toolink la data factory di tooyour cluster Spark e hello altri toolink la data factory tooyour di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-157">In this step, you create two linked services, one toolink your Spark cluster tooyour data factory, and hello other toolink your Azure storage tooyour data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="2a3c4-158">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2a3c4-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="2a3c4-159">In questo passaggio si collega la data factory tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-159">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="2a3c4-160">Un set di dati create in un passaggio più avanti in questa procedura dettagliata fa riferimento a servizio toothis collegato.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-160">A dataset you create in a step later in this walkthrough refers toothis linked service.</span></span> <span data-ttu-id="2a3c4-161">servizio collegato di HDInsight definito nel passaggio successivo hello Hello servizio toothis collegato fa riferimento troppo.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-161">hello HDInsight linked service that you define in hello next step refers toothis linked service too.</span></span>  

1. <span data-ttu-id="2a3c4-162">Fare clic su **autore e distribuire** su hello **Data Factory** pannello per il data factory.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-162">Click **Author and deploy** on hello **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="2a3c4-163">Dovrebbe essere hello Editor delle Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-163">You should see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="2a3c4-164">Fare clic su **Nuovo archivio dati** e scegliere **Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nuovo archivio dati - Archiviazione di Azure - Menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="2a3c4-166">Dovrebbe essere hello **script JSON** per la creazione di una risorsa di archiviazione di Azure il servizio nell'editor di hello collegato.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-166">You should see hello **JSON script** for creating an Azure Storage linked service in hello editor.</span></span>

   ![Servizio collegato Archiviazione di Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="2a3c4-168">Sostituire **nome account** e **chiave dell'account** con chiave hello di accesso e sul nome dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-168">Replace **account name** and **account key** with hello name and access key of your Azure storage account.</span></span> <span data-ttu-id="2a3c4-169">toolearn come accedere a tooget lo spazio di archiviazione della chiave, vedere informazioni come tooview, copiare e rigenerare archiviazione accedere alle chiavi in hello [gestire account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-169">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="2a3c4-170">toodeploy hello servizio collegato, fare clic su **Distribuisci** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-170">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="2a3c4-171">Dopo aver hello servizio collegato viene distribuito correttamente, hello **bozza 1** dovrebbe scomparire una finestra e viene visualizzato **AzureStorageLinkedService** nella visualizzazione ad albero di hello a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-171">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="2a3c4-172">Creare un servizio collegato HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a3c4-172">Create HDInsight linked service</span></span>
<span data-ttu-id="2a3c4-173">In questo passaggio è creare toolink di servizio collegato di Azure HDInsight la data factory di toohello cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-173">In this step, you create Azure HDInsight linked service toolink your HDInsight Spark cluster toohello data factory.</span></span> <span data-ttu-id="2a3c4-174">cluster HDInsight Hello è programma Spark di hello toorun utilizzati specificato nell'attività di Spark hello della pipeline hello in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-174">hello HDInsight cluster is used toorun hello Spark program specified in hello Spark activity of hello pipeline in this sample.</span></span>  

1. <span data-ttu-id="2a3c4-175">Fare clic su **... Ulteriori** sulla barra degli strumenti hello, fare clic su **nuovo calcolo**, quindi fare clic su **cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-175">Click **... More** on hello toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Creare un servizio collegato HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="2a3c4-177">Copiare e incollare hello seguente frammento di codice toohello **bozza 1** finestra.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-177">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="2a3c4-178">Nell'editor di JSON hello, hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2a3c4-178">In hello JSON editor, do hello following steps:</span></span>
    1. <span data-ttu-id="2a3c4-179">Specificare hello **URI** per HDInsight Spark hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-179">Specify hello **URI** for hello HDInsight Spark cluster.</span></span> <span data-ttu-id="2a3c4-180">Ad esempio: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="2a3c4-181">Specificare il nome di hello di hello **utente** chi ha cluster Spark toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-181">Specify hello name of hello **user** who has access toohello Spark cluster.</span></span>
    3. <span data-ttu-id="2a3c4-182">Specificare hello **password** per utente.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-182">Specify hello **password** for user.</span></span>
    4. <span data-ttu-id="2a3c4-183">Specificare hello **servizio collegato di archiviazione di Azure** associato hello cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-183">Specify hello **Azure Storage linked service** that is associated with hello HDInsight Spark cluster.</span></span> <span data-ttu-id="2a3c4-184">Nell'esempio è: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

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
    > - <span data-ttu-id="2a3c4-185">L'attività Spark non supporta i cluster Spark HDInsight che usano Azure Data Lake Store come risorsa di archiviazione primaria.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="2a3c4-186">L'attività Spark supporta solo cluster Spark HDInsight esistenti (personalizzati).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="2a3c4-187">Non supporta un servizio collegato HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="2a3c4-188">Vedere [servizio collegato di HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) per informazioni dettagliate su hello servizio collegato di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about hello HDInsight linked service.</span></span>
3.  <span data-ttu-id="2a3c4-189">toodeploy hello servizio collegato, fare clic su **Distribuisci** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-189">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="2a3c4-190">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="2a3c4-190">Create output dataset</span></span>
<span data-ttu-id="2a3c4-191">set di dati output hello è quali unità hello pianificazione (oraria, giornaliera, e così via.).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-191">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="2a3c4-192">Pertanto, è necessario specificare un set di dati di output per l'attività di spark hello nella pipeline di hello, anche se l'attività hello effettivamente generato alcun output.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-192">Therefore, you must specify an output dataset for hello spark activity in hello pipeline even though hello activity does not really produce any output.</span></span> <span data-ttu-id="2a3c4-193">Un set di dati di input per l'attività hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-193">Specifying an input dataset for hello activity is optional.</span></span>

1. <span data-ttu-id="2a3c4-194">In hello **Editor delle Data Factory**, fare clic su **... Ulteriori** nella barra dei comandi di hello, fare clic su **nuovo set di dati**e selezionare **archiviazione Blob di Azure**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-194">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="2a3c4-195">Copiare e incollare hello successiva finestra di frammento toohello bozza-1.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-195">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="2a3c4-196">frammento di codice JSON Hello definisce un set di dati denominato **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-196">hello JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="2a3c4-197">Inoltre, si specifica che i risultati di hello vengono archiviati nel contenitore blob hello chiamato **adfspark** e cartella hello denominata **pyFiles/output**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-197">In addition, you specify that hello results are stored in hello blob container called **adfspark** and hello folder called **pyFiles/output**.</span></span> <span data-ttu-id="2a3c4-198">Come accennato in precedenza, questo set di dati è un set di dati fittizio.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="2a3c4-199">programma di Spark Hello in questo esempio non produce alcun output.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-199">hello Spark program in this example does not produce any output.</span></span> <span data-ttu-id="2a3c4-200">Hello **disponibilità** sezione specifica di tale set di dati di output di hello viene prodotta ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-200">hello **availability** section specifies that hello output dataset is produced daily.</span></span>  

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
3. <span data-ttu-id="2a3c4-201">toodeploy hello set di dati, fare clic su **Distribuisci** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-201">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="2a3c4-202">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="2a3c4-202">Create pipeline</span></span>
<span data-ttu-id="2a3c4-203">In questo passaggio viene creata una pipeline con un'**attività HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="2a3c4-204">Set di dati di output è attualmente, quali unità hello pianificazione, pertanto è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-204">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="2a3c4-205">Se l'attività hello non accetta alcun input, è possibile ignorare i set di dati input hello creazione.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-205">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="2a3c4-206">Pertanto in questo esempio non viene specificato alcun set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="2a3c4-207">In hello **Editor delle Data Factory**, fare clic su **... Ulteriori** hello barra dei comandi e quindi fare clic su **nuova pipeline**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-207">In hello **Data Factory Editor**, click **… More** on hello command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="2a3c4-208">Sostituire script hello nella finestra di hello bozza-1 con hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="2a3c4-208">Replace hello script in hello Draft-1 window with hello following script:</span></span>

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
    <span data-ttu-id="2a3c4-209">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="2a3c4-209">Note hello following points:</span></span>
    - <span data-ttu-id="2a3c4-210">Hello **tipo** impostata troppo**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-210">hello **type** property is set too**HDInsightSpark**.</span></span>
    - <span data-ttu-id="2a3c4-211">Hello **rootPath** è troppo**adfspark\\pyFiles** dove adfspark è il contenitore di Blob di Azure hello e pyFiles è cartella correttamente in tale contenitore.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-211">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="2a3c4-212">In questo esempio hello archiviazione Blob di Azure è hello uno associato al cluster Spark hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-212">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="2a3c4-213">È possibile caricare tooa file hello archiviazione di Azure diversi.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-213">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="2a3c4-214">In tal caso, creare un toolink di servizio collegato di archiviazione di Azure che data factory toohello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-214">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="2a3c4-215">Quindi, specificare il nome di hello del servizio hello collegato come valore per hello **sparkJobLinkedService** proprietà.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-215">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="2a3c4-216">Vedere [le proprietà dell'attività di Spark](#spark-activity-properties) per informazioni dettagliate su questa proprietà e altre proprietà supportate dall'attività Spark hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>  
    - <span data-ttu-id="2a3c4-217">Hello **entryFilePath** è impostato toohello **test.py**, ossia file python hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-217">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span>
    - <span data-ttu-id="2a3c4-218">Hello **getDebugInfo** impostata troppo**sempre**, ovvero i file di log hello vengono sempre generati (esito positivo o negativo).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-218">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="2a3c4-219">È consigliabile non impostare questa proprietà troppo`Always` in un ambiente di produzione a meno che non si sta risolvendo un problema.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-219">We recommend that you do not set this property too`Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="2a3c4-220">Hello **restituisce** sezione ha un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-220">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="2a3c4-221">Anche se il programma di spark hello non genera alcun output, è necessario specificare un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-221">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="2a3c4-222">pianificazione di hello unità per set di dati di output Hello per pipeline hello (oraria, giornaliera, e così via.).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-222">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="2a3c4-223">Per informazioni dettagliate sulle proprietà hello è supportata dall'attività Spark, vedere [nascita le proprietà dell'attività](#spark-activity-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-223">For details about hello properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="2a3c4-224">pipeline di hello toodeploy, fare clic su **Distribuisci** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-224">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="2a3c4-225">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="2a3c4-225">Monitor pipeline</span></span>
1. <span data-ttu-id="2a3c4-226">Fare clic su **X** tooclose Editor delle Data Factory pannelli e toonavigate nuovamente home page di toohello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-226">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory home page.</span></span> <span data-ttu-id="2a3c4-227">Fare clic su **monitoraggio e gestione** hello toolaunch monitoraggio dell'applicazione in un'altra scheda.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-227">Click **Monitor and Manage** toolaunch hello monitoring application in another tab.</span></span>

    ![Riquadro Monitoraggio e gestione](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="2a3c4-229">Hello modifica **ora di inizio** filtro nella parte superiore di hello troppo**1/2/2017**, fare clic su **applica**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-229">Change hello **Start time** filter at hello top too**2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="2a3c4-230">Verrà visualizzato solo una finestra di attività perché non esiste un solo giorno tra hello (2017-02-01) di inizio e di fine (2017-02-02) della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-230">You should see only one activity window as there is only one day between hello start (2017-02-01) and end times (2017-02-02) of hello pipeline.</span></span> <span data-ttu-id="2a3c4-231">Verificare che la sezione dati hello viene **pronto** stato.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-231">Confirm that hello data slice is in **ready** state.</span></span>

    ![Pipeline hello monitoraggio](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="2a3c4-233">Seleziona hello **finestra attività** toosee dettagli sull'esecuzione dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-233">Select hello **activity window** toosee details about hello activity run.</span></span> <span data-ttu-id="2a3c4-234">Se si verifica un errore, si noterà dettagli nel riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-234">If there is an error, you see details about it in hello right pane.</span></span>

### <a name="verify-hello-results"></a><span data-ttu-id="2a3c4-235">Verificare i risultati di hello</span><span class="sxs-lookup"><span data-stu-id="2a3c4-235">Verify hello results</span></span>

1. <span data-ttu-id="2a3c4-236">Avviare **Jupyter Notebook** per il cluster Spark HDInsight accedendo a: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="2a3c4-237">È possibile anche avviare il dashboard del cluster per il cluster Spark HDInsight e quindi avviare **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="2a3c4-238">Fare clic su **New** -> **PySpark** toostart un nuovo blocco appunti.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-238">Click **New** -> **PySpark** toostart a new notebook.</span></span>

    ![Nuovo notebook Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="2a3c4-240">Esecuzione hello il seguente comando copia e Incolla di testo hello e premendo **MAIUSC + INVIO** alla fine di hello della seconda istruzione hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-240">Run hello following command by copy/pasting hello text and pressing **SHIFT + ENTER** at hello end of hello second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="2a3c4-241">Confermare la visualizzazione dei dati hello hello impianto tabella:</span><span class="sxs-lookup"><span data-stu-id="2a3c4-241">Confirm that you see hello data from hello hvac table:</span></span>  

    ![Risultati della query Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="2a3c4-243">Per informazioni dettagliate, vedere la sezione [Eseguire una query SQL Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="2a3c4-244">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="2a3c4-244">Troubleshooting</span></span>
<span data-ttu-id="2a3c4-245">Poiché è impostato **getDebugInfo** troppo**sempre**, vedrai un **log** sottocartella hello **pyFiles** cartella nel contenitore del Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-245">Since you set **getDebugInfo** too**Always**, you see a **log** subfolder in hello **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="2a3c4-246">file di log Hello nella cartella dei log hello fornisce dettagli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-246">hello log file in hello log folder provides additional details.</span></span> <span data-ttu-id="2a3c4-247">Tale file è particolarmente utile quando si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="2a3c4-248">In un ambiente di produzione, è opportuno tooset è troppo**errore**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-248">In a production environment, you may want tooset it too**Failure**.</span></span>

<span data-ttu-id="2a3c4-249">Per un'ulteriore risoluzione dei problemi, hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2a3c4-249">For further troubleshooting, do hello following steps:</span></span>


1. <span data-ttu-id="2a3c4-250">Passare troppo`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-250">Navigate too`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Applicazione interfaccia utente di Yarn](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="2a3c4-252">Fare clic su **registri** per uno di hello eseguire tentativi.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-252">Click **Logs** for one of hello run attempts.</span></span>

    ![Pagina Applicazione](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="2a3c4-254">Informazioni aggiuntive sull'errore nella pagina log hello dovrebbe.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-254">You should see additional error information in hello log page.</span></span>

    ![Errore log](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="2a3c4-256">Hello le sezioni seguenti fornisce informazioni sul Data Factory entità toouse Apache Spark cluster e la data factory di attività Spark.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-256">hello following sections provide information about Data Factory entities toouse Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="2a3c4-257">Proprietà dell'attività Spark</span><span class="sxs-lookup"><span data-stu-id="2a3c4-257">Spark activity properties</span></span>
<span data-ttu-id="2a3c4-258">Ecco definizione JSON di esempio hello di una pipeline con attività Spark:</span><span class="sxs-lookup"><span data-stu-id="2a3c4-258">Here is hello sample JSON definition of a pipeline with Spark Activity:</span></span>    

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
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="2a3c4-259">Hello tabella seguente vengono descritte le proprietà JSON hello utilizzate nella definizione JSON hello:</span><span class="sxs-lookup"><span data-stu-id="2a3c4-259">hello following table describes hello JSON properties used in hello JSON definition:</span></span>

| <span data-ttu-id="2a3c4-260">Proprietà</span><span class="sxs-lookup"><span data-stu-id="2a3c4-260">Property</span></span> | <span data-ttu-id="2a3c4-261">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a3c4-261">Description</span></span> | <span data-ttu-id="2a3c4-262">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2a3c4-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="2a3c4-263">name</span><span class="sxs-lookup"><span data-stu-id="2a3c4-263">name</span></span> | <span data-ttu-id="2a3c4-264">Nome dell'attività hello nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-264">Name of hello activity in hello pipeline.</span></span> | <span data-ttu-id="2a3c4-265">Sì</span><span class="sxs-lookup"><span data-stu-id="2a3c4-265">Yes</span></span> |
| <span data-ttu-id="2a3c4-266">description</span><span class="sxs-lookup"><span data-stu-id="2a3c4-266">description</span></span> | <span data-ttu-id="2a3c4-267">Testo che descrive le attività di hello esegue.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-267">Text describing what hello activity does.</span></span> | <span data-ttu-id="2a3c4-268">No</span><span class="sxs-lookup"><span data-stu-id="2a3c4-268">No</span></span> |
| <span data-ttu-id="2a3c4-269">type</span><span class="sxs-lookup"><span data-stu-id="2a3c4-269">type</span></span> | <span data-ttu-id="2a3c4-270">Questa proprietà deve essere impostata tooHDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-270">This property must be set tooHDInsightSpark.</span></span> | <span data-ttu-id="2a3c4-271">Sì</span><span class="sxs-lookup"><span data-stu-id="2a3c4-271">Yes</span></span> |
| <span data-ttu-id="2a3c4-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="2a3c4-272">linkedServiceName</span></span> | <span data-ttu-id="2a3c4-273">Nome di hello HDInsight collegato del servizio in cui hello Spark programma in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-273">Name of hello HDInsight linked service on which hello Spark program runs.</span></span> | <span data-ttu-id="2a3c4-274">Sì</span><span class="sxs-lookup"><span data-stu-id="2a3c4-274">Yes</span></span> |
| <span data-ttu-id="2a3c4-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="2a3c4-275">rootPath</span></span> | <span data-ttu-id="2a3c4-276">contenitore di Blob di Azure Hello e della cartella che contiene file Spark hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-276">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="2a3c4-277">nome del file Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-277">hello file name is case-sensitive.</span></span> | <span data-ttu-id="2a3c4-278">Sì</span><span class="sxs-lookup"><span data-stu-id="2a3c4-278">Yes</span></span> |
| <span data-ttu-id="2a3c4-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="2a3c4-279">entryFilePath</span></span> | <span data-ttu-id="2a3c4-280">Cartella radice di percorso relativo toohello di hello Spark codice o del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-280">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="2a3c4-281">Sì</span><span class="sxs-lookup"><span data-stu-id="2a3c4-281">Yes</span></span> |
| <span data-ttu-id="2a3c4-282">className</span><span class="sxs-lookup"><span data-stu-id="2a3c4-282">className</span></span> | <span data-ttu-id="2a3c4-283">Classe principale Java/Spark dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="2a3c4-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="2a3c4-284">No</span><span class="sxs-lookup"><span data-stu-id="2a3c4-284">No</span></span> |
| <span data-ttu-id="2a3c4-285">arguments</span><span class="sxs-lookup"><span data-stu-id="2a3c4-285">arguments</span></span> | <span data-ttu-id="2a3c4-286">Un elenco di programmi di Spark toohello gli argomenti della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-286">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="2a3c4-287">No</span><span class="sxs-lookup"><span data-stu-id="2a3c4-287">No</span></span> |
| <span data-ttu-id="2a3c4-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="2a3c4-288">proxyUser</span></span> | <span data-ttu-id="2a3c4-289">programma di Hello utente account tooimpersonate tooexecute hello Spark</span><span class="sxs-lookup"><span data-stu-id="2a3c4-289">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="2a3c4-290">No</span><span class="sxs-lookup"><span data-stu-id="2a3c4-290">No</span></span> |
| <span data-ttu-id="2a3c4-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="2a3c4-291">sparkConfig</span></span> | <span data-ttu-id="2a3c4-292">Specificare i valori per le proprietà di configurazione di Spark elencati nell'argomento hello: [configurazione Spark - proprietà applicazione](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="2a3c4-292">Specify values for Spark configuration properties listed in hello topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="2a3c4-293">No</span><span class="sxs-lookup"><span data-stu-id="2a3c4-293">No</span></span> |
| <span data-ttu-id="2a3c4-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="2a3c4-294">getDebugInfo</span></span> | <span data-ttu-id="2a3c4-295">Specifica quando i file di log Spark hello toohello copiato archiviazione di Azure usati dal cluster HDInsight (o) specificato da sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-295">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="2a3c4-296">Valori consentiti: None, Always o Failure.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="2a3c4-297">Valore predefinito: None.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-297">Default value: None.</span></span> | <span data-ttu-id="2a3c4-298">No</span><span class="sxs-lookup"><span data-stu-id="2a3c4-298">No</span></span> |
| <span data-ttu-id="2a3c4-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="2a3c4-299">sparkJobLinkedService</span></span> | <span data-ttu-id="2a3c4-300">servizio collegato di archiviazione di Azure che contiene i registri, le dipendenze e hello Spark processo file Hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-300">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="2a3c4-301">Se non si specifica un valore per questa proprietà, viene utilizzata l'archiviazione di hello associato al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-301">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="2a3c4-302">No</span><span class="sxs-lookup"><span data-stu-id="2a3c4-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="2a3c4-303">Struttura di cartelle</span><span class="sxs-lookup"><span data-stu-id="2a3c4-303">Folder structure</span></span>
<span data-ttu-id="2a3c4-304">Hello attività Spark non supporta uno script in linea come Pig e Hive attività eseguire.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-304">hello Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="2a3c4-305">I processi Spark sono anche più estendibili dei processi Pig/Hive.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="2a3c4-306">Per i processi di Spark, è possibile fornire più dipendenze, ad esempio file jar di pacchetti (inseriti nel linguaggio hello CLASSPATH), i file di python (posizionati hello PYTHONPATH) e qualsiasi altro file.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in hello java CLASSPATH), python files (placed on hello PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="2a3c4-307">Creare hello seguente struttura di cartelle in hello archiviazione Blob di Azure a cui fa riferimento hello servizio collegato di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-307">Create hello following folder structure in hello Azure Blob storage referenced by hello HDInsight linked service.</span></span> <span data-ttu-id="2a3c4-308">Successivamente, caricare le cartelle di file dipendenti toohello sub appropriato nella cartella radice hello rappresentato da **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-308">Then, upload dependent files toohello appropriate sub folders in hello root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="2a3c4-309">Ad esempio, caricare python file toohello pyFiles sottocartella e file jar toohello JAR sottocartella della cartella radice hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-309">For example, upload python files toohello pyFiles subfolder and jar files toohello jars subfolder of hello root folder.</span></span> <span data-ttu-id="2a3c4-310">In fase di esecuzione, il servizio Data Factory prevede hello seguente struttura di cartelle in hello archiviazione Blob di Azure:</span><span class="sxs-lookup"><span data-stu-id="2a3c4-310">At runtime, Data Factory service expects hello following folder structure in hello Azure Blob storage:</span></span>     

| <span data-ttu-id="2a3c4-311">Path</span><span class="sxs-lookup"><span data-stu-id="2a3c4-311">Path</span></span> | <span data-ttu-id="2a3c4-312">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a3c4-312">Description</span></span> | <span data-ttu-id="2a3c4-313">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2a3c4-313">Required</span></span> | <span data-ttu-id="2a3c4-314">Tipo</span><span class="sxs-lookup"><span data-stu-id="2a3c4-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="2a3c4-315">.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-315">.</span></span> | <span data-ttu-id="2a3c4-316">percorso radice Hello del processo di Spark hello nel servizio di archiviazione collegato hello</span><span class="sxs-lookup"><span data-stu-id="2a3c4-316">hello root path of hello Spark job in hello storage linked service</span></span>    | <span data-ttu-id="2a3c4-317">Sì</span><span class="sxs-lookup"><span data-stu-id="2a3c4-317">Yes</span></span> | <span data-ttu-id="2a3c4-318">Cartella</span><span class="sxs-lookup"><span data-stu-id="2a3c4-318">Folder</span></span> |
| <span data-ttu-id="2a3c4-319">&lt;definito dall'utente &gt;</span><span class="sxs-lookup"><span data-stu-id="2a3c4-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="2a3c4-320">percorso di Hello che fa riferimento il file voce toohello del processo di Spark hello</span><span class="sxs-lookup"><span data-stu-id="2a3c4-320">hello path pointing toohello entry file of hello Spark job</span></span> | <span data-ttu-id="2a3c4-321">Sì</span><span class="sxs-lookup"><span data-stu-id="2a3c4-321">Yes</span></span> | <span data-ttu-id="2a3c4-322">File</span><span class="sxs-lookup"><span data-stu-id="2a3c4-322">File</span></span> |
| <span data-ttu-id="2a3c4-323">./jars</span><span class="sxs-lookup"><span data-stu-id="2a3c4-323">./jars</span></span> | <span data-ttu-id="2a3c4-324">Tutti i file in questa cartella vengono caricati e inseriti in classpath java hello del cluster hello</span><span class="sxs-lookup"><span data-stu-id="2a3c4-324">All files under this folder are uploaded and placed on hello java classpath of hello cluster</span></span> | <span data-ttu-id="2a3c4-325">No</span><span class="sxs-lookup"><span data-stu-id="2a3c4-325">No</span></span> | <span data-ttu-id="2a3c4-326">Cartella</span><span class="sxs-lookup"><span data-stu-id="2a3c4-326">Folder</span></span> |
| <span data-ttu-id="2a3c4-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="2a3c4-327">./pyFiles</span></span> | <span data-ttu-id="2a3c4-328">Tutti i file in questa cartella vengono caricati e inseriti in hello PYTHONPATH del cluster hello</span><span class="sxs-lookup"><span data-stu-id="2a3c4-328">All files under this folder are uploaded and placed on hello PYTHONPATH of hello cluster</span></span> | <span data-ttu-id="2a3c4-329">No</span><span class="sxs-lookup"><span data-stu-id="2a3c4-329">No</span></span> | <span data-ttu-id="2a3c4-330">Cartella</span><span class="sxs-lookup"><span data-stu-id="2a3c4-330">Folder</span></span> |
| <span data-ttu-id="2a3c4-331">./files</span><span class="sxs-lookup"><span data-stu-id="2a3c4-331">./files</span></span> | <span data-ttu-id="2a3c4-332">Tutti i file in questa cartella vengono caricati e inseriti nella directory di lavoro executor</span><span class="sxs-lookup"><span data-stu-id="2a3c4-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="2a3c4-333">No</span><span class="sxs-lookup"><span data-stu-id="2a3c4-333">No</span></span> | <span data-ttu-id="2a3c4-334">Cartella</span><span class="sxs-lookup"><span data-stu-id="2a3c4-334">Folder</span></span> |
| <span data-ttu-id="2a3c4-335">./archives</span><span class="sxs-lookup"><span data-stu-id="2a3c4-335">./archives</span></span> | <span data-ttu-id="2a3c4-336">Tutti i file in questa cartella sono decompressi</span><span class="sxs-lookup"><span data-stu-id="2a3c4-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="2a3c4-337">No</span><span class="sxs-lookup"><span data-stu-id="2a3c4-337">No</span></span> | <span data-ttu-id="2a3c4-338">Cartella</span><span class="sxs-lookup"><span data-stu-id="2a3c4-338">Folder</span></span> |
| <span data-ttu-id="2a3c4-339">./logs</span><span class="sxs-lookup"><span data-stu-id="2a3c4-339">./logs</span></span> | <span data-ttu-id="2a3c4-340">cartella Hello in cui sono archiviati i log da cluster Spark hello.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-340">hello folder where logs from hello Spark cluster are stored.</span></span>| <span data-ttu-id="2a3c4-341">No</span><span class="sxs-lookup"><span data-stu-id="2a3c4-341">No</span></span> | <span data-ttu-id="2a3c4-342">Cartella</span><span class="sxs-lookup"><span data-stu-id="2a3c4-342">Folder</span></span> |

<span data-ttu-id="2a3c4-343">Di seguito è riportato un esempio per una risorsa di archiviazione che contiene due file di processo Spark in hello archiviazione Blob di Azure a cui fa riferimento hello servizio collegato di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a3c4-343">Here is an example for a storage containing two Spark job files in hello Azure Blob Storage referenced by hello HDInsight linked service.</span></span>

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
