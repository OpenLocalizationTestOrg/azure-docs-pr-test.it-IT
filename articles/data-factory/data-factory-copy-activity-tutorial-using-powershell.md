---
title: 'Esercitazione: Creare una pipeline di dati toomove tramite Azure PowerShell | Documenti Microsoft'
description: "In questa esercitazione viene creata una pipeline di Azure Data Factory con un'attività di copia usando Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="79d7e-103">Esercitazione: Creare una pipeline di Data Factory per lo spostamento di dati con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="79d7e-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79d7e-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="79d7e-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="79d7e-105">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="79d7e-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="79d7e-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="79d7e-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="79d7e-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79d7e-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="79d7e-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="79d7e-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="79d7e-109">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="79d7e-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="79d7e-110">API REST</span><span class="sxs-lookup"><span data-stu-id="79d7e-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="79d7e-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="79d7e-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="79d7e-112">In questo articolo viene illustrato come toouse PowerShell toocreate una data factory con una pipeline che copia i dati da un database di SQL Azure tooan di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-112">In this article, you learn how toouse PowerShell toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="79d7e-113">Se si tooAzure nuova Data Factory, leggere hello [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo prima di eseguire questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="79d7e-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="79d7e-114">In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="79d7e-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="79d7e-115">attività di copia Hello copia dati da un archivio dati di sink supportati tooa di archivio di dati supportati.</span><span class="sxs-lookup"><span data-stu-id="79d7e-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="79d7e-116">Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="79d7e-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="79d7e-117">attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="79d7e-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="79d7e-118">Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="79d7e-119">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="79d7e-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="79d7e-120">Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="79d7e-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="79d7e-121">Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="79d7e-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="79d7e-122">In questo articolo non copre tutti i cmdlet di hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="79d7e-122">This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="79d7e-123">Per la documentazione completa su questi cmdlet, vedere [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) (Informazioni di riferimento sui cmdlet di Data Factory).</span><span class="sxs-lookup"><span data-stu-id="79d7e-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="79d7e-124">pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione.</span><span class="sxs-lookup"><span data-stu-id="79d7e-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="79d7e-125">Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare una pipeline di dati tootransform utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79d7e-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="79d7e-126">Prerequisites</span></span>
- <span data-ttu-id="79d7e-127">Completare i prerequisiti elencati in hello [prerequisiti per l'esercitazione](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="79d7e-127">Complete prerequisites listed in hello [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="79d7e-128">Installare **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="79d7e-129">Seguire le istruzioni hello [come tooinstall e configurare Azure PowerShell](../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-129">Follow hello instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="79d7e-130">Passi</span><span class="sxs-lookup"><span data-stu-id="79d7e-130">Steps</span></span>
<span data-ttu-id="79d7e-131">Ecco i passaggi di hello che è eseguire come parte di questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="79d7e-131">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="79d7e-132">Creare una **data factory** di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="79d7e-133">In questo passaggio viene creata una data factory denominata ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="79d7e-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="79d7e-134">Creare **servizi collegati** nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-134">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="79d7e-135">In questo passaggio si creano due servizi collegati di tipo Archiviazione di Azure e database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="79d7e-136">Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-136">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="79d7e-137">È stato creato un contenitore e caricare l'account di archiviazione di dati toothis come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-137">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="79d7e-138">AzureSqlLinkedService collega il toohello data factory di Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="79d7e-138">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="79d7e-139">dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database.</span><span class="sxs-lookup"><span data-stu-id="79d7e-139">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="79d7e-140">Come parte dei [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) è stata creata una tabella SQL in questo database.</span><span class="sxs-lookup"><span data-stu-id="79d7e-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="79d7e-141">Creazione di input e output **set di dati** nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-141">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="79d7e-142">il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-142">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="79d7e-143">E specifica di set di dati blob di input hello hello contenitore e della cartella di hello che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-143">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="79d7e-144">Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="79d7e-144">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="79d7e-145">E specifica di set di dati nella tabella SQL output hello tabella hello nei dati di hello database toowhich hello dall'archiviazione blob hello viene copiata.</span><span class="sxs-lookup"><span data-stu-id="79d7e-145">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
4. <span data-ttu-id="79d7e-146">Creare un **pipeline** nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-146">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="79d7e-147">In questo passaggio viene creata una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="79d7e-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="79d7e-148">attività di copia Hello copia dati da un blob nella tabella tooa di archiviazione blob di Azure hello in database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-148">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="79d7e-149">È possibile utilizzare un'attività di copia in una pipeline di dati da qualsiasi destinazione tooany supportato di origine supportata toocopy.</span><span class="sxs-lookup"><span data-stu-id="79d7e-149">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="79d7e-150">Per un elenco degli archivi dati supportati, vedere l'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="79d7e-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="79d7e-151">Pipeline di hello monitor.</span><span class="sxs-lookup"><span data-stu-id="79d7e-151">Monitor hello pipeline.</span></span> <span data-ttu-id="79d7e-152">In questo passaggio si **monitoraggio** hello sezioni dei set di dati di input e output tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79d7e-152">In this step, you **monitor** hello slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="79d7e-153">Creare un'istanza di Data factory</span><span class="sxs-lookup"><span data-stu-id="79d7e-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="79d7e-154">Completamento [prerequisiti per l'esercitazione hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) se non è già fatto.</span><span class="sxs-lookup"><span data-stu-id="79d7e-154">Complete [prerequisites for hello tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="79d7e-155">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="79d7e-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="79d7e-156">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="79d7e-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="79d7e-157">Ad esempio, una data toocopy attività di copia da un archivio dati di origine tooa destinazione e un toorun attività Hive di HDInsight un tootransform script Hive i dati di output tooproduct dati di input.</span><span class="sxs-lookup"><span data-stu-id="79d7e-157">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="79d7e-158">Iniziamo con la creazione di data factory di hello in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="79d7e-158">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="79d7e-159">Avviare **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-159">Launch **PowerShell**.</span></span> <span data-ttu-id="79d7e-160">Mantenere aperta fino al fine di hello dell'esercitazione Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79d7e-160">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="79d7e-161">Se si chiude e riapre, è necessario comandi hello toorun nuovamente.</span><span class="sxs-lookup"><span data-stu-id="79d7e-161">If you close and reopen, you need toorun hello commands again.</span></span>

    <span data-ttu-id="79d7e-162">Eseguire hello comando seguente e immettere nome utente hello e la password usati toosign in toohello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="79d7e-162">Run hello following command, and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="79d7e-163">Eseguire hello successivo comando tooview tutte le sottoscrizioni di hello per questo account:</span><span class="sxs-lookup"><span data-stu-id="79d7e-163">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="79d7e-164">Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="79d7e-164">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="79d7e-165">Sostituire  **&lt;NameOfAzureSubscription** &gt; con nome hello della sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="79d7e-165">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="79d7e-166">Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="79d7e-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="79d7e-167">Alcuni dei passaggi di hello in questa esercitazione si supponga di utilizza il gruppo di risorse hello denominato **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-167">Some of hello steps in this tutorial assume that you use hello resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="79d7e-168">Se si utilizza un gruppo di risorse diverso, è necessario toouse, al posto di ADFTutorialResourceGroup in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="79d7e-168">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="79d7e-169">Eseguire hello **New AzureRmDataFactory** toocreate cmdlet una data factory denominata **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="79d7e-169">Run hello **New-AzureRmDataFactory** cmdlet toocreate a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="79d7e-170">È possibile che questo nome sia già in uso.</span><span class="sxs-lookup"><span data-stu-id="79d7e-170">This name may already have been taken.</span></span> <span data-ttu-id="79d7e-171">Pertanto, rendere il nome di hello della data factory di hello univoco aggiungendo un prefisso o suffisso (ad esempio: ADFTutorialDataFactoryPSH05152017) ed eseguire nuovamente il comando hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-171">Therefore, make hello name of hello data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run hello command again.</span></span>  

<span data-ttu-id="79d7e-172">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="79d7e-172">Note hello following points:</span></span>

* <span data-ttu-id="79d7e-173">nome Hello di hello Azure data factory deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="79d7e-173">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="79d7e-174">Se viene visualizzato il seguente errore hello, modificare il nome di hello (ad esempio, yournameADFTutorialDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="79d7e-174">If you receive hello following error, change hello name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="79d7e-175">Durante l'esecuzione di passaggi in questa esercitazione usare questo nome anziché ADFTutorialFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="79d7e-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="79d7e-176">Per informazioni sugli elementi di Data Factory, vedere [Data Factory - Regole di denominazione](data-factory-naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="79d7e-177">le istanze di Data Factory toocreate, è necessario essere un collaboratore o amministratore di hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-177">toocreate Data Factory instances, you must be a contributor or administrator of hello Azure subscription.</span></span>
* <span data-ttu-id="79d7e-178">nome di Hello della data factory di hello registrato come un nome DNS in futuro hello e pertanto diventano visibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="79d7e-178">hello name of hello data factory may be registered as a DNS name in hello future, and hence become publicly visible.</span></span>
* <span data-ttu-id="79d7e-179">È possibile che venga visualizzato hello il seguente errore: "**questa sottoscrizione non è registrato toouse dello spazio dei nomi Microsoft. DataFactory.**"</span><span class="sxs-lookup"><span data-stu-id="79d7e-179">You may receive hello following error: "**This subscription is not registered toouse namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="79d7e-180">Effettuare una delle seguenti hello e riprovare:</span><span class="sxs-lookup"><span data-stu-id="79d7e-180">Do one of hello following, and try publishing again:</span></span>

  * <span data-ttu-id="79d7e-181">In Azure PowerShell, eseguire hello seguenti provider di comandi tooregister hello Data Factory:</span><span class="sxs-lookup"><span data-stu-id="79d7e-181">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="79d7e-182">Eseguire hello successivo comando tooconfirm tale hello Data Factory di provider è stato registrato:</span><span class="sxs-lookup"><span data-stu-id="79d7e-182">Run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="79d7e-183">Accedi tramite hello sottoscrizione di Azure toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="79d7e-183">Sign in by using hello Azure subscription toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="79d7e-184">Andare a pannello di Data Factory tooa o creare una data factory in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-184">Go tooa Data Factory blade, or create a data factory in hello Azure portal.</span></span> <span data-ttu-id="79d7e-185">Questa azione registra automaticamente i provider di hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-185">This action automatically registers hello provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="79d7e-186">Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="79d7e-186">Create linked services</span></span>
<span data-ttu-id="79d7e-187">Creare servizi collegati in un toolink factory dati i dati vengono archiviati e toohello data factory di servizi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="79d7e-187">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="79d7e-188">In questa esercitazione non si usano servizi di calcolo come Azure HDInsight o Azure Data Lake Analytics,</span><span class="sxs-lookup"><span data-stu-id="79d7e-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="79d7e-189">ma due archivi dati di tipo Archiviazione di Azure (origine) e database SQL di Azure (destinazione).</span><span class="sxs-lookup"><span data-stu-id="79d7e-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="79d7e-190">Si creano quindi due servizi collegati denominati AzureStorageLinkedService e AzureSqlLinkedService di tipo AzureStorage e AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="79d7e-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="79d7e-191">Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-191">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="79d7e-192">Questo account di archiviazione è hello uno in cui è stato creato un contenitore e caricato dati hello come parte del [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-192">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="79d7e-193">AzureSqlLinkedService collega il toohello data factory di Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="79d7e-193">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="79d7e-194">dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database.</span><span class="sxs-lookup"><span data-stu-id="79d7e-194">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="79d7e-195">Tabella emp hello è stato creato in questo database come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-195">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="79d7e-196">Creare un servizio collegato per un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="79d7e-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="79d7e-197">In questo passaggio si collega la data factory tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-197">In this step, you link your Azure storage account tooyour data factory.</span></span>

1. <span data-ttu-id="79d7e-198">Creare un file JSON denominato **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** cartella con hello seguente contenuto: (Crea hello cartella ADFGetStartedPSH se non esiste già.)</span><span class="sxs-lookup"><span data-stu-id="79d7e-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with hello following content: (Create hello folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="79d7e-199">Sostituire &lt;accountname&gt; e &lt;accountkey&gt; con nome e la chiave dell'account di archiviazione di Azure prima di salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving hello file.</span></span> 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
2. <span data-ttu-id="79d7e-200">In **Azure PowerShell**, passare toohello **ADFGetStartedPSH** cartella.</span><span class="sxs-lookup"><span data-stu-id="79d7e-200">In **Azure PowerShell**, switch toohello **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="79d7e-201">Eseguire hello **New AzureRmDataFactoryLinkedService** cmdlet toocreate hello servizio collegato: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-201">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet toocreate hello linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="79d7e-202">Questo cmdlet e altri cmdlet di Data Factory da usare in questa esercitazione è necessario toopass valori per hello **ResourceGroupName** e **DataFactoryName** parametri.</span><span class="sxs-lookup"><span data-stu-id="79d7e-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="79d7e-203">In alternativa, è possibile passare l'oggetto DataFactory hello restituito dal cmdlet New-AzureRmDataFactory hello senza digitare ResourceGroupName e DataFactoryName ogni volta che si esegue un cmdlet.</span><span class="sxs-lookup"><span data-stu-id="79d7e-203">Alternatively, you can pass hello DataFactory object returned by hello New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="79d7e-204">Ecco l'output di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="79d7e-204">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="79d7e-205">Altre modalità di creazione di questo servizio collegato è toospecify nome gruppo di risorse e nome della data factory anziché specificare l'oggetto DataFactory hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-205">Other way of creating this linked service is toospecify resource group name and data factory name instead of specifying hello DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="79d7e-206">Creare un servizio collegato per un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="79d7e-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="79d7e-207">In questo passaggio si collega il tooyour data factory di Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="79d7e-207">In this step, you link your Azure SQL database tooyour data factory.</span></span>

1. <span data-ttu-id="79d7e-208">Creare un file JSON denominato AzureSqlLinkedService.json nella cartella C:\ADFGetStartedPSH con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="79d7e-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with hello following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="79d7e-209">Sostituire &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; e &lt;password&gt; con i nomi del server, database, account utente e password di Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="79d7e-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. <span data-ttu-id="79d7e-210">Eseguire un servizio collegato di hello toocreate di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="79d7e-210">Run hello following command toocreate a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="79d7e-211">Ecco l'output di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="79d7e-211">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="79d7e-212">Verificare che **Consenti l'accesso ai servizi tooAzure** è attivata per il server di database SQL.</span><span class="sxs-lookup"><span data-stu-id="79d7e-212">Confirm that **Allow access tooAzure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="79d7e-213">tooverify e accenderlo, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="79d7e-213">tooverify and turn it on, do hello following steps:</span></span>

    1. <span data-ttu-id="79d7e-214">Accedi toohello [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="79d7e-214">Log in toohello [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="79d7e-215">Fare clic su **più servizi >** a sinistra di hello e fare clic su **istanze di SQL Server** in hello **database** categoria.</span><span class="sxs-lookup"><span data-stu-id="79d7e-215">Click **More services >** on hello left, and click **SQL servers** in hello **DATABASES** category.</span></span>
    3. <span data-ttu-id="79d7e-216">Selezionare il server nell'elenco di hello di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="79d7e-216">Select your server in hello list of SQL servers.</span></span>
    4. <span data-ttu-id="79d7e-217">Nel Pannello di hello SQL server, fare clic su **Mostra le impostazioni del firewall** collegamento.</span><span class="sxs-lookup"><span data-stu-id="79d7e-217">On hello SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="79d7e-218">In hello **le impostazioni del Firewall** pannello, fare clic su **ON** per **Consenti l'accesso ai servizi tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-218">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
    6. <span data-ttu-id="79d7e-219">Fare clic su **salvare** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-219">Click **Save** on hello toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="79d7e-220">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="79d7e-220">Create datasets</span></span>
<span data-ttu-id="79d7e-221">Nel passaggio precedente hello, servizi collegati toolink è creato l'account di archiviazione di Azure e la data factory di Azure SQL database tooyour.</span><span class="sxs-lookup"><span data-stu-id="79d7e-221">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="79d7e-222">In questo passaggio si definiscono due set di dati denominati InputDataset e OutputDataset che rappresentano l'input e output i dati archiviati in archivi dati hello a cui fa riferimento AzureStorageLinkedService e AzureSqlLinkedService rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="79d7e-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="79d7e-223">il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-223">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="79d7e-224">E, set di dati blob di input hello (InputDataset) specifica il contenitore di hello e la cartella di hello che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-224">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="79d7e-225">Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="79d7e-225">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="79d7e-226">E, di output di hello set di dati nella tabella SQL (OututDataset) specifica la tabella hello in hello di toowhich hello database vengono copiati dati dall'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-226">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="79d7e-227">Creare un set di dati di input</span><span class="sxs-lookup"><span data-stu-id="79d7e-227">Create an input dataset</span></span>
<span data-ttu-id="79d7e-228">In questo passaggio, creare un set di dati denominato InputDataset che punta il file di blob tooa (emp.txt) nella cartella radice hello di un contenitore di blob (adftutorial) in hello rappresentato da hello AzureStorageLinkedService collegato servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-228">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="79d7e-229">Se non specifica un valore per il nome file hello (o ignorarlo), i dati da tutti i BLOB nella cartella input hello sono copiati toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="79d7e-229">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="79d7e-230">In questa esercitazione, si specifica un valore per il nome file hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-230">In this tutorial, you specify a value for hello fileName.</span></span>  

1. <span data-ttu-id="79d7e-231">Creare un file JSON denominato **InputDataset.json** in hello **C:\ADFGetStartedPSH** cartella, con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="79d7e-231">Create a JSON file named **InputDataset.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "emp.txt",
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

    <span data-ttu-id="79d7e-232">Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="79d7e-232">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="79d7e-233">Proprietà</span><span class="sxs-lookup"><span data-stu-id="79d7e-233">Property</span></span> | <span data-ttu-id="79d7e-234">Descrizione</span><span class="sxs-lookup"><span data-stu-id="79d7e-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="79d7e-235">type</span><span class="sxs-lookup"><span data-stu-id="79d7e-235">type</span></span> | <span data-ttu-id="79d7e-236">proprietà tipo Hello è troppo**AzureBlob** perché i dati risiedono in una risorsa di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-236">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="79d7e-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="79d7e-237">linkedServiceName</span></span> | <span data-ttu-id="79d7e-238">Fa riferimento toohello **AzureStorageLinkedService** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="79d7e-238">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="79d7e-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="79d7e-239">folderPath</span></span> | <span data-ttu-id="79d7e-240">Specifica il blob hello **contenitore** hello e **cartella** che contiene il BLOB di input.</span><span class="sxs-lookup"><span data-stu-id="79d7e-240">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="79d7e-241">In questa esercitazione, adftutorial è il contenitore di blob hello e cartella è hello radice.</span><span class="sxs-lookup"><span data-stu-id="79d7e-241">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="79d7e-242">fileName</span><span class="sxs-lookup"><span data-stu-id="79d7e-242">fileName</span></span> | <span data-ttu-id="79d7e-243">Questa proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="79d7e-243">This property is optional.</span></span> <span data-ttu-id="79d7e-244">Se si omette questa proprietà, vengono selezionati tutti i file da folderPath hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-244">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="79d7e-245">In questa esercitazione, **emp.txt** specificato per hello fileName, in modo che solo tale file viene prelevato per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="79d7e-245">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="79d7e-246">format -> type</span><span class="sxs-lookup"><span data-stu-id="79d7e-246">format -> type</span></span> |<span data-ttu-id="79d7e-247">file di input di Hello è in formato testo hello, permette di usare **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-247">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="79d7e-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="79d7e-248">columnDelimiter</span></span> | <span data-ttu-id="79d7e-249">Hello colonne nel file di input hello sono delimitate da **carattere virgola (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-249">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="79d7e-250">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="79d7e-250">frequency/interval</span></span> | <span data-ttu-id="79d7e-251">frequenza Hello è troppo**ora** e l'intervallo viene impostato troppo**1**, il che significa che hello di input sono disponibili sezioni **oraria**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-251">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="79d7e-252">In altre parole, hello servizio Data Factory esegue la ricerca di dati di input ogni ora nella cartella radice hello del contenitore di blob (**adftutorial**) specificato.</span><span class="sxs-lookup"><span data-stu-id="79d7e-252">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="79d7e-253">La ricerca di dati hello all'interno di hello pipeline inizio e fine volte, non prima o dopo tali periodi.</span><span class="sxs-lookup"><span data-stu-id="79d7e-253">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="79d7e-254">external</span><span class="sxs-lookup"><span data-stu-id="79d7e-254">external</span></span> | <span data-ttu-id="79d7e-255">Questa proprietà è impostata troppo**true** se dati hello non viene generati da questa pipeline.</span><span class="sxs-lookup"><span data-stu-id="79d7e-255">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="79d7e-256">dati di input Hello in questa esercitazione sono nel file di emp.txt hello, che non viene generato da questa pipeline, è necessario impostare tootrue questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="79d7e-256">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="79d7e-257">Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="79d7e-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="79d7e-258">Eseguire hello seguente set di dati di comando toocreate hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="79d7e-258">Run hello following command toocreate hello Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="79d7e-259">Ecco l'output di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="79d7e-259">Here is hello sample output:</span></span>

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a><span data-ttu-id="79d7e-260">Creare un set di dati di output</span><span class="sxs-lookup"><span data-stu-id="79d7e-260">Create an output dataset</span></span>
<span data-ttu-id="79d7e-261">In questa parte del passaggio di hello, si crea un set di dati di output denominato **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-261">In this part of hello step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="79d7e-262">Questo set di dati fa riferimento nella tabella SQL tooa nel database di SQL Azure hello rappresentato da **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-262">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="79d7e-263">Creare un file JSON denominato **OutputDataset.json** in hello **C:\ADFGetStartedPSH** cartella con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="79d7e-263">Create a JSON file named **OutputDataset.json** in hello **C:\ADFGetStartedPSH** folder with hello following content:</span></span>

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
            "linkedServiceName": "AzureSqlLinkedService",
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

    <span data-ttu-id="79d7e-264">Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="79d7e-264">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="79d7e-265">Proprietà</span><span class="sxs-lookup"><span data-stu-id="79d7e-265">Property</span></span> | <span data-ttu-id="79d7e-266">Descrizione</span><span class="sxs-lookup"><span data-stu-id="79d7e-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="79d7e-267">type</span><span class="sxs-lookup"><span data-stu-id="79d7e-267">type</span></span> | <span data-ttu-id="79d7e-268">proprietà tipo Hello è troppo**AzureSqlTable** perché dati tabella tooa copiato in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-268">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="79d7e-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="79d7e-269">linkedServiceName</span></span> | <span data-ttu-id="79d7e-270">Fa riferimento toohello **AzureSqlLinkedService** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="79d7e-270">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="79d7e-271">tableName</span><span class="sxs-lookup"><span data-stu-id="79d7e-271">tableName</span></span> | <span data-ttu-id="79d7e-272">Hello specificato **tabella** toowhich hello dati vengono copiati.</span><span class="sxs-lookup"><span data-stu-id="79d7e-272">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="79d7e-273">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="79d7e-273">frequency/interval</span></span> | <span data-ttu-id="79d7e-274">Hello frequency è impostato troppo**ora** e l'intervallo è **1**, il che significa che vengono create le sezioni di output di hello **oraria** tra hello pipeline iniziale e finale volte, non prima o Dopo tali periodi.</span><span class="sxs-lookup"><span data-stu-id="79d7e-274">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="79d7e-275">Sono presenti tre colonne: **ID**, **FirstName**, e **LastName** : nella tabella emp hello nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-275">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="79d7e-276">ID è una colonna identity, pertanto è necessario solo toospecify **FirstName** e **LastName** qui.</span><span class="sxs-lookup"><span data-stu-id="79d7e-276">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="79d7e-277">Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore SQL di Azure](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="79d7e-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="79d7e-278">Eseguire hello seguente set di dati di comando toocreate hello data factory.</span><span class="sxs-lookup"><span data-stu-id="79d7e-278">Run hello following command toocreate hello data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="79d7e-279">Ecco l'output di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="79d7e-279">Here is hello sample output:</span></span>

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="79d7e-280">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="79d7e-280">Create a pipeline</span></span>
<span data-ttu-id="79d7e-281">In questo passaggio viene creata una pipeline con un'**attività di copia** che usa **InputDataset** come input e **OutputDataset** come output.</span><span class="sxs-lookup"><span data-stu-id="79d7e-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="79d7e-282">Set di dati di output è attualmente, quali unità hello pianificazione.</span><span class="sxs-lookup"><span data-stu-id="79d7e-282">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="79d7e-283">In questa esercitazione, set di dati di output è tooproduce configurato una sezione di una volta all'ora.</span><span class="sxs-lookup"><span data-stu-id="79d7e-283">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="79d7e-284">pipeline Hello dispone ora di inizio e ora di fine di un giorno separato, ovvero 24 ore.</span><span class="sxs-lookup"><span data-stu-id="79d7e-284">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="79d7e-285">Pertanto, 24 sezioni del set di dati di output vengono generate dalla pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-285">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 


1. <span data-ttu-id="79d7e-286">Creare un file JSON denominato **ADFTutorialPipeline.json** in hello **C:\ADFGetStartedPSH** cartella, con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="79d7e-286">Create a JSON file named **ADFTutorialPipeline.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```
    <span data-ttu-id="79d7e-287">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="79d7e-287">Note hello following points:</span></span>
   
    - <span data-ttu-id="79d7e-288">Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**copia**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="79d7e-289">Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-289">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="79d7e-290">Nelle soluzioni Data Factory è anche possibile usare le [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="79d7e-291">Input per attività hello è troppo**InputDataset** e di output per attività hello è troppo**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-291">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="79d7e-292">In hello **typeProperties** sezione **BlobSource** è specificato come tipo di origine hello e **SqlSink** è specificato come tipo di sink hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-292">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="79d7e-293">Per un elenco completo degli archivi di dati supportati dall'attività di copia hello come origini e sink, vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="79d7e-293">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="79d7e-294">toolearn sulla modalità di memorizzazione toouse dati specifici supportati come origine/sink, fare clic su collegamento hello nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-294">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="79d7e-295">Sostituire il valore di hello di hello **avviare** proprietà con hello giorno corrente e **fine** valore con hello giorno successivo.</span><span class="sxs-lookup"><span data-stu-id="79d7e-295">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="79d7e-296">È possibile specificare solo parte della data hello e Ignora parte dell'ora hello di hello data ora.</span><span class="sxs-lookup"><span data-stu-id="79d7e-296">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="79d7e-297">Ad esempio, "2016-02-03", che equivale troppo "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="79d7e-297">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="79d7e-298">Per la data e l'ora di inizio è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="79d7e-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="79d7e-299">ad esempio 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="79d7e-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="79d7e-300">Hello **fine** è facoltativo, ma viene usata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="79d7e-300">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="79d7e-301">Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore**".</span><span class="sxs-lookup"><span data-stu-id="79d7e-301">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="79d7e-302">specificare in modo indefinito, pipeline hello toorun **9999-09-09** come valore hello hello **fine** proprietà.</span><span class="sxs-lookup"><span data-stu-id="79d7e-302">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="79d7e-303">In hello sopra riportato, sono presenti sezioni dati 24 come ogni sezione di dati viene prodotta ogni ora.</span><span class="sxs-lookup"><span data-stu-id="79d7e-303">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="79d7e-304">Per le descrizioni delle proprietà JSON nella definizione di una pipeline, vedere l'articolo su come [creare pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="79d7e-305">Per le descrizioni delle proprietà JSON nella definizione di un'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="79d7e-306">Per le descrizioni delle proprietà JSON supportate da BlobSource, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="79d7e-307">Per le descrizioni delle proprietà JSON supportate da SqlSink, vedere l'articolo relativo al [connettore del database SQL di Azure](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="79d7e-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="79d7e-308">Eseguire hello comando toocreate hello data factory nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="79d7e-308">Run hello following command toocreate hello data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="79d7e-309">Ecco l'output di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="79d7e-309">Here is hello sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="79d7e-310">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="79d7e-310">**Congratulations!**</span></span> <span data-ttu-id="79d7e-311">Una data factory di Azure è stato creato con una pipeline toocopy dati da un database di SQL Azure tooan di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-311">You have successfully created an Azure data factory with a pipeline toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

## <a name="monitor-hello-pipeline"></a><span data-ttu-id="79d7e-312">Pipeline hello monitoraggio</span><span class="sxs-lookup"><span data-stu-id="79d7e-312">Monitor hello pipeline</span></span>
<span data-ttu-id="79d7e-313">In questo passaggio, utilizzare Azure PowerShell toomonitor cosa accade in un data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-313">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="79d7e-314">Sostituire &lt;DataFactoryName&gt; con nome hello della data factory e l'esecuzione **Get AzureRmDataFactory**e assegnare hello output tooa $df variabile.</span><span class="sxs-lookup"><span data-stu-id="79d7e-314">Replace &lt;DataFactoryName&gt; with hello name of your data factory and run **Get-AzureRmDataFactory**, and assign hello output tooa variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="79d7e-315">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="79d7e-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="79d7e-316">Eseguire quindi il contenuto di stampa hello di hello toosee $df seguente output:</span><span class="sxs-lookup"><span data-stu-id="79d7e-316">Then, run print hello contents of $df toosee hello following output:</span></span> 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. <span data-ttu-id="79d7e-317">Eseguire **Get AzureRmDataFactorySlice** tooget dettagli su tutte le sezioni di hello **OutputDataset**, ovvero il set di dati di hello output della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-317">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **OutputDataset**, which is hello output dataset of hello pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="79d7e-318">Questa impostazione deve corrispondere hello **avviare** valore in formato JSON della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-318">This setting should match hello **Start** value in hello pipeline JSON.</span></span> <span data-ttu-id="79d7e-319">Dovrebbe essere 24 sezioni, una per ogni ora dalla Mezzanotte di hello odierna too12 STO di hello giorno successivo.</span><span class="sxs-lookup"><span data-stu-id="79d7e-319">You should see 24 slices, one for each hour from 12 AM of hello current day too12 AM of hello next day.</span></span>

   <span data-ttu-id="79d7e-320">Ecco tre sezioni di esempio dall'output di hello:</span><span class="sxs-lookup"><span data-stu-id="79d7e-320">Here are three sample slices from hello output:</span></span> 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="79d7e-321">Eseguire **Get AzureRmDataFactoryRun** tooget hello dettagli dell'attività viene eseguita per un **specifico** sezione.</span><span class="sxs-lookup"><span data-stu-id="79d7e-321">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="79d7e-322">Copiare il valore di data / ora hello dall'output di hello hello comando toospecify hello valore precedente per il parametro StartDateTime hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-322">Copy hello date-time value from hello output of hello previous command toospecify hello value for hello StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="79d7e-323">Ecco l'output di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="79d7e-323">Here is hello sample output:</span></span> 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

<span data-ttu-id="79d7e-324">Vedere le [informazioni di riferimento per i cmdlet di Data factory](/powershell/module/azurerm.datafactories) per la documentazione completa sui cmdlet di Data factory.</span><span class="sxs-lookup"><span data-stu-id="79d7e-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="79d7e-325">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="79d7e-325">Summary</span></span>
<span data-ttu-id="79d7e-326">In questa esercitazione è creato un Azure factory toocopy dati da un database di SQL Azure tooan blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d7e-326">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="79d7e-327">È stato utilizzato PowerShell toocreate hello data factory, i servizi collegati, i set di dati e una pipeline.</span><span class="sxs-lookup"><span data-stu-id="79d7e-327">You used PowerShell toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="79d7e-328">Ecco i passaggi di alto livello hello effettuati in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="79d7e-328">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="79d7e-329">Creare un'istanza di Azure **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="79d7e-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="79d7e-330">Creare **servizi collegati**:</span><span class="sxs-lookup"><span data-stu-id="79d7e-330">Created **linked services**:</span></span>

   <span data-ttu-id="79d7e-331">a.</span><span class="sxs-lookup"><span data-stu-id="79d7e-331">a.</span></span> <span data-ttu-id="79d7e-332">Un **di archiviazione di Azure** collegati toolink service account di archiviazione Azure che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="79d7e-332">An **Azure Storage** linked service toolink your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="79d7e-333">b.</span><span class="sxs-lookup"><span data-stu-id="79d7e-333">b.</span></span> <span data-ttu-id="79d7e-334">Un **SQL Azure** collegati toolink servizio database di SQL che contiene i dati di output di hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-334">An **Azure SQL** linked service toolink your SQL database that holds hello output data.</span></span>
3. <span data-ttu-id="79d7e-335">Creare **set di dati** che descrivono dati di input e di output per le pipeline.</span><span class="sxs-lookup"><span data-stu-id="79d7e-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="79d7e-336">Creare un **pipeline** con **attività di copia**, con **BlobSource** come origine di hello e **SqlSink** come sink hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as hello source and **SqlSink** as hello sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79d7e-337">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="79d7e-337">Next steps</span></span>
<span data-ttu-id="79d7e-338">In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="79d7e-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="79d7e-339">Hello nella tabella seguente fornisce un elenco di archivi di dati supportato come origini e destinazioni da attività di copia hello:</span><span class="sxs-lookup"><span data-stu-id="79d7e-339">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="79d7e-340">toolearn su come archiviano dati toocopy da e verso un tipo di dati, fare clic su collegamento hello per hello archivio di dati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="79d7e-340">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span> 

