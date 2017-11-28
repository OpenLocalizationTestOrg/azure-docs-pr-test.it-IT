---
title: aaaBuild la prima data factory (portale di Azure) | Documenti Microsoft
description: "In questa esercitazione è creare una pipeline di Data Factory di Azure di esempio utilizzando l'Editor delle Data Factory nel portale di Azure hello."
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
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="770db-103">Esercitazione: Creare la prima data factory di Azure con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="770db-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="770db-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="770db-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="770db-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="770db-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="770db-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="770db-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="770db-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="770db-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="770db-108">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="770db-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="770db-109">API REST</span><span class="sxs-lookup"><span data-stu-id="770db-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="770db-110">In questo articolo viene illustrato come toouse [portale di Azure](https://portal.azure.com/) toocreate prima data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="770db-110">In this article, you learn how toouse [Azure portal](https://portal.azure.com/) toocreate your first Azure data factory.</span></span> <span data-ttu-id="770db-111">esercitazione di hello toodo tramite altri strumenti/SDK, selezionare una delle opzioni di hello dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="770db-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span> 

<span data-ttu-id="770db-112">pipeline Hello in questa esercitazione è un'attività: **attività Hive di HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="770db-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="770db-113">Questa attività esegue uno script hive in un cluster HDInsight di Azure che trasformazioni i dati di output tooproduce di dati di input.</span><span class="sxs-lookup"><span data-stu-id="770db-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="770db-114">pipeline di Hello è toorun pianificato dopo un mese tra hello specificato di ore di inizio e fine.</span><span class="sxs-lookup"><span data-stu-id="770db-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="770db-115">pipeline di dati Hello in questa esercitazione Trasforma i dati di output tooproduce di dati di input.</span><span class="sxs-lookup"><span data-stu-id="770db-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="770db-116">Per un'esercitazione su come dati di toocopy tramite Data Factory di Azure, vedere [esercitazione: copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="770db-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="770db-117">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="770db-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="770db-118">Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="770db-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="770db-119">Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="770db-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="770db-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="770db-120">Prerequisites</span></span>
1. <span data-ttu-id="770db-121">Leggere [esercitazione Panoramica](data-factory-build-your-first-pipeline.md) articolo e hello completo **prerequisito** passaggi.</span><span class="sxs-lookup"><span data-stu-id="770db-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
2. <span data-ttu-id="770db-122">In questo articolo non fornisce una panoramica concettuale di hello servizio Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="770db-122">This article does not provide a conceptual overview of hello Azure Data Factory service.</span></span> <span data-ttu-id="770db-123">È consigliabile eseguire [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo per una panoramica dettagliata del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="770db-123">We recommend that you go through [Introduction tooAzure Data Factory](data-factory-introduction.md) article for a detailed overview of hello service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="770db-124">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="770db-124">Create data factory</span></span>
<span data-ttu-id="770db-125">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="770db-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="770db-126">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="770db-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="770db-127">Ad esempio, una data toocopy attività di copia da un archivio dati di origine tooa destinazione e un toorun attività Hive di HDInsight un tootransform script Hive i dati di output tooproduct dati di input.</span><span class="sxs-lookup"><span data-stu-id="770db-127">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="770db-128">Iniziamo con la creazione di data factory di hello in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="770db-128">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="770db-129">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="770db-129">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="770db-130">Fare clic su **NEW** scegliere dal menu a sinistra, hello **dati + Analitica**, fare clic su **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="770db-130">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Pannello Crea](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="770db-132">In hello **nuova data factory** pannello immettere **GetStartedDF** per hello Name.</span><span class="sxs-lookup"><span data-stu-id="770db-132">In hello **New data factory** blade, enter **GetStartedDF** for hello Name.</span></span>

   ![Pannello Nuova data factory](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="770db-134">nome Hello di hello Azure data factory deve essere **univoco globale**.</span><span class="sxs-lookup"><span data-stu-id="770db-134">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="770db-135">Se viene visualizzato l'errore hello: **"GetStartedDF" nome della Data factory non è disponibile**.</span><span class="sxs-lookup"><span data-stu-id="770db-135">If you receive hello error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="770db-136">Modificare il nome di hello di hello data factory (ad esempio, yournameGetStartedDF) e provare a creare di nuovo.</span><span class="sxs-lookup"><span data-stu-id="770db-136">Change hello name of hello data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="770db-137">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="770db-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="770db-138">nome Hello della hello data factory può essere registrato come un **DNS** nome nel futuro hello e pertanto diventano visibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="770db-138">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="770db-139">Seleziona hello **sottoscrizione di Azure** in cui si desidera hello data factory toobe creato.</span><span class="sxs-lookup"><span data-stu-id="770db-139">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="770db-140">Selezionare un **gruppo di risorse** esistente o crearne uno.</span><span class="sxs-lookup"><span data-stu-id="770db-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="770db-141">Per l'esercitazione hello, creare un gruppo di risorse denominato: **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="770db-141">For hello tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="770db-142">Seleziona hello **percorso** per data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="770db-142">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="770db-143">Solo le aree supportate dal servizio Data Factory hello vengono visualizzate nell'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="770db-143">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
7. <span data-ttu-id="770db-144">Selezionare **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="770db-144">Select **Pin toodashboard**.</span></span> 
8. <span data-ttu-id="770db-145">Fare clic su **crea** su hello **nuova data factory** blade.</span><span class="sxs-lookup"><span data-stu-id="770db-145">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="770db-146">le istanze di Data Factory toocreate, è necessario essere un membro di hello [Data Factory collaboratore](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) ruolo a livello di gruppo di risorse di sottoscrizione/hello.</span><span class="sxs-lookup"><span data-stu-id="770db-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="770db-147">Nel dashboard di hello, si vedrà hello segue riquadro con stato: data factory di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="770db-147">On hello dashboard, you see hello following tile with status: Deploying data factory.</span></span>    

   ![Stato creazione della data factory](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="770db-149">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="770db-149">Congratulations!</span></span> <span data-ttu-id="770db-150">La creazione della prima data factory è così completata.</span><span class="sxs-lookup"><span data-stu-id="770db-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="770db-151">Dopo aver hello data factory è stata creata correttamente, vedrai hello data factory pagina nella quale viene hello contenuto di data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="770db-151">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>     

    ![Pannello Data factory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="770db-153">Prima di creare una pipeline in data factory di hello, è necessario toocreate alcune entità Data Factory prima.</span><span class="sxs-lookup"><span data-stu-id="770db-153">Before creating a pipeline in hello data factory, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="770db-154">Creare innanzitutto i dati di servizi collegati toolink archivi/calcola tooyour dati archiviano, definiscono l'input e output dei dati di input/output toorepresent di set di dati in archivi dati collegato e quindi creare pipeline hello con un'attività che utilizza questi set di dati.</span><span class="sxs-lookup"><span data-stu-id="770db-154">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="770db-155">Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="770db-155">Create linked services</span></span>
<span data-ttu-id="770db-156">In questo passaggio è collegare l'account di archiviazione di Azure e una factory del dati tooyour cluster Azure HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="770db-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="770db-157">contiene account di archiviazione di Azure Hello hello dati di input e outpui per la pipeline di hello in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="770db-157">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="770db-158">servizio collegato di HDInsight Hello è toorun usato uno script Hive specificato nell'attività hello della pipeline hello in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="770db-158">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="770db-159">Identificare le [archivio dati](data-factory-data-movement-activities.md)/[servizi di calcolo](data-factory-compute-linked-services.md) vengono utilizzati nello scenario e collegare tali toohello data factory di servizi mediante la creazione di servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="770db-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services toohello data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="770db-160">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="770db-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="770db-161">In questo passaggio si collega la data factory tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="770db-161">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="770db-162">In questa esercitazione è utilizzare hello stesso account di archiviazione di Azure i dati di input/output toostore e hello HQL file di script.</span><span class="sxs-lookup"><span data-stu-id="770db-162">In this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="770db-163">Fare clic su **autore e distribuire** su hello **DATA FACTORY** pannello **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="770db-163">Click **Author and deploy** on hello **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="770db-164">Dovrebbe essere hello Editor delle Data Factory.</span><span class="sxs-lookup"><span data-stu-id="770db-164">You should see hello Data Factory Editor.</span></span>

   ![Riquadro Creare e distribuire](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="770db-166">Fare clic su **Nuovo archivio dati** e scegliere **Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="770db-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nuovo archivio dati - Archiviazione di Azure - Menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="770db-168">Dovrebbe essere hello script JSON per la creazione di una risorsa di archiviazione di Azure il servizio nell'editor di hello collegato.</span><span class="sxs-lookup"><span data-stu-id="770db-168">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![Servizio collegato Archiviazione di Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="770db-170">Sostituire **nome account** con nome hello dell'account di archiviazione di Azure e **chiave dell'account** con la chiave di accesso hello di hello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="770db-170">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="770db-171">toolearn come accedere a tooget lo spazio di archiviazione della chiave, vedere informazioni come tooview, copiare e rigenerare archiviazione accedere alle chiavi in hello [gestire account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="770db-171">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="770db-172">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.</span><span class="sxs-lookup"><span data-stu-id="770db-172">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Pulsante Distribuisci](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="770db-174">Dopo aver hello servizio collegato viene distribuito correttamente, hello **bozza 1** dovrebbe scomparire una finestra e viene visualizzato **AzureStorageLinkedService** nella visualizzazione ad albero di hello a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="770db-174">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

    ![Servizio collegato Archiviazione nel menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="770db-176">Creare un servizio collegato Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="770db-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="770db-177">In questo passaggio si collega una factory del dati tooyour cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="770db-177">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="770db-178">cluster HDInsight Hello viene automaticamente creato in fase di esecuzione ed eliminato al termine per l'elaborazione e inattività per l'intervallo di tempo specificato hello.</span><span class="sxs-lookup"><span data-stu-id="770db-178">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span>

1. <span data-ttu-id="770db-179">In hello **Editor delle Data Factory**, fare clic su **... Altro** e quindi su **Nuovo calcolo** e selezionare **Cluster HDInsight su richiesta**.</span><span class="sxs-lookup"><span data-stu-id="770db-179">In hello **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Nuovo calcolo](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="770db-181">Copiare e incollare hello seguente frammento di codice toohello **bozza 1** finestra.</span><span class="sxs-lookup"><span data-stu-id="770db-181">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="770db-182">frammento di codice JSON Hello descrive le proprietà di hello hello toocreate utilizzati cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="770db-182">hello JSON snippet describes hello properties that are used toocreate hello HDInsight cluster on-demand.</span></span>

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

    <span data-ttu-id="770db-183">Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="770db-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="770db-184">Proprietà</span><span class="sxs-lookup"><span data-stu-id="770db-184">Property</span></span> | <span data-ttu-id="770db-185">Descrizione</span><span class="sxs-lookup"><span data-stu-id="770db-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="770db-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="770db-186">ClusterSize</span></span> |<span data-ttu-id="770db-187">Specifica dimensioni hello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="770db-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="770db-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="770db-188">TimeToLive</span></span> | <span data-ttu-id="770db-189">Specifica il tempo di inattività hello per il cluster HDInsight hello, prima che venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="770db-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="770db-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="770db-190">linkedServiceName</span></span> | <span data-ttu-id="770db-191">Specifica l'account di archiviazione hello toostore utilizzati hello registri generati da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="770db-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="770db-192">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="770db-192">Note hello following points:</span></span>

   * <span data-ttu-id="770db-193">Hello Data Factory viene creata una **basati su Linux** cluster HDInsight per l'utente con hello JSON.</span><span class="sxs-lookup"><span data-stu-id="770db-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="770db-194">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="770db-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="770db-195">È possibile usare il **proprio cluster HDInsight** anziché un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="770db-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="770db-196">Per i dettagli, vedere [Servizio collegato Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="770db-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="770db-197">Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato in JSON hello (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="770db-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="770db-198">HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="770db-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="770db-199">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="770db-199">This behavior is by design.</span></span> <span data-ttu-id="770db-200">Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che viene elaborata una sezione, a meno che non esista un cluster attivo (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="770db-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="770db-201">cluster Hello viene eliminato automaticamente quando viene eseguita un'elaborazione hello.</span><span class="sxs-lookup"><span data-stu-id="770db-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="770db-202">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="770db-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="770db-203">Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="770db-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="770db-204">i nomi di Hello di questi contenitori seguono un modello: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="770db-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="770db-205">Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="770db-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="770db-206">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="770db-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="770db-207">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.</span><span class="sxs-lookup"><span data-stu-id="770db-207">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Distribuire il servizio collegato HDInsight su richiesta](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="770db-209">Assicurarsi di visualizzare entrambi **AzureStorageLinkedService** e **HDInsightOnDemandLinkedService** nella visualizzazione ad albero di hello a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="770db-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in hello tree view on hello left.</span></span>

    ![Visualizzazione albero con servizi collegati](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="770db-211">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="770db-211">Create datasets</span></span>
<span data-ttu-id="770db-212">In questo passaggio creare set di dati toorepresent hello input e output dei dati per l'elaborazione Hive.</span><span class="sxs-lookup"><span data-stu-id="770db-212">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="770db-213">Questi set di dati di riferimento toohello **AzureStorageLinkedService** creata precedentemente in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="770db-213">These datasets refer toohello **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="770db-214">Hello tooan punti di servizio collegato account di archiviazione di Azure e i set di dati specificare contenitore, cartella, nome del file nell'archiviazione hello che contiene l'input e output di dati.</span><span class="sxs-lookup"><span data-stu-id="770db-214">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="770db-215">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="770db-215">Create input dataset</span></span>
1. <span data-ttu-id="770db-216">In hello **Editor delle Data Factory**, fare clic su **... Ulteriori** nella barra dei comandi di hello, fare clic su **nuovo set di dati**e selezionare **archiviazione Blob di Azure**.</span><span class="sxs-lookup"><span data-stu-id="770db-216">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Nuovo set di dati](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="770db-218">Copiare e incollare hello successiva finestra di frammento toohello bozza-1.</span><span class="sxs-lookup"><span data-stu-id="770db-218">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="770db-219">Nel frammento di codice JSON hello, si sta creando un set di dati denominato **AzureBlobInput** che rappresenta i dati di input per un'attività nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="770db-219">In hello JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="770db-220">Inoltre, si specifica che i dati di input hello si trovano nel contenitore di blob hello chiamato **adfgetstarted** e cartella hello denominata **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="770db-220">In addition, you specify that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

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
    <span data-ttu-id="770db-221">Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="770db-221">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="770db-222">Proprietà</span><span class="sxs-lookup"><span data-stu-id="770db-222">Property</span></span> | <span data-ttu-id="770db-223">Descrizione</span><span class="sxs-lookup"><span data-stu-id="770db-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="770db-224">type</span><span class="sxs-lookup"><span data-stu-id="770db-224">type</span></span> |<span data-ttu-id="770db-225">proprietà tipo Hello è troppo**AzureBlob** perché i dati risiedono in una risorsa di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="770db-225">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="770db-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="770db-226">linkedServiceName</span></span> |<span data-ttu-id="770db-227">Fa riferimento toohello **AzureStorageLinkedService** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="770db-227">Refers toohello **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="770db-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="770db-228">folderPath</span></span> | <span data-ttu-id="770db-229">Specifica il blob hello **contenitore** hello e **cartella** che contiene il BLOB di input.</span><span class="sxs-lookup"><span data-stu-id="770db-229">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="770db-230">fileName</span><span class="sxs-lookup"><span data-stu-id="770db-230">fileName</span></span> |<span data-ttu-id="770db-231">Questa proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="770db-231">This property is optional.</span></span> <span data-ttu-id="770db-232">Se si omette questa proprietà, vengono selezionati tutti i file hello folderPath hello.</span><span class="sxs-lookup"><span data-stu-id="770db-232">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="770db-233">In questa esercitazione, hello solo **input.log** viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="770db-233">In this tutorial, only hello **input.log** is processed.</span></span> |
   | <span data-ttu-id="770db-234">type</span><span class="sxs-lookup"><span data-stu-id="770db-234">type</span></span> |<span data-ttu-id="770db-235">file di log Hello sono in formato testo, permette di usare **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="770db-235">hello log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="770db-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="770db-236">columnDelimiter</span></span> |<span data-ttu-id="770db-237">nei file di log hello colonne sono delimitate da **carattere virgola (`,`)**</span><span class="sxs-lookup"><span data-stu-id="770db-237">columns in hello log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="770db-238">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="770db-238">frequency/interval</span></span> |<span data-ttu-id="770db-239">frequenza impostata troppo**mese** e l'intervallo è **1**, il che significa che hello input sezioni sono disponibili ogni mese.</span><span class="sxs-lookup"><span data-stu-id="770db-239">frequency set too**Month** and interval is **1**, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="770db-240">external</span><span class="sxs-lookup"><span data-stu-id="770db-240">external</span></span> | <span data-ttu-id="770db-241">Questa proprietà è impostata troppo**true** se i dati di input hello non viene generati da questa pipeline.</span><span class="sxs-lookup"><span data-stu-id="770db-241">This property is set too**true** if hello input data is not generated by this pipeline.</span></span> <span data-ttu-id="770db-242">In questa esercitazione, i file input.log hello non viene generato da questa pipeline, è necessario impostare tootrue proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="770db-242">In this tutorial, hello input.log file is not generated by this pipeline, so we set hello property tootrue.</span></span> |

    <span data-ttu-id="770db-243">Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="770db-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="770db-244">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello appena creato set di dati.</span><span class="sxs-lookup"><span data-stu-id="770db-244">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span> <span data-ttu-id="770db-245">Dovrebbe essere hello set di dati nella visualizzazione ad albero di hello a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="770db-245">You should see hello dataset in hello tree view on hello left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="770db-246">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="770db-246">Create output dataset</span></span>
<span data-ttu-id="770db-247">È quindi possibile creare hello output dataset toorepresent hello output dati archiviati in archiviazione Blob di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="770db-247">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="770db-248">In hello **Editor delle Data Factory**, fare clic su **... Ulteriori** nella barra dei comandi di hello, fare clic su **nuovo set di dati**e selezionare **archiviazione Blob di Azure**.</span><span class="sxs-lookup"><span data-stu-id="770db-248">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="770db-249">Copiare e incollare hello successiva finestra di frammento toohello bozza-1.</span><span class="sxs-lookup"><span data-stu-id="770db-249">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="770db-250">Nel frammento di codice JSON hello, si sta creando un set di dati denominato **AzureBlobOutput**e specificare la struttura di dati hello derivante da script Hive hello hello.</span><span class="sxs-lookup"><span data-stu-id="770db-250">In hello JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying hello structure of hello data that is produced by hello Hive script.</span></span> <span data-ttu-id="770db-251">Inoltre, si specifica che i risultati di hello vengono archiviati nel contenitore blob hello chiamato **adfgetstarted** e cartella hello denominata **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="770db-251">In addition, you specify that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="770db-252">Hello **disponibilità** sezione specifica di tale set di dati di output di hello viene prodotto su base mensile.</span><span class="sxs-lookup"><span data-stu-id="770db-252">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

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
    <span data-ttu-id="770db-253">Vedere **creare set di dati input hello** sezione per le descrizioni di queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="770db-253">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="770db-254">Non si imposta proprietà esterna hello in un set di dati di output come set di dati hello viene generato dal servizio Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="770db-254">You do not set hello external property on an output dataset as hello dataset is produced by hello Data Factory service.</span></span>
3. <span data-ttu-id="770db-255">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello appena creato set di dati.</span><span class="sxs-lookup"><span data-stu-id="770db-255">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span>
4. <span data-ttu-id="770db-256">Verificare che Hello set di dati è stata creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="770db-256">Verify that hello dataset is created successfully.</span></span>

    ![Visualizzazione albero con servizi collegati](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="770db-258">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="770db-258">Create pipeline</span></span>
<span data-ttu-id="770db-259">In questo passaggio viene creata la prima pipeline con un'attività **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="770db-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="770db-260">Sezione di input è disponibile ogni mese (frequenza: mese, intervallo: 1), sezione di output viene prodotta ogni mese e hello dell'utilità di pianificazione per l'attività hello viene anche impostata toomonthly.</span><span class="sxs-lookup"><span data-stu-id="770db-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="770db-261">le impostazioni di Hello per set di dati output hello e utilità di pianificazione attività hello devono corrispondere.</span><span class="sxs-lookup"><span data-stu-id="770db-261">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="770db-262">Set di dati di output è attualmente, quali unità hello pianificazione, pertanto è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="770db-262">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="770db-263">Se l'attività hello non accetta alcun input, è possibile ignorare i set di dati input hello creazione.</span><span class="sxs-lookup"><span data-stu-id="770db-263">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="770db-264">proprietà Hello utilizzate nei hello JSON seguente sono illustrate alla fine di hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="770db-264">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="770db-265">In hello **Editor delle Data Factory**, fare clic su **i puntini di sospensione (...) Altri comandi** e quindi fare clic su **nuova pipeline**.</span><span class="sxs-lookup"><span data-stu-id="770db-265">In hello **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![Pulsante Nuova pipeline](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="770db-267">Copiare e incollare hello successiva finestra di frammento toohello bozza-1.</span><span class="sxs-lookup"><span data-stu-id="770db-267">Copy and paste hello following snippet toohello Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="770db-268">Sostituire **storageaccountname** con nome hello dell'account di archiviazione in hello JSON.</span><span class="sxs-lookup"><span data-stu-id="770db-268">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
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

    <span data-ttu-id="770db-269">Nel frammento di codice JSON hello, si sta creando una pipeline che è costituito da una singola attività che utilizza Hive tooprocess dati in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="770db-269">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="770db-270">file di script Hive Hello, **partitionweblogs.hql**, viene archiviato nell'account di archiviazione Azure hello (specificato da scriptLinkedService hello, chiamato **AzureStorageLinkedService**) e in  **script** cartella nel contenitore hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="770db-270">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="770db-271">Hello **definisce** sezione è le impostazioni di runtime hello toospecify utilizzati script hive toohello passati come valori di configurazione di Hive (ad esempio ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).</span><span class="sxs-lookup"><span data-stu-id="770db-271">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="770db-272">Hello **avviare** e **fine** le proprietà della pipeline hello specifica periodo attivo di hello della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="770db-272">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="770db-273">In formato JSON dell'attività hello, specificare tale script Hive hello viene eseguito sul calcolo hello specificato da hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="770db-273">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="770db-274">Vedere la sezione "JSON di Pipeline" in [pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md) per dettagli sulle proprietà JSON utilizzato nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="770db-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello example.</span></span>
   >
   >
3. <span data-ttu-id="770db-275">Verificare l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="770db-275">Confirm hello following:</span></span>

   1. <span data-ttu-id="770db-276">**input.log** file esista in hello **inputdata** cartella di hello **adfgetstarted** contenitore nell'archiviazione blob di Azure hello</span><span class="sxs-lookup"><span data-stu-id="770db-276">**input.log** file exists in hello **inputdata** folder of hello **adfgetstarted** container in hello Azure blob storage</span></span>
   2. <span data-ttu-id="770db-277">**partitionweblogs.hql** file esista in hello **script** cartella di hello **adfgetstarted** contenitore nell'archiviazione blob di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="770db-277">**partitionweblogs.hql** file exists in hello **script** folder of hello **adfgetstarted** container in hello Azure blob storage.</span></span> <span data-ttu-id="770db-278">Prerequisito hello completato i passaggi in hello [esercitazione Panoramica](data-factory-build-your-first-pipeline.md) se questi file non viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="770db-278">Complete hello prerequisite steps in hello [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="770db-279">Confermare che è stato sostituito **storageaccountname** con nome hello dell'account di archiviazione in hello JSON di pipeline.</span><span class="sxs-lookup"><span data-stu-id="770db-279">Confirm that you replaced **storageaccountname** with hello name of your storage account in hello pipeline JSON.</span></span>
4. <span data-ttu-id="770db-280">Fare clic su **Distribuisci** sul comando hello barra pipeline hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="770db-280">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span> <span data-ttu-id="770db-281">Poiché hello **avviare** e **fine** volte in cui vengono impostate in hello precedente e **isPaused** è toofalse set, pipeline hello esecuzioni (attività nella pipeline hello) immediatamente dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="770db-281">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="770db-282">Verificare che sia visualizzato pipeline hello nella visualizzazione ad albero di hello.</span><span class="sxs-lookup"><span data-stu-id="770db-282">Confirm that you see hello pipeline in hello tree view.</span></span>

    ![Visualizzazione albero con pipeline](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="770db-284">La creazione della prima pipeline è così completata.</span><span class="sxs-lookup"><span data-stu-id="770db-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="770db-285">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="770db-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="770db-286">Monitorare la pipeline con la vista diagramma</span><span class="sxs-lookup"><span data-stu-id="770db-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="770db-287">Fare clic su **X** tooclose Editor delle Data Factory pannelli e toonavigate il pannello Data Factory toohello e fare clic su **diagramma**.</span><span class="sxs-lookup"><span data-stu-id="770db-287">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Riquadro Diagramma](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="770db-289">In vista diagramma hello, si visualizza una panoramica di pipeline hello e set di dati utilizzati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="770db-289">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Vista Diagramma](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="770db-291">tooview tutte le attività nella pipeline di hello, pipeline pulsante destro del mouse in hello diagramma e fare clic su Apri Pipeline.</span><span class="sxs-lookup"><span data-stu-id="770db-291">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![Menu Apri pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="770db-293">Confermare la visualizzazione attività HDInsightHive hello nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="770db-293">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![Visualizzazione Apri pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="770db-295">toonavigate nuovamente toohello visualizzazione precedente, fare clic su **Data factory** nel menu di navigazione hello nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="770db-295">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
5. <span data-ttu-id="770db-296">In hello **vista diagramma**, fare doppio clic sul set di dati hello **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="770db-296">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="770db-297">Verificare che tale sezione hello sia **pronto** stato.</span><span class="sxs-lookup"><span data-stu-id="770db-297">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="770db-298">Potrebbe richiedere un paio di minuti per hello sezione tooshow fino nello stato pronto.</span><span class="sxs-lookup"><span data-stu-id="770db-298">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="770db-299">Se non si verifica dopo attendere qualche minuto, verificare se si dispone di hello file di input (input.log) inserito in un contenitore destra hello (adfgetstarted) e cartella (inputdata).</span><span class="sxs-lookup"><span data-stu-id="770db-299">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Sezione di input nello stato Pronto](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="770db-301">Fare clic su **X** tooclose **AzureBlobInput** blade.</span><span class="sxs-lookup"><span data-stu-id="770db-301">Click **X** tooclose **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="770db-302">In hello **vista diagramma**, fare doppio clic sul set di dati hello **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="770db-302">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="770db-303">Vedrai tale sezione hello che è in corso di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="770db-303">You see that hello slice that is currently being processed.</span></span>

   ![Set di dati](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="770db-305">Quando viene eseguita l'elaborazione, vedrai sezione hello **pronto** stato.</span><span class="sxs-lookup"><span data-stu-id="770db-305">When processing is done, you see hello slice in **Ready** state.</span></span>

   ![Set di dati](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="770db-307">La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti).</span><span class="sxs-lookup"><span data-stu-id="770db-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="770db-308">Pertanto, prevedere pipeline hello richiedere troppo **circa 30 minuti** tooprocess hello sezione.</span><span class="sxs-lookup"><span data-stu-id="770db-308">Therefore, expect hello pipeline too      take **approximately 30 minutes** tooprocess hello slice.</span></span>
   >
   >

9. <span data-ttu-id="770db-309">Quando si trova in sezione hello **pronto** stato, controllare hello **partitioneddata** cartella hello **adfgetstarted** contenitore nell'archiviazione blob per hello i dati di output.</span><span class="sxs-lookup"><span data-stu-id="770db-309">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

   ![Dati di output](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="770db-311">Fare clic su hello sezione toosee dettagli in un **sezione dati** blade.</span><span class="sxs-lookup"><span data-stu-id="770db-311">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

   ![Dettagli sezione dati](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="770db-313">Fare clic su un'attività eseguire in hello **elenco viene eseguita l'attività** toosee dettagli su un'attività (attività Hive nello scenario di esempio) di eseguire in un **Dettagli esecuzione attività** finestra.</span><span class="sxs-lookup"><span data-stu-id="770db-313">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Dettagli esecuzione attività](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="770db-315">Dai file di log hello, è possibile visualizzare informazioni sullo stato e query Hive hello che è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="770db-315">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="770db-316">Tali file di log sono utili per risolvere eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="770db-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="770db-317">Vedere l'articolo [Monitorare e gestire le pipeline di Azure Data Factory](data-factory-monitor-manage-pipelines.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="770db-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="770db-318">file di input Hello eliminato quando la sezione hello viene elaborata correttamente.</span><span class="sxs-lookup"><span data-stu-id="770db-318">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="770db-319">Pertanto, se si desidera toorerun hello sezione o hello esercitazione nuovamente, hello del file di input (input.log) toohello inputdata cartella del contenitore adfgetstarted hello di caricamento.</span><span class="sxs-lookup"><span data-stu-id="770db-319">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="770db-320">Monitorare la pipeline con l'app Monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="770db-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="770db-321">È possibile anche utilizzare Monitoraggio e Gestione applicazione toomonitor le pipeline.</span><span class="sxs-lookup"><span data-stu-id="770db-321">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="770db-322">Per informazioni dettagliate sull'uso di questa applicazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory con la nuova app di monitoraggio e gestione](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="770db-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="770db-323">Fare clic su **monitoraggio e gestione** riquadro hello home page per la data factory.</span><span class="sxs-lookup"><span data-stu-id="770db-323">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>

    ![Riquadro Monitoraggio e gestione](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="770db-325">Verrà visualizzata l'applicazione **Monitoraggio e gestione**.</span><span class="sxs-lookup"><span data-stu-id="770db-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="770db-326">Hello modifica **ora di inizio** e **ora di fine** toomatch avvio e fine della pipeline e fare clic su **applica**.</span><span class="sxs-lookup"><span data-stu-id="770db-326">Change hello **Start time** and **End time** toomatch start and end times of your pipeline, and click **Apply**.</span></span>

    ![App Monitoraggio e gestione](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="770db-328">Selezionare una finestra attività in hello **attività Windows** elenco dettagli toosee.</span><span class="sxs-lookup"><span data-stu-id="770db-328">Select an activity window in hello **Activity Windows** list toosee details about it.</span></span>

    ![Dettagli finestra attività](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="770db-330">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="770db-330">Summary</span></span>
<span data-ttu-id="770db-331">In questa esercitazione, creato un Azure factory tooprocess dati tramite l'esecuzione di script Hive in un cluster di HDInsight hadoop.</span><span class="sxs-lookup"><span data-stu-id="770db-331">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="770db-332">È stato utilizzato hello Editor delle Data Factory in hello toodo portale Azure hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="770db-332">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="770db-333">Creare un'istanza di Azure **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="770db-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="770db-334">Creare due **servizi collegati**:</span><span class="sxs-lookup"><span data-stu-id="770db-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="770db-335">**Archiviazione di Azure** collegati toolink servizio di archiviazione blob di Azure che contiene una data factory toohello di file di input/output.</span><span class="sxs-lookup"><span data-stu-id="770db-335">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="770db-336">**Azure HDInsight** toolink servizio collegato su richiesta di una factory del dati toohello cluster HDInsight Hadoop su richiesta.</span><span class="sxs-lookup"><span data-stu-id="770db-336">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="770db-337">Data Factory di Azure crea un HDInsight Hadoop dati di input tooprocess just-in-time di cluster e generare dati di output.</span><span class="sxs-lookup"><span data-stu-id="770db-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="770db-338">Creare due **set di dati**, che descrivono i dati di input e outpui per l'attività Hive di HDInsight nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="770db-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="770db-339">Creare una **pipeline** con un'attività **Hive di HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="770db-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="770db-340">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="770db-340">Next Steps</span></span>
<span data-ttu-id="770db-341">In questo articolo è stata creata una pipeline con un'attività di trasformazione (attività HDInsight) che esegue uno script Hive in un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="770db-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="770db-342">toosee toouse un dati toocopy attività di copia da un tooAzure Blob di Azure SQL, vedere [esercitazione: copiare i dati da un tooAzure blob di Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="770db-342">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="770db-343">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="770db-343">See Also</span></span>
| <span data-ttu-id="770db-344">Argomento</span><span class="sxs-lookup"><span data-stu-id="770db-344">Topic</span></span> | <span data-ttu-id="770db-345">Descrizione</span><span class="sxs-lookup"><span data-stu-id="770db-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="770db-346">Pipeline</span><span class="sxs-lookup"><span data-stu-id="770db-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="770db-347">In questo articolo consente di comprendere le pipeline e attività nella Data Factory di Azure e come toouse li tooconstruct end-to-end basato sui dati dei flussi di lavoro degli scenario o dell'azienda.</span><span class="sxs-lookup"><span data-stu-id="770db-347">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="770db-348">Set di dati</span><span class="sxs-lookup"><span data-stu-id="770db-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="770db-349">Questo articolo fornisce informazioni sui set di dati in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="770db-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="770db-350">Pianificazione ed esecuzione</span><span class="sxs-lookup"><span data-stu-id="770db-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="770db-351">Questo articolo illustra gli aspetti hello di pianificazione e l'esecuzione del modello di applicazione di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="770db-351">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="770db-352">Monitorare e gestire le pipeline con l'app di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="770db-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="770db-353">In questo articolo viene descritto come toomonitor, gestire ed eseguire il debug pipeline utilizzando hello monitoraggio e gestione delle App.</span><span class="sxs-lookup"><span data-stu-id="770db-353">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
