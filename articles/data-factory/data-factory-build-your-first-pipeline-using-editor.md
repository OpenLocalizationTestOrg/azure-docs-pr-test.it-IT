---
title: Creare la prima data factory di Azure con il Portale di Azure | Microsoft Docs
description: In questa esercitazione viene creata una pipeline di esempio di Azure Data Factory usando l'editor di Data Factory nel portale di Azure.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 9c958aecb841fa02349c6b9e5e1984f6ba4fb611
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="97900-103">Esercitazione: Creare la prima data factory di Azure con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="97900-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97900-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="97900-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="97900-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="97900-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="97900-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="97900-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="97900-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="97900-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="97900-108">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="97900-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="97900-109">API REST</span><span class="sxs-lookup"><span data-stu-id="97900-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="97900-110">Questo articolo descrive come usare il [portale di Azure](https://portal.azure.com/) per creare la prima istanza di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="97900-110">In this article, you learn how to use [Azure portal](https://portal.azure.com/) to create your first Azure data factory.</span></span> <span data-ttu-id="97900-111">Per eseguire l'esercitazione usando altri strumenti/SDK, selezionare una delle opzioni dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="97900-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span> 

<span data-ttu-id="97900-112">La pipeline in questa esercitazione include un'attività, l'**attività Hive di HDInsight**,</span><span class="sxs-lookup"><span data-stu-id="97900-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="97900-113">che esegue uno script Hive in un cluster Azure HDInsight per trasformare i dati di input e generare i dati di output.</span><span class="sxs-lookup"><span data-stu-id="97900-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="97900-114">L'esecuzione della pipeline è pianificata una volta al mese tra le ore di inizio e di fine specificate.</span><span class="sxs-lookup"><span data-stu-id="97900-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="97900-115">La pipeline di dati in questa esercitazione trasforma i dati di input per produrre dati di output.</span><span class="sxs-lookup"><span data-stu-id="97900-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="97900-116">Per un'esercitazione su come copiare dati usando Azure Data Factory, vedere [Copiare dati da un archivio BLOB al database SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="97900-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="97900-117">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="97900-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="97900-118">ed è possibile concatenarne due, ovvero eseguire un'attività dopo l'altra, impostando il set di dati di output di un'attività come set di dati di input dell'altra.</span><span class="sxs-lookup"><span data-stu-id="97900-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="97900-119">Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="97900-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97900-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="97900-120">Prerequisites</span></span>
1. <span data-ttu-id="97900-121">Vedere la [panoramica dell'esercitazione](data-factory-build-your-first-pipeline.md) ed eseguire i passaggi relativi ai **prerequisiti** .</span><span class="sxs-lookup"><span data-stu-id="97900-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
2. <span data-ttu-id="97900-122">Questo articolo non fornisce una panoramica concettuale del servizio Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="97900-122">This article does not provide a conceptual overview of the Azure Data Factory service.</span></span> <span data-ttu-id="97900-123">Si consiglia di leggere l'articolo [Introduzione al servizio Data factory di Azure](data-factory-introduction.md) per una panoramica dettagliata del servizio.</span><span class="sxs-lookup"><span data-stu-id="97900-123">We recommend that you go through [Introduction to Azure Data Factory](data-factory-introduction.md) article for a detailed overview of the service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="97900-124">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="97900-124">Create data factory</span></span>
<span data-ttu-id="97900-125">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="97900-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="97900-126">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="97900-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="97900-127">Ad esempio, un'attività di copia per copiare dati da un archivio dati di origine a uno di destinazione e un'attività Hive HDInsight per eseguire uno script Hive e trasformare i dati di input in dati di output di prodotto.</span><span class="sxs-lookup"><span data-stu-id="97900-127">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="97900-128">In questo passaggio iniziale viene creata la data factory.</span><span class="sxs-lookup"><span data-stu-id="97900-128">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="97900-129">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="97900-129">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="97900-130">Fare clic su **NUOVO** nel menu a sinistra e quindi su **Dati e analisi** e **Data factory**.</span><span class="sxs-lookup"><span data-stu-id="97900-130">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Pannello Crea](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="97900-132">Nel pannello **Nuova data factory** immettere **GetStartedDF** come nome.</span><span class="sxs-lookup"><span data-stu-id="97900-132">In the **New data factory** blade, enter **GetStartedDF** for the Name.</span></span>

   ![Pannello Nuova data factory](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="97900-134">Il nome della data factory di Azure deve essere **univoco a livello globale**.</span><span class="sxs-lookup"><span data-stu-id="97900-134">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="97900-135">Se viene visualizzato l'errore **Il nome "GetStartedDF" per la data factory non è disponibile**,</span><span class="sxs-lookup"><span data-stu-id="97900-135">If you receive the error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="97900-136">cambiare il nome della data factory, ad esempio nomeutenteGetStartedDF, e provare di nuovo a crearla.</span><span class="sxs-lookup"><span data-stu-id="97900-136">Change the name of the data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="97900-137">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="97900-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="97900-138">Il nome della data factory può essere registrato in futuro come nome **DNS** e diventare quindi visibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="97900-138">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="97900-139">Selezionare la **sottoscrizione di Azure** in cui creare la data factory.</span><span class="sxs-lookup"><span data-stu-id="97900-139">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="97900-140">Selezionare un **gruppo di risorse** esistente o crearne uno.</span><span class="sxs-lookup"><span data-stu-id="97900-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="97900-141">Per l'esercitazione creare un gruppo di risorse denominato **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="97900-141">For the tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="97900-142">Selezionare la **località** per la data factory.</span><span class="sxs-lookup"><span data-stu-id="97900-142">Select the **location** for the data factory.</span></span> <span data-ttu-id="97900-143">Nell'elenco a discesa vengono visualizzate solo le aree supportate dal servizio Data Factory.</span><span class="sxs-lookup"><span data-stu-id="97900-143">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
7. <span data-ttu-id="97900-144">Selezionare **Aggiungi al dashboard**.</span><span class="sxs-lookup"><span data-stu-id="97900-144">Select **Pin to dashboard**.</span></span> 
8. <span data-ttu-id="97900-145">Fare clic su **Crea** nel pannello **Nuova data factory**.</span><span class="sxs-lookup"><span data-stu-id="97900-145">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="97900-146">Per creare istanze di data factory, è necessario essere membri del ruolo [Collaboratore Data factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) a livello di sottoscrizione/gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97900-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="97900-147">Nel dashboard viene visualizzato il riquadro seguente con lo stato: Deploying data factory (Distribuzione della data factory).</span><span class="sxs-lookup"><span data-stu-id="97900-147">On the dashboard, you see the following tile with status: Deploying data factory.</span></span>    

   ![Stato creazione della data factory](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="97900-149">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="97900-149">Congratulations!</span></span> <span data-ttu-id="97900-150">La creazione della prima data factory è così completata.</span><span class="sxs-lookup"><span data-stu-id="97900-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="97900-151">Dopo la creazione della data factory, viene visualizzata la pagina corrispondente con elencato il contenuto della data factory.</span><span class="sxs-lookup"><span data-stu-id="97900-151">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>     

    ![Pannello Data factory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="97900-153">Prima di creare una pipeline nella data factory è necessario creare alcune entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="97900-153">Before creating a pipeline in the data factory, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="97900-154">Creare prima di tutto i servizi collegati per collegare archivi dati/servizi di calcolo all'archivio dati, definire i set di dati di input e di output per rappresentare i dati di input/output negli archivi dati collegati e quindi creare la pipeline con un'attività che usa questi set di dati.</span><span class="sxs-lookup"><span data-stu-id="97900-154">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="97900-155">Creazione di servizi collegati</span><span class="sxs-lookup"><span data-stu-id="97900-155">Create linked services</span></span>
<span data-ttu-id="97900-156">In questo passaggio l'account di archiviazione di Azure e un cluster HDInsight su richiesta di Azure vengono collegati alla data factory.</span><span class="sxs-lookup"><span data-stu-id="97900-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="97900-157">In questo esempio l'account di archiviazione di Azure contiene i dati di input e di output per la pipeline.</span><span class="sxs-lookup"><span data-stu-id="97900-157">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="97900-158">Il servizio HDInsight collegato viene usato per eseguire uno script Hive specificato nell'attività della pipeline in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="97900-158">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="97900-159">Identificare l'[archivio dati](data-factory-data-movement-activities.md)/[i servizi di calcolo](data-factory-compute-linked-services.md) usati nello scenario e collegare tali servizi alla data factory creando servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="97900-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services to the data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="97900-160">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="97900-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="97900-161">In questo passaggio l'account di archiviazione di Azure viene collegato alla data factory.</span><span class="sxs-lookup"><span data-stu-id="97900-161">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="97900-162">In questa esercitazione viene usato lo stesso account di archiviazione di Azure per archiviare i dati di input/output e il file di script HQL.</span><span class="sxs-lookup"><span data-stu-id="97900-162">In this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="97900-163">Fare clic su **Creare e distribuire** nel pannello **DATA FACTORY** relativo a **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="97900-163">Click **Author and deploy** on the **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="97900-164">Verrà visualizzato l'editor di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="97900-164">You should see the Data Factory Editor.</span></span>

   ![Riquadro Creare e distribuire](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="97900-166">Fare clic su **Nuovo archivio dati** e scegliere **Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="97900-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nuovo archivio dati - Archiviazione di Azure - Menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="97900-168">Nell'editor verrà visualizzato lo script JSON per la creazione di un servizio collegato Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="97900-168">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![Servizio collegato Archiviazione di Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="97900-170">Sostituire **account name** con il nome dell'account di archiviazione di Azure e **account key** con la chiave di accesso dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="97900-170">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="97900-171">Per informazioni su come ottenere la chiave di accesso alle risorse di archiviazione, vedere le informazioni su come visualizzare, copiare e rigenerare le chiavi di accesso alle risorse di archiviazione in [Gestire l'account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="97900-171">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="97900-172">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="97900-172">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Pulsante Distribuisci](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="97900-174">Al termine della distribuzione del servizio collegato, la finestra **Bozza-1** verrà nascosta e nella visualizzazione albero a sinistra verrà visualizzato **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="97900-174">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

    ![Servizio collegato Archiviazione nel menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="97900-176">Creare un servizio collegato Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="97900-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="97900-177">In questo passaggio viene collegato un cluster HDInsight su richiesta alla data factory.</span><span class="sxs-lookup"><span data-stu-id="97900-177">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="97900-178">Il cluster HDInsight viene creato automaticamente in fase di esecuzione ed eliminato al termine dell'elaborazione, se rimane inattivo per il periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="97900-178">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span>

1. <span data-ttu-id="97900-179">Nell'**editor di Data Factory** fare clic su **... Altro** e quindi su **Nuovo calcolo** e selezionare **Cluster HDInsight su richiesta**.</span><span class="sxs-lookup"><span data-stu-id="97900-179">In the **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Nuovo calcolo](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="97900-181">Copiare e incollare il frammento di codice seguente nella finestra **Bozza-1** .</span><span class="sxs-lookup"><span data-stu-id="97900-181">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="97900-182">Il frammento di codice JSON descrive le proprietà che vengono usate per creare il cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="97900-182">The JSON snippet describes the properties that are used to create the HDInsight cluster on-demand.</span></span>

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    <span data-ttu-id="97900-183">La tabella seguente fornisce le descrizioni delle proprietà JSON usate nel frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="97900-183">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="97900-184">Proprietà</span><span class="sxs-lookup"><span data-stu-id="97900-184">Property</span></span> | <span data-ttu-id="97900-185">Descrizione</span><span class="sxs-lookup"><span data-stu-id="97900-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="97900-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="97900-186">ClusterSize</span></span> |<span data-ttu-id="97900-187">Specifica le dimensioni del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97900-187">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="97900-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="97900-188">TimeToLive</span></span> | <span data-ttu-id="97900-189">Specifica il tempo di inattività del cluster HDInsight, prima che sia eliminato.</span><span class="sxs-lookup"><span data-stu-id="97900-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="97900-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="97900-190">linkedServiceName</span></span> | <span data-ttu-id="97900-191">Specifica l'account di archiviazione che viene usato per archiviare i log generati da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97900-191">Specifies the storage account that is used to store the logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="97900-192">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="97900-192">Note the following points:</span></span>

   * <span data-ttu-id="97900-193">Data Factory crea automaticamente un cluster HDInsight **basato su Linux** con il codice JSON.</span><span class="sxs-lookup"><span data-stu-id="97900-193">The Data Factory creates a **Linux-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="97900-194">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="97900-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="97900-195">È possibile usare il **proprio cluster HDInsight** anziché un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="97900-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="97900-196">Per i dettagli, vedere [Servizio collegato Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="97900-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="97900-197">Il cluster HDInsight crea un **contenitore predefinito** nell'archivio BLOB specificato nel file JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="97900-197">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="97900-198">HDInsight non elimina il contenitore quando viene eliminato il cluster.</span><span class="sxs-lookup"><span data-stu-id="97900-198">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="97900-199">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="97900-199">This behavior is by design.</span></span> <span data-ttu-id="97900-200">Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che viene elaborata una sezione, a meno che non esista un cluster attivo (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="97900-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="97900-201">Il cluster viene eliminato al termine dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="97900-201">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="97900-202">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="97900-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="97900-203">Se non sono necessari per risolvere i problemi relativi ai processi, è possibile eliminarli per ridurre i costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="97900-203">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="97900-204">I nomi dei contenitori seguono questo schema: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="97900-204">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="97900-205">Per eliminare i contenitori nell'archivio BLOB di Azure, usare strumenti come [Microsoft Azure Storage Explorer](http://storageexplorer.com/) .</span><span class="sxs-lookup"><span data-stu-id="97900-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="97900-206">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="97900-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="97900-207">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="97900-207">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Distribuire il servizio collegato HDInsight su richiesta](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="97900-209">Verificare che nella visualizzazione albero a sinistra siano presenti sia **AzureStorageLinkedService** che **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="97900-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in the tree view on the left.</span></span>

    ![Visualizzazione albero con servizi collegati](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="97900-211">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="97900-211">Create datasets</span></span>
<span data-ttu-id="97900-212">In questo passaggio vengono creati set di dati per rappresentare i dati di input e di output per l'elaborazione Hive.</span><span class="sxs-lookup"><span data-stu-id="97900-212">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="97900-213">I set di dati fanno riferimento all'oggetto **AzureStorageLinkedService** creato in precedenza in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="97900-213">These datasets refer to the **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="97900-214">Il servizio collegato punta a un account di archiviazione di Azure e i set di dati specificano il contenitore, la cartella e il nome del file nella risorsa di archiviazione che contiene i dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="97900-214">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="97900-215">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="97900-215">Create input dataset</span></span>
1. <span data-ttu-id="97900-216">Nell'**editor di Data Factory** fare clic su **... Altro** sulla barra dei comandi e quindi fare clic su **Nuovo set di dati** e selezionare **Archivio BLOB di Azure**.</span><span class="sxs-lookup"><span data-stu-id="97900-216">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Nuovo set di dati](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="97900-218">Copiare e incollare il frammento di codice seguente nella finestra Bozza-1.</span><span class="sxs-lookup"><span data-stu-id="97900-218">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="97900-219">Nel frammento di codice JSON si crea un set di dati denominato **AzureBlobInput** che rappresenta i dati di input per un'attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="97900-219">In the JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="97900-220">Si specifica anche che i dati di input si trovano nel contenitore BLOB denominato **adfgetstarted** e nella cartella denominata **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="97900-220">In addition, you specify that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
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
    <span data-ttu-id="97900-221">La tabella seguente fornisce le descrizioni delle proprietà JSON usate nel frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="97900-221">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="97900-222">Proprietà</span><span class="sxs-lookup"><span data-stu-id="97900-222">Property</span></span> | <span data-ttu-id="97900-223">Descrizione</span><span class="sxs-lookup"><span data-stu-id="97900-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="97900-224">type</span><span class="sxs-lookup"><span data-stu-id="97900-224">type</span></span> |<span data-ttu-id="97900-225">La proprietà type è impostata su **AzureBlob** perché i dati risiedono in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="97900-225">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="97900-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="97900-226">linkedServiceName</span></span> |<span data-ttu-id="97900-227">Fa riferimento all'oggetto **AzureStorageLinkedService** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="97900-227">Refers to the **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="97900-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="97900-228">folderPath</span></span> | <span data-ttu-id="97900-229">Specifica il **contenitore** BLOB e la **cartella** che contiene i BLOB di input.</span><span class="sxs-lookup"><span data-stu-id="97900-229">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="97900-230">fileName</span><span class="sxs-lookup"><span data-stu-id="97900-230">fileName</span></span> |<span data-ttu-id="97900-231">Questa proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="97900-231">This property is optional.</span></span> <span data-ttu-id="97900-232">Se si omette questa proprietà, vengono prelevati tutti i file da folderPath.</span><span class="sxs-lookup"><span data-stu-id="97900-232">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="97900-233">In questo tutorial viene elaborato solo il file **input.log**.</span><span class="sxs-lookup"><span data-stu-id="97900-233">In this tutorial, only the **input.log** is processed.</span></span> |
   | <span data-ttu-id="97900-234">type</span><span class="sxs-lookup"><span data-stu-id="97900-234">type</span></span> |<span data-ttu-id="97900-235">I file di log sono in formato testo, quindi viene usato **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="97900-235">The log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="97900-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="97900-236">columnDelimiter</span></span> |<span data-ttu-id="97900-237">Le colonne nei file di log sono delimitate da **virgola (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="97900-237">columns in the log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="97900-238">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="97900-238">frequency/interval</span></span> |<span data-ttu-id="97900-239">La frequenza è impostata su **Month** e l'intervallo è **1**; ciò significa che le sezioni di input sono disponibili con cadenza mensile.</span><span class="sxs-lookup"><span data-stu-id="97900-239">frequency set to **Month** and interval is **1**, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="97900-240">external</span><span class="sxs-lookup"><span data-stu-id="97900-240">external</span></span> | <span data-ttu-id="97900-241">Questa proprietà è impostata su **true** se i dati di input non vengono generati dalla pipeline.</span><span class="sxs-lookup"><span data-stu-id="97900-241">This property is set to **true** if the input data is not generated by this pipeline.</span></span> <span data-ttu-id="97900-242">In questa esercitazione il file input.log non viene generato dalla pipeline, quindi questa proprietà viene impostata su true.</span><span class="sxs-lookup"><span data-stu-id="97900-242">In this tutorial, the input.log file is not generated by this pipeline, so we set the property to true.</span></span> |

    <span data-ttu-id="97900-243">Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="97900-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="97900-244">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire il set di dati appena creato.</span><span class="sxs-lookup"><span data-stu-id="97900-244">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span> <span data-ttu-id="97900-245">Il set di dati viene visualizzato nella visualizzazione albero a sinistra.</span><span class="sxs-lookup"><span data-stu-id="97900-245">You should see the dataset in the tree view on the left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="97900-246">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="97900-246">Create output dataset</span></span>
<span data-ttu-id="97900-247">Viene creato ora il set di dati di output per rappresentare i dati di output archiviati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="97900-247">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="97900-248">Nell'**editor di Data Factory** fare clic su **... Altro** sulla barra dei comandi e quindi fare clic su **Nuovo set di dati** e selezionare **Archivio BLOB di Azure**.</span><span class="sxs-lookup"><span data-stu-id="97900-248">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="97900-249">Copiare e incollare il frammento di codice seguente nella finestra Bozza-1.</span><span class="sxs-lookup"><span data-stu-id="97900-249">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="97900-250">Nel frammento di codice JSON si crea un set di dati denominato **AzureBlobOutput**e si specifica la struttura dei dati che vengono generati dallo script Hive.</span><span class="sxs-lookup"><span data-stu-id="97900-250">In the JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying the structure of the data that is produced by the Hive script.</span></span> <span data-ttu-id="97900-251">Si specifica anche che i risultati vengono archiviati nel contenitore BLOB denominato **adfgetstarted** e nella cartella denominata **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="97900-251">In addition, you specify that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="97900-252">La sezione **availability** specifica che il set di dati di output viene generato su base mensile.</span><span class="sxs-lookup"><span data-stu-id="97900-252">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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
    <span data-ttu-id="97900-253">Per le descrizioni di queste proprietà, vedere la sezione **Creare il set di dati di input** .</span><span class="sxs-lookup"><span data-stu-id="97900-253">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="97900-254">La proprietà esterna non viene impostata su un set di dati di output perché il set di dati viene generato dal servizio Data factory.</span><span class="sxs-lookup"><span data-stu-id="97900-254">You do not set the external property on an output dataset as the dataset is produced by the Data Factory service.</span></span>
3. <span data-ttu-id="97900-255">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire il set di dati appena creato.</span><span class="sxs-lookup"><span data-stu-id="97900-255">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span>
4. <span data-ttu-id="97900-256">Verificare se il set di dati è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="97900-256">Verify that the dataset is created successfully.</span></span>

    ![Visualizzazione albero con servizi collegati](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="97900-258">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="97900-258">Create pipeline</span></span>
<span data-ttu-id="97900-259">In questo passaggio viene creata la prima pipeline con un'attività **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="97900-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="97900-260">La sezione di input è disponibile ogni mese (frequency: Month, interval: 1), la sezione di output viene generata ogni mese e anche la proprietà dell'utilità di pianificazione dell'attività è impostata su una frequenza mensile.</span><span class="sxs-lookup"><span data-stu-id="97900-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="97900-261">Le impostazioni per il set di dati di output e l'utilità di pianificazione dell'attività devono corrispondere.</span><span class="sxs-lookup"><span data-stu-id="97900-261">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="97900-262">In questo momento la pianificazione è basata sul set di dati di output, quindi è necessario creare un set di dati di output anche se l'attività non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="97900-262">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="97900-263">Se l'attività non richiede input, è possibile ignorare la creazione del set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="97900-263">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="97900-264">Le proprietà usate nel codice JSON seguente sono illustrate in fondo a questa sezione.</span><span class="sxs-lookup"><span data-stu-id="97900-264">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="97900-265">Nell'**editor di Data Factory** fare clic sui **puntini di sospensione (…)** per visualizzare altri comandi e quindi su **Nuova pipeline**.</span><span class="sxs-lookup"><span data-stu-id="97900-265">In the **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![Pulsante Nuova pipeline](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="97900-267">Copiare e incollare il frammento di codice seguente nella finestra Bozza-1.</span><span class="sxs-lookup"><span data-stu-id="97900-267">Copy and paste the following snippet to the Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="97900-268">Nel codice JSON sostituire **storageaccountname** con il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="97900-268">Replace **storageaccountname** with the name of your storage account in the JSON.</span></span>
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    <span data-ttu-id="97900-269">Nel frammento di codice JSON si crea una pipeline costituita da una singola attività che usa Hive per elaborare i dati in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97900-269">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="97900-270">Il file di script Hive, **partitionweblogs.hql**, è archiviato nell'account di archiviazione di Azure (specificato da scriptLinkedService, denominato **AzureStorageLinkedService**) e nella cartella **script** nel contenitore **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="97900-270">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="97900-271">La sezione **defines** è usata per specificare le impostazioni di runtime che vengono passate allo script Hive come valori di configurazione Hive, ad esempio, ${hiveconf:inputtable}, ${hiveconf:partitionedtable}.</span><span class="sxs-lookup"><span data-stu-id="97900-271">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="97900-272">Le proprietà **start** ed **end** della pipeline ne specificano il periodo attivo.</span><span class="sxs-lookup"><span data-stu-id="97900-272">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="97900-273">Nel codice JSON dell'attività si specifica che lo script Hive viene eseguito sulla risorsa di calcolo specificata da **linkedServiceName** - **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="97900-273">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="97900-274">Per informazioni dettagliate sulle proprietà JSON usate nell'esempio, vedere la sezione "Pipeline JSON" dell'articolo [Pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="97900-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the example.</span></span>
   >
   >
3. <span data-ttu-id="97900-275">Verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="97900-275">Confirm the following:</span></span>

   1. <span data-ttu-id="97900-276">Il file **input.log** è presente nella cartella **inputdata** del contenitore **adfgetstarted** nell'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="97900-276">**input.log** file exists in the **inputdata** folder of the **adfgetstarted** container in the Azure blob storage</span></span>
   2. <span data-ttu-id="97900-277">Il file **partitionweblogs.hql** è presente nella cartella **script** del contenitore **adfgetstarted** nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="97900-277">**partitionweblogs.hql** file exists in the **script** folder of the **adfgetstarted** container in the Azure blob storage.</span></span> <span data-ttu-id="97900-278">Se questi file non sono visibili, completare i passaggi preliminari nella sezione [Panoramica dell'esercitazione](data-factory-build-your-first-pipeline.md) .</span><span class="sxs-lookup"><span data-stu-id="97900-278">Complete the prerequisite steps in the [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="97900-279">Verificare di avere sostituito **storageaccountname** con il nome dell'account di archiviazione nel codice JSON della pipeline.</span><span class="sxs-lookup"><span data-stu-id="97900-279">Confirm that you replaced **storageaccountname** with the name of your storage account in the pipeline JSON.</span></span>
4. <span data-ttu-id="97900-280">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="97900-280">Click **Deploy** on the command bar to deploy the pipeline.</span></span> <span data-ttu-id="97900-281">Dal momento che gli orari di **inizio** e **fine** sono impostati nel passato e **isPaused** è impostato su false, la pipeline (l'attività nella pipeline) viene eseguita immediatamente dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="97900-281">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="97900-282">Verificare che la pipeline sia visibile nella visualizzazione albero.</span><span class="sxs-lookup"><span data-stu-id="97900-282">Confirm that you see the pipeline in the tree view.</span></span>

    ![Visualizzazione albero con pipeline](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="97900-284">La creazione della prima pipeline è così completata.</span><span class="sxs-lookup"><span data-stu-id="97900-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="97900-285">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="97900-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="97900-286">Monitorare la pipeline con la vista diagramma</span><span class="sxs-lookup"><span data-stu-id="97900-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="97900-287">Fare clic su **X** per chiudere i pannelli dell'editor di Data Factory, tornare al pannello Data Factory e quindi fare clic su **Diagramma**.</span><span class="sxs-lookup"><span data-stu-id="97900-287">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![Riquadro Diagramma](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="97900-289">In Vista diagramma saranno visualizzati una panoramica delle pipeline e i set di dati usati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="97900-289">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Vista Diagramma](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="97900-291">Per visualizzare tutte le attività nella pipeline, fare clic con il pulsante destro del mouse sulla pipeline nel diagramma e scegliere Apri pipeline.</span><span class="sxs-lookup"><span data-stu-id="97900-291">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![Menu Apri pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="97900-293">Assicurarsi che l'attività HDInsightHive sia visualizzata nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="97900-293">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![Visualizzazione Apri pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="97900-295">Per tornare alla visualizzazione precedente, fare clic su **Data Factory** nel menu di navigazione nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="97900-295">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
5. <span data-ttu-id="97900-296">In **Vista diagramma** fare doppio clic sul set di dati **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="97900-296">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="97900-297">Verificare che lo stato della sezione sia **Pronto** .</span><span class="sxs-lookup"><span data-stu-id="97900-297">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="97900-298">Potrebbero essere necessari alcuni minuti perché lo stato della sezione venga visualizzato come Pronto.</span><span class="sxs-lookup"><span data-stu-id="97900-298">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="97900-299">Se dopo qualche minuto ciò non accade, verificare che il file di input, input.log, sia posizionato nel contenitore adfgetstarted e nella cartella inputdata corretti.</span><span class="sxs-lookup"><span data-stu-id="97900-299">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Sezione di input nello stato Pronto](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="97900-301">Fare clic su **X** per chiudere il pannello **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="97900-301">Click **X** to close **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="97900-302">In **Vista diagramma** fare doppio clic sul set di dati **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="97900-302">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="97900-303">Viene visualizzata la sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="97900-303">You see that the slice that is currently being processed.</span></span>

   ![Set di dati](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="97900-305">Al termine dell'elaborazione lo stato della sezione è **Pronta** .</span><span class="sxs-lookup"><span data-stu-id="97900-305">When processing is done, you see the slice in **Ready** state.</span></span>

   ![Set di dati](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="97900-307">La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti).</span><span class="sxs-lookup"><span data-stu-id="97900-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="97900-308">Di conseguenza, prevedere **circa 30 minuti** per l'elaborazione della sezione nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="97900-308">Therefore, expect the pipeline to       take **approximately 30 minutes** to process the slice.</span></span>
   >
   >

9. <span data-ttu-id="97900-309">Quando lo stato della sezione è **Pronto**, cercare i dati di output nella cartella **partitioneddata** del contenitore **adfgetstarted** nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="97900-309">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

   ![Dati di output](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="97900-311">Fare clic sulla sezione per visualizzare i relativi dettagli in un pannello **Sezione dati** .</span><span class="sxs-lookup"><span data-stu-id="97900-311">Click the slice to see details about it in a **Data slice** blade.</span></span>

   ![Dettagli sezione dati](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="97900-313">Fare clic su un'esecuzione di attività nell'elenco **Esecuzioni attività** (in questo scenario, un'attività Hive) per visualizzare i relativi dettagli nella finestra **Dettagli esecuzione attività**.</span><span class="sxs-lookup"><span data-stu-id="97900-313">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Dettagli esecuzione attività](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="97900-315">Nei file di log sono riportate la query Hive eseguita e le informazioni sullo stato.</span><span class="sxs-lookup"><span data-stu-id="97900-315">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="97900-316">Tali file di log sono utili per risolvere eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="97900-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="97900-317">Vedere l'articolo [Monitorare e gestire le pipeline di Azure Data Factory](data-factory-monitor-manage-pipelines.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="97900-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97900-318">Il file di input viene eliminato quando la sezione viene elaborata correttamente.</span><span class="sxs-lookup"><span data-stu-id="97900-318">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="97900-319">Per eseguire di nuovo la sezione o ripetere l'esercitazione, caricare quindi il file di input (input.log) nella cartella inputdata del contenitore adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="97900-319">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="97900-320">Monitorare la pipeline con l'app Monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="97900-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="97900-321">È anche possibile usare l'applicazione Monitoraggio e gestione per monitorare le pipeline.</span><span class="sxs-lookup"><span data-stu-id="97900-321">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="97900-322">Per informazioni dettagliate sull'uso di questa applicazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory con la nuova app di monitoraggio e gestione](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="97900-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="97900-323">Fare clic sul riquadro **Monitoraggio e gestione** nella home page della data factory.</span><span class="sxs-lookup"><span data-stu-id="97900-323">Click **Monitor & Manage** tile on the home page for your data factory.</span></span>

    ![Riquadro Monitoraggio e gestione](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="97900-325">Verrà visualizzata l'applicazione **Monitoraggio e gestione**.</span><span class="sxs-lookup"><span data-stu-id="97900-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="97900-326">Modificare **Ora di inizio** e **Ora di fine** in modo che corrispondano alle ore di inizio e di fine della pipeline e quindi fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="97900-326">Change the **Start time** and **End time** to match start and end times of your pipeline, and click **Apply**.</span></span>

    ![App Monitoraggio e gestione](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="97900-328">Selezionare una finestra attività nell'elenco **Activity Windows** (Finestre attività) per visualizzare i relativi dettagli.</span><span class="sxs-lookup"><span data-stu-id="97900-328">Select an activity window in the **Activity Windows** list to see details about it.</span></span>

    ![Dettagli finestra attività](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="97900-330">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="97900-330">Summary</span></span>
<span data-ttu-id="97900-331">In questa esercitazione è stata creata un'istanza di Azure Data Factory per elaborare i dati eseguendo lo script Hive in un cluster Hadoop di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97900-331">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="97900-332">È stato usato l'editor di Data Factory nel portale di Azure per eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="97900-332">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="97900-333">Creare un'istanza di Azure **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="97900-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="97900-334">Creare due **servizi collegati**:</span><span class="sxs-lookup"><span data-stu-id="97900-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="97900-335">**Archiviazione di Azure** per collegare l'archivio BLOB di Azure che contiene i file di input/output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="97900-335">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="97900-336">**Azure HDInsight** per collegare un cluster Hadoop di HDInsight alla data factory.</span><span class="sxs-lookup"><span data-stu-id="97900-336">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="97900-337">Azure Data Factory crea un cluster Hadoop di HDInsight JIT per elaborare i dati di input e generare i dati di output.</span><span class="sxs-lookup"><span data-stu-id="97900-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="97900-338">Creare due **set di dati**che descrivono i dati di input e di output per l'attività Hive di HDInsight nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="97900-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="97900-339">Creare una **pipeline** con un'attività **Hive di HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="97900-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97900-340">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="97900-340">Next Steps</span></span>
<span data-ttu-id="97900-341">In questo articolo è stata creata una pipeline con un'attività di trasformazione (attività HDInsight) che esegue uno script Hive in un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="97900-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="97900-342">Per informazioni su come usare un'attività di copia per copiare i dati da un BLOB di Azure ad Azure SQL, vedere [Esercitazione: Copiare i dati di un BLOB di Azure in Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="97900-342">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="97900-343">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="97900-343">See Also</span></span>
| <span data-ttu-id="97900-344">Argomento</span><span class="sxs-lookup"><span data-stu-id="97900-344">Topic</span></span> | <span data-ttu-id="97900-345">Descrizione</span><span class="sxs-lookup"><span data-stu-id="97900-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="97900-346">Pipeline</span><span class="sxs-lookup"><span data-stu-id="97900-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="97900-347">Questo articolo fornisce informazioni sulle pipeline e sulle attività in Azure Data Factory e su come usarle per costruire flussi di lavoro end-to-end basati sui dati per lo scenario o l'azienda.</span><span class="sxs-lookup"><span data-stu-id="97900-347">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="97900-348">Set di dati</span><span class="sxs-lookup"><span data-stu-id="97900-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="97900-349">Questo articolo fornisce informazioni sui set di dati in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="97900-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="97900-350">Pianificazione ed esecuzione</span><span class="sxs-lookup"><span data-stu-id="97900-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="97900-351">Questo articolo descrive gli aspetti di pianificazione ed esecuzione del modello applicativo di Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="97900-351">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="97900-352">Monitorare e gestire le pipeline con l'app di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="97900-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="97900-353">Questo articolo descrive come monitorare, gestire ed eseguire il debug delle pipeline usando l'app di monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="97900-353">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
