---
title: aaaBuild la prima data factory (PowerShell) | Documenti Microsoft
description: In questa esercitazione viene creata una pipeline di esempio di Azure Data Factory usando Azure PowerShell.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="0d359-103">Esercitazione: Creare la prima data factory di Azure con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d359-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d359-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0d359-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="0d359-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0d359-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="0d359-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0d359-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="0d359-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d359-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="0d359-108">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0d359-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="0d359-109">API REST</span><span class="sxs-lookup"><span data-stu-id="0d359-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="0d359-110">In questo articolo, utilizzare Azure PowerShell toocreate prima data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d359-110">In this article, you use Azure PowerShell toocreate your first Azure data factory.</span></span> <span data-ttu-id="0d359-111">esercitazione di hello toodo tramite altri strumenti/SDK, selezionare una delle opzioni di hello dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="0d359-112">pipeline Hello in questa esercitazione è un'attività: **attività Hive di HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0d359-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="0d359-113">Questa attività esegue uno script hive in un cluster HDInsight di Azure che trasformazioni i dati di output tooproduce di dati di input.</span><span class="sxs-lookup"><span data-stu-id="0d359-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="0d359-114">pipeline di Hello è toorun pianificato dopo un mese tra hello specificato di ore di inizio e fine.</span><span class="sxs-lookup"><span data-stu-id="0d359-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="0d359-115">pipeline di dati Hello in questa esercitazione Trasforma i dati di output tooproduce di dati di input.</span><span class="sxs-lookup"><span data-stu-id="0d359-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="0d359-116">Non copia dati da un archivio dati di origine dati archivio tooa destinazione.</span><span class="sxs-lookup"><span data-stu-id="0d359-116">It does not copy data from a source data store tooa destination data store.</span></span> <span data-ttu-id="0d359-117">Per un'esercitazione su come dati di toocopy tramite Data Factory di Azure, vedere [esercitazione: copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0d359-117">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="0d359-118">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="0d359-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="0d359-119">Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="0d359-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="0d359-120">Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="0d359-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d359-121">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0d359-121">Prerequisites</span></span>
* <span data-ttu-id="0d359-122">Leggere [esercitazione Panoramica](data-factory-build-your-first-pipeline.md) articolo e hello completo **prerequisito** passaggi.</span><span class="sxs-lookup"><span data-stu-id="0d359-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="0d359-123">Seguire le istruzioni [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo tooinstall versione più recente di Azure PowerShell nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="0d359-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="0d359-124">(facoltativo) In questo articolo non copre tutti i cmdlet di hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0d359-124">(optional) This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="0d359-125">Vedere [Riferimento ai cmdlet di Data factory](/powershell/module/azurerm.datafactories) per la documentazione completa sui cmdlet di Data factory.</span><span class="sxs-lookup"><span data-stu-id="0d359-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="0d359-126">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="0d359-126">Create data factory</span></span>
<span data-ttu-id="0d359-127">In questo passaggio, si usa Azure PowerShell toocreate una Data Factory di Azure denominato **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="0d359-127">In this step, you use Azure PowerShell toocreate an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="0d359-128">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="0d359-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="0d359-129">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="0d359-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="0d359-130">Dati di input, ad esempio, una data toocopy attività di copia da un archivio dati di origine tooa destinazione e un toorun attività Hive di HDInsight un tootransform script Hive.</span><span class="sxs-lookup"><span data-stu-id="0d359-130">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="0d359-131">Iniziamo con la creazione di data factory di hello in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="0d359-131">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="0d359-132">Avviare PowerShell di Azure ed eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="0d359-132">Start Azure PowerShell and run hello following command.</span></span> <span data-ttu-id="0d359-133">Mantenere aperta fino al fine di hello dell'esercitazione Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d359-133">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="0d359-134">Se si chiude e riapre, è necessario toorun questi comandi nuovamente.</span><span class="sxs-lookup"><span data-stu-id="0d359-134">If you close and reopen, you need toorun these commands again.</span></span>
   * <span data-ttu-id="0d359-135">Eseguire hello comando seguente e immettere nome utente hello e la password usati toosign in toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d359-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="0d359-136">Eseguire hello successivo comando tooview tutte le sottoscrizioni di hello per questo account.</span><span class="sxs-lookup"><span data-stu-id="0d359-136">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="0d359-137">Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0d359-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="0d359-138">La sottoscrizione deve essere hello uguali a quelli hello usato nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-138">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="0d359-139">Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d359-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="0d359-140">Alcuni dei passaggi di hello in questa esercitazione si supponga di utilizza il gruppo di risorse di hello denominato ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="0d359-140">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="0d359-141">Se si utilizza un gruppo di risorse diverso, è necessario toouse, al posto di ADFTutorialResourceGroup in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0d359-141">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="0d359-142">Eseguire hello **New AzureRmDataFactory** cmdlet che crea una factory di dati denominata **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="0d359-142">Run hello **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="0d359-143">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="0d359-143">Note hello following points:</span></span>

* <span data-ttu-id="0d359-144">nome Hello di hello Azure Data Factory deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="0d359-144">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="0d359-145">Se viene visualizzato l'errore hello **"FirstDataFactoryPSH" nome della Data factory non è disponibile**, modificare il nome di hello (ad esempio, yournameFirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="0d359-145">If you receive hello error **Data factory name “FirstDataFactoryPSH” is not available**, change hello name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="0d359-146">Durante l'esecuzione di passaggi in questa esercitazione usare questo nome anziché ADFTutorialFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="0d359-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="0d359-147">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="0d359-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="0d359-148">le istanze di Data Factory toocreate, è necessario toobe un amministratore o un collaboratore di hello sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="0d359-148">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="0d359-149">nome Hello della hello data factory può essere registrato come un nome DNS in futuro hello e pertanto diventano visibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="0d359-149">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
* <span data-ttu-id="0d359-150">Se viene visualizzato l'errore hello: "**questa sottoscrizione non è registrato toouse dello spazio dei nomi Microsoft. DataFactory**", effettuare una delle seguenti hello e riprovare:</span><span class="sxs-lookup"><span data-stu-id="0d359-150">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="0d359-151">In Azure PowerShell, eseguire hello seguenti provider di comandi tooregister hello Data Factory:</span><span class="sxs-lookup"><span data-stu-id="0d359-151">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="0d359-152">È possibile eseguire hello successivo comando tooconfirm tale hello Data Factory di provider è stato registrato:</span><span class="sxs-lookup"><span data-stu-id="0d359-152">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="0d359-153">Account di accesso tramite hello sottoscrizione di Azure in hello [portale di Azure](https://portal.azure.com) e passare a pannello di Data Factory tooa creare una data factory nel portale di Azure hello (o).</span><span class="sxs-lookup"><span data-stu-id="0d359-153">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="0d359-154">Questa azione registra automaticamente i provider di hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-154">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="0d359-155">Prima di creare una pipeline, è necessario toocreate alcune entità Data Factory prima.</span><span class="sxs-lookup"><span data-stu-id="0d359-155">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="0d359-156">Creare innanzitutto i dati di servizi collegati toolink archivi/calcola tooyour dati archiviano, definiscono l'input e output dei dati di input/output toorepresent di set di dati in archivi dati collegato e quindi creare pipeline hello con un'attività che utilizza questi set di dati.</span><span class="sxs-lookup"><span data-stu-id="0d359-156">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="0d359-157">Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="0d359-157">Create linked services</span></span>
<span data-ttu-id="0d359-158">In questo passaggio è collegare l'account di archiviazione di Azure e una factory del dati tooyour cluster Azure HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="0d359-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="0d359-159">contiene account di archiviazione di Azure Hello hello dati di input e outpui per la pipeline di hello in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="0d359-159">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="0d359-160">servizio collegato di HDInsight Hello è toorun usato uno script Hive specificato nell'attività hello della pipeline hello in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="0d359-160">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="0d359-161">Identificazione dei dati archivio/calcolo servizi vengono utilizzati nello scenario e collegano tali toohello data factory di servizi mediante la creazione di servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="0d359-161">Identify what data store/compute services are used in your scenario and link those services toohello data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="0d359-162">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0d359-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="0d359-163">In questo passaggio si collega la data factory tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d359-163">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="0d359-164">Utilizzare hello stesso account di archiviazione di Azure i dati di input/output toostore e hello HQL file di script.</span><span class="sxs-lookup"><span data-stu-id="0d359-164">You use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="0d359-165">Creare un file JSON denominato StorageLinkedService.json nella cartella C:\ADFGetStarted hello con hello seguente contenuto.</span><span class="sxs-lookup"><span data-stu-id="0d359-165">Create a JSON file named StorageLinkedService.json in hello C:\ADFGetStarted folder with hello following content.</span></span> <span data-ttu-id="0d359-166">Creare la cartella hello ADFGetStarted se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="0d359-166">Create hello folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="0d359-167">Sostituire **nome account** con nome hello dell'account di archiviazione di Azure e **chiave dell'account** con la chiave di accesso hello di hello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d359-167">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="0d359-168">toolearn come accedere a tooget lo spazio di archiviazione della chiave, vedere informazioni come tooview, copiare e rigenerare archiviazione accedere alle chiavi in hello [gestire account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="0d359-168">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="0d359-169">In Azure PowerShell, passare toohello ADFGetStarted cartella.</span><span class="sxs-lookup"><span data-stu-id="0d359-169">In Azure PowerShell, switch toohello ADFGetStarted folder.</span></span>
3. <span data-ttu-id="0d359-170">È possibile utilizzare hello **New AzureRmDataFactoryLinkedService** cmdlet che crea un servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="0d359-170">You can use hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="0d359-171">Questo cmdlet e gli altri cmdlet di Data Factory da usare in questa esercitazione richiede valori toopass per hello *ResourceGroupName* e *DataFactoryName* parametri.</span><span class="sxs-lookup"><span data-stu-id="0d359-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="0d359-172">In alternativa, è possibile utilizzare **Get AzureRmDataFactory** tooget un **DataFactory** , quindi passare l'oggetto hello senza digitare *ResourceGroupName* e  *DataFactoryName* ogni volta che si esegue un cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0d359-172">Alternatively, you can use **Get-AzureRmDataFactory** tooget a **DataFactory** object and pass hello object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="0d359-173">Comando che segue hello fase output di hello tooassign di hello **Get AzureRmDataFactory** cmdlet tooa **$df** variabile.</span><span class="sxs-lookup"><span data-stu-id="0d359-173">Run hello following command tooassign hello output of hello **Get-AzureRmDataFactory** cmdlet tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="0d359-174">A questo punto, eseguire hello **New AzureRmDataFactoryLinkedService** cmdlet che crea hello collegato **StorageLinkedService** servizio.</span><span class="sxs-lookup"><span data-stu-id="0d359-174">Now, run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="0d359-175">Se non è stato eseguito hello **Get AzureRmDataFactory** cmdlet e hello assegnato output toohello **$df** variabile, sarebbe necessario valori toospecify per hello *ResourceGroupName*e *DataFactoryName* parametri come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0d359-175">If you hadn't run hello **Get-AzureRmDataFactory** cmdlet and assigned hello output toohello **$df** variable, you would have toospecify values for hello *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="0d359-176">Se si chiude Azure PowerShell centro hello di esercitazione hello, è necessario hello toorun **Get AzureRmDataFactory** cmdlet successivo avvio di esercitazione hello toocomplete di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d359-176">If you close Azure PowerShell in hello middle of hello tutorial, you have toorun hello **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell toocomplete hello tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="0d359-177">Creare un servizio collegato Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0d359-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="0d359-178">In questo passaggio si collega una factory del dati tooyour cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="0d359-178">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="0d359-179">cluster HDInsight Hello viene automaticamente creato in fase di esecuzione ed eliminato al termine per l'elaborazione e inattività per l'intervallo di tempo specificato hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-179">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="0d359-180">È possibile usare il proprio cluster HDInsight anziché un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="0d359-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="0d359-181">Per informazioni dettagliate, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="0d359-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="0d359-182">Creare un file JSON denominato **HDInsightOnDemandLinkedService**JSON in hello **C:\ADFGetStarted** cartella con hello dopo contenuto.</span><span class="sxs-lookup"><span data-stu-id="0d359-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in hello **C:\ADFGetStarted** folder with hello following content.</span></span>

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
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    <span data-ttu-id="0d359-183">Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="0d359-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="0d359-184">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0d359-184">Property</span></span> | <span data-ttu-id="0d359-185">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0d359-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="0d359-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="0d359-186">ClusterSize</span></span> |<span data-ttu-id="0d359-187">Specifica dimensioni hello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="0d359-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="0d359-188">TimeToLive</span></span> |<span data-ttu-id="0d359-189">Specifica il tempo di inattività hello per il cluster HDInsight hello, prima che venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="0d359-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="0d359-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0d359-190">linkedServiceName</span></span> |<span data-ttu-id="0d359-191">Specifica l'account di archiviazione hello toostore utilizzati hello registri generati da HDInsight</span><span class="sxs-lookup"><span data-stu-id="0d359-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="0d359-192">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="0d359-192">Note hello following points:</span></span>

   * <span data-ttu-id="0d359-193">Hello Data Factory viene creata una **basati su Linux** cluster HDInsight per l'utente con hello JSON.</span><span class="sxs-lookup"><span data-stu-id="0d359-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="0d359-194">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="0d359-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="0d359-195">È possibile usare il **proprio cluster HDInsight** anziché un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="0d359-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="0d359-196">Per i dettagli, vedere [Servizio collegato Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="0d359-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="0d359-197">Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato in JSON hello (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="0d359-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="0d359-198">HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="0d359-199">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="0d359-199">This behavior is by design.</span></span> <span data-ttu-id="0d359-200">Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che viene elaborata una sezione, a meno che non esista un cluster attivo (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="0d359-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="0d359-201">cluster Hello viene eliminato automaticamente quando viene eseguita un'elaborazione hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="0d359-202">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d359-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="0d359-203">Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0d359-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="0d359-204">i nomi di Hello di questi contenitori seguono un modello: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="0d359-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="0d359-205">Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="0d359-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="0d359-206">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="0d359-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="0d359-207">Eseguire hello **New AzureRmDataFactoryLinkedService** cmdlet che crea hello collegato servizio denominato HDInsightOnDemandLinkedService.</span><span class="sxs-lookup"><span data-stu-id="0d359-207">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="0d359-208">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="0d359-208">Create datasets</span></span>
<span data-ttu-id="0d359-209">In questo passaggio creare set di dati toorepresent hello input e output dei dati per l'elaborazione Hive.</span><span class="sxs-lookup"><span data-stu-id="0d359-209">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="0d359-210">Questi set di dati di riferimento toohello **StorageLinkedService** creata precedentemente in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0d359-210">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="0d359-211">Hello tooan punti di servizio collegato account di archiviazione di Azure e i set di dati specificare contenitore, cartella, nome del file nell'archiviazione hello che contiene l'input e output di dati.</span><span class="sxs-lookup"><span data-stu-id="0d359-211">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="0d359-212">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="0d359-212">Create input dataset</span></span>
1. <span data-ttu-id="0d359-213">Creare un file JSON denominato **InputTable.json** in hello **C:\ADFGetStarted** cartella con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="0d359-213">Create a JSON file named **InputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="0d359-214">Hello JSON definisce un set di dati denominato **AzureBlobInput**, che rappresenta i dati di input per un'attività nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-214">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="0d359-215">Inoltre, specifica che i dati di input hello si trovano nel contenitore di blob hello chiamato **adfgetstarted** e cartella hello denominata **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="0d359-215">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    <span data-ttu-id="0d359-216">Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="0d359-216">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="0d359-217">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0d359-217">Property</span></span> | <span data-ttu-id="0d359-218">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0d359-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="0d359-219">type</span><span class="sxs-lookup"><span data-stu-id="0d359-219">type</span></span> |<span data-ttu-id="0d359-220">proprietà tipo Hello è impostato tooAzureBlob perché risiedono dati nell'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d359-220">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="0d359-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0d359-221">linkedServiceName</span></span> |<span data-ttu-id="0d359-222">si riferisce toohello StorageLinkedService creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0d359-222">refers toohello StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="0d359-223">fileName</span><span class="sxs-lookup"><span data-stu-id="0d359-223">fileName</span></span> |<span data-ttu-id="0d359-224">Questa proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="0d359-224">This property is optional.</span></span> <span data-ttu-id="0d359-225">Se si omette questa proprietà, vengono selezionati tutti i file hello folderPath hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-225">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="0d359-226">In questo caso, viene elaborato solo hello input.log.</span><span class="sxs-lookup"><span data-stu-id="0d359-226">In this case, only hello input.log is processed.</span></span> |
   | <span data-ttu-id="0d359-227">type</span><span class="sxs-lookup"><span data-stu-id="0d359-227">type</span></span> |<span data-ttu-id="0d359-228">file di log Hello sono in formato testo, permette di usare TextFormat.</span><span class="sxs-lookup"><span data-stu-id="0d359-228">hello log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="0d359-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="0d359-229">columnDelimiter</span></span> |<span data-ttu-id="0d359-230">le colonne nei file di log hello sono delimitate dal carattere virgola di hello (,).</span><span class="sxs-lookup"><span data-stu-id="0d359-230">columns in hello log files are delimited by hello comma character (,).</span></span> |
   | <span data-ttu-id="0d359-231">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="0d359-231">frequency/interval</span></span> |<span data-ttu-id="0d359-232">frequenza impostata tooMonth e l'intervallo è 1, che significa che le sezioni di input hello sono disponibili ogni mese.</span><span class="sxs-lookup"><span data-stu-id="0d359-232">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="0d359-233">external</span><span class="sxs-lookup"><span data-stu-id="0d359-233">external</span></span> |<span data-ttu-id="0d359-234">Questa proprietà è impostata tootrue se i dati di input hello non viene generati dal servizio Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-234">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |
2. <span data-ttu-id="0d359-235">Eseguire hello comando nel set di dati Data Factory hello toocreate Azure PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="0d359-235">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="0d359-236">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="0d359-236">Create output dataset</span></span>
<span data-ttu-id="0d359-237">È quindi possibile creare hello output dataset toorepresent hello output dati archiviati in archiviazione Blob di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-237">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="0d359-238">Creare un file JSON denominato **OutputTable.json** in hello **C:\ADFGetStarted** cartella con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="0d359-238">Create a JSON file named **OutputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="0d359-239">Hello JSON definisce un set di dati denominato **AzureBlobOutput**, che rappresenta i dati di output per un'attività nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-239">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="0d359-240">Inoltre, specifica che i risultati di hello vengono archiviati nel contenitore blob hello chiamato **adfgetstarted** e cartella hello denominata **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="0d359-240">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="0d359-241">Hello **disponibilità** sezione specifica di tale set di dati di output di hello viene prodotto su base mensile.</span><span class="sxs-lookup"><span data-stu-id="0d359-241">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="0d359-242">Eseguire hello comando nel set di dati Data Factory hello toocreate Azure PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="0d359-242">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="0d359-243">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="0d359-243">Create pipeline</span></span>
<span data-ttu-id="0d359-244">In questo passaggio viene creata la prima pipeline con un'attività **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="0d359-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="0d359-245">Sezione di input è disponibile ogni mese (frequenza: mese, intervallo: 1), sezione di output viene prodotta ogni mese e hello dell'utilità di pianificazione per l'attività hello viene anche impostata toomonthly.</span><span class="sxs-lookup"><span data-stu-id="0d359-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="0d359-246">le impostazioni di Hello per set di dati output hello e utilità di pianificazione attività hello devono corrispondere.</span><span class="sxs-lookup"><span data-stu-id="0d359-246">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="0d359-247">Set di dati di output è attualmente, quali unità hello pianificazione, pertanto è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="0d359-247">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="0d359-248">Se l'attività hello non accetta alcun input, è possibile ignorare i set di dati input hello creazione.</span><span class="sxs-lookup"><span data-stu-id="0d359-248">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="0d359-249">proprietà Hello utilizzate nei hello JSON seguente sono illustrate alla fine di hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="0d359-249">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="0d359-250">Creare un file JSON denominato MyFirstPipelinePSH.json nella cartella C:\ADFGetStarted hello con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="0d359-250">Create a JSON file named MyFirstPipelinePSH.json in hello C:\ADFGetStarted folder with hello following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0d359-251">Sostituire **storageaccountname** con nome hello dell'account di archiviazione in hello JSON.</span><span class="sxs-lookup"><span data-stu-id="0d359-251">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
   >
   >

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
                        "scriptLinkedService": "StorageLinkedService",
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
    <span data-ttu-id="0d359-252">Nel frammento di codice JSON hello, si sta creando una pipeline che è costituito da una singola attività che utilizza Hive tooprocess dati in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0d359-252">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="0d359-253">file di script Hive Hello, **partitionweblogs.hql**, viene archiviato nell'account di archiviazione Azure hello (specificato da scriptLinkedService hello, chiamato **StorageLinkedService**) e in **script**  cartella nel contenitore hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="0d359-253">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="0d359-254">Hello **definisce** sezione è le impostazioni di runtime hello toospecify utilizzati che essere passato script hive toohello come valori di configurazione di Hive (ad esempio ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).</span><span class="sxs-lookup"><span data-stu-id="0d359-254">hello **defines** section is used toospecify hello runtime settings that be passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="0d359-255">Hello **avviare** e **fine** le proprietà della pipeline hello specifica periodo attivo di hello della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-255">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="0d359-256">In formato JSON dell'attività hello, specificare tale script Hive hello viene eseguito sul calcolo hello specificato da hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="0d359-256">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0d359-257">Vedere la sezione "JSON di Pipeline" in [pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md) per dettagli sulle proprietà JSON che vengono utilizzati nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in hello example.</span></span>

2. <span data-ttu-id="0d359-258">Assicurarsi di visualizzare hello **input.log** file hello **adfgetstarted/inputdata** cartella hello archiviazione blob di Azure e hello fase della pipeline hello toodeploy dei comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="0d359-258">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="0d359-259">Poiché hello **avviare** e **fine** volte in cui vengono impostate in hello precedente e **isPaused** è toofalse set, pipeline hello esecuzioni (attività nella pipeline hello) immediatamente dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0d359-259">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="0d359-260">La creazione della prima pipeline tramite Azure PowerShell è così completata.</span><span class="sxs-lookup"><span data-stu-id="0d359-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="0d359-261">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="0d359-261">Monitor pipeline</span></span>
<span data-ttu-id="0d359-262">In questo passaggio, utilizzare Azure PowerShell toomonitor cosa accade in un data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d359-262">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="0d359-263">Eseguire **Get AzureRmDataFactory** e assegnare hello output tooa **$df** variabile.</span><span class="sxs-lookup"><span data-stu-id="0d359-263">Run **Get-AzureRmDataFactory** and assign hello output tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="0d359-264">Eseguire **Get AzureRmDataFactorySlice** tooget dettagli su tutte le sezioni di hello **EmpSQLTable**, che è una tabella di output di hello della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-264">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **EmpSQLTable**, which is hello output table of hello pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="0d359-265">Si noti che è possibile specificare StartDateTime hello hello che stessa ora di inizio specificata in formato JSON della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-265">Notice that hello StartDateTime you specify here is hello same start time specified in hello pipeline JSON.</span></span> <span data-ttu-id="0d359-266">Ecco l'output di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="0d359-266">Here is hello sample output:</span></span>

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="0d359-267">Eseguire **Get AzureRmDataFactoryRun** tooget hello dettagli dell'attività viene eseguita per una specifica sezione.</span><span class="sxs-lookup"><span data-stu-id="0d359-267">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="0d359-268">Ecco l'output di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="0d359-268">Here is hello sample output:</span></span> 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    <span data-ttu-id="0d359-269">È possibile mantenere in esecuzione questo cmdlet finché non viene visualizzata la sezione hello in **pronto** stato o **Failed** stato.</span><span class="sxs-lookup"><span data-stu-id="0d359-269">You can keep running this cmdlet until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="0d359-270">Quando la sezione hello è nello stato pronto, controllare hello **partitioneddata** cartella hello **adfgetstarted** contenitore nell'archiviazione blob per hello i dati di output.</span><span class="sxs-lookup"><span data-stu-id="0d359-270">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="0d359-271">La creazione di un cluster HDInsight su richiesta di solito richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="0d359-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![Dati di output](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="0d359-273">La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti).</span><span class="sxs-lookup"><span data-stu-id="0d359-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="0d359-274">Pertanto, prevedere hello pipeline tootake **circa 30 minuti** tooprocess hello sezione.</span><span class="sxs-lookup"><span data-stu-id="0d359-274">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
> <span data-ttu-id="0d359-275">file di input Hello eliminato quando la sezione hello viene elaborata correttamente.</span><span class="sxs-lookup"><span data-stu-id="0d359-275">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="0d359-276">Pertanto, se si desidera toorerun hello sezione o hello esercitazione nuovamente, hello del file di input (input.log) toohello inputdata cartella del contenitore adfgetstarted hello di caricamento.</span><span class="sxs-lookup"><span data-stu-id="0d359-276">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="0d359-277">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="0d359-277">Summary</span></span>
<span data-ttu-id="0d359-278">In questa esercitazione, creato un Azure factory tooprocess dati tramite l'esecuzione di script Hive in un cluster di HDInsight hadoop.</span><span class="sxs-lookup"><span data-stu-id="0d359-278">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="0d359-279">È stato utilizzato hello Editor delle Data Factory in hello toodo portale Azure hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0d359-279">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="0d359-280">Creare un'istanza di Azure **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="0d359-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="0d359-281">Creare due **servizi collegati**:</span><span class="sxs-lookup"><span data-stu-id="0d359-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="0d359-282">**Archiviazione di Azure** collegati toolink servizio di archiviazione blob di Azure che contiene una data factory toohello di file di input/output.</span><span class="sxs-lookup"><span data-stu-id="0d359-282">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="0d359-283">**Azure HDInsight** toolink servizio collegato su richiesta di una factory del dati toohello cluster HDInsight Hadoop su richiesta.</span><span class="sxs-lookup"><span data-stu-id="0d359-283">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="0d359-284">Data Factory di Azure crea un HDInsight Hadoop dati di input tooprocess just-in-time di cluster e generare dati di output.</span><span class="sxs-lookup"><span data-stu-id="0d359-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="0d359-285">Creare due **set di dati**, che descrivono i dati di input e outpui per l'attività Hive di HDInsight nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="0d359-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="0d359-286">Creare una **pipeline** con un'attività **Hive di HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0d359-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d359-287">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d359-287">Next steps</span></span>
<span data-ttu-id="0d359-288">In questo articolo è stata creata una pipeline con un'attività di trasformazione (attività HDInsight) che esegue uno script Hive in un cluster HDInsight su richiesta di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d359-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="0d359-289">toosee toouse un dati toocopy attività di copia da un tooAzure Blob di Azure SQL, vedere [esercitazione: copiare i dati da un tooAzure Blob di Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0d359-289">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0d359-290">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0d359-290">See Also</span></span>
| <span data-ttu-id="0d359-291">Argomento</span><span class="sxs-lookup"><span data-stu-id="0d359-291">Topic</span></span> | <span data-ttu-id="0d359-292">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0d359-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="0d359-293">Informazioni di riferimento sui cmdlet di Data factory</span><span class="sxs-lookup"><span data-stu-id="0d359-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="0d359-294">Vedere la documentazione completa sui cmdlet di Data factory</span><span class="sxs-lookup"><span data-stu-id="0d359-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="0d359-295">Pipeline</span><span class="sxs-lookup"><span data-stu-id="0d359-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="0d359-296">In questo articolo consente di comprendere le pipeline e attività nella Data Factory di Azure e come toouse li tooconstruct end-to-end basato sui dati dei flussi di lavoro degli scenario o dell'azienda.</span><span class="sxs-lookup"><span data-stu-id="0d359-296">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="0d359-297">Set di dati</span><span class="sxs-lookup"><span data-stu-id="0d359-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="0d359-298">Questo articolo fornisce informazioni sui set di dati in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0d359-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="0d359-299">Pianificazione ed esecuzione</span><span class="sxs-lookup"><span data-stu-id="0d359-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="0d359-300">Questo articolo illustra gli aspetti hello di pianificazione e l'esecuzione del modello di applicazione di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0d359-300">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="0d359-301">Monitorare e gestire le pipeline con l'app di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="0d359-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="0d359-302">In questo articolo viene descritto come toomonitor, gestire ed eseguire il debug pipeline utilizzando hello monitoraggio e gestione delle App.</span><span class="sxs-lookup"><span data-stu-id="0d359-302">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
