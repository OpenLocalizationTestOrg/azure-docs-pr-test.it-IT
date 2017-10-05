---
title: Creare la prima data factory (Visual Studio) | Documentazione Microsoft
description: In questa esercitazione viene creata una pipeline di esempio di Azure Data Factory usando Visual Studio.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 77042219cbe698a33ab9447aa952586772897241
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a><span data-ttu-id="0212f-103">Esercitazione: Creare una data factory con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0212f-103">Tutorial: Create a data factory by using Visual Studio</span></span>
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [<span data-ttu-id="0212f-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0212f-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="0212f-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0212f-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="0212f-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0212f-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="0212f-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0212f-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="0212f-108">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0212f-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="0212f-109">API REST</span><span class="sxs-lookup"><span data-stu-id="0212f-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="0212f-110">Questa esercitazione illustra come creare una data factory di Azure con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0212f-110">This tutorial shows you how to create an Azure data factory by using Visual Studio.</span></span> <span data-ttu-id="0212f-111">Si crea un progetto di Visual Studio usando il modello di progetto DataFactory, si definiscono le entità della data factory (servizi collegati, set di dati e pipeline) in formato JSON e quindi si pubblicano/distribuiscono queste entità nel cloud.</span><span class="sxs-lookup"><span data-stu-id="0212f-111">You create a Visual Studio project using the Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities to the cloud.</span></span> 

<span data-ttu-id="0212f-112">La pipeline in questa esercitazione include un'attività, l'**attività Hive di HDInsight**,</span><span class="sxs-lookup"><span data-stu-id="0212f-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="0212f-113">che esegue uno script Hive in un cluster Azure HDInsight per trasformare i dati di input e generare i dati di output.</span><span class="sxs-lookup"><span data-stu-id="0212f-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="0212f-114">L'esecuzione della pipeline è pianificata una volta al mese tra le ore di inizio e di fine specificate.</span><span class="sxs-lookup"><span data-stu-id="0212f-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="0212f-115">Questa esercitazione non illustra come copiare dati con Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-115">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="0212f-116">Per un'esercitazione su come copiare dati usando Azure Data Factory, vedere [Copiare dati da un archivio BLOB al database SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0212f-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="0212f-117">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="0212f-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="0212f-118">ed è possibile concatenarne due, ovvero eseguire un'attività dopo l'altra, impostando il set di dati di output di un'attività come set di dati di input dell'altra.</span><span class="sxs-lookup"><span data-stu-id="0212f-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="0212f-119">Per altre informazioni, vedere [pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="0212f-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="walkthrough-create-and-publish-data-factory-entities"></a><span data-ttu-id="0212f-120">Procedura dettagliata: Creare e pubblicare le entità della data factory</span><span class="sxs-lookup"><span data-stu-id="0212f-120">Walkthrough: Create and publish Data Factory entities</span></span>
<span data-ttu-id="0212f-121">Di seguito sono elencati i passaggi da eseguire nell'ambito di questa procedura dettagliata:</span><span class="sxs-lookup"><span data-stu-id="0212f-121">Here are the steps you perform as part of this walkthrough:</span></span>

1. <span data-ttu-id="0212f-122">Creare due servizi collegati, **AzureStorageLinkedService1** e **HDInsightOnDemandLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="0212f-122">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span></span> 
   
    <span data-ttu-id="0212f-123">In questa esercitazione, i dati sia di input che di output per l'attività Hive si trovano nello stesso archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-123">In this tutorial, both input and output data for the hive activity are in the same Azure Blob Storage.</span></span> <span data-ttu-id="0212f-124">Per elaborare i dati di input esistenti e generare i dati di output si usa un cluster HDInsight su richiesta,</span><span class="sxs-lookup"><span data-stu-id="0212f-124">You use an on-demand HDInsight cluster to process existing input data to produce output data.</span></span> <span data-ttu-id="0212f-125">che viene creato automaticamente da Azure Data Factory in fase di esecuzione quando i dati di input sono pronti per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-125">The on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when the input data is ready to be processed.</span></span> <span data-ttu-id="0212f-126">È necessario collegare i calcoli e gli archivi dati alla data factory affinché il servizio Data Factory possa connettervisi in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0212f-126">You need to link your data stores or computes to your data factory so that the Data Factory service can connect to them at runtime.</span></span> <span data-ttu-id="0212f-127">Di conseguenza, si collega l'account di archiviazione di Azure alla data factory usando AzureStorageLinkedService1 e si collega un cluster HDInsight su richiesta usando HDInsightOnDemandLinkedService1.</span><span class="sxs-lookup"><span data-stu-id="0212f-127">Therefore, you link your Azure Storage Account to the data factory by using the AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using the HDInsightOnDemandLinkedService1.</span></span> <span data-ttu-id="0212f-128">Durante la pubblicazione, si specifica il nome della data factory da creare o di una data factory esistente.</span><span class="sxs-lookup"><span data-stu-id="0212f-128">When publishing, you specify the name for the data factory to be created or an existing data factory.</span></span>  
2. <span data-ttu-id="0212f-129">Creare due set di dati, **InputDataset** e **OutputDataset**, che rappresentano i dati di input e di output archiviati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-129">Create two datasets: **InputDataset** and **OutputDataset**, which represent the input/output data that is stored in the Azure blob storage.</span></span> 
   
    <span data-ttu-id="0212f-130">Le definizioni dei set di dati fanno riferimento al servizio collegato Archiviazione di Azure creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="0212f-130">These dataset definitions refer to the Azure Storage linked service you created in the previous step.</span></span> <span data-ttu-id="0212f-131">Per InputDataset, si specificano il contenitore BLOB (adfgetstarted) e la cartella (inputdata) che contiene un BLOB con i dati di input.</span><span class="sxs-lookup"><span data-stu-id="0212f-131">For the InputDataset, you specify the blob container (adfgetstarted) and the folder (inptutdata) that contains a blob with the input data.</span></span> <span data-ttu-id="0212f-132">Per OutputDataset, si specificano il contenitore BLOB (adfgetstarted) e la cartella (partitioneddata) che contiene i dati di output.</span><span class="sxs-lookup"><span data-stu-id="0212f-132">For the OutputDataset, you specify the blob container (adfgetstarted) and the folder (partitioneddata) that holds the output data.</span></span> <span data-ttu-id="0212f-133">Specificare anche altre proprietà come struttura, disponibilità e criteri.</span><span class="sxs-lookup"><span data-stu-id="0212f-133">You also specify other properties such as structure, availability, and policy.</span></span>
3. <span data-ttu-id="0212f-134">Creare una pipeline denominata **MyFirstPipeline**.</span><span class="sxs-lookup"><span data-stu-id="0212f-134">Create a pipeline named **MyFirstPipeline**.</span></span> 
  
    <span data-ttu-id="0212f-135">In questa procedura dettagliata, la pipeline include una sola attività, l'**attività Hive di HDInsight**,</span><span class="sxs-lookup"><span data-stu-id="0212f-135">In this walkthrough, the pipeline has only one activity: **HDInsight Hive Activity**.</span></span> <span data-ttu-id="0212f-136">che trasforma i dati di input per generare i dati di output eseguendo uno script Hive in un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="0212f-136">This activity transform input data to produce output data by running a hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="0212f-137">Per altre informazioni in merito, vedere l'articolo relativo all'[attività Hive](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="0212f-137">To learn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span></span> 
4. <span data-ttu-id="0212f-138">Creare una data factory denominata **DataFactoryUsingVS**.</span><span class="sxs-lookup"><span data-stu-id="0212f-138">Create a data factory named **DataFactoryUsingVS**.</span></span> <span data-ttu-id="0212f-139">Distribuire la data factory e tutte le entità di Data Factory, ovvero i servizi collegati, le tabelle e la pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-139">Deploy the data factory and all Data Factory entities (linked services, tables, and the pipeline).</span></span>
5. <span data-ttu-id="0212f-140">Dopo la pubblicazione, si useranno i pannelli del portale e l'app di monitoraggio e gestione di Azure per monitorare la pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-140">After you publish, you use Azure portal blades and Monitoring & Management App to monitor the pipeline.</span></span> 
  
### <a name="prerequisites"></a><span data-ttu-id="0212f-141">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0212f-141">Prerequisites</span></span>
1. <span data-ttu-id="0212f-142">Vedere la [panoramica dell'esercitazione](data-factory-build-your-first-pipeline.md) ed eseguire i passaggi relativi ai **prerequisiti** .</span><span class="sxs-lookup"><span data-stu-id="0212f-142">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span> <span data-ttu-id="0212f-143">È anche possibile selezionare l'opzione **Panoramica e prerequisiti** nell'elenco a discesa in alto per passare a tale articolo.</span><span class="sxs-lookup"><span data-stu-id="0212f-143">You can also select the **Overview and prerequisites** option in the drop-down list at the top to switch to the article.</span></span> <span data-ttu-id="0212f-144">Dopo aver completato i prerequisiti, tornare a questo articolo selezionando l'opzione **Visual Studio** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="0212f-144">After you complete the prerequisites, switch back to this article by selecting **Visual Studio** option in the drop-down list.</span></span>
2. <span data-ttu-id="0212f-145">Per creare istanze di data factory, è necessario essere membri del ruolo [Collaboratore Data factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) a livello di sottoscrizione/gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0212f-145">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>  
3. <span data-ttu-id="0212f-146">È necessario disporre dei seguenti prodotti installati nel computer in uso:</span><span class="sxs-lookup"><span data-stu-id="0212f-146">You must have the following installed on your computer:</span></span>
   * <span data-ttu-id="0212f-147">Visual Studio 2013 o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="0212f-147">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="0212f-148">Download di Azure SDK per Visual Studio 2013 o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="0212f-148">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="0212f-149">Passare alla [pagina di download di Azure](https://azure.microsoft.com/downloads/) e fare clic su **VS 2013** o **VS 2015** nella sezione **.NET**.</span><span class="sxs-lookup"><span data-stu-id="0212f-149">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="0212f-150">Scaricare il plug-in Azure Data Factory più recente per Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) o [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="0212f-150">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="0212f-151">È anche possibile aggiornare il plug-in nel modo seguente: dal menu scegliere **Strumenti** -> **Estensioni e aggiornamenti** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="0212f-151">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

<span data-ttu-id="0212f-152">Verrà ora usato Visual Studio per creare una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-152">Now, let's use Visual Studio to create an Azure data factory.</span></span>

### <a name="create-visual-studio-project"></a><span data-ttu-id="0212f-153">Creare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0212f-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="0212f-154">Avviare **Visual Studio 2013** o **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="0212f-154">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span></span> <span data-ttu-id="0212f-155">Fare clic su **File**, scegliere **Nuovo** e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="0212f-155">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="0212f-156">Si dovrebbe vedere la finestra di dialogo **Nuovo progetto** .</span><span class="sxs-lookup"><span data-stu-id="0212f-156">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="0212f-157">Nella finestra di dialogo **Nuovo progetto** selezionare il modello **DataFactory** e fare clic su **Progetto data factory vuoto**.</span><span class="sxs-lookup"><span data-stu-id="0212f-157">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>   

    ![Finestra di dialogo Nuovo progetto](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. <span data-ttu-id="0212f-159">Immettere un **nome** per il progetto, un **percorso** e un nome per la **soluzione** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0212f-159">Enter a **name** for the project, **location**, and a name for the **solution**, and click **OK**.</span></span>

    ![Esplora soluzioni](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a><span data-ttu-id="0212f-161">Creazione di servizi collegati</span><span class="sxs-lookup"><span data-stu-id="0212f-161">Create linked services</span></span>
<span data-ttu-id="0212f-162">In questo passaggio si creano due servizi collegati: **Archiviazione di Azure** e **HDInsight su richiesta**.</span><span class="sxs-lookup"><span data-stu-id="0212f-162">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span></span> 

<span data-ttu-id="0212f-163">Il servizio collegato Archiviazione di Azure collega l'account di archiviazione di Azure alla data factory fornendo le informazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="0212f-163">The Azure Storage linked service links your Azure Storage account to the data factory by providing the connection information.</span></span> <span data-ttu-id="0212f-164">Il servizio Data Factory usa la stringa di connessione dell'impostazione del servizio collegato per connettersi alla risorsa di archiviazione di Azure in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0212f-164">Data Factory service uses the connection string from the linked service setting to connect to the Azure storage at runtime.</span></span> <span data-ttu-id="0212f-165">Tale risorsa di archiviazione contiene i dati di input e di output per la pipeline e il file di script Hive usato dall'attività Hive.</span><span class="sxs-lookup"><span data-stu-id="0212f-165">This storage holds input and output data for the pipeline, and the hive script file used by the hive activity.</span></span> 

<span data-ttu-id="0212f-166">Con il servizio collegato HDInsight su richiesta, il cluster HDInsight viene creato automaticamente in fase di esecuzione quando i dati di input sono pronti per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-166">With on-demand HDInsight linked service, The HDInsight cluster is automatically created at runtime when the input data is ready to processed.</span></span> <span data-ttu-id="0212f-167">Il cluster viene eliminato al termine dell'elaborazione e dopo che è rimasto inattivo per il periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="0212f-167">The cluster is deleted after it is done processing and idle for the specified amount of time.</span></span> 

> [!NOTE]
> <span data-ttu-id="0212f-168">Per creare una data factory, specificarne il nome e le impostazioni al momento della pubblicazione della soluzione Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-168">You create a data factory by specifying its name and settings at the time of publishing your Data Factory solution.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="0212f-169">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0212f-169">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="0212f-170">Fare clic con il pulsante destro del mouse su **Servizi collegati** in Esplora soluzioni, scegliere **Aggiungi** e fare clic su **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="0212f-170">Right-click **Linked Services** in the solution explorer, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="0212f-171">Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **Servizio collegato Archiviazione di Azure** nell'elenco e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0212f-171">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span>
    <span data-ttu-id="0212f-172">![Servizio collegato Archiviazione di Azure](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="0212f-172">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span></span>
3. <span data-ttu-id="0212f-173">Sostituire `<accountname>` e `<accountkey>` con il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-173">Replace `<accountname>` and `<accountkey>` with the name of your Azure storage account and its key.</span></span> <span data-ttu-id="0212f-174">Per informazioni su come ottenere la chiave di accesso alle risorse di archiviazione, vedere le informazioni su come visualizzare, copiare e rigenerare le chiavi di accesso alle risorse di archiviazione in [Gestire l'account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="0212f-174">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
    <span data-ttu-id="0212f-175">![Servizio collegato Archiviazione di Azure](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="0212f-175">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span></span>
4. <span data-ttu-id="0212f-176">Salvare il file **AzureStorageLinkedService1.json** .</span><span class="sxs-lookup"><span data-stu-id="0212f-176">Save the **AzureStorageLinkedService1.json** file.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="0212f-177">Creare un servizio collegato Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0212f-177">Create Azure HDInsight linked service</span></span>
1. <span data-ttu-id="0212f-178">Fare clic con il pulsante destro del mouse su **Servizi collegati** in **Esplora soluzioni**, scegliere **Aggiungi** e fare clic su **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="0212f-178">In the **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="0212f-179">Selezionare **HDInsight On Demand Linked Service** (Servizio collegato HDInsight su richiesta) e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0212f-179">Select **HDInsight On Demand Linked Service**, and click **Add**.</span></span>
3. <span data-ttu-id="0212f-180">Sostituire il codice **JSON** con quello seguente:</span><span class="sxs-lookup"><span data-stu-id="0212f-180">Replace the **JSON** with the following JSON:</span></span>

     ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
        "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    <span data-ttu-id="0212f-181">La tabella seguente fornisce le descrizioni delle proprietà JSON usate nel frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="0212f-181">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    <span data-ttu-id="0212f-182">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0212f-182">Property</span></span> | <span data-ttu-id="0212f-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0212f-183">Description</span></span>
    -------- | ----------- 
    <span data-ttu-id="0212f-184">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="0212f-184">ClusterSize</span></span> | <span data-ttu-id="0212f-185">Specifica le dimensioni del cluster Hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0212f-185">Specifies the size of the HDInsight Hadoop cluster.</span></span>
    <span data-ttu-id="0212f-186">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="0212f-186">TimeToLive</span></span> | <span data-ttu-id="0212f-187">Specifica il tempo di inattività del cluster HDInsight, prima che sia eliminato.</span><span class="sxs-lookup"><span data-stu-id="0212f-187">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span>
    <span data-ttu-id="0212f-188">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0212f-188">linkedServiceName</span></span> | <span data-ttu-id="0212f-189">Specifica l'account di archiviazione usato per archiviare i log generati dal cluster Hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0212f-189">Specifies the storage account that is used to store the logs that are generated by HDInsight Hadoop cluster.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="0212f-190">Il cluster HDInsight crea un **contenitore predefinito** nell'archivio BLOB specificato nel file JSON (linkedServiceName).</span><span class="sxs-lookup"><span data-stu-id="0212f-190">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName).</span></span> <span data-ttu-id="0212f-191">HDInsight non elimina il contenitore quando viene eliminato il cluster.</span><span class="sxs-lookup"><span data-stu-id="0212f-191">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="0212f-192">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-192">This behavior is by design.</span></span> <span data-ttu-id="0212f-193">Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che viene elaborata una sezione, a meno che non esista un cluster attivo (timeToLive).</span><span class="sxs-lookup"><span data-stu-id="0212f-193">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="0212f-194">Il cluster viene eliminato al termine dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-194">The cluster is automatically deleted when the processing is done.</span></span>
    > 
    > <span data-ttu-id="0212f-195">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-195">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="0212f-196">Se non sono necessari per risolvere i problemi relativi ai processi, è possibile eliminarli per ridurre i costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-196">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="0212f-197">I nomi dei contenitori seguono il modello `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="0212f-197">The names of these containers follow a pattern: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span></span> <span data-ttu-id="0212f-198">Per eliminare i contenitori nell'archivio BLOB di Azure, usare strumenti come [Microsoft Azure Storage Explorer](http://storageexplorer.com/) .</span><span class="sxs-lookup"><span data-stu-id="0212f-198">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

    <span data-ttu-id="0212f-199">Per altre informazioni sulle proprietà JSON, vedere l'articolo relativo ai [servizi collegati di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="0212f-199">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span></span> 
4. <span data-ttu-id="0212f-200">Salvare il file **HDInsightOnDemandLinkedService1.json** .</span><span class="sxs-lookup"><span data-stu-id="0212f-200">Save the **HDInsightOnDemandLinkedService1.json** file.</span></span>

### <a name="create-datasets"></a><span data-ttu-id="0212f-201">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="0212f-201">Create datasets</span></span>
<span data-ttu-id="0212f-202">In questo passaggio vengono creati set di dati per rappresentare i dati di input e di output per l'elaborazione Hive.</span><span class="sxs-lookup"><span data-stu-id="0212f-202">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="0212f-203">I set di dati fanno riferimento all'oggetto **AzureStorageLinkedService1** creato in precedenza in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-203">These datasets refer to the **AzureStorageLinkedService1** you have created earlier in this tutorial.</span></span> <span data-ttu-id="0212f-204">Il servizio collegato punta a un account di archiviazione di Azure e i set di dati specificano il contenitore, la cartella e il nome del file nella risorsa di archiviazione che contiene i dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="0212f-204">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

#### <a name="create-input-dataset"></a><span data-ttu-id="0212f-205">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="0212f-205">Create input dataset</span></span>
1. <span data-ttu-id="0212f-206">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Tabelle**, scegliere **Aggiungi** e fare clic su **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="0212f-206">In the **Solution Explorer**, right-click **Tables**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="0212f-207">Selezionare **BLOB di Azure** dall'elenco, cambiare il nome del file in **InputDataSet.json** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0212f-207">Select **Azure Blob** from the list, change the name of the file to **InputDataSet.json**, and click **Add**.</span></span>
3. <span data-ttu-id="0212f-208">Sostituire il codice **JSON** nell'editor con il frammento di codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="0212f-208">Replace the **JSON** in the editor with the following JSON snippet:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    <span data-ttu-id="0212f-209">Questo frammento JSON definisce un set di dati denominato **AzureBlobInput** che rappresenta i dati di input per l'attività Hive nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-209">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for the hive activity in the pipeline.</span></span> <span data-ttu-id="0212f-210">Si specifica che i dati di input si trovano nel contenitore BLOB denominato `adfgetstarted` e nella cartella denominata `inputdata`.</span><span class="sxs-lookup"><span data-stu-id="0212f-210">You specify that the input data is located in the blob container called `adfgetstarted` and the folder called `inputdata`.</span></span>

    <span data-ttu-id="0212f-211">La tabella seguente fornisce le descrizioni delle proprietà JSON usate nel frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="0212f-211">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    <span data-ttu-id="0212f-212">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0212f-212">Property</span></span> | <span data-ttu-id="0212f-213">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0212f-213">Description</span></span> |
    -------- | ----------- |
    <span data-ttu-id="0212f-214">type</span><span class="sxs-lookup"><span data-stu-id="0212f-214">type</span></span> |<span data-ttu-id="0212f-215">La proprietà type è impostata su **AzureBlob** perché i dati risiedono nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-215">The type property is set to **AzureBlob** because data resides in Azure Blob Storage.</span></span>
    <span data-ttu-id="0212f-216">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0212f-216">linkedServiceName</span></span> | <span data-ttu-id="0212f-217">Fa riferimento all'oggetto AzureStorageLinkedService1 creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0212f-217">Refers to the AzureStorageLinkedService1 you created earlier.</span></span>
    <span data-ttu-id="0212f-218">fileName</span><span class="sxs-lookup"><span data-stu-id="0212f-218">fileName</span></span> |<span data-ttu-id="0212f-219">Questa proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="0212f-219">This property is optional.</span></span> <span data-ttu-id="0212f-220">Se si omette questa proprietà, vengono prelevati tutti i file da folderPath.</span><span class="sxs-lookup"><span data-stu-id="0212f-220">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="0212f-221">In tal caso viene elaborato solo il file input.log.</span><span class="sxs-lookup"><span data-stu-id="0212f-221">In this case, only the input.log is processed.</span></span>
    <span data-ttu-id="0212f-222">type</span><span class="sxs-lookup"><span data-stu-id="0212f-222">type</span></span> | <span data-ttu-id="0212f-223">I file di log sono in formato testo, quindi viene usato TextFormat.</span><span class="sxs-lookup"><span data-stu-id="0212f-223">The log files are in text format, so we use TextFormat.</span></span> |
    <span data-ttu-id="0212f-224">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="0212f-224">columnDelimiter</span></span> | <span data-ttu-id="0212f-225">Le colonne nei file di log sono delimitate dalla virgola (`,`).</span><span class="sxs-lookup"><span data-stu-id="0212f-225">columns in the log files are delimited by the comma character (`,`)</span></span>
    <span data-ttu-id="0212f-226">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="0212f-226">frequency/interval</span></span> | <span data-ttu-id="0212f-227">La frequenza è impostata su Month e l'intervallo è 1, ciò significa che le sezioni di input sono disponibili con cadenza mensile.</span><span class="sxs-lookup"><span data-stu-id="0212f-227">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span>
    <span data-ttu-id="0212f-228">external</span><span class="sxs-lookup"><span data-stu-id="0212f-228">external</span></span> | <span data-ttu-id="0212f-229">Questa proprietà è impostata su true se i dati di input per l'attività non vengono generati dalla pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-229">This property is set to true if the input data for the activity is not generated by the pipeline.</span></span> <span data-ttu-id="0212f-230">Viene specificata solo per i set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="0212f-230">This property is only specified on input datasets.</span></span> <span data-ttu-id="0212f-231">Per il set di dati di input della prima attività, impostare sempre questa proprietà su true.</span><span class="sxs-lookup"><span data-stu-id="0212f-231">For the input dataset of the first activity, always set it to true.</span></span>
4. <span data-ttu-id="0212f-232">Salvare il file **InputDataset.json** .</span><span class="sxs-lookup"><span data-stu-id="0212f-232">Save the **InputDataset.json** file.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="0212f-233">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="0212f-233">Create output dataset</span></span>
<span data-ttu-id="0212f-234">Viene ora creato il set di dati di output per rappresentare i dati di output archiviati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-234">Now, you create the output dataset to represent output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="0212f-235">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Tabelle**, scegliere **Aggiungi** e fare clic su **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="0212f-235">In the **Solution Explorer**, right-click **tables**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="0212f-236">Selezionare **Blob di Azure** dall'elenco, cambiare il nome del file in **OutputDataset.json** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0212f-236">Select **Azure Blob** from the list, change the name of the file to **OutputDataset.json**, and click **Add**.</span></span>
3. <span data-ttu-id="0212f-237">Sostituire il codice **JSON** nell'editor con il codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="0212f-237">Replace the **JSON** in the editor with the following JSON:</span></span>
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "folderPath": "adfgetstarted/partitioneddata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            }
        }
    }
    ```
    <span data-ttu-id="0212f-238">Questo frammento JSON definisce un set di dati denominato **AzureBlobOutput** che rappresenta i dati di output generati dall'attività Hive nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-238">The JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by the hive activity in the pipeline.</span></span> <span data-ttu-id="0212f-239">Si specifica che i dati di output generati dall'attività Hive verranno inseriti nel contenitore BLOB denominato `adfgetstarted` e nella cartella denominata `partitioneddata`.</span><span class="sxs-lookup"><span data-stu-id="0212f-239">You specify that the output data is produced by the hive activity is placed in the blob container called `adfgetstarted` and the folder called `partitioneddata`.</span></span> 
    
    <span data-ttu-id="0212f-240">La sezione **availability** specifica che il set di dati di output viene generato su base mensile.</span><span class="sxs-lookup"><span data-stu-id="0212f-240">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span> <span data-ttu-id="0212f-241">Il set di dati di output determina la pianificazione della pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-241">The output dataset drives the schedule of the pipeline.</span></span> <span data-ttu-id="0212f-242">La pipeline viene eseguita con cadenza mensile tra le relative ore di inizio e di fine.</span><span class="sxs-lookup"><span data-stu-id="0212f-242">The pipeline runs monthly between its start and end times.</span></span> 

    <span data-ttu-id="0212f-243">Per le descrizioni di queste proprietà, vedere la sezione **Creare il set di dati di input** .</span><span class="sxs-lookup"><span data-stu-id="0212f-243">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="0212f-244">La proprietà external non viene impostata per un set di dati di output perché il set di dati viene generato dalla pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-244">You do not set the external property on an output dataset as the dataset is produced by the pipeline.</span></span>
4. <span data-ttu-id="0212f-245">Salvare il file **OutputDataset.json** .</span><span class="sxs-lookup"><span data-stu-id="0212f-245">Save the **OutputDataset.json** file.</span></span>

### <a name="create-pipeline"></a><span data-ttu-id="0212f-246">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="0212f-246">Create pipeline</span></span>
<span data-ttu-id="0212f-247">Finora sono stati creati il servizio collegato Archiviazione di Azure e i set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="0212f-247">You have created the Azure Storage linked service, and input and output datasets so far.</span></span> <span data-ttu-id="0212f-248">Ora si creerà una pipeline con un'attività **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="0212f-248">Now, you create a pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="0212f-249">L'**input** per l'attività Hive viene impostato su **AzureBlobInput** e l'**output** viene impostato su **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="0212f-249">The **input** for the hive activity is set to **AzureBlobInput** and **output** is set to **AzureBlobOutput**.</span></span> <span data-ttu-id="0212f-250">Una sezione del set di dati di input è disponibile con cadenza mensile (frequency: Month, interval: 1) e anche la sezione di output viene generata ogni mese.</span><span class="sxs-lookup"><span data-stu-id="0212f-250">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and the output slice is produced monthly too.</span></span> 

1. <span data-ttu-id="0212f-251">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Pipeline**, scegliere **Aggiungi** e fare clic su **Nuovo elemento.**</span><span class="sxs-lookup"><span data-stu-id="0212f-251">In the **Solution Explorer**, right-click **Pipelines**, point to **Add**, and click **New Item.**</span></span>
2. <span data-ttu-id="0212f-252">Selezionare **Hive Transformation Pipeline** (Pipeline di trasformazione Hive) dall'elenco e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0212f-252">Select **Hive Transformation Pipeline** from the list, and click **Add**.</span></span>
3. <span data-ttu-id="0212f-253">Sostituire il codice **JSON** con il frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="0212f-253">Replace the **JSON** with the following snippet:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0212f-254">Sostituire `<storageaccountname>` con il nome del proprio account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-254">Replace `<storageaccountname>` with the name of your storage account.</span></span>

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService1",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="0212f-255">Sostituire `<storageaccountname>` con il nome del proprio account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-255">Replace `<storageaccountname>` with the name of your storage account.</span></span>

    <span data-ttu-id="0212f-256">Il frammento JSON definisce una pipeline costituita da una singola attività Hive,</span><span class="sxs-lookup"><span data-stu-id="0212f-256">The JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span></span> <span data-ttu-id="0212f-257">che esegue uno script Hive per elaborare i dati di input in un cluster HDInsight su richiesta e generare i dati di output.</span><span class="sxs-lookup"><span data-stu-id="0212f-257">This activity runs a Hive script to process input data on an on-demand HDInsight cluster to produce output data.</span></span> <span data-ttu-id="0212f-258">Nella matrice nella sezione activities del codice JSON della pipeline è presente una sola attività il cui tipo è impostato su **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="0212f-258">In the activities section of the pipeline JSON, you see only one activity in the array with type set to **HDInsightHive**.</span></span> 

    <span data-ttu-id="0212f-259">Nelle proprietà del tipo specifiche dell'attività Hive di HDInsight si specificano il servizio collegato Archiviazione di Azure in cui si trova il file di script Hive, il percorso del file di script e i parametri per tale file.</span><span class="sxs-lookup"><span data-stu-id="0212f-259">In the type properties that are specific to HDInsight Hive activity, you specify what Azure Storage linked service has the hive script file, the path to the script file, and parameters to the script file.</span></span> 

    <span data-ttu-id="0212f-260">Il file di script Hive, **partitionweblogs.hql**, è archiviato nell'account di archiviazione di Azure (specificato da scriptLinkedService) e nella cartella `script` nel contenitore `adfgetstarted`.</span><span class="sxs-lookup"><span data-stu-id="0212f-260">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService), and in the `script` folder in the container `adfgetstarted`.</span></span>

    <span data-ttu-id="0212f-261">La sezione `defines` viene usata per specificare le impostazioni di runtime che vengono passate allo script Hive come valori di configurazione Hive, ad esempio `${hiveconf:inputtable}` e `${hiveconf:partitionedtable})`.</span><span class="sxs-lookup"><span data-stu-id="0212f-261">The `defines` section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span></span>

    <span data-ttu-id="0212f-262">Le proprietà **start** ed **end** della pipeline ne specificano il periodo attivo.</span><span class="sxs-lookup"><span data-stu-id="0212f-262">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span> <span data-ttu-id="0212f-263">Poiché il set di dati è stato configurato per essere generato con cadenza mensile, la pipeline genera una sola sezione perché le date di inizio e di fine sono incluse nello stesso mese.</span><span class="sxs-lookup"><span data-stu-id="0212f-263">You configured the dataset to be produced monthly, therefore, only once slice is produced by the pipeline (because the month is same in start and end dates).</span></span>

    <span data-ttu-id="0212f-264">Nel codice JSON dell'attività si specifica che lo script Hive viene eseguito sulla risorsa di calcolo specificata da **linkedServiceName** - **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="0212f-264">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>
4. <span data-ttu-id="0212f-265">Salvare il file **HiveActivity1.json** .</span><span class="sxs-lookup"><span data-stu-id="0212f-265">Save the **HiveActivity1.json** file.</span></span>

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a><span data-ttu-id="0212f-266">Aggiungere partitionweblogs.hql e input.log come dipendenza</span><span class="sxs-lookup"><span data-stu-id="0212f-266">Add partitionweblogs.hql and input.log as a dependency</span></span>
1. <span data-ttu-id="0212f-267">Fare clic con il pulsante destro del mouse su **Dipendenze** nella finestra **Esplora soluzioni**, scegliere **Aggiungi** e quindi fare clic su **Elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="0212f-267">Right-click **Dependencies** in the **Solution Explorer** window, point to **Add**, and click **Existing Item**.</span></span>  
2. <span data-ttu-id="0212f-268">Passare a **C:\ADFGettingStarted**, selezionare i file **partitionweblogs.hql** e **input.log** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0212f-268">Navigate to the **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span></span> <span data-ttu-id="0212f-269">Questi due file sono stati creati come prerequisiti in [Panoramica dell'esercitazione](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="0212f-269">You created these two files as part of prerequisites from the [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="0212f-270">Quando si pubblica la soluzione nel passaggio successivo, il file **partitionweblogs.hql** viene caricato nella cartella **script** del contenitore BLOB `adfgetstarted`.</span><span class="sxs-lookup"><span data-stu-id="0212f-270">When you publish the solution in the next step, the **partitionweblogs.hql** file is uploaded to the **script** folder in the `adfgetstarted` blob container.</span></span>   

### <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="0212f-271">Pubblicare/Distribuire le entità della data factory</span><span class="sxs-lookup"><span data-stu-id="0212f-271">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="0212f-272">In questo passaggio si pubblicano le entità della data factory (servizi collegati, set di dati e pipeline) del progetto nel servizio Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-272">In this step, you publish the Data Factory entities (linked services, datasets, and pipeline) in your project to the Azure Data Factory service.</span></span> <span data-ttu-id="0212f-273">Nel corso del processo di pubblicazione si specifica il nome della data factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-273">In the process of publishing, you specify the name for your data factory.</span></span> 

1. <span data-ttu-id="0212f-274">Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="0212f-274">Right-click project in the Solution Explorer, and click **Publish**.</span></span>
2. <span data-ttu-id="0212f-275">Se viene visualizzato **Sign in to your Microsoft account** (Accedere all'account Microsoft), nella finestra di dialogo immettere le credenziali per l'account associato alla sottoscrizione di Azure e fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="0212f-275">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="0212f-276">Verrà visualizzata la finestra di dialogo seguente:</span><span class="sxs-lookup"><span data-stu-id="0212f-276">You should see the following dialog box:</span></span>

   ![Finestra di dialogo Pubblica](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. <span data-ttu-id="0212f-278">Nella pagina **Configure data factory** (Configura data factory), procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="0212f-278">In the **Configure data factory** page, do the following steps:</span></span>

    ![Pubblicazione: impostazioni per una nuova data factory](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. <span data-ttu-id="0212f-280">Selezionare l’opzione **Crea nuova data factory** .</span><span class="sxs-lookup"><span data-stu-id="0212f-280">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="0212f-281">Immettere un **nome** univoco per la data factory,</span><span class="sxs-lookup"><span data-stu-id="0212f-281">Enter a unique **name** for the data factory.</span></span> <span data-ttu-id="0212f-282">ad esempio **DataFactoryUsingVS09152016**.</span><span class="sxs-lookup"><span data-stu-id="0212f-282">For example: **DataFactoryUsingVS09152016**.</span></span> <span data-ttu-id="0212f-283">Il nome deve essere univoco a livello globale.</span><span class="sxs-lookup"><span data-stu-id="0212f-283">The name must be globally unique.</span></span>
   3. <span data-ttu-id="0212f-284">Selezionare la sottoscrizione adatta per il campo **Sottoscrizione** .</span><span class="sxs-lookup"><span data-stu-id="0212f-284">Select the right subscription for the **Subscription** field.</span></span> 
        > [!IMPORTANT]
        > <span data-ttu-id="0212f-285">Se non viene visualizzata alcuna sottoscrizione, verificare di aver eseguito l'accesso con un account amministratore o coamministratore della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0212f-285">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.</span></span>
   4. <span data-ttu-id="0212f-286">Selezionare il **gruppo di risorse** per la data factory da creare.</span><span class="sxs-lookup"><span data-stu-id="0212f-286">Select the **resource group** for the data factory to be created.</span></span>
   5. <span data-ttu-id="0212f-287">Selezionare l' **area** per la data factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-287">Select the **region** for the data factory.</span></span>
   6. <span data-ttu-id="0212f-288">Fare clic su **Avanti** per passare alla pagina **Pubblica elementi**.</span><span class="sxs-lookup"><span data-stu-id="0212f-288">Click **Next** to switch to the **Publish Items** page.</span></span> <span data-ttu-id="0212f-289">Premere **TAB** per uscire dal campo Nome se il pulsante **Avanti** è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="0212f-289">(Press **TAB** to move out of the Name field to if the **Next** button is disabled.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0212f-290">Se al momento della pubblicazione viene visualizzato l'errore **Il nome "DataFactoryUsingVS" per la data factory non è disponibile**, modificare il nome (ad esempio in nomeutenteDataFactoryUsingVS).</span><span class="sxs-lookup"><span data-stu-id="0212f-290">If you receive the error **Data factory name “DataFactoryUsingVS” is not available** when publishing, change the name (for example, yournameDataFactoryUsingVS).</span></span> <span data-ttu-id="0212f-291">Per informazioni sulle regole di denominazione per gli elementi di Data Factory, vedere l'argomento [Azure Data Factory - Regole di denominazione](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="0212f-291">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
1. <span data-ttu-id="0212f-292">Nella pagina **Pubblica elementi** assicurarsi che tutte le data factory siano selezionate e fare clic su **Avanti** per passare alla pagina **Riepilogo**.</span><span class="sxs-lookup"><span data-stu-id="0212f-292">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>

    ![Pagina Publish Items (Pubblica elementi)](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. <span data-ttu-id="0212f-294">Esaminare il riepilogo e fare clic su **Avanti** per avviare il processo di distribuzione e visualizzare lo **Stato della distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="0212f-294">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>

    ![Pagina Riepilogo](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. <span data-ttu-id="0212f-296">Nella pagina **Stato della distribuzione** , è possibile visualizzare lo stato del processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0212f-296">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="0212f-297">Fare clic su Finish (Fine) dopo il termine della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0212f-297">Click Finish after the deployment is done.</span></span>

<span data-ttu-id="0212f-298">Elementi importanti da considerare:</span><span class="sxs-lookup"><span data-stu-id="0212f-298">Important points to note:</span></span>

- <span data-ttu-id="0212f-299">Se viene visualizzato l'errore **La sottoscrizione non è registrata per l'uso dello spazio dei nomi Microsoft.DataFactory**, eseguire una di queste operazioni e provare a ripetere la pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="0212f-299">If you receive the error: **This subscription is not registered to use namespace Microsoft.DataFactory**, do one of the following and try publishing again:</span></span>
    - <span data-ttu-id="0212f-300">In Azure PowerShell eseguire questo comando per registrare il provider di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-300">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span>
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        <span data-ttu-id="0212f-301">È possibile eseguire questo comando per verificare che il provider di Data Factory sia registrato.</span><span class="sxs-lookup"><span data-stu-id="0212f-301">You can run the following command to confirm that the Data Factory provider is registered.</span></span>

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - <span data-ttu-id="0212f-302">Accedere usando la sottoscrizione di Azure nel [portale di Azure](https://portal.azure.com) e passare al pannello Data Factory oppure creare un'istanza di Data Factory nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-302">Login using the Azure subscription in to the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="0212f-303">Questa azione registra automaticamente il provider.</span><span class="sxs-lookup"><span data-stu-id="0212f-303">This action automatically registers the provider for you.</span></span>
- <span data-ttu-id="0212f-304">Il nome di Data Factory può essere registrato come un nome DNS in futuro e pertanto divenire visibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="0212f-304">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>
- <span data-ttu-id="0212f-305">Per creare istanze di data factory, è necessario essere un amministratore o un coamministratore della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-305">To create Data Factory instances, you need to be an admin or co-admin of the Azure subscription</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="0212f-306">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="0212f-306">Monitor pipeline</span></span>
<span data-ttu-id="0212f-307">In questo passaggio si monitora la pipeline usando la vista diagramma della data factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-307">In this step, you monitor the pipeline using Diagram View of the data factory.</span></span> 

#### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="0212f-308">Monitorare la pipeline con la vista diagramma</span><span class="sxs-lookup"><span data-stu-id="0212f-308">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="0212f-309">Accedere al [portale di Azure](https://portal.azure.com/) e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0212f-309">Log in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>
   1. <span data-ttu-id="0212f-310">Fare clic su **Altri servizi** e quindi su **Data factory**.</span><span class="sxs-lookup"><span data-stu-id="0212f-310">Click **More services** and click **Data factories**.</span></span>
       
        ![Esplora data factory](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. <span data-ttu-id="0212f-312">Selezionare il nome della data factory (ad esempio, **DataFactoryUsingVS09152016**) nell'elenco di data factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-312">Select the name of your data factory (for example: **DataFactoryUsingVS09152016**) from the list of data factories.</span></span>
   
       ![Selezionare la data factory](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. <span data-ttu-id="0212f-314">Nella home page della data factory fare clic su **Diagramma**.</span><span class="sxs-lookup"><span data-stu-id="0212f-314">In the home page for your data factory, click **Diagram**.</span></span>

    ![Riquadro Diagramma](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. <span data-ttu-id="0212f-316">In Vista diagramma saranno visualizzati una panoramica delle pipeline e i set di dati usati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-316">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Vista Diagramma](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. <span data-ttu-id="0212f-318">Per visualizzare tutte le attività nella pipeline, fare clic con il pulsante destro del mouse sulla pipeline nel diagramma e scegliere Apri pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-318">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![Menu Apri pipeline](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. <span data-ttu-id="0212f-320">Assicurarsi che l'attività HDInsightHive sia visualizzata nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-320">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![Visualizzazione Apri pipeline](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    <span data-ttu-id="0212f-322">Per tornare alla visualizzazione precedente, fare clic su **Data Factory** nel menu di navigazione nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="0212f-322">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
6. <span data-ttu-id="0212f-323">In **Vista diagramma** fare doppio clic sul set di dati **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="0212f-323">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="0212f-324">Verificare che lo stato della sezione sia **Pronto** .</span><span class="sxs-lookup"><span data-stu-id="0212f-324">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="0212f-325">Potrebbero essere necessari alcuni minuti perché lo stato della sezione venga visualizzato come Pronto.</span><span class="sxs-lookup"><span data-stu-id="0212f-325">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="0212f-326">Se dopo qualche minuto ciò non accade, verificare che il file di input (input.log) sia posizionato nel contenitore (`adfgetstarted`) e nella cartella (`inputdata`) corretti.</span><span class="sxs-lookup"><span data-stu-id="0212f-326">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (`adfgetstarted`) and folder (`inputdata`).</span></span> <span data-ttu-id="0212f-327">Verificare anche che la proprietà **external** per il set di dati di input sia impostata su **true**.</span><span class="sxs-lookup"><span data-stu-id="0212f-327">And, make sure that the **external** property on the input dataset is set to **true**.</span></span> 

   ![Sezione di input nello stato Pronto](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. <span data-ttu-id="0212f-329">Fare clic su **X** per chiudere il pannello **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="0212f-329">Click **X** to close **AzureBlobInput** blade.</span></span>
8. <span data-ttu-id="0212f-330">In **Vista diagramma** fare doppio clic sul set di dati **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="0212f-330">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="0212f-331">Viene visualizzata la sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-331">You see that the slice that is currently being processed.</span></span>

   ![Set di dati](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. <span data-ttu-id="0212f-333">Al termine dell'elaborazione lo stato della sezione è **Pronta** .</span><span class="sxs-lookup"><span data-stu-id="0212f-333">When processing is done, you see the slice in **Ready** state.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0212f-334">La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti).</span><span class="sxs-lookup"><span data-stu-id="0212f-334">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="0212f-335">Di conseguenza, prevedere **circa 30 minuti** per l'elaborazione della sezione nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-335">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>  
   
    ![Set di dati](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. <span data-ttu-id="0212f-337">Quando lo stato sella sezione è **Pronto**, cercare i dati di output nella cartella `partitioneddata` del contenitore `adfgetstarted` nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="0212f-337">When the slice is in **Ready** state, check the `partitioneddata` folder in the `adfgetstarted` container in your blob storage for the output data.</span></span>  

    ![Dati di output](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. <span data-ttu-id="0212f-339">Fare clic sulla sezione per visualizzare i relativi dettagli in un pannello **Sezione dati** .</span><span class="sxs-lookup"><span data-stu-id="0212f-339">Click the slice to see details about it in a **Data slice** blade.</span></span>

    ![Dettagli sezione dati](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. <span data-ttu-id="0212f-341">Fare clic su un'esecuzione di attività nell'elenco **Esecuzioni attività** (in questo scenario, un'attività Hive) per visualizzare i relativi dettagli nella finestra **Dettagli esecuzione attività**.</span><span class="sxs-lookup"><span data-stu-id="0212f-341">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span> 
  
    ![Dettagli esecuzione attività](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    <span data-ttu-id="0212f-343">Nei file di log sono riportate la query Hive eseguita e le informazioni sullo stato.</span><span class="sxs-lookup"><span data-stu-id="0212f-343">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="0212f-344">Tali file di log sono utili per risolvere eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="0212f-344">These logs are useful for troubleshooting any issues.</span></span>  

<span data-ttu-id="0212f-345">Per istruzioni su come usare il portale di Azure per monitorare la pipeline e i set di dati creati in questa esercitazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="0212f-345">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal to monitor the pipeline and datasets you have created in this tutorial.</span></span>

#### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="0212f-346">Monitorare la pipeline con l'app Monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="0212f-346">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="0212f-347">È anche possibile usare l'applicazione Monitoraggio e gestione per monitorare le pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-347">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="0212f-348">Per informazioni dettagliate sull'uso di questa applicazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory con la nuova app di monitoraggio e gestione](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="0212f-348">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="0212f-349">Fare clic sul riquadro Monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="0212f-349">Click Monitor & Manage tile.</span></span>

    ![Riquadro Monitoraggio e gestione](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. <span data-ttu-id="0212f-351">Verrà visualizzata l'applicazione Monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="0212f-351">You should see Monitor & Manage application.</span></span> <span data-ttu-id="0212f-352">Modificare **Ora di inizio** e **Ora di fine** in modo che corrispondano alle ore di inizio (04-01-2016 12:00 AM) e di fine (04-02-2016 12:00 AM) della pipeline e quindi fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="0212f-352">Change the **Start time** and **End time** to match start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span></span>

    ![App Monitoraggio e gestione](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. <span data-ttu-id="0212f-354">Per visualizzare i dettagli di una finestra attività, selezionarla nell'**elenco delle finestre attività**.</span><span class="sxs-lookup"><span data-stu-id="0212f-354">To see details about an activity window, select it in the **Activity Windows list** to see details about it.</span></span>
    <span data-ttu-id="0212f-355">![Dettagli finestra attività](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="0212f-355">![Activity window details](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0212f-356">Il file di input viene eliminato quando la sezione viene elaborata correttamente.</span><span class="sxs-lookup"><span data-stu-id="0212f-356">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="0212f-357">Per eseguire di nuovo la sezione o ripetere l'esercitazione, caricare quindi il file di input (input.log) nella cartella `inputdata` del contenitore `adfgetstarted`.</span><span class="sxs-lookup"><span data-stu-id="0212f-357">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the `inputdata` folder of the `adfgetstarted` container.</span></span>

### <a name="additional-notes"></a><span data-ttu-id="0212f-358">Note aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0212f-358">Additional notes</span></span>
- <span data-ttu-id="0212f-359">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-359">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="0212f-360">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="0212f-360">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="0212f-361">Ad esempio, un'attività di copia per copiare dati da un archivio dati di origine a uno di destinazione e un'attività Hive HDInsight per eseguire uno script Hive e trasformare i dati di input.</span><span class="sxs-lookup"><span data-stu-id="0212f-361">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data.</span></span> <span data-ttu-id="0212f-362">Vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) per tutte le origini e i sink supportati dall'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="0212f-362">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="0212f-363">Per l'elenco di servizi di calcolo supportati da Data Factory, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="0212f-363">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span>
- <span data-ttu-id="0212f-364">I servizi collegati collegano archivi dati o servizi di calcolo a una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-364">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="0212f-365">Vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) per tutte le origini e i sink supportati dall'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="0212f-365">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="0212f-366">Vedere l'articolo relativo ai [servizi collegati di calcolo](data-factory-compute-linked-services.md) per un elenco dei servizi di calcolo supportati da Data Factory e le [attività di trasformazione](data-factory-data-transformation-activities.md) eseguibili in tali servizi.</span><span class="sxs-lookup"><span data-stu-id="0212f-366">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span></span>
- <span data-ttu-id="0212f-367">Per informazioni dettagliate sulle proprietà JSON usate nella definizione del servizio collegato Archiviazione di Azure, vedere l'articolo relativo allo [spostamento di dati da e verso BLOB di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="0212f-367">See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in the Azure Storage linked service definition.</span></span>
- <span data-ttu-id="0212f-368">È possibile usare il proprio cluster HDInsight anziché un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="0212f-368">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="0212f-369">Per informazioni dettagliate, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="0212f-369">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>
-  <span data-ttu-id="0212f-370">Data Factory crea automaticamente un cluster HDInsight **basato su Linux** con il codice JSON precedente.</span><span class="sxs-lookup"><span data-stu-id="0212f-370">The Data Factory creates a **Linux-based** HDInsight cluster for you with the preceding JSON.</span></span> <span data-ttu-id="0212f-371">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="0212f-371">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
- <span data-ttu-id="0212f-372">Il cluster HDInsight crea un **contenitore predefinito** nell'archivio BLOB specificato nel file JSON (linkedServiceName).</span><span class="sxs-lookup"><span data-stu-id="0212f-372">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName).</span></span> <span data-ttu-id="0212f-373">HDInsight non elimina il contenitore quando viene eliminato il cluster.</span><span class="sxs-lookup"><span data-stu-id="0212f-373">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="0212f-374">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-374">This behavior is by design.</span></span> <span data-ttu-id="0212f-375">Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che viene elaborata una sezione, a meno che non esista un cluster attivo (timeToLive).</span><span class="sxs-lookup"><span data-stu-id="0212f-375">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="0212f-376">Il cluster viene eliminato al termine dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-376">The cluster is automatically deleted when the processing is done.</span></span>
    
    <span data-ttu-id="0212f-377">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-377">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="0212f-378">Se non sono necessari per risolvere i problemi relativi ai processi, è possibile eliminarli per ridurre i costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-378">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="0212f-379">I nomi dei contenitori seguono il modello `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="0212f-379">The names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="0212f-380">Per eliminare i contenitori nell'archivio BLOB di Azure, usare strumenti come [Microsoft Azure Storage Explorer](http://storageexplorer.com/) .</span><span class="sxs-lookup"><span data-stu-id="0212f-380">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>
- <span data-ttu-id="0212f-381">In questo momento la pianificazione è basata sul set di dati di output, quindi è necessario creare un set di dati di output anche se l'attività non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="0212f-381">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="0212f-382">Se l'attività non richiede input, è possibile ignorare la creazione del set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="0212f-382">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 
- <span data-ttu-id="0212f-383">Questa esercitazione non illustra come copiare dati con Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-383">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="0212f-384">Per un'esercitazione su come copiare dati usando Azure Data Factory, vedere [Copiare dati da un archivio BLOB al database SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0212f-384">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>


## <a name="use-server-explorer-to-view-data-factories"></a><span data-ttu-id="0212f-385">Usare Esplora Server per visualizzare le data factory</span><span class="sxs-lookup"><span data-stu-id="0212f-385">Use Server Explorer to view data factories</span></span>
1. <span data-ttu-id="0212f-386">In **Visual Studio** fare clic su **Visualizza** nel menu e fare clic su **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="0212f-386">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="0212f-387">Nella finestra Esplora server espandere **Azure** e **Data factory**.</span><span class="sxs-lookup"><span data-stu-id="0212f-387">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="0212f-388">Se viene visualizzata la finestra **Accedi a Visual Studio**, immettere l'**account** associato alla sottoscrizione di Azure e fare clic su **Continua**.</span><span class="sxs-lookup"><span data-stu-id="0212f-388">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="0212f-389">Immettere la **password** e fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="0212f-389">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="0212f-390">Visual Studio cerca di ottenere le informazioni su tutte le data factory di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0212f-390">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="0212f-391">Lo stato di questa operazione viene visualizzato nella finestra **Data Factory Task List** (Elenco attività Data Factory).</span><span class="sxs-lookup"><span data-stu-id="0212f-391">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![Esplora server](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. <span data-ttu-id="0212f-393">È possibile fare clic con il pulsante destro del mouse su una data factory e scegliere l'opzione **Export Data Factory to New Project** (Esporta la data factory in un nuovo progetto) per creare un progetto di Visual Studio basato su una data factory esistente.</span><span class="sxs-lookup"><span data-stu-id="0212f-393">You can right-click a data factory, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![Data factory di Azure](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="0212f-395">Aggiornare gli strumenti di Data factory di Azure per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0212f-395">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="0212f-396">Per aggiornare gli strumenti di Azure Data Factory per Visual Studio, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="0212f-396">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="0212f-397">Fare clic su **Strumenti**nel menu e selezionare **Estensioni e aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="0212f-397">Click **Tools** on the menu and select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="0212f-398">Selezionare **Aggiornamenti** nel riquadro sinistro e quindi selezionare **Visual Studio Gallery**.</span><span class="sxs-lookup"><span data-stu-id="0212f-398">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="0212f-399">Selezionare **Azure Data Factory tools for Visual Studio** e fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="0212f-399">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="0212f-400">Se questa voce non è visibile, si dispone già della versione più recente dello strumento.</span><span class="sxs-lookup"><span data-stu-id="0212f-400">If you do not see this entry, you already have the latest version of the tools.</span></span>

## <a name="use-configuration-files"></a><span data-ttu-id="0212f-401">Usare i file di configurazione</span><span class="sxs-lookup"><span data-stu-id="0212f-401">Use configuration files</span></span>
<span data-ttu-id="0212f-402">È possibile usare i file di configurazione in Visual Studio per configurare le proprietà di pipeline/tabelle/servizi collegati in modo diverso a seconda dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="0212f-402">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="0212f-403">Considerare la definizione JSON seguente per un servizio collegato Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-403">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="0212f-404">Per specificare **connectionString** con valori diversi per accountname e accountkey in base all'ambiente di sviluppo, di test o di produzione, in cui vengono distribuite le entità di Data Factory,</span><span class="sxs-lookup"><span data-stu-id="0212f-404">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="0212f-405">usare un file di configurazione separato per ogni ambiente.</span><span class="sxs-lookup"><span data-stu-id="0212f-405">You can achieve this behavior by using separate configuration file for each environment.</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a><span data-ttu-id="0212f-406">Aggiungere un file di configurazione</span><span class="sxs-lookup"><span data-stu-id="0212f-406">Add a configuration file</span></span>
<span data-ttu-id="0212f-407">Per aggiungere un file di configurazione per ogni ambiente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0212f-407">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="0212f-408">Fare clic con il pulsante destro del mouse sul progetto Data Factory nella soluzione di Visual Studio, scegliere **Aggiungi** e fare clic su **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="0212f-408">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="0212f-409">Selezionare **Config** nell'elenco di modelli installati a sinistra, selezionare **File di configurazione**, immettere un **nome** per il file di configurazione e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0212f-409">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![Aggiungere un file di configurazione](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="0212f-411">Aggiungere i parametri di configurazione e i relativi valori nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="0212f-411">Add configuration parameters and their values in the following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="0212f-412">Questo esempio configura la proprietà connectionString di un servizio collegato Archiviazione di Azure e di un servizio collegato Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="0212f-412">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="0212f-413">Si noti che la sintassi per specificare il nome è [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="0212f-413">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="0212f-414">Se JSON ha una proprietà con una matrice di valori come indicato nel codice seguente:</span><span class="sxs-lookup"><span data-stu-id="0212f-414">If JSON has a property that has an array of values as shown in the following code:</span></span>  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    <span data-ttu-id="0212f-415">Configurare le proprietà come illustrato nel file di configurazione seguente, ovvero usare l'indicizzazione in base zero:</span><span class="sxs-lookup"><span data-stu-id="0212f-415">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="0212f-416">Nomi delle proprietà con spazi</span><span class="sxs-lookup"><span data-stu-id="0212f-416">Property names with spaces</span></span>
<span data-ttu-id="0212f-417">Se il nome di una proprietà contiene spazi, usare le parentesi quadre come illustrato nell'esempio seguente per il nome del server di database:</span><span class="sxs-lookup"><span data-stu-id="0212f-417">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="0212f-418">Distribuire la soluzione usando una configurazione</span><span class="sxs-lookup"><span data-stu-id="0212f-418">Deploy solution using a configuration</span></span>
<span data-ttu-id="0212f-419">Quando si pubblicano entità di Data factory di Azure in VS, è possibile specificare la configurazione che si vuole usare per tale operazione di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="0212f-419">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="0212f-420">Per pubblicare entità in un progetto di Data factory di Azure usando il file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="0212f-420">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="0212f-421">Fare clic con il pulsante destro del mouse sul progetto Data Factory e scegliere **Pubblica** per visualizzare la finestra di dialogo **Publish Items** (Pubblica elementi).</span><span class="sxs-lookup"><span data-stu-id="0212f-421">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="0212f-422">Selezionare una data factory esistente o specificare i valori per crearne una nella pagina **Configure data factory** (Configura data factory) e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0212f-422">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="0212f-423">Nella pagina **Publish Items** (Pubblica elementi) è presente un elenco a discesa con le configurazioni disponibili per il campo **Select Deployment Config** (Seleziona configurazione di distribuzione).</span><span class="sxs-lookup"><span data-stu-id="0212f-423">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![Selezionare un file di configurazione](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="0212f-425">Selezionare il **file di configurazione** che si vuole usare e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0212f-425">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="0212f-426">Verificare che il nome del file JSON sia presente nella pagina **Riepilogo** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0212f-426">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="0212f-427">Fare clic su **Fine** al termine dell'operazione di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0212f-427">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="0212f-428">Al momento della distribuzione, i valori del file di configurazione vengono usati per impostare i valori per le proprietà nei file JSON prima che le entità vengano distribuite nel servizio Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-428">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="0212f-429">Usare l'Insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="0212f-429">Use Azure Key Vault</span></span>
<span data-ttu-id="0212f-430">Non è consigliabile ed è spesso contrario ai criteri di sicurezza eseguire il commit di dati sensibili come le stringhe di connessione nel repository del codice.</span><span class="sxs-lookup"><span data-stu-id="0212f-430">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="0212f-431">Per altre informazioni sull'archiviazione di informazioni riservate in Azure Key Vault e sul relativo uso durante la pubblicazione di entità di Data Factory, vedere l'esempio di [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) in GitHub.</span><span class="sxs-lookup"><span data-stu-id="0212f-431">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="0212f-432">L'estensione Secure Publish per Visual Studio permette di archiviare i segreti in Key Vault, mentre in servizi collegati o configurazioni di distribuzione vengono specificati solo riferimenti a tali segreti.</span><span class="sxs-lookup"><span data-stu-id="0212f-432">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="0212f-433">I riferimenti vengono risolti quando si pubblicano entità di Data Factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-433">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="0212f-434">È possibile eseguire il commit di questi file al repository di origine senza esporre i segreti.</span><span class="sxs-lookup"><span data-stu-id="0212f-434">These files can then be committed to source repository without exposing any secrets.</span></span>

## <a name="summary"></a><span data-ttu-id="0212f-435">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="0212f-435">Summary</span></span>
<span data-ttu-id="0212f-436">In questa esercitazione è stata creata un'istanza di Azure Data Factory per elaborare i dati eseguendo lo script Hive in un cluster Hadoop di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0212f-436">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="0212f-437">È stato usato l'editor di Data Factory nel portale di Azure per eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0212f-437">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="0212f-438">Creare un'istanza di Azure **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="0212f-438">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="0212f-439">Creare due **servizi collegati**:</span><span class="sxs-lookup"><span data-stu-id="0212f-439">Created two **linked services**:</span></span>
   1. <span data-ttu-id="0212f-440">**Archiviazione di Azure** per collegare l'archivio BLOB di Azure che contiene i file di input/output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-440">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="0212f-441">**Azure HDInsight** per collegare un cluster Hadoop di HDInsight alla data factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-441">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="0212f-442">Azure Data Factory crea un cluster Hadoop di HDInsight JIT per elaborare i dati di input e generare i dati di output.</span><span class="sxs-lookup"><span data-stu-id="0212f-442">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="0212f-443">Creare due **set di dati**che descrivono i dati di input e di output per l'attività Hive di HDInsight nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="0212f-443">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="0212f-444">Creare una **pipeline** con un'attività **Hive di HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0212f-444">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="0212f-445">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0212f-445">Next Steps</span></span>
<span data-ttu-id="0212f-446">In questo articolo è stata creata una pipeline con un'attività di trasformazione (attività HDInsight) che esegue uno script Hive in un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="0212f-446">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="0212f-447">Per informazioni su come usare un'attività di copia per copiare i dati da un BLOB di Azure ad Azure SQL, vedere [Esercitazione: Copiare i dati di un BLOB di Azure in Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0212f-447">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="0212f-448">È possibile concatenare due attività, ovvero eseguire un'attività dopo l'altra, impostando il set di dati di output di un'attività come set di dati di input di altre attività.</span><span class="sxs-lookup"><span data-stu-id="0212f-448">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="0212f-449">Per informazioni dettagliate, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="0212f-449">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 


## <a name="see-also"></a><span data-ttu-id="0212f-450">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0212f-450">See Also</span></span>
| <span data-ttu-id="0212f-451">Argomento</span><span class="sxs-lookup"><span data-stu-id="0212f-451">Topic</span></span> | <span data-ttu-id="0212f-452">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0212f-452">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="0212f-453">Pipeline</span><span class="sxs-lookup"><span data-stu-id="0212f-453">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="0212f-454">Questo articolo contiene informazioni sulle pipeline e sulle attività in Azure Data Factory e su come usarle per costruire flussi di lavoro basati sui dati per lo scenario o l'azienda.</span><span class="sxs-lookup"><span data-stu-id="0212f-454">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="0212f-455">Set di dati</span><span class="sxs-lookup"><span data-stu-id="0212f-455">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="0212f-456">Questo articolo fornisce informazioni sui set di dati in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-456">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="0212f-457">Attività di trasformazione dei dati</span><span class="sxs-lookup"><span data-stu-id="0212f-457">Data Transformation Activities</span></span>](data-factory-data-transformation-activities.md) |<span data-ttu-id="0212f-458">Questo articolo fornisce un elenco di attività di trasformazione dei dati (ad esempio, la trasformazione Hive di HDInsight usata in questa esercitazione) supportate da Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0212f-458">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span></span> |
| [<span data-ttu-id="0212f-459">Pianificazione ed esecuzione</span><span class="sxs-lookup"><span data-stu-id="0212f-459">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="0212f-460">Questo articolo descrive gli aspetti di pianificazione ed esecuzione del modello applicativo di Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="0212f-460">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="0212f-461">Monitorare e gestire le pipeline con l'app di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="0212f-461">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="0212f-462">Questo articolo descrive come monitorare, gestire ed eseguire il debug delle pipeline usando l'app di monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="0212f-462">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
