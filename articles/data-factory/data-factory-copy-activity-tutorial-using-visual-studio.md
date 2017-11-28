---
title: "Esercitazione: Creare una pipeline con l'attività di copia usando Visual Studio | Documentazione Microsoft"
description: "In questa esercitazione viene creata una pipeline di Azure Data Factory con un'attività di copia usando Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="ba7f8-103">Esercitazione: Creare una pipeline con l’attività Copia utilizzando Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ba7f8-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba7f8-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ba7f8-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="ba7f8-105">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="ba7f8-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="ba7f8-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ba7f8-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="ba7f8-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ba7f8-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="ba7f8-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba7f8-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="ba7f8-109">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ba7f8-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="ba7f8-110">API REST</span><span class="sxs-lookup"><span data-stu-id="ba7f8-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="ba7f8-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="ba7f8-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="ba7f8-112">In questo articolo viene illustrato come toouse hello Microsoft Visual Studio toocreate una data factory con una pipeline che copia i dati da un database di SQL Azure tooan di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-112">In this article, you learn how toouse hello Microsoft Visual Studio toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="ba7f8-113">Se si tooAzure nuova Data Factory, leggere hello [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo prima di eseguire questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="ba7f8-114">In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="ba7f8-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="ba7f8-115">attività di copia Hello copia dati da un archivio dati di sink supportati tooa di archivio di dati supportati.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="ba7f8-116">Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="ba7f8-117">attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="ba7f8-118">Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="ba7f8-119">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="ba7f8-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="ba7f8-120">Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="ba7f8-121">Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="ba7f8-122">pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-122">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="ba7f8-123">Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare una pipeline di dati tootransform utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-123">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba7f8-124">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ba7f8-124">Prerequisites</span></span>
1. <span data-ttu-id="ba7f8-125">Leggere [esercitazione Panoramica](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) articolo e hello completo **prerequisito** passaggi.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete hello **prerequisite** steps.</span></span>       
2. <span data-ttu-id="ba7f8-126">le istanze di Data Factory toocreate, è necessario essere un membro di hello [Data Factory collaboratore](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) ruolo a livello di gruppo di risorse di sottoscrizione/hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-126">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
3. <span data-ttu-id="ba7f8-127">È necessario disporre delle seguenti hello installato nel computer:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-127">You must have hello following installed on your computer:</span></span> 
   * <span data-ttu-id="ba7f8-128">Visual Studio 2013 o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ba7f8-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="ba7f8-129">Download di Azure SDK per Visual Studio 2013 o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="ba7f8-130">Passare troppo[pagina di Download di Azure](https://azure.microsoft.com/downloads/) e fare clic su **VS 2013** o **Visual Studio 2015** in hello **.NET** sezione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-130">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="ba7f8-131">Scaricare hello plug-in Data Factory di Azure più recenti per Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) o [Visual Studio 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-131">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="ba7f8-132">È inoltre possibile aggiornare i plug-in hello effettuando hello alla procedura seguente: hello scegliere **strumenti** -> **estensioni e aggiornamenti** -> **Online**  ->  **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools per Visual Studio** -> **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-132">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="ba7f8-133">Passi</span><span class="sxs-lookup"><span data-stu-id="ba7f8-133">Steps</span></span>
<span data-ttu-id="ba7f8-134">Ecco i passaggi di hello che è eseguire come parte di questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-134">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="ba7f8-135">Creare **servizi collegati** nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-135">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="ba7f8-136">In questo passaggio si creano due servizi collegati di tipo Archiviazione di Azure e database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="ba7f8-137">Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-137">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="ba7f8-138">È stato creato un contenitore e caricare l'account di archiviazione di dati toothis come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-138">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="ba7f8-139">AzureSqlLinkedService collega il toohello data factory di Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-139">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="ba7f8-140">dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-140">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="ba7f8-141">Come parte dei [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) è stata creata una tabella SQL in questo database.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="ba7f8-142">Creazione di input e output **set di dati** nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-142">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="ba7f8-143">il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-143">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="ba7f8-144">E specifica di set di dati blob di input hello hello contenitore e della cartella di hello che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-144">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="ba7f8-145">Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-145">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="ba7f8-146">E specifica di set di dati nella tabella SQL output hello tabella hello nei dati di hello database toowhich hello dall'archiviazione blob hello viene copiata.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-146">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
3. <span data-ttu-id="ba7f8-147">Creare un **pipeline** nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-147">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="ba7f8-148">In questo passaggio viene creata una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="ba7f8-149">attività di copia Hello copia dati da un blob nella tabella tooa di archiviazione blob di Azure hello in database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-149">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="ba7f8-150">È possibile utilizzare un'attività di copia in una pipeline di dati da qualsiasi destinazione tooany supportato di origine supportata toocopy.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-150">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="ba7f8-151">Per un elenco degli archivi dati supportati, vedere l'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="ba7f8-152">Creare una **data factory** di Azure durante la distribuzione delle entità di Data Factory (servizi collegati, set di dati/tabelle e pipeline).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="ba7f8-153">Creare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ba7f8-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="ba7f8-154">Avviare **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="ba7f8-155">Fare clic su **File**, punto troppo**New**, fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="ba7f8-156">Dovrebbe essere hello **nuovo progetto** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="ba7f8-157">In hello **nuovo progetto** finestra di dialogo, seleziona hello **DataFactory** modello e fare clic su **progetto vuoto di Factory dati**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![Finestra di dialogo Nuovo progetto](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="ba7f8-159">Specificare nome hello del progetto di hello, percorso per la soluzione hello e nome della soluzione hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-159">Specify hello name of hello project, location for hello solution, and name of hello solution, and then click **OK**.</span></span>
   
    ![Esplora soluzioni](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="ba7f8-161">Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="ba7f8-161">Create linked services</span></span>
<span data-ttu-id="ba7f8-162">Creare servizi collegati in un toolink factory dati i dati vengono archiviati e toohello data factory di servizi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-162">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="ba7f8-163">In questa esercitazione non si usano servizi di calcolo come Azure HDInsight o Azure Data Lake Analytics,</span><span class="sxs-lookup"><span data-stu-id="ba7f8-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="ba7f8-164">ma due archivi dati di tipo Archiviazione di Azure (origine) e database SQL di Azure (destinazione).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="ba7f8-165">Di conseguenza, si creano due servizi collegati di tipo AzureStorage e AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="ba7f8-166">Archiviazione di Azure Hello collegato collegamenti al servizio la data factory toohello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-166">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="ba7f8-167">Questo account di archiviazione è hello uno in cui è stato creato un contenitore e caricato dati hello come parte del [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-167">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="ba7f8-168">Collegato SQL Azure collegamenti al servizio il toohello data factory di Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-168">Azure SQL linked service links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="ba7f8-169">dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-169">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="ba7f8-170">Tabella emp hello è stato creato in questo database come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-170">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="ba7f8-171">Servizi collegati collegano archivi dati o servizi tooan data factory di Azure di calcolo.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-171">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="ba7f8-172">Vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) per tutti hello origini e sink supportati dall'attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="ba7f8-173">Vedere [servizi collegati di calcolo](data-factory-compute-linked-services.md) per elenco hello di servizi di calcolo supportati da Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-173">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span> <span data-ttu-id="ba7f8-174">Questa esercitazione non prevede l'uso di servizi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-hello-azure-storage-linked-service"></a><span data-ttu-id="ba7f8-175">Creare il servizio di archiviazione di Azure collegati hello</span><span class="sxs-lookup"><span data-stu-id="ba7f8-175">Create hello Azure Storage linked service</span></span>
1. <span data-ttu-id="ba7f8-176">In **Esplora**, fare doppio clic su **servizi collegati**, punto troppo**Aggiungi**, fare clic su **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-176">In **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="ba7f8-177">In hello **Aggiungi nuovo elemento** nella finestra di dialogo **servizio collegato di archiviazione di Azure** hello elenco e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-177">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span> 
   
    ![Nuovo servizio collegato](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="ba7f8-179">Sostituire `<accountname>` e `<accountkey>`* con il nome di hello dell'account di archiviazione Azure e la relativa chiave.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-179">Replace `<accountname>` and `<accountkey>`* with hello name of your Azure storage account and its key.</span></span> 
   
    ![Servizio collegato Archiviazione di Azure](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="ba7f8-181">Salvare hello **AzureStorageLinkedService1.json** file.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-181">Save hello **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="ba7f8-182">Per ulteriori informazioni sulle proprietà JSON nella definizione di servizio collegato hello, vedere [connettore di archiviazione Blob di Azure](data-factory-azure-blob-connector.md#linked-service-properties) articolo.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-182">For more information about JSON properties in hello linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-hello-azure-sql-linked-service"></a><span data-ttu-id="ba7f8-183">Creare servizio collegato SQL Azure hello</span><span class="sxs-lookup"><span data-stu-id="ba7f8-183">Create hello Azure SQL linked service</span></span>
1. <span data-ttu-id="ba7f8-184">Fare clic su **servizi collegati** nodo hello **Esplora** nuovamente, scegliere troppo**Aggiungi**, fare clic su **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-184">Right-click on **Linked Services** node in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="ba7f8-185">Questa volta selezionare **Servizio collegato SQL Azure** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="ba7f8-186">In hello **AzureSqlLinkedService1.json file**, sostituire `<servername>`, `<databasename>`, `<username@servername>`, e `<password>` con nomi del server SQL Azure, database, account utente e password.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-186">In hello **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="ba7f8-187">Salvare hello **AzureSqlLinkedService1.json** file.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-187">Save hello **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="ba7f8-188">Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore del database SQL di Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="ba7f8-189">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="ba7f8-189">Create datasets</span></span>
<span data-ttu-id="ba7f8-190">Nel passaggio precedente hello, servizi collegati toolink è creato l'account di archiviazione di Azure e la data factory di Azure SQL database tooyour.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-190">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="ba7f8-191">In questo passaggio si definiscono due set di dati denominati InputDataset e OutputDataset che rappresentano l'input e output i dati archiviati in archivi dati hello a cui fa riferimento AzureStorageLinkedService1 e AzureSqlLinkedService1 rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="ba7f8-192">il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-192">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="ba7f8-193">E, set di dati blob di input hello (InputDataset) specifica il contenitore di hello e la cartella di hello che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-193">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="ba7f8-194">Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-194">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="ba7f8-195">E, di output di hello set di dati nella tabella SQL (OututDataset) specifica la tabella hello in hello di toowhich hello database vengono copiati dati dall'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-195">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="ba7f8-196">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="ba7f8-196">Create input dataset</span></span>
<span data-ttu-id="ba7f8-197">In questo passaggio, creare un set di dati denominato InputDataset che punta il file di blob tooa (emp.txt) nella cartella radice hello di un contenitore di blob (adftutorial) in hello rappresentato da hello AzureStorageLinkedService1 collegato servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-197">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="ba7f8-198">Se non specifica un valore per il nome file hello (o ignorarlo), i dati da tutti i BLOB nella cartella input hello sono copiati toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-198">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="ba7f8-199">In questa esercitazione, si specifica un valore per il nome file hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-199">In this tutorial, you specify a value for hello fileName.</span></span> 

<span data-ttu-id="ba7f8-200">In questo caso, utilizzare il termine hello "tables" anziché "set di dati".</span><span class="sxs-lookup"><span data-stu-id="ba7f8-200">Here, you use hello term "tables" rather than "datasets".</span></span> <span data-ttu-id="ba7f8-201">Una tabella è un set di dati rettangolare e hello solo i set di dati al momento è supportato.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-201">A table is a rectangular dataset and is hello only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="ba7f8-202">Fare doppio clic su **tabelle** in hello **Esplora**, punto troppo**Aggiungi**, fare clic su **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-202">Right-click **Tables** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="ba7f8-203">In hello **Aggiungi nuovo elemento** nella finestra di dialogo **Blob di Azure**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-203">In hello **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="ba7f8-204">Sostituire il testo JSON hello con hello segue testo e salvare hello **AzureBlobLocation1.json** file.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-204">Replace hello JSON text with hello following text and save hello **AzureBlobLocation1.json** file.</span></span> 

  ```json   
  {
    "name": "InputDataset",
    "properties": {
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
      "type": "AzureBlob",
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
        "format": {
          "type": "TextFormat",
          "columnDelimiter": ","
        }
      },
      "external": true,
      "availability": {
        "frequency": "Hour",
        "interval": 1
      }
    }
  }
  ``` 
    <span data-ttu-id="ba7f8-205">Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-205">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="ba7f8-206">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ba7f8-206">Property</span></span> | <span data-ttu-id="ba7f8-207">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ba7f8-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="ba7f8-208">type</span><span class="sxs-lookup"><span data-stu-id="ba7f8-208">type</span></span> | <span data-ttu-id="ba7f8-209">proprietà tipo Hello è troppo**AzureBlob** perché i dati risiedono in una risorsa di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-209">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="ba7f8-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ba7f8-210">linkedServiceName</span></span> | <span data-ttu-id="ba7f8-211">Fa riferimento toohello **AzureStorageLinkedService** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-211">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="ba7f8-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="ba7f8-212">folderPath</span></span> | <span data-ttu-id="ba7f8-213">Specifica il blob hello **contenitore** hello e **cartella** che contiene il BLOB di input.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-213">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="ba7f8-214">In questa esercitazione, adftutorial è il contenitore di blob hello e cartella è hello radice.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-214">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="ba7f8-215">fileName</span><span class="sxs-lookup"><span data-stu-id="ba7f8-215">fileName</span></span> | <span data-ttu-id="ba7f8-216">Questa proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-216">This property is optional.</span></span> <span data-ttu-id="ba7f8-217">Se si omette questa proprietà, vengono selezionati tutti i file da folderPath hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-217">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="ba7f8-218">In questa esercitazione, **emp.txt** specificato per hello fileName, in modo che solo tale file viene prelevato per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-218">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="ba7f8-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="ba7f8-219">format -> type</span></span> |<span data-ttu-id="ba7f8-220">file di input di Hello è in formato testo hello, permette di usare **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-220">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="ba7f8-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="ba7f8-221">columnDelimiter</span></span> | <span data-ttu-id="ba7f8-222">Hello colonne nel file di input hello sono delimitate da **carattere virgola (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-222">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="ba7f8-223">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="ba7f8-223">frequency/interval</span></span> | <span data-ttu-id="ba7f8-224">frequenza Hello è troppo**ora** e l'intervallo viene impostato troppo**1**, il che significa che hello di input sono disponibili sezioni **oraria**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-224">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="ba7f8-225">In altre parole, hello servizio Data Factory esegue la ricerca di dati di input ogni ora nella cartella radice hello del contenitore di blob (**adftutorial**) specificato.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-225">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="ba7f8-226">La ricerca di dati hello all'interno di hello pipeline inizio e fine volte, non prima o dopo tali periodi.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-226">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="ba7f8-227">external</span><span class="sxs-lookup"><span data-stu-id="ba7f8-227">external</span></span> | <span data-ttu-id="ba7f8-228">Questa proprietà è impostata troppo**true** se dati hello non viene generati da questa pipeline.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-228">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="ba7f8-229">dati di input Hello in questa esercitazione sono nel file di emp.txt hello, che non viene generato da questa pipeline, è necessario impostare tootrue questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-229">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="ba7f8-230">Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="ba7f8-231">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="ba7f8-231">Create output dataset</span></span>
<span data-ttu-id="ba7f8-232">In questo passaggio si crea un set di dati di output denominato **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="ba7f8-233">Questo set di dati fa riferimento nella tabella SQL tooa nel database di SQL Azure hello rappresentato da **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-233">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="ba7f8-234">Fare doppio clic su **tabelle** in hello **Esplora** nuovamente, scegliere troppo**Aggiungi**, fare clic su **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-234">Right-click **Tables** in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="ba7f8-235">In hello **Aggiungi nuovo elemento** nella finestra di dialogo **SQL Azure**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-235">In hello **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="ba7f8-236">Sostituire il testo JSON hello con hello JSON seguente e salvare hello **AzureSqlTableLocation1.json** file.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-236">Replace hello JSON text with hello following JSON and save hello **AzureSqlTableLocation1.json** file.</span></span>

  ```json
    {
     "name": "OutputDataset",
     "properties": {
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
       "type": "AzureSqlTable",
       "linkedServiceName": "AzureSqlLinkedService1",
       "typeProperties": {
         "tableName": "emp"
       },
       "availability": {
         "frequency": "Hour",
         "interval": 1
       }
     }
    }
    ```
    <span data-ttu-id="ba7f8-237">Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-237">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="ba7f8-238">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ba7f8-238">Property</span></span> | <span data-ttu-id="ba7f8-239">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ba7f8-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="ba7f8-240">type</span><span class="sxs-lookup"><span data-stu-id="ba7f8-240">type</span></span> | <span data-ttu-id="ba7f8-241">proprietà tipo Hello è troppo**AzureSqlTable** perché dati tabella tooa copiato in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-241">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="ba7f8-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ba7f8-242">linkedServiceName</span></span> | <span data-ttu-id="ba7f8-243">Fa riferimento toohello **AzureSqlLinkedService** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-243">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="ba7f8-244">tableName</span><span class="sxs-lookup"><span data-stu-id="ba7f8-244">tableName</span></span> | <span data-ttu-id="ba7f8-245">Hello specificato **tabella** toowhich hello dati vengono copiati.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-245">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="ba7f8-246">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="ba7f8-246">frequency/interval</span></span> | <span data-ttu-id="ba7f8-247">Hello frequency è impostato troppo**ora** e l'intervallo è **1**, il che significa che vengono create le sezioni di output di hello **oraria** tra hello pipeline iniziale e finale volte, non prima o Dopo tali periodi.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-247">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="ba7f8-248">Sono presenti tre colonne: **ID**, **FirstName**, e **LastName** : nella tabella emp hello nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-248">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="ba7f8-249">ID è una colonna identity, pertanto è necessario solo toospecify **FirstName** e **LastName** qui.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-249">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="ba7f8-250">Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore SQL di Azure](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="ba7f8-251">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="ba7f8-251">Create pipeline</span></span>
<span data-ttu-id="ba7f8-252">In questo passaggio viene creata una pipeline con un'**attività di copia** che usa **InputDataset** come input e **OutputDataset** come output.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="ba7f8-253">Set di dati di output è attualmente, quali unità hello pianificazione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-253">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="ba7f8-254">In questa esercitazione, set di dati di output è tooproduce configurato una sezione di una volta all'ora.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-254">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="ba7f8-255">pipeline Hello dispone ora di inizio e ora di fine di un giorno separato, ovvero 24 ore.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-255">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="ba7f8-256">Pertanto, 24 sezioni del set di dati di output vengono generate dalla pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-256">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="ba7f8-257">Fare doppio clic su **pipeline** in hello **Esplora**, punto troppo**Aggiungi**, fare clic su **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-257">Right-click **Pipelines** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="ba7f8-258">Selezionare **copia dati Pipeline** in hello **Aggiungi nuovo elemento** la finestra di dialogo e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-258">Select **Copy Data Pipeline** in hello **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="ba7f8-259">Sostituire hello JSON con hello JSON seguente e salvare hello **CopyActivity1.json** file.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-259">Replace hello JSON with hello following JSON and save hello **CopyActivity1.json** file.</span></span>

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob tooAzure SQL table",
       "activities": [
         {
           "name": "CopyFromBlobToSQL",
           "type": "Copy",
           "inputs": [
             {
               "name": "InputDataset"
             }
           ],
           "outputs": [
             {
               "name": "OutputDataset"
             }
           ],
           "typeProperties": {
             "source": {
               "type": "BlobSource"
             },
             "sink": {
               "type": "SqlSink",
               "writeBatchSize": 10000,
               "writeBatchTimeout": "60:00:00"
             }
           },
           "Policy": {
             "concurrency": 1,
             "executionPriorityOrder": "NewestFirst",
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - <span data-ttu-id="ba7f8-260">Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**copia**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-260">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="ba7f8-261">Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-261">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="ba7f8-262">Nelle soluzioni Data Factory è anche possibile usare le [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="ba7f8-263">Input per attività hello è troppo**InputDataset** e di output per attività hello è troppo**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-263">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="ba7f8-264">In hello **typeProperties** sezione **BlobSource** è specificato come tipo di origine hello e **SqlSink** è specificato come tipo di sink hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-264">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="ba7f8-265">Per un elenco completo degli archivi di dati supportati dall'attività di copia hello come origini e sink, vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-265">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="ba7f8-266">toolearn sulla modalità di memorizzazione toouse dati specifici supportati come origine/sink, fare clic su collegamento hello nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-266">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="ba7f8-267">Sostituire il valore di hello di hello **avviare** proprietà con hello giorno corrente e **fine** valore con hello giorno successivo.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-267">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="ba7f8-268">È possibile specificare solo parte della data hello e Ignora parte dell'ora hello di hello data ora.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-268">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="ba7f8-269">Ad esempio, "2016-02-03", che equivale troppo "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="ba7f8-269">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="ba7f8-270">Per la data e l'ora di inizio è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="ba7f8-271">ad esempio 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="ba7f8-272">Hello **fine** è facoltativo, ma viene usata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-272">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="ba7f8-273">Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore**".</span><span class="sxs-lookup"><span data-stu-id="ba7f8-273">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="ba7f8-274">specificare in modo indefinito, pipeline hello toorun **9999-09-09** come valore hello hello **fine** proprietà.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-274">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="ba7f8-275">In hello sopra riportato, sono presenti sezioni dati 24 come ogni sezione di dati viene prodotta ogni ora.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-275">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="ba7f8-276">Per le descrizioni delle proprietà JSON nella definizione di una pipeline, vedere l'articolo su come [creare pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ba7f8-277">Per le descrizioni delle proprietà JSON nella definizione di un'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="ba7f8-278">Per le descrizioni delle proprietà JSON supportate da BlobSource, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="ba7f8-279">Per le descrizioni delle proprietà JSON supportate da SqlSink, vedere l'articolo relativo al [connettore del database SQL di Azure](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="ba7f8-280">Pubblicare/Distribuire le entità della data factory</span><span class="sxs-lookup"><span data-stu-id="ba7f8-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="ba7f8-281">In questo passaggio vengono pubblicate le entità di Data Factory, ovvero i servizi collegati, i set di dati e la pipeline, create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="ba7f8-282">È inoltre possibile specificare il nome di hello di hello nuova data factory toobe creato toohold queste entità.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-282">You also specify hello name of hello new data factory toobe created toohold these entities.</span></span>  

1. <span data-ttu-id="ba7f8-283">Fare clic sul progetto in Esplora soluzioni hello e fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-283">Right-click project in hello Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="ba7f8-284">Se viene visualizzato **Accedi tooyour account Microsoft** nella finestra di dialogo immettere le credenziali di account hello con sottoscrizione di Azure e fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-284">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="ba7f8-285">È necessario visualizzare hello la finestra di dialogo seguenti:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-285">You should see hello following dialog box:</span></span>
   
   ![Finestra di dialogo Pubblica](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="ba7f8-287">Nella pagina di fabbrica dati Configura hello, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-287">In hello Configure data factory page, do hello following steps:</span></span> 
   
   1. <span data-ttu-id="ba7f8-288">Selezionare l’opzione **Crea nuova data factory** .</span><span class="sxs-lookup"><span data-stu-id="ba7f8-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="ba7f8-289">Immettere **VSTutorialFactory** per **Nome**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="ba7f8-290">nome Hello di hello Azure data factory deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-290">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="ba7f8-291">Se si riceve un errore relativo a nome hello della data factory per la pubblicazione, è possibile modificare il nome di hello di hello data factory (ad esempio, yournameVSTutorialFactory) e provare a pubblicare di nuovo.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-291">If you receive an error about hello name of data factory when publishing, change hello name of hello data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="ba7f8-292">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="ba7f8-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="ba7f8-293">Selezionare la sottoscrizione di Azure per hello **sottoscrizione** campo.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-293">Select your Azure subscription for hello **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="ba7f8-294">Se non viene visualizzata alcuna sottoscrizione, assicurarsi che si è connessi con un account che è un amministratore o co-amministratore della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="ba7f8-295">Seleziona hello **gruppo di risorse** per hello data factory toobe creato.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-295">Select hello **resource group** for hello data factory toobe created.</span></span> 
   5. <span data-ttu-id="ba7f8-296">Seleziona hello **area** per data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-296">Select hello **region** for hello data factory.</span></span> <span data-ttu-id="ba7f8-297">Solo le aree supportate dal servizio Data Factory hello vengono visualizzate nell'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-297">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
   6. <span data-ttu-id="ba7f8-298">Fare clic su **Avanti** tooswitch toohello **pubblicare elementi** pagina.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-298">Click **Next** tooswitch toohello **Publish Items** page.</span></span>
      
       ![Pagina Configure data factory (Configura data factory)](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="ba7f8-300">In hello **pubblicare elementi** pagina, assicurarsi che tutti hello Data factory di entità vengono selezionate e fare clic su **Avanti** tooswitch toohello **riepilogo** pagina.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-300">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>
   
   ![Pagina Publish Items (Pubblica elementi)](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="ba7f8-302">Esaminare hello riepilogo e fare clic su **Avanti** toostart hello distribuzione elaborare e visualizzare hello **lo stato di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-302">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>
   
   ![Pagina Riepilogo pubblicazione](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="ba7f8-304">In hello **lo stato di distribuzione** pagina, dovrebbe essere stato hello hello processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-304">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="ba7f8-305">Dopo la distribuzione hello viene eseguita, fare clic su Fine.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-305">Click Finish after hello deployment is done.</span></span>
 
   ![Pagina Stato distribuzione](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="ba7f8-307">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-307">Note hello following points:</span></span> 

* <span data-ttu-id="ba7f8-308">Se viene visualizzato l'errore hello: "questa sottoscrizione non è registrato toouse dello spazio dei nomi Microsoft. DataFactory", effettuare una delle seguenti hello e riprovare:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-308">If you receive hello error: "This subscription is not registered toouse namespace Microsoft.DataFactory", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="ba7f8-309">In Azure PowerShell, eseguire hello seguenti provider di comandi tooregister hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-309">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="ba7f8-310">È possibile eseguire hello successivo comando tooconfirm tale hello Data Factory di provider è registrato.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-310">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="ba7f8-311">Account di accesso tramite hello sottoscrizione di Azure in hello [portale di Azure](https://portal.azure.com) e passare a pannello di Data Factory tooa creare una data factory nel portale di Azure hello (o).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-311">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="ba7f8-312">Questa azione registra automaticamente i provider di hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-312">This action automatically registers hello provider for you.</span></span>
* <span data-ttu-id="ba7f8-313">nome Hello della hello data factory può essere registrato come un nome DNS in futuro hello e pertanto diventano visibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-313">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba7f8-314">le istanze di Data Factory toocreate, è necessario toobe admin un co-amministratore della sottoscrizione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="ba7f8-314">toocreate Data Factory instances, you need toobe a admin/co-admin of hello Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="ba7f8-315">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="ba7f8-315">Monitor pipeline</span></span>
<span data-ttu-id="ba7f8-316">Passare toohello home page per la data factory:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-316">Navigate toohello home page for your data factory:</span></span>

1. <span data-ttu-id="ba7f8-317">Accedi troppo[portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-317">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ba7f8-318">Fare clic su **più servizi** hello menu a sinistra e fare clic su **Data factory**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-318">Click **More services** on hello left menu, and click **Data factories**.</span></span>

    ![Esplora data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="ba7f8-320">Iniziare a digitare il nome di hello della data factory.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-320">Start typing hello name of your data factory.</span></span>

    ![Nome della data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="ba7f8-322">Scegliere la data factory di hello risultati elenco toosee hello home page per la data factory.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-322">Click your data factory in hello results list toosee hello home page for your data factory.</span></span>

    ![Home page di Data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="ba7f8-324">Seguire le istruzioni da [monitorare set di dati e della pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pipeline hello toomonitor e set di dati è stato creato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="ba7f8-325">Attualmente, Visual Studio non supporta il monitoraggio delle pipeline di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="ba7f8-326">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="ba7f8-326">Summary</span></span>
<span data-ttu-id="ba7f8-327">In questa esercitazione è creato un Azure factory toocopy dati da un database di SQL Azure tooan blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-327">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="ba7f8-328">È stato utilizzato Visual Studio toocreate hello data factory, i servizi collegati, i set di dati e una pipeline.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-328">You used Visual Studio toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="ba7f8-329">Ecco i passaggi di alto livello hello effettuati in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-329">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="ba7f8-330">Creare un'istanza di Azure **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="ba7f8-331">Creare **servizi collegati**:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="ba7f8-332">Un **di archiviazione di Azure** collegati toolink service account di archiviazione di Azure che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-332">An **Azure Storage** linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="ba7f8-333">Un **SQL Azure** collegati toolink servizio database SQL di Azure che contiene i dati di output di hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-333">An **Azure SQL** linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="ba7f8-334">Creare **set di dati**che descrivono dati di input e dati di output per le pipeline.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="ba7f8-335">Creare una **pipeline** con un'**attività di copia** con **BlobSource** come origine e **SqlSink** come sink.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="ba7f8-336">toosee toouse un'attività Hive di HDInsight tootransform di dati tramite il cluster HDInsight di Azure, vedere [ esercitazione: creare i primi dati tootransform pipeline utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-336">toosee how toouse a HDInsight Hive Activity tootransform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="ba7f8-337">È possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-337">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="ba7f8-338">Per informazioni dettagliate, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="ba7f8-339">Visualizzare tutte le data factory in Esplora server</span><span class="sxs-lookup"><span data-stu-id="ba7f8-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="ba7f8-340">In questa sezione viene descritto come toouse hello Esplora Server in Visual Studio tooview tutte le data factory hello nella sottoscrizione di Azure e creare un progetto di Visual Studio basato su una data factory esistente.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-340">This section describes how toouse hello Server Explorer in Visual Studio tooview all hello data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="ba7f8-341">In **Visual Studio**, fare clic su **vista** hello menu e fare clic su **Esplora Server**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-341">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="ba7f8-342">Nella finestra di Esplora Server hello, espandere **Azure** espandere **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-342">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="ba7f8-343">Se viene visualizzato **Accedi tooVisual Studio**, immettere hello **account** associata con la sottoscrizione di Azure e fare clic su **continua**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-343">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="ba7f8-344">Immettere la **password** e fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="ba7f8-345">Visual Studio tenta tooget informazioni su tutte le data factory di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-345">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="ba7f8-346">Viene visualizzato lo stato di hello di questa operazione in hello **elenco attività di Data Factory** finestra.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-346">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Esplora server](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="ba7f8-348">Creare un progetto di Visual Studio per una data factory esistente</span><span class="sxs-lookup"><span data-stu-id="ba7f8-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="ba7f8-349">Fare doppio clic su una data factory in Esplora Server e selezionare **tooNew esportare Data Factory progetto** toocreate un progetto di Visual Studio basato su una data factory esistente.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-349">Right-click a data factory in Server Explorer, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![Progetto VS tooa di esportazione data factory](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="ba7f8-351">Aggiornare gli strumenti di Data factory di Azure per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ba7f8-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="ba7f8-352">hello tooupdate strumenti di Data Factory di Azure per Visual Studio, come segue:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-352">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="ba7f8-353">Fare clic su **strumenti** nel menu hello e selezionare **estensioni e aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-353">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="ba7f8-354">Selezionare **aggiornamenti** in hello riquadro sinistro e quindi selezionare **Visual Studio Gallery**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-354">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="ba7f8-355">Selezionare **Azure Data Factory tools for Visual Studio** e fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="ba7f8-356">Se non viene visualizzata questa voce, si dispone già di più recente degli strumenti hello hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-356">If you do not see this entry, you already have hello latest version of hello tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="ba7f8-357">Usare i file di configurazione</span><span class="sxs-lookup"><span data-stu-id="ba7f8-357">Use configuration files</span></span>
<span data-ttu-id="ba7f8-358">È possibile utilizzare i file di configurazione nelle proprietà tooconfigure di Visual Studio per servizi/tabelle/pipeline del collegato in modo diverso per ogni ambiente.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-358">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="ba7f8-359">Prendere in considerazione hello seguente definizione JSON per un servizio collegato di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-359">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="ba7f8-360">toospecify **connectionString** con valori diversi per accountname e accountkey in base a hello ambiente (sviluppo/Test o produzione) toowhich si distribuiscono le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-360">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="ba7f8-361">usare un file di configurazione separato per ogni ambiente.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="ba7f8-362">Aggiungere un file di configurazione</span><span class="sxs-lookup"><span data-stu-id="ba7f8-362">Add a configuration file</span></span>
<span data-ttu-id="ba7f8-363">Aggiungere un file di configurazione per ogni ambiente eseguendo hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-363">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="ba7f8-364">Fare clic sul progetto Data Factory hello nella soluzione Visual Studio, scegliere troppo**Aggiungi**, fare clic su **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-364">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="ba7f8-365">Selezionare **Config** selezionare nell'elenco dei modelli installati a sinistra di hello hello **File di configurazione**, immettere un **nome** per la configurazione di hello file e fare clic su **Aggiungere**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-365">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![Aggiungere un file di configurazione](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="ba7f8-367">Aggiungere parametri di configurazione e i relativi valori in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-367">Add configuration parameters and their values in hello following format:</span></span>

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

    <span data-ttu-id="ba7f8-368">Questo esempio configura la proprietà connectionString di un servizio collegato Archiviazione di Azure e di un servizio collegato Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="ba7f8-369">Si noti che la sintassi di hello per specificare nome [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-369">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="ba7f8-370">Se JSON ha una proprietà che è una matrice di valori, come illustrato nel seguente codice hello:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-370">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

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

    <span data-ttu-id="ba7f8-371">Configurare le proprietà come illustrato nel seguente file di configurazione (utilizzare indicizzazione in base zero) hello:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-371">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="ba7f8-372">Nomi delle proprietà con spazi</span><span class="sxs-lookup"><span data-stu-id="ba7f8-372">Property names with spaces</span></span>
<span data-ttu-id="ba7f8-373">Se un nome di proprietà contiene spazi, utilizzare le parentesi quadre, come illustrato in hello (nome server di Database) di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-373">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="ba7f8-374">Distribuire la soluzione usando una configurazione</span><span class="sxs-lookup"><span data-stu-id="ba7f8-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="ba7f8-375">Quando si pubblicano le entità di Azure Data Factory in Visual Studio, è possibile specificare una configurazione di hello che si vuole toouse per tale operazione di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-375">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="ba7f8-376">entità toopublish in un progetto di Data Factory di Azure tramite file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-376">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="ba7f8-377">Fare clic sul progetto Data Factory e fare clic su **pubblica** toosee hello **pubblicare elementi** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-377">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="ba7f8-378">Selezionare una data factory esistente oppure specificare valori per la creazione di una data factory in hello **Configura data factory di** pagina e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-378">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="ba7f8-379">In hello **pubblicare elementi** pagina: viene visualizzato un elenco a discesa con le configurazioni disponibili per hello **selezionare configurazione della distribuzione** campo.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-379">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![Selezionare un file di configurazione](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="ba7f8-381">Seleziona hello **file di configurazione** che desideri toouse e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-381">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="ba7f8-382">Assicurarsi di visualizzare il nome di hello del file JSON in hello **riepilogo** pagina e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-382">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="ba7f8-383">Fare clic su **fine** al termine dell'operazione di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-383">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="ba7f8-384">Quando si distribuisce, i valori hello dal file di configurazione hello sono tooset utilizzati valori di proprietà nei file JSON hello prima entità hello tooAzure distribuito il servizio Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-384">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="ba7f8-385">Usare l'Insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="ba7f8-385">Use Azure Key Vault</span></span>
<span data-ttu-id="ba7f8-386">Non è consigliabile e spesso rispetto ai dati sensibili toocommit criteri di sicurezza, ad esempio repository di codice toohello stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-386">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="ba7f8-387">Vedere [ADF Secure pubblicare](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample in GitHub toolearn sull'archiviazione di informazioni riservate nell'insieme di credenziali chiave di Azure e l'uso durante la pubblicazione entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="ba7f8-388">Hello Secure pubblicare l'estensione di Visual Studio consente hello toobe di segreti archiviati nell'insieme di credenziali chiave e solo i riferimenti toothem vengono specificati in servizi collegati o configurazioni di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-388">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="ba7f8-389">Questi riferimenti vengono risolti durante la pubblicazione tooAzure entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-389">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="ba7f8-390">Questi file possono quindi essere eseguito il commit toosource repository senza esporre tutti i segreti.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-390">These files can then be committed toosource repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ba7f8-391">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ba7f8-391">Next steps</span></span>
<span data-ttu-id="ba7f8-392">In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="ba7f8-393">Hello nella tabella seguente fornisce un elenco di archivi di dati supportato come origini e destinazioni da attività di copia hello:</span><span class="sxs-lookup"><span data-stu-id="ba7f8-393">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="ba7f8-394">toolearn su come archiviano dati toocopy da e verso un tipo di dati, fare clic su collegamento hello per hello archivio di dati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-394">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
