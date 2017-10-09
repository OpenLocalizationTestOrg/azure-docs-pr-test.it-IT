---
title: 'Esercitazione: Utilizzare l''API REST toocreate una pipeline di Data Factory di Azure | Documenti Microsoft'
description: "In questa esercitazione è utilizzare API REST toocreate una pipeline di Data Factory di Azure con i dati di toocopy un attività di copia da un archivio blob di Azure, un database SQL di Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="3f770-103">Esercitazione: Utilizzare l'API REST toocreate un dati toocopy della pipeline di Data Factory di Azure</span><span class="sxs-lookup"><span data-stu-id="3f770-103">Tutorial: Use REST API toocreate an Azure Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3f770-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3f770-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="3f770-105">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="3f770-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="3f770-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3f770-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="3f770-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3f770-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="3f770-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f770-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="3f770-109">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3f770-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="3f770-110">API REST</span><span class="sxs-lookup"><span data-stu-id="3f770-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="3f770-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="3f770-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="3f770-112">In questo articolo viene illustrato come toouse REST API toocreate una data factory con una pipeline che copia i dati da un database di SQL Azure tooan di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-112">In this article, you learn how toouse REST API toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="3f770-113">Se si tooAzure nuova Data Factory, leggere hello [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo prima di eseguire questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3f770-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="3f770-114">In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="3f770-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="3f770-115">attività di copia Hello copia dati da un archivio dati di sink supportati tooa di archivio di dati supportati.</span><span class="sxs-lookup"><span data-stu-id="3f770-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="3f770-116">Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="3f770-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="3f770-117">attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="3f770-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="3f770-118">Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="3f770-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="3f770-119">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="3f770-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="3f770-120">Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="3f770-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="3f770-121">Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="3f770-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="3f770-122">In questo articolo non copre tutti hello API REST di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3f770-122">This article does not cover all hello Data Factory REST API.</span></span> <span data-ttu-id="3f770-123">Per la documentazione completa sui cmdlet di Data Factory, vedere [Informazioni di riferimento sull'API REST di Data Factory](/rest/api/datafactory/) .</span><span class="sxs-lookup"><span data-stu-id="3f770-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="3f770-124">pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione.</span><span class="sxs-lookup"><span data-stu-id="3f770-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="3f770-125">Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare una pipeline di dati tootransform utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="3f770-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f770-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3f770-126">Prerequisites</span></span>
* <span data-ttu-id="3f770-127">Seguire i passaggi [esercitazione Panoramica](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) e hello completo **prerequisito** passaggi.</span><span class="sxs-lookup"><span data-stu-id="3f770-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="3f770-128">Installare [Curl](https://curl.haxx.se/dlwiz/) nel computer.</span><span class="sxs-lookup"><span data-stu-id="3f770-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="3f770-129">Lo strumento di Curl hello con altri comandi toocreate una data factory.</span><span class="sxs-lookup"><span data-stu-id="3f770-129">You use hello Curl tool with REST commands toocreate a data factory.</span></span> 
* <span data-ttu-id="3f770-130">Seguire le istruzioni disponibili in [questo articolo](../azure-resource-manager/resource-group-create-service-principal-portal.md) per:</span><span class="sxs-lookup"><span data-stu-id="3f770-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="3f770-131">Creare un'applicazione Web denominata **ADFCopyTutorialApp** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f770-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="3f770-132">Ottenere i valori per l'**ID client** e la **chiave privata**.</span><span class="sxs-lookup"><span data-stu-id="3f770-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="3f770-133">Ottenere l' **ID tenant**.</span><span class="sxs-lookup"><span data-stu-id="3f770-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="3f770-134">Assegnare hello **ADFCopyTutorialApp** applicazione toohello **Data Factory collaboratore** ruolo.</span><span class="sxs-lookup"><span data-stu-id="3f770-134">Assign hello **ADFCopyTutorialApp** application toohello **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="3f770-135">Installare [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3f770-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="3f770-136">Avviare **PowerShell** e hello i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="3f770-136">Launch **PowerShell** and do hello following steps.</span></span> <span data-ttu-id="3f770-137">Mantenere aperta fino al fine di hello dell'esercitazione Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f770-137">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="3f770-138">Se si chiude e riapre, è necessario comandi hello toorun nuovamente.</span><span class="sxs-lookup"><span data-stu-id="3f770-138">If you close and reopen, you need toorun hello commands again.</span></span>
  
  1. <span data-ttu-id="3f770-139">Eseguire hello comando seguente e immettere nome utente hello e la password usati toosign in toohello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="3f770-139">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="3f770-140">Eseguire hello successivo comando tooview tutte le sottoscrizioni di hello per questo account:</span><span class="sxs-lookup"><span data-stu-id="3f770-140">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="3f770-141">Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3f770-141">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="3f770-142">Sostituire  **&lt;NameOfAzureSubscription** &gt; con nome hello della sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-142">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="3f770-143">Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo hello comando in hello PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="3f770-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="3f770-144">Se il gruppo di risorse hello esiste già, specificare se tooupdate è (Y) o mantenerlo come (N).</span><span class="sxs-lookup"><span data-stu-id="3f770-144">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="3f770-145">Alcuni dei passaggi di hello in questa esercitazione si supponga di utilizza il gruppo di risorse di hello denominato ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="3f770-145">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="3f770-146">Se si utilizza un gruppo di risorse diverso, è necessario il nome hello toouse del gruppo di risorse al posto di ADFTutorialResourceGroup in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3f770-146">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="3f770-147">Creare le definizioni JSON</span><span class="sxs-lookup"><span data-stu-id="3f770-147">Create JSON definitions</span></span>
<span data-ttu-id="3f770-148">Creare i seguenti file JSON nella cartella hello curl.exe in cui si trova.</span><span class="sxs-lookup"><span data-stu-id="3f770-148">Create following JSON files in hello folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="3f770-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="3f770-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3f770-150">Nome deve essere globalmente univoco, pertanto è consigliabile toomake ADFCopyTutorialDF tooprefix/suffisso è un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="3f770-150">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="3f770-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="3f770-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3f770-152">Sostituire **accountname** e **accountkey** con il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="3f770-153">toolearn modalità di accesso di archiviazione di tooget chiave, vedere [visualizzazione, copia e l'archiviazione di rigenerare le chiavi di accesso](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="3f770-153">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

```JSON
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

<span data-ttu-id="3f770-154">Per informazioni dettagliate sulle proprietà JSON, vedere [Servizio collegato Archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="3f770-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="3f770-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="3f770-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3f770-156">Sostituire **servername**, **databasename**, **username**, e **password** con il nome del server SQL Azure, nome del database SQL, utente account e password per account hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for hello account.</span></span>  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="3f770-157">Per informazioni dettagliate sulle proprietà JSON, vedere la sezione relativa al [servizio collegato SQL di Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3f770-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="3f770-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="3f770-158">inputdataset.json</span></span>

```JSON
{
  "name": "AzureBlobInput",
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
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
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

<span data-ttu-id="3f770-159">Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="3f770-159">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="3f770-160">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3f770-160">Property</span></span> | <span data-ttu-id="3f770-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3f770-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3f770-162">type</span><span class="sxs-lookup"><span data-stu-id="3f770-162">type</span></span> | <span data-ttu-id="3f770-163">proprietà tipo Hello è troppo**AzureBlob** perché i dati risiedono in una risorsa di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-163">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="3f770-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="3f770-164">linkedServiceName</span></span> | <span data-ttu-id="3f770-165">Fa riferimento toohello **AzureStorageLinkedService** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3f770-165">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="3f770-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="3f770-166">folderPath</span></span> | <span data-ttu-id="3f770-167">Specifica il blob hello **contenitore** hello e **cartella** che contiene il BLOB di input.</span><span class="sxs-lookup"><span data-stu-id="3f770-167">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="3f770-168">In questa esercitazione, adftutorial è il contenitore di blob hello e cartella è hello radice.</span><span class="sxs-lookup"><span data-stu-id="3f770-168">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
| <span data-ttu-id="3f770-169">fileName</span><span class="sxs-lookup"><span data-stu-id="3f770-169">fileName</span></span> | <span data-ttu-id="3f770-170">Questa proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="3f770-170">This property is optional.</span></span> <span data-ttu-id="3f770-171">Se si omette questa proprietà, vengono selezionati tutti i file da folderPath hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-171">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="3f770-172">In questa esercitazione, **emp.txt** specificato per hello fileName, in modo che solo tale file viene prelevato per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="3f770-172">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="3f770-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="3f770-173">format -> type</span></span> |<span data-ttu-id="3f770-174">file di input di Hello è in formato testo hello, permette di usare **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="3f770-174">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="3f770-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="3f770-175">columnDelimiter</span></span> | <span data-ttu-id="3f770-176">Hello colonne nel file di input hello sono delimitate da **carattere virgola (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="3f770-176">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="3f770-177">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="3f770-177">frequency/interval</span></span> | <span data-ttu-id="3f770-178">frequenza Hello è troppo**ora** e l'intervallo viene impostato troppo**1**, il che significa che hello di input sono disponibili sezioni **oraria**.</span><span class="sxs-lookup"><span data-stu-id="3f770-178">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="3f770-179">In altre parole, hello servizio Data Factory esegue la ricerca di dati di input ogni ora nella cartella radice hello del contenitore di blob (**adftutorial**) specificato.</span><span class="sxs-lookup"><span data-stu-id="3f770-179">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="3f770-180">La ricerca di dati hello all'interno di hello pipeline inizio e fine volte, non prima o dopo tali periodi.</span><span class="sxs-lookup"><span data-stu-id="3f770-180">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="3f770-181">external</span><span class="sxs-lookup"><span data-stu-id="3f770-181">external</span></span> | <span data-ttu-id="3f770-182">Questa proprietà è impostata troppo**true** se dati hello non viene generati da questa pipeline.</span><span class="sxs-lookup"><span data-stu-id="3f770-182">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="3f770-183">dati di input Hello in questa esercitazione sono nel file di emp.txt hello, che non viene generato da questa pipeline, è necessario impostare tootrue questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="3f770-183">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

<span data-ttu-id="3f770-184">Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3f770-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="3f770-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="3f770-185">outputdataset.json</span></span>

```JSON
{
  "name": "AzureSqlOutput",
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
<span data-ttu-id="3f770-186">Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="3f770-186">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="3f770-187">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3f770-187">Property</span></span> | <span data-ttu-id="3f770-188">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3f770-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3f770-189">type</span><span class="sxs-lookup"><span data-stu-id="3f770-189">type</span></span> | <span data-ttu-id="3f770-190">proprietà tipo Hello è troppo**AzureSqlTable** perché dati tabella tooa copiato in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-190">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
| <span data-ttu-id="3f770-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="3f770-191">linkedServiceName</span></span> | <span data-ttu-id="3f770-192">Fa riferimento toohello **AzureSqlLinkedService** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3f770-192">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="3f770-193">tableName</span><span class="sxs-lookup"><span data-stu-id="3f770-193">tableName</span></span> | <span data-ttu-id="3f770-194">Hello specificato **tabella** toowhich hello dati vengono copiati.</span><span class="sxs-lookup"><span data-stu-id="3f770-194">Specified hello **table** toowhich hello data is copied.</span></span> | 
| <span data-ttu-id="3f770-195">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="3f770-195">frequency/interval</span></span> | <span data-ttu-id="3f770-196">Hello frequency è impostato troppo**ora** e l'intervallo è **1**, il che significa che vengono create le sezioni di output di hello **oraria** tra hello pipeline iniziale e finale volte, non prima o Dopo tali periodi.</span><span class="sxs-lookup"><span data-stu-id="3f770-196">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="3f770-197">Sono presenti tre colonne: **ID**, **FirstName**, e **LastName** : nella tabella emp hello nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-197">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="3f770-198">ID è una colonna identity, pertanto è necessario solo toospecify **FirstName** e **LastName** qui.</span><span class="sxs-lookup"><span data-stu-id="3f770-198">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="3f770-199">Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore SQL di Azure](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3f770-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="3f770-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="3f770-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
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

<span data-ttu-id="3f770-201">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="3f770-201">Note hello following points:</span></span>

- <span data-ttu-id="3f770-202">Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**copia**.</span><span class="sxs-lookup"><span data-stu-id="3f770-202">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="3f770-203">Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="3f770-203">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="3f770-204">Nelle soluzioni Data Factory è anche possibile usare le [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="3f770-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="3f770-205">Input per attività hello è troppo**AzureBlobInput** e di output per attività hello è troppo**AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="3f770-205">Input for hello activity is set too**AzureBlobInput** and output for hello activity is set too**AzureSqlOutput**.</span></span> 
- <span data-ttu-id="3f770-206">In hello **typeProperties** sezione **BlobSource** è specificato come tipo di origine hello e **SqlSink** è specificato come tipo di sink hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-206">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="3f770-207">Per un elenco completo degli archivi di dati supportati dall'attività di copia hello come origini e sink, vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="3f770-207">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="3f770-208">toolearn sulla modalità di memorizzazione toouse dati specifici supportati come origine/sink, fare clic su collegamento hello nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-208">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
 
<span data-ttu-id="3f770-209">Sostituire il valore di hello di hello **avviare** proprietà con hello giorno corrente e **fine** valore con hello giorno successivo.</span><span class="sxs-lookup"><span data-stu-id="3f770-209">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="3f770-210">È possibile specificare solo parte della data hello e Ignora parte dell'ora hello di hello data ora.</span><span class="sxs-lookup"><span data-stu-id="3f770-210">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="3f770-211">Ad esempio, "2017-02-03", che equivale troppo "2017-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="3f770-211">For example, "2017-02-03", which is equivalent too"2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="3f770-212">Per la data e l'ora di inizio è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="3f770-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="3f770-213">ad esempio 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="3f770-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="3f770-214">Hello **fine** è facoltativo, ma viene usata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3f770-214">hello **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="3f770-215">Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore**".</span><span class="sxs-lookup"><span data-stu-id="3f770-215">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="3f770-216">specificare in modo indefinito, pipeline hello toorun **9999-09-09** come valore hello hello **fine** proprietà.</span><span class="sxs-lookup"><span data-stu-id="3f770-216">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
 
<span data-ttu-id="3f770-217">In hello sopra riportato, sono presenti sezioni dati 24 come ogni sezione di dati viene prodotta ogni ora.</span><span class="sxs-lookup"><span data-stu-id="3f770-217">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="3f770-218">Per le descrizioni delle proprietà JSON nella definizione di una pipeline, vedere l'articolo su come [creare pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="3f770-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3f770-219">Per le descrizioni delle proprietà JSON nella definizione di un'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="3f770-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="3f770-220">Per le descrizioni delle proprietà JSON supportate da BlobSource, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="3f770-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="3f770-221">Per le descrizioni delle proprietà JSON supportate da SqlSink, vedere l'articolo relativo al [connettore del database SQL di Azure](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="3f770-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="3f770-222">Configurare le variabili globali</span><span class="sxs-lookup"><span data-stu-id="3f770-222">Set global variables</span></span>
<span data-ttu-id="3f770-223">In Azure PowerShell, eseguire hello seguenti comandi dopo la sostituzione di valori hello con valori personalizzati:</span><span class="sxs-lookup"><span data-stu-id="3f770-223">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f770-224">Per istruzioni su come ottenere i valori per ID client, segreto client, ID tenant e ID sottoscrizione, vedere la sezione [Prerequisiti](#prerequisites) .</span><span class="sxs-lookup"><span data-stu-id="3f770-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="3f770-225">Eseguire hello comando seguente dopo l'aggiornamento del nome hello di hello data factory in uso:</span><span class="sxs-lookup"><span data-stu-id="3f770-225">Run hello following command after updating hello name of hello data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="3f770-226">Eseguire l'autenticazione con AAD</span><span class="sxs-lookup"><span data-stu-id="3f770-226">Authenticate with AAD</span></span>
<span data-ttu-id="3f770-227">Comando che segue di esecuzione hello tooauthenticate con Azure Active Directory (AAD):</span><span class="sxs-lookup"><span data-stu-id="3f770-227">Run hello following command tooauthenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="3f770-228">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="3f770-228">Create data factory</span></span>
<span data-ttu-id="3f770-229">In questo passaggio si crea un'istanza di Azure Data Factory denominata **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="3f770-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="3f770-230">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="3f770-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="3f770-231">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="3f770-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="3f770-232">Ad esempio, un attività di copia toocopy da un'origine di destinazione tooa archivio dati.</span><span class="sxs-lookup"><span data-stu-id="3f770-232">For example, a Copy Activity toocopy data from a source tooa destination data store.</span></span> <span data-ttu-id="3f770-233">Un toorun attività Hive di HDInsight un tootransform script Hive dati di output tooproduct di dati di input.</span><span class="sxs-lookup"><span data-stu-id="3f770-233">A HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="3f770-234">Eseguire hello data factory di comandi toocreate hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="3f770-234">Run hello following commands toocreate hello data factory:</span></span> 

1. <span data-ttu-id="3f770-235">Assegnare toovariable comando hello denominato **cmd**.</span><span class="sxs-lookup"><span data-stu-id="3f770-235">Assign hello command toovariable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="3f770-236">Verificare che nome hello di hello data factory specificato (ADFCopyTutorialDF) corrispondenze hello nome specificato in hello **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="3f770-236">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="3f770-237">Eseguire il comando hello utilizzando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="3f770-237">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="3f770-238">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-238">View hello results.</span></span> <span data-ttu-id="3f770-239">Se hello data factory è stata creata correttamente, viene visualizzato hello JSON per data factory di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="3f770-239">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="3f770-240">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="3f770-240">Note hello following points:</span></span>

* <span data-ttu-id="3f770-241">nome Hello di hello Azure Data Factory deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="3f770-241">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="3f770-242">Se viene visualizzato l'errore hello nei risultati: **"ADFCopyTutorialDF" nome della Data factory non è disponibile**, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3f770-242">If you see hello error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do hello following steps:</span></span>  
  
  1. <span data-ttu-id="3f770-243">Modifica il nome hello (ad esempio, yournameADFCopyTutorialDF) in hello **datafactory.json** file.</span><span class="sxs-lookup"><span data-stu-id="3f770-243">Change hello name (for example, yournameADFCopyTutorialDF) in hello **datafactory.json** file.</span></span>
  2. <span data-ttu-id="3f770-244">Nel primo comando hello in hello **$cmd** variabile viene assegnato un valore, sostituire ADFCopyTutorialDF con nome hello ed eseguire il comando di hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-244">In hello first command where hello **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with hello new name and run hello command.</span></span> 
  3. <span data-ttu-id="3f770-245">Eseguire hello due comandi successivi tooinvoke hello API REST toocreate hello data factory e stampa hello risultati dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-245">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span> 
     
     <span data-ttu-id="3f770-246">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="3f770-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="3f770-247">le istanze di Data Factory toocreate, è necessario toobe un amministratore o un collaboratore di hello sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="3f770-247">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="3f770-248">nome Hello della hello data factory può essere registrato come un nome DNS in futuro hello e pertanto diventano visibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="3f770-248">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="3f770-249">Se viene visualizzato l'errore hello: "**questa sottoscrizione non è registrato toouse dello spazio dei nomi Microsoft. DataFactory**", effettuare una delle seguenti hello e riprovare:</span><span class="sxs-lookup"><span data-stu-id="3f770-249">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="3f770-250">In Azure PowerShell, eseguire hello seguenti provider di comandi tooregister hello Data Factory:</span><span class="sxs-lookup"><span data-stu-id="3f770-250">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="3f770-251">È possibile eseguire hello successivo comando tooconfirm tale hello Data Factory di provider è registrato.</span><span class="sxs-lookup"><span data-stu-id="3f770-251">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="3f770-252">Account di accesso tramite hello sottoscrizione di Azure in hello [portale di Azure](https://portal.azure.com) e passare a pannello di Data Factory tooa creare una data factory nel portale di Azure hello (o).</span><span class="sxs-lookup"><span data-stu-id="3f770-252">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="3f770-253">Questa azione registra automaticamente i provider di hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-253">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="3f770-254">Prima di creare una pipeline, è necessario toocreate alcune entità Data Factory prima.</span><span class="sxs-lookup"><span data-stu-id="3f770-254">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="3f770-255">Creare innanzitutto l'origine toolink servizi collegati e i dati di destinazione archivia dati tooyour archiviare.</span><span class="sxs-lookup"><span data-stu-id="3f770-255">You first create linked services toolink source and destination data stores tooyour data store.</span></span> <span data-ttu-id="3f770-256">Quindi, definire i set di dati di input e output toorepresent dati in archivi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="3f770-256">Then, define input and output datasets toorepresent data in linked data stores.</span></span> <span data-ttu-id="3f770-257">Infine, è possibile creare pipeline hello con un'attività che utilizza questi set di dati.</span><span class="sxs-lookup"><span data-stu-id="3f770-257">Finally, create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="3f770-258">Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="3f770-258">Create linked services</span></span>
<span data-ttu-id="3f770-259">Creare servizi collegati in un toolink factory dati i dati vengono archiviati e toohello data factory di servizi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="3f770-259">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="3f770-260">In questa esercitazione non si usano servizi di calcolo come Azure HDInsight o Azure Data Lake Analytics,</span><span class="sxs-lookup"><span data-stu-id="3f770-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="3f770-261">ma due archivi dati di tipo Archiviazione di Azure (origine) e database SQL di Azure (destinazione).</span><span class="sxs-lookup"><span data-stu-id="3f770-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="3f770-262">Si creano quindi due servizi collegati denominati AzureStorageLinkedService e AzureSqlLinkedService di tipo AzureStorage e AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="3f770-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="3f770-263">Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-263">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="3f770-264">Questo account di archiviazione è hello uno in cui è stato creato un contenitore e caricato dati hello come parte del [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="3f770-264">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="3f770-265">AzureSqlLinkedService collega il toohello data factory di Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="3f770-265">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="3f770-266">dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database.</span><span class="sxs-lookup"><span data-stu-id="3f770-266">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="3f770-267">Tabella emp hello è stato creato in questo database come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="3f770-267">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="3f770-268">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3f770-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="3f770-269">In questo passaggio si collega la data factory tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-269">In this step, you link your Azure storage account tooyour data factory.</span></span> <span data-ttu-id="3f770-270">Specificare il nome di hello e chiave dell'account di archiviazione di Azure in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="3f770-270">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="3f770-271">Vedere [servizio collegato di archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) per informazioni dettagliate su JSON proprietà utilizzate toodefine servizio collegato di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="3f770-272">Assegnare toovariable comando hello denominato **cmd**.</span><span class="sxs-lookup"><span data-stu-id="3f770-272">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="3f770-273">Eseguire il comando hello utilizzando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="3f770-273">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="3f770-274">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-274">View hello results.</span></span> <span data-ttu-id="3f770-275">Se collegato hello servizio è stato creato correttamente, hello JSON per il servizio collegato hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="3f770-275">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="3f770-276">Creare un servizio collegato di Azure SQL</span><span class="sxs-lookup"><span data-stu-id="3f770-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="3f770-277">In questo passaggio si collega il tooyour data factory di Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="3f770-277">In this step, you link your Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="3f770-278">Specificare nome del server SQL Azure hello, nome del database, nome utente e password dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="3f770-278">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="3f770-279">Vedere [servizio collegato SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine servizio collegato SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>

1. <span data-ttu-id="3f770-280">Assegnare toovariable comando hello denominato **cmd**.</span><span class="sxs-lookup"><span data-stu-id="3f770-280">Assign hello command toovariable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="3f770-281">Eseguire il comando hello utilizzando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="3f770-281">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="3f770-282">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-282">View hello results.</span></span> <span data-ttu-id="3f770-283">Se collegato hello servizio è stato creato correttamente, hello JSON per il servizio collegato hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="3f770-283">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="3f770-284">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="3f770-284">Create datasets</span></span>
<span data-ttu-id="3f770-285">Nel passaggio precedente hello, servizi collegati toolink è creato l'account di archiviazione di Azure e la data factory di Azure SQL database tooyour.</span><span class="sxs-lookup"><span data-stu-id="3f770-285">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="3f770-286">In questo passaggio si definiscono due set di dati denominati AzureBlobInput e AzureSqlOutput che rappresentano l'input e output i dati archiviati in archivi dati hello a cui fa riferimento AzureStorageLinkedService e AzureSqlLinkedService rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="3f770-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="3f770-287">il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-287">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="3f770-288">E, set di dati blob di input hello (AzureBlobInput) specifica il contenitore di hello e la cartella di hello che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-288">And, hello input blob dataset (AzureBlobInput) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="3f770-289">Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3f770-289">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="3f770-290">E, di output di hello set di dati nella tabella SQL (OututDataset) specifica la tabella hello in hello di toowhich hello database vengono copiati dati dall'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-290">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="3f770-291">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="3f770-291">Create input dataset</span></span>
<span data-ttu-id="3f770-292">In questo passaggio, creare un set di dati denominato AzureBlobInput che punta il file di blob tooa (emp.txt) nella cartella radice hello di un contenitore di blob (adftutorial) in hello rappresentato da hello AzureStorageLinkedService collegato servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-292">In this step, you create a dataset named AzureBlobInput that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="3f770-293">Se non specifica un valore per il nome file hello (o ignorarlo), i dati da tutti i BLOB nella cartella input hello sono copiati toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="3f770-293">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="3f770-294">In questa esercitazione, si specifica un valore per il nome file hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-294">In this tutorial, you specify a value for hello fileName.</span></span> 

1. <span data-ttu-id="3f770-295">Assegnare toovariable comando hello denominato **cmd**.</span><span class="sxs-lookup"><span data-stu-id="3f770-295">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="3f770-296">Eseguire il comando hello utilizzando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="3f770-296">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="3f770-297">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-297">View hello results.</span></span> <span data-ttu-id="3f770-298">Se il set di dati hello è stato creato correttamente, viene visualizzato hello JSON per set di dati di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="3f770-298">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="3f770-299">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="3f770-299">Create output dataset</span></span>
<span data-ttu-id="3f770-300">servizio collegato Database di SQL Azure Hello specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3f770-300">hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="3f770-301">Hello output SQL tabella dataset (OututDataset) create in questo passaggio specifica tabella hello nei dati di hello database toowhich hello dall'archiviazione blob hello viene copiata.</span><span class="sxs-lookup"><span data-stu-id="3f770-301">hello output SQL table dataset (OututDataset) you create in this step specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

1. <span data-ttu-id="3f770-302">Assegnare toovariable comando hello denominato **cmd**.</span><span class="sxs-lookup"><span data-stu-id="3f770-302">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="3f770-303">Eseguire il comando hello utilizzando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="3f770-303">Run hello command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="3f770-304">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-304">View hello results.</span></span> <span data-ttu-id="3f770-305">Se il set di dati hello è stato creato correttamente, viene visualizzato hello JSON per set di dati di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="3f770-305">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="3f770-306">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="3f770-306">Create pipeline</span></span>
<span data-ttu-id="3f770-307">In questo passaggio viene creata una pipeline con un'**attività di copia** che usa **AzureBlobInput** come input e **AzureSqlOutput** come output.</span><span class="sxs-lookup"><span data-stu-id="3f770-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="3f770-308">Set di dati di output è attualmente, quali unità hello pianificazione.</span><span class="sxs-lookup"><span data-stu-id="3f770-308">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="3f770-309">In questa esercitazione, set di dati di output è tooproduce configurato una sezione di una volta all'ora.</span><span class="sxs-lookup"><span data-stu-id="3f770-309">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="3f770-310">pipeline Hello dispone ora di inizio e ora di fine di un giorno separato, ovvero 24 ore.</span><span class="sxs-lookup"><span data-stu-id="3f770-310">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="3f770-311">Pertanto, 24 sezioni del set di dati di output vengono generate dalla pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-311">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="3f770-312">Assegnare toovariable comando hello denominato **cmd**.</span><span class="sxs-lookup"><span data-stu-id="3f770-312">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="3f770-313">Eseguire il comando hello utilizzando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="3f770-313">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="3f770-314">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-314">View hello results.</span></span> <span data-ttu-id="3f770-315">Se il set di dati hello è stato creato correttamente, viene visualizzato hello JSON per set di dati di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="3f770-315">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="3f770-316">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="3f770-316">**Congratulations!**</span></span> <span data-ttu-id="3f770-317">Una data factory di Azure, è stato creato con una pipeline che copia i dati dal database SQL tooAzure di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage tooAzure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="3f770-318">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="3f770-318">Monitor pipeline</span></span>
<span data-ttu-id="3f770-319">In questo passaggio è utilizzare le sezioni di toomonitor API REST di Data Factory viene generate dalla pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-319">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="3f770-320">Assicurarsi che hello inizio e fine tempi hello specificato nel seguente comando inizio hello corrispondenza e di fine della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-320">Make sure that hello start and end times specified in hello following command match hello start and end times of hello pipeline.</span></span> 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

<span data-ttu-id="3f770-321">Eseguire Invoke-Command hello e hello successivo finché non viene visualizzata una sezione in **pronto** stato o **Failed** stato.</span><span class="sxs-lookup"><span data-stu-id="3f770-321">Run hello Invoke-Command and hello next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="3f770-322">Quando la sezione hello è nello stato pronto, controllare hello **emp** tabella nel database SQL di Azure per i dati di output di hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-322">When hello slice is in Ready state, check hello **emp** table in your Azure SQL database for hello output data.</span></span> 

<span data-ttu-id="3f770-323">Per ogni intervallo di due righe di dati dal file di origine hello sono tabella emp toohello copiati nel database di SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-323">For each slice, two rows of data from hello source file are copied toohello emp table in hello Azure SQL database.</span></span> <span data-ttu-id="3f770-324">Pertanto, vedrai 24 nuovi record nella tabella emp hello quando vengono elaborate tutte le sezioni di hello (nello stato Ready).</span><span class="sxs-lookup"><span data-stu-id="3f770-324">Therefore, you see 24 new records in hello emp table when all hello slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="3f770-325">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="3f770-325">Summary</span></span>
<span data-ttu-id="3f770-326">In questa esercitazione è stato utilizzato API REST toocreate un Azure data factory toocopy di dati da un database di SQL Azure tooan blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f770-326">In this tutorial, you used REST API toocreate an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="3f770-327">Ecco i passaggi di alto livello hello effettuati in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="3f770-327">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="3f770-328">Creare un'istanza di Azure **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="3f770-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="3f770-329">Creare **servizi collegati**:</span><span class="sxs-lookup"><span data-stu-id="3f770-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="3f770-330">Una risorsa di archiviazione di Azure collegati toolink service account di archiviazione di Azure che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="3f770-330">An Azure Storage linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="3f770-331">SQL Azure collegato toolink servizio database SQL di Azure che contiene i dati di output di hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-331">An Azure SQL linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="3f770-332">Creare **set di dati**che descrivono dati di input e dati di output per le pipeline.</span><span class="sxs-lookup"><span data-stu-id="3f770-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="3f770-333">Creare una **pipeline** con un'attività di copia con BlobSource come origine e SqlSink come sink.</span><span class="sxs-lookup"><span data-stu-id="3f770-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3f770-334">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3f770-334">Next steps</span></span>
<span data-ttu-id="3f770-335">In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="3f770-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="3f770-336">Hello nella tabella seguente fornisce un elenco di archivi di dati supportato come origini e destinazioni da attività di copia hello:</span><span class="sxs-lookup"><span data-stu-id="3f770-336">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="3f770-337">toolearn su come archiviano dati toocopy da e verso un tipo di dati, fare clic su collegamento hello per hello archivio di dati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="3f770-337">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
