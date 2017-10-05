---
title: 'Esercitazione: Usare l''API REST per creare una pipeline di Azure Data Factory | Microsoft Docs'
description: "In questa esercitazione si usa l'API REST per creare una pipeline di Azure Data Factory con un'attività di copia per copiare i dati da un archivio BLOB di Azure a un database SQL di Azure."
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
ms.openlocfilehash: 6663774497aa18aa98e7e8c5aed6183c599b2172
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-use-rest-api-to-create-an-azure-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="6f0ea-103">Esercitazione: Usare l'API REST per creare una pipeline di Azure Data Factory per copiare dati</span><span class="sxs-lookup"><span data-stu-id="6f0ea-103">Tutorial: Use REST API to create an Azure Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f0ea-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6f0ea-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="6f0ea-105">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="6f0ea-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="6f0ea-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6f0ea-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="6f0ea-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f0ea-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="6f0ea-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f0ea-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="6f0ea-109">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6f0ea-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="6f0ea-110">API REST</span><span class="sxs-lookup"><span data-stu-id="6f0ea-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="6f0ea-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="6f0ea-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="6f0ea-112">Questo articolo illustra l'uso dell'API REST per creare una data factory con una pipeline che copia i dati da un archivio BLOB di Azure a un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-112">In this article, you learn how to use REST API to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="6f0ea-113">Se non si ha familiarità con Azure Data Factory, prima di eseguire questa esercitazione vedere l'articolo [Introduzione ad Azure Data Factory](data-factory-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="6f0ea-114">In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="6f0ea-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="6f0ea-115">che copia i dati da un archivio dati supportato a un archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="6f0ea-116">Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="6f0ea-117">e si basa su un servizio disponibile a livello globale che può copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="6f0ea-118">Per altre informazioni sull'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="6f0ea-119">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="6f0ea-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="6f0ea-120">ed è possibile concatenarne due, ovvero eseguire un'attività dopo l'altra, impostando il set di dati di output di un'attività come set di dati di input dell'altra.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="6f0ea-121">Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="6f0ea-122">Questo articolo non illustra tutte le API REST di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-122">This article does not cover all the Data Factory REST API.</span></span> <span data-ttu-id="6f0ea-123">Per la documentazione completa sui cmdlet di Data Factory, vedere [Informazioni di riferimento sull'API REST di Data Factory](/rest/api/datafactory/) .</span><span class="sxs-lookup"><span data-stu-id="6f0ea-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="6f0ea-124">La pipeline di dati in questa esercitazione copia i dati da un archivio dati di origine a un archivio dati di destinazione.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-124">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="6f0ea-125">Per un'esercitazione su come trasformare i dati usando Azure Data Factory, vedere [Esercitazione: Creare una pipeline per trasformare i dati usando un cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-125">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f0ea-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6f0ea-126">Prerequisites</span></span>
* <span data-ttu-id="6f0ea-127">Vedere [Panoramica dell'esercitazione](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ed eseguire i passaggi relativi ai **prerequisiti** .</span><span class="sxs-lookup"><span data-stu-id="6f0ea-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="6f0ea-128">Installare [Curl](https://curl.haxx.se/dlwiz/) nel computer.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="6f0ea-129">Lo strumento Curl viene usato insieme ai comandi REST per creare una data factory.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-129">You use the Curl tool with REST commands to create a data factory.</span></span> 
* <span data-ttu-id="6f0ea-130">Seguire le istruzioni disponibili in [questo articolo](../azure-resource-manager/resource-group-create-service-principal-portal.md) per:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="6f0ea-131">Creare un'applicazione Web denominata **ADFCopyTutorialApp** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="6f0ea-132">Ottenere i valori per l'**ID client** e la **chiave privata**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="6f0ea-133">Ottenere l' **ID tenant**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="6f0ea-134">Assegnare l'applicazione **ADFCopyTutorialApp** al ruolo **Collaboratore Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-134">Assign the **ADFCopyTutorialApp** application to the **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="6f0ea-135">Installare [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="6f0ea-136">Avviare **PowerShell** e seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-136">Launch **PowerShell** and do the following steps.</span></span> <span data-ttu-id="6f0ea-137">Mantenere aperto Azure PowerShell fino alla fine dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-137">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="6f0ea-138">Se si chiude e si riapre, sarà necessario eseguire di nuovo questi comandi.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-138">If you close and reopen, you need to run the commands again.</span></span>
  
  1. <span data-ttu-id="6f0ea-139">Eseguire questo comando e immettere il nome utente e la password usati per accedere al portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-139">Run the following command and enter the user name and password that you use to sign in to the Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="6f0ea-140">Eseguire questo comando per visualizzare tutte le sottoscrizioni per l'account:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-140">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="6f0ea-141">Eseguire il comando seguente per selezionare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-141">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="6f0ea-142">Sostituire **&lt;NameOfAzureSubscription**&gt; con il nome della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-142">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="6f0ea-143">Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo questo comando in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="6f0ea-144">Se il gruppo di risorse esiste già, specificare se deve essere aggiornato (Y) o mantenuto invariato (N).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-144">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="6f0ea-145">Per alcuni dei passaggi in questa esercitazione si presuppone l'uso del gruppo di risorse denominato ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-145">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="6f0ea-146">Se si usa un gruppo di risorse diverso, è necessario usare il nome del gruppo di risorse invece di ADFTutorialResourceGroup in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-146">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="6f0ea-147">Creare le definizioni JSON</span><span class="sxs-lookup"><span data-stu-id="6f0ea-147">Create JSON definitions</span></span>
<span data-ttu-id="6f0ea-148">Creare i file JSON seguenti nella cartella che include curl.exe.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-148">Create following JSON files in the folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="6f0ea-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="6f0ea-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6f0ea-150">Il nome deve essere univoco a livello globale, quindi è consigliabile aggiungere un prefisso/suffisso ad ADFCopyTutorialDF per renderlo univoco.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-150">Name must be globally unique, so you may want to prefix/suffix ADFCopyTutorialDF to make it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="6f0ea-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="6f0ea-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6f0ea-152">Sostituire **accountname** e **accountkey** con il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="6f0ea-153">Per informazioni su come ottenere la chiave di accesso alle risorse di archiviazione, vedere la sezione [Visualizzare, copiare e rigenerare le chiavi di accesso nelle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-153">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

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

<span data-ttu-id="6f0ea-154">Per informazioni dettagliate sulle proprietà JSON, vedere [Servizio collegato Archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="6f0ea-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="6f0ea-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6f0ea-156">Sostituire **servername**, **databasename**, **username** e **password** con il nome del server di Azure SQL, il nome del database SQL, l'account utente e la password per l'account.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for the account.</span></span>  
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

<span data-ttu-id="6f0ea-157">Per informazioni dettagliate sulle proprietà JSON, vedere la sezione relativa al [servizio collegato SQL di Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="6f0ea-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="6f0ea-158">inputdataset.json</span></span>

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

<span data-ttu-id="6f0ea-159">La tabella seguente fornisce le descrizioni delle proprietà JSON usate nel frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-159">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="6f0ea-160">Proprietà</span><span class="sxs-lookup"><span data-stu-id="6f0ea-160">Property</span></span> | <span data-ttu-id="6f0ea-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6f0ea-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6f0ea-162">type</span><span class="sxs-lookup"><span data-stu-id="6f0ea-162">type</span></span> | <span data-ttu-id="6f0ea-163">La proprietà type è impostata su **AzureBlob** perché i dati risiedono in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-163">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="6f0ea-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="6f0ea-164">linkedServiceName</span></span> | <span data-ttu-id="6f0ea-165">Fa riferimento all'oggetto **AzureStorageLinkedService** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-165">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="6f0ea-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="6f0ea-166">folderPath</span></span> | <span data-ttu-id="6f0ea-167">Specifica il **contenitore** BLOB e la **cartella** che contiene i BLOB di input.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-167">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="6f0ea-168">In questa esercitazione adftutorial è il contenitore BLOB e la cartella è la cartella radice.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-168">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
| <span data-ttu-id="6f0ea-169">fileName</span><span class="sxs-lookup"><span data-stu-id="6f0ea-169">fileName</span></span> | <span data-ttu-id="6f0ea-170">Questa proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-170">This property is optional.</span></span> <span data-ttu-id="6f0ea-171">Se si omette questa proprietà, vengono selezionati tutti i file da folderPath.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-171">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="6f0ea-172">In questa esercitazione come fileName si specifica **emp.txt** e viene quindi selezionato per l'elaborazione solo tale file.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-172">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="6f0ea-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="6f0ea-173">format -> type</span></span> |<span data-ttu-id="6f0ea-174">Il file di input è in formato testo, quindi viene usato **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-174">The input file is in the text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="6f0ea-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="6f0ea-175">columnDelimiter</span></span> | <span data-ttu-id="6f0ea-176">Le colonne nel file di input sono delimitate da **virgola (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-176">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="6f0ea-177">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="6f0ea-177">frequency/interval</span></span> | <span data-ttu-id="6f0ea-178">La frequenza è impostata su **Hour** e l'intervallo è impostato su **1**, quindi le sezioni di input sono disponibili con cadenza **oraria**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-178">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="6f0ea-179">In altre parole, il servizio Data Factory cerca i dati di input ogni ora nella cartella radice del contenitore BLOB specificato (**adftutorial**).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-179">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="6f0ea-180">Cerca i dati compresi tra l'ora di inizio e di fine della pipeline e non prima o dopo queste ore.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-180">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="6f0ea-181">external</span><span class="sxs-lookup"><span data-stu-id="6f0ea-181">external</span></span> | <span data-ttu-id="6f0ea-182">Questa proprietà è impostata su **true** se i dati non vengono generati da questa pipeline.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-182">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="6f0ea-183">I dati di input in questa esercitazione sono nel file emp.txt, che non viene generato da questa pipeline, quindi questa proprietà viene impostata su true.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-183">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

<span data-ttu-id="6f0ea-184">Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="6f0ea-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="6f0ea-185">outputdataset.json</span></span>

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
<span data-ttu-id="6f0ea-186">La tabella seguente fornisce le descrizioni delle proprietà JSON usate nel frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-186">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="6f0ea-187">Proprietà</span><span class="sxs-lookup"><span data-stu-id="6f0ea-187">Property</span></span> | <span data-ttu-id="6f0ea-188">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6f0ea-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6f0ea-189">type</span><span class="sxs-lookup"><span data-stu-id="6f0ea-189">type</span></span> | <span data-ttu-id="6f0ea-190">La proprietà type viene impostata su **AzureSqlTable** perché i dati vengono copiati in una tabella in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-190">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
| <span data-ttu-id="6f0ea-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="6f0ea-191">linkedServiceName</span></span> | <span data-ttu-id="6f0ea-192">Fa riferimento all'oggetto **AzureSqlLinkedService** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-192">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="6f0ea-193">tableName</span><span class="sxs-lookup"><span data-stu-id="6f0ea-193">tableName</span></span> | <span data-ttu-id="6f0ea-194">Specifica la **tabella** in cui i dati vengono copiati.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-194">Specified the **table** to which the data is copied.</span></span> | 
| <span data-ttu-id="6f0ea-195">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="6f0ea-195">frequency/interval</span></span> | <span data-ttu-id="6f0ea-196">La frequenza viene impostata su **Hour** e l'intervallo è **1**, quindi le sezioni di output vengono generate **ogni ora** tra l'ora di inizio e di fine della pipeline e non prima o dopo queste ore.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-196">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="6f0ea-197">La tabella emp del database include tre colonne: **ID**, **FirstName** e **LastName**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-197">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="6f0ea-198">ID è una colonna Identity, quindi in questo caso è necessario specificare solo **FirstName** e **LastName**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-198">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="6f0ea-199">Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore SQL di Azure](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="6f0ea-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="6f0ea-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data to Azure SQL database",
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

<span data-ttu-id="6f0ea-201">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-201">Note the following points:</span></span>

- <span data-ttu-id="6f0ea-202">Nella sezione delle attività esiste una sola attività con l'oggetto **type** impostato su **Copy**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-202">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="6f0ea-203">Per altre informazioni sull'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-203">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="6f0ea-204">Nelle soluzioni Data Factory è anche possibile usare le [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="6f0ea-205">L'input per l'attività è impostato su **AzureBlobInput** e l'output per l'attività è impostato su **AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-205">Input for the activity is set to **AzureBlobInput** and output for the activity is set to **AzureSqlOutput**.</span></span> 
- <span data-ttu-id="6f0ea-206">Nella sezione **typeProperties** vengono specificati **BlobSource** come tipo di origine e **SqlSink** come tipo di sink.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-206">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="6f0ea-207">Per un elenco completo degli archivi dati supportati dall'attività di copia come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-207">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="6f0ea-208">Per informazioni su come usare uno specifico archivio dati supportato come origine/sink, fare clic sul collegamento nella tabella.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-208">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
 
<span data-ttu-id="6f0ea-209">Sostituire il valore della proprietà **start** con il giorno corrente e il valore di **end** con il giorno successivo.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-209">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="6f0ea-210">È possibile specificare solo la parte relativa alla data e ignorare la parte relativa all'ora,</span><span class="sxs-lookup"><span data-stu-id="6f0ea-210">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="6f0ea-211">ad esempio "2017-02-03", che equivale a "2017-02-03T00:00:00Z".</span><span class="sxs-lookup"><span data-stu-id="6f0ea-211">For example, "2017-02-03", which is equivalent to "2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="6f0ea-212">Per la data e ora di inizio è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601),</span><span class="sxs-lookup"><span data-stu-id="6f0ea-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="6f0ea-213">ad esempio 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="6f0ea-214">Il valore di **end** è facoltativo, ma in questa esercitazione viene usato.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-214">The **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="6f0ea-215">Se non si specifica alcun valore per la proprietà **end**, il valore verrà calcolato come "**start + 48 hours**".</span><span class="sxs-lookup"><span data-stu-id="6f0ea-215">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="6f0ea-216">Per eseguire la pipeline illimitatamente, specificare **9999-09-09** come valore per la proprietà **end**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-216">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
 
<span data-ttu-id="6f0ea-217">Nell'esempio precedente sono visualizzate 24 sezioni di dati, perché viene generata una sezione di dati ogni ora.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-217">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="6f0ea-218">Per le descrizioni delle proprietà JSON nella definizione di una pipeline, vedere l'articolo su come [creare pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6f0ea-219">Per le descrizioni delle proprietà JSON nella definizione di un'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="6f0ea-220">Per le descrizioni delle proprietà JSON supportate da BlobSource, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="6f0ea-221">Per le descrizioni delle proprietà JSON supportate da SqlSink, vedere l'articolo relativo al [connettore del database SQL di Azure](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="6f0ea-222">Configurare le variabili globali</span><span class="sxs-lookup"><span data-stu-id="6f0ea-222">Set global variables</span></span>
<span data-ttu-id="6f0ea-223">In Azure PowerShell eseguire i comandi seguenti dopo avere sostituito i valori con quelli personalizzati:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-223">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f0ea-224">Per istruzioni su come ottenere i valori per ID client, segreto client, ID tenant e ID sottoscrizione, vedere la sezione [Prerequisiti](#prerequisites) .</span><span class="sxs-lookup"><span data-stu-id="6f0ea-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="6f0ea-225">Dopo aver aggiornato il nome della data factory usata, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-225">Run the following command after updating the name of the data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="6f0ea-226">Eseguire l'autenticazione con AAD</span><span class="sxs-lookup"><span data-stu-id="6f0ea-226">Authenticate with AAD</span></span>
<span data-ttu-id="6f0ea-227">Eseguire questo comando per l'autenticazione con Azure Active Directory (AAD):</span><span class="sxs-lookup"><span data-stu-id="6f0ea-227">Run the following command to authenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="6f0ea-228">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="6f0ea-228">Create data factory</span></span>
<span data-ttu-id="6f0ea-229">In questo passaggio si crea un'istanza di Azure Data Factory denominata **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="6f0ea-230">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="6f0ea-231">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="6f0ea-232">Ad esempio, un'attività di copia per copiare dati da un'origine a un archivio dati di destinazione.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-232">For example, a Copy Activity to copy data from a source to a destination data store.</span></span> <span data-ttu-id="6f0ea-233">Un'attività Hive HDInsight per eseguire uno script Hive e trasformare i dati di input in dati di output di prodotto.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-233">A HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="6f0ea-234">Eseguire i comandi seguenti per creare la data factory:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-234">Run the following commands to create the data factory:</span></span> 

1. <span data-ttu-id="6f0ea-235">Assegnare il comando alla variabile denominata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-235">Assign the command to variable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="6f0ea-236">Verificare che il nome della data factory specificato qui (ADFCopyTutorialDF) corrisponda al nome specificato in **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-236">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="6f0ea-237">Eseguire il comando usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-237">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="6f0ea-238">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-238">View the results.</span></span> <span data-ttu-id="6f0ea-239">Se la data factory è stata creata correttamente, in **results** viene visualizzato il codice JSON per la data factory. In caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-239">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="6f0ea-240">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-240">Note the following points:</span></span>

* <span data-ttu-id="6f0ea-241">È necessario specificare un nome univoco globale per la Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-241">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="6f0ea-242">Se nei risultati viene visualizzato l'errore **Il nome "ADFCopyTutorialDF" per la data factory non è disponibile**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-242">If you see the error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do the following steps:</span></span>  
  
  1. <span data-ttu-id="6f0ea-243">Cambiare il nome, ad esempio nomeutenteADFCopyTutorialDF, nel file **datafactory.json** .</span><span class="sxs-lookup"><span data-stu-id="6f0ea-243">Change the name (for example, yournameADFCopyTutorialDF) in the **datafactory.json** file.</span></span>
  2. <span data-ttu-id="6f0ea-244">Nel primo comando in cui viene assegnato un valore alla variabile **$cmd** sostituire ADFCopyTutorialDF con il nuovo nome ed eseguire il comando.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-244">In the first command where the **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with the new name and run the command.</span></span> 
  3. <span data-ttu-id="6f0ea-245">Eseguire i due comandi seguenti per richiamare l'API REST per creare la data factory e stampare i risultati dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-245">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span> 
     
     <span data-ttu-id="6f0ea-246">Per informazioni sulle regole di denominazione per gli elementi di Data Factory, vedere l'argomento [Azure Data Factory - Regole di denominazione](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="6f0ea-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="6f0ea-247">Per creare istanze di data factory, è necessario essere un collaboratore/amministratore della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-247">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="6f0ea-248">Il nome della data factory può essere registrato come nome DNS in futuro e quindi divenire visibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-248">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="6f0ea-249">Se viene visualizzato l'errore "**La sottoscrizione non è registrata per l'uso dello spazio dei nomi Microsoft.DataFactory**", eseguire una di queste operazioni e provare a ripetere la pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-249">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="6f0ea-250">In Azure PowerShell eseguire questo comando per registrare il provider di Data Factory:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-250">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="6f0ea-251">È possibile eseguire questo comando per verificare che il provider di Data Factory sia registrato.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-251">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="6f0ea-252">Accedere usando la sottoscrizione di Azure nel [portale di Azure](https://portal.azure.com) e passare al pannello Data Factory oppure creare un'istanza di Data Factory nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-252">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="6f0ea-253">Questa azione registra automaticamente il provider.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-253">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="6f0ea-254">Prima di creare una pipeline è necessario creare alcune entità di Data factory.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-254">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="6f0ea-255">Prima di tutto, creare i servizi collegati per collegare gli archivi dati di origine e di destinazione al proprio archivio dati.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-255">You first create linked services to link source and destination data stores to your data store.</span></span> <span data-ttu-id="6f0ea-256">Quindi, definire i set di dati di input e di output per rappresentare i dati in archivi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-256">Then, define input and output datasets to represent data in linked data stores.</span></span> <span data-ttu-id="6f0ea-257">Infine, creare la pipeline con un'attività che usa questi set di dati.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-257">Finally, create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="6f0ea-258">Creazione di servizi collegati</span><span class="sxs-lookup"><span data-stu-id="6f0ea-258">Create linked services</span></span>
<span data-ttu-id="6f0ea-259">Si creano servizi collegati in una data factory per collegare gli archivi dati e i servizi di calcolo alla data factory.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-259">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="6f0ea-260">In questa esercitazione non si usano servizi di calcolo come Azure HDInsight o Azure Data Lake Analytics,</span><span class="sxs-lookup"><span data-stu-id="6f0ea-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="6f0ea-261">ma due archivi dati di tipo Archiviazione di Azure (origine) e database SQL di Azure (destinazione).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="6f0ea-262">Si creano quindi due servizi collegati denominati AzureStorageLinkedService e AzureSqlLinkedService di tipo AzureStorage e AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="6f0ea-263">AzureStorageLinkedService collega l'account di archiviazione di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-263">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="6f0ea-264">L'account di archiviazione è quello in cui, come parte dei [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), è stato creato un contenitore e sono stati caricati i dati.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-264">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="6f0ea-265">AzureSqlLinkedService collega il database SQL di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-265">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="6f0ea-266">I dati copiati dall'archivio BLOB vengono archiviati in questo database.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-266">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="6f0ea-267">Come parte dei [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) è stata creata la tabella emp in questo database.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-267">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="6f0ea-268">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6f0ea-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="6f0ea-269">In questo passaggio l'account di archiviazione di Azure viene collegato alla data factory.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-269">In this step, you link your Azure storage account to your data factory.</span></span> <span data-ttu-id="6f0ea-270">In questa sezione si specificano il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-270">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="6f0ea-271">Per informazioni dettagliate sulle proprietà JSON usate per definire un servizio collegato di Archiviazione di Azure, vedere [Servizio collegato Archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="6f0ea-272">Assegnare il comando alla variabile denominata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-272">Assign the command to variable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="6f0ea-273">Eseguire il comando usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-273">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="6f0ea-274">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-274">View the results.</span></span> <span data-ttu-id="6f0ea-275">Se il servizio collegato è stato creato correttamente, in **results** viene visualizzato il codice JSON per il servizio collegato. In caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-275">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="6f0ea-276">Creare un servizio collegato di Azure SQL</span><span class="sxs-lookup"><span data-stu-id="6f0ea-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="6f0ea-277">In questo passaggio il database SQL di Azure viene collegato alla data factory.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-277">In this step, you link your Azure SQL database to your data factory.</span></span> <span data-ttu-id="6f0ea-278">In questa sezione si specificano il nome del server di Azure SQL, il nome del database, il nome utente e la password utente.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-278">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="6f0ea-279">Per informazioni dettagliate sulle proprietà JSON usate per definire un servizio collegato di Azure SQL, vedere [Servizio collegato Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6f0ea-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>

1. <span data-ttu-id="6f0ea-280">Assegnare il comando alla variabile denominata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-280">Assign the command to variable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="6f0ea-281">Eseguire il comando usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-281">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="6f0ea-282">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-282">View the results.</span></span> <span data-ttu-id="6f0ea-283">Se il servizio collegato è stato creato correttamente, in **results** viene visualizzato il codice JSON per il servizio collegato. In caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-283">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="6f0ea-284">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="6f0ea-284">Create datasets</span></span>
<span data-ttu-id="6f0ea-285">Nel passaggio precedente sono stati creati servizi collegati per collegare l'account di archiviazione di Azure e un database SQL di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-285">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="6f0ea-286">In questo passaggio vengono definiti due set di dati denominati AzureBlobInput e AzureSqlOutput, che rappresentano i dati di input e di output memorizzati negli archivi dati a cui fanno riferimento rispettivamente AzureStorageLinkedService e AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="6f0ea-287">Il servizio collegato Archiviazione di Azure specifica la stringa di connessione usata dal servizio Data Factory in fase di esecuzione per connettersi all'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-287">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="6f0ea-288">Il set di dati del BLOB di input (AzureBlobInput) specifica il contenitore e la cartella che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-288">And, the input blob dataset (AzureBlobInput) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="6f0ea-289">Analogamente, il servizio collegato per il database SQL di Azure specifica la stringa di connessione usata dal servizio Data Factory in fase di esecuzione per connettersi al database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="6f0ea-289">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="6f0ea-290">e il set di dati della tabella SQL di output (OututDataset) specifica la tabella del database in cui vengono copiati i dati dell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-290">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="6f0ea-291">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="6f0ea-291">Create input dataset</span></span>
<span data-ttu-id="6f0ea-292">In questo passaggio viene creato un set di dati denominato AzureBlobInput che punta a un file BLOB (emp.txt) nella cartella radice di un contenitore BLOB (adftutorial) nella risorsa di archiviazione di Azure rappresentata dal servizio collegato AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-292">In this step, you create a dataset named AzureBlobInput that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="6f0ea-293">Se non si specifica un valore per fileName (o lo si ignora), i dati di tutti i BLOB della cartella di input vengono copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-293">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="6f0ea-294">In questa esercitazione si specifica un valore per fileName.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-294">In this tutorial, you specify a value for the fileName.</span></span> 

1. <span data-ttu-id="6f0ea-295">Assegnare il comando alla variabile denominata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-295">Assign the command to variable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="6f0ea-296">Eseguire il comando usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-296">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="6f0ea-297">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-297">View the results.</span></span> <span data-ttu-id="6f0ea-298">Se il set di dati è stato creato correttamente, in **results** viene visualizzato il codice JSON per il set di dati. In caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-298">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="6f0ea-299">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="6f0ea-299">Create output dataset</span></span>
<span data-ttu-id="6f0ea-300">Il servizio collegato per il database SQL di Azure specifica la stringa di connessione usata dal servizio Data Factory in fase di esecuzione per connettersi al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-300">The Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="6f0ea-301">Il set di dati della tabella SQL di output (OututDataset) creato in questo passaggio specifica la tabella del database in cui vengono copiati i dati dell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-301">The output SQL table dataset (OututDataset) you create in this step specifies the table in the database to which the data from the blob storage is copied.</span></span>

1. <span data-ttu-id="6f0ea-302">Assegnare il comando alla variabile denominata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-302">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="6f0ea-303">Eseguire il comando usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-303">Run the command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="6f0ea-304">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-304">View the results.</span></span> <span data-ttu-id="6f0ea-305">Se il set di dati è stato creato correttamente, in **results** viene visualizzato il codice JSON per il set di dati. In caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-305">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="6f0ea-306">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="6f0ea-306">Create pipeline</span></span>
<span data-ttu-id="6f0ea-307">In questo passaggio viene creata una pipeline con un'**attività di copia** che usa **AzureBlobInput** come input e **AzureSqlOutput** come output.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="6f0ea-308">Attualmente, è il set di dati di output a determinare la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-308">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="6f0ea-309">In questa esercitazione il set di dati di output viene configurato per generare una sezione una volta ogni ora.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-309">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="6f0ea-310">La pipeline ha un'ora di inizio e un'ora di fine intervallate da un giorno, ovvero 24 ore.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-310">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="6f0ea-311">Vengono quindi generate dalla pipeline 24 sezioni di set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-311">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="6f0ea-312">Assegnare il comando alla variabile denominata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-312">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="6f0ea-313">Eseguire il comando usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-313">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="6f0ea-314">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-314">View the results.</span></span> <span data-ttu-id="6f0ea-315">Se il set di dati è stato creato correttamente, in **results** viene visualizzato il codice JSON per il set di dati. In caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-315">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="6f0ea-316">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="6f0ea-316">**Congratulations!**</span></span> <span data-ttu-id="6f0ea-317">È stata creata una data factory di Azure con una pipeline che copia dati da un archivio BLOB di Azure al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage to Azure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="6f0ea-318">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="6f0ea-318">Monitor pipeline</span></span>
<span data-ttu-id="6f0ea-319">In questo passaggio viene usata l'API REST di Azure Data Factory per monitorare le sezioni prodotte dalla pipeline.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-319">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="6f0ea-320">Assicurarsi che l'ora di inizio e l'ora di fine specificate nel comando seguente corrispondano a quelle della pipeline.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-320">Make sure that the start and end times specified in the following command match the start and end times of the pipeline.</span></span> 

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

<span data-ttu-id="6f0ea-321">Eseguire Invoke-Command e il comando successivo fino a quando lo stato di una sezione non sarà **Pronto** o **Non riuscito**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-321">Run the Invoke-Command and the next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="6f0ea-322">Quando lo stato della sezione è Pronta, cercare dati di output nella tabella **emp** del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-322">When the slice is in Ready state, check the **emp** table in your Azure SQL database for the output data.</span></span> 

<span data-ttu-id="6f0ea-323">Per ogni sezione vengono copiate due righe di dati dal file di origine nella tabella emp del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-323">For each slice, two rows of data from the source file are copied to the emp table in the Azure SQL database.</span></span> <span data-ttu-id="6f0ea-324">Nella tabella emp vengono quindi visualizzati 24 nuovi record quando tutte le sezioni sono state elaborate correttamente e hanno stato Pronta.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-324">Therefore, you see 24 new records in the emp table when all the slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="6f0ea-325">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="6f0ea-325">Summary</span></span>
<span data-ttu-id="6f0ea-326">In questa esercitazione è stata usata l'API REST per creare una data factory di Azure per copiare dati da un BLOB di Azure a un database SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-326">In this tutorial, you used REST API to create an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="6f0ea-327">Ecco i passaggi generali eseguiti in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-327">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="6f0ea-328">Creare un'istanza di Azure **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="6f0ea-329">Creare **servizi collegati**:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="6f0ea-330">Un servizio collegato di Archiviazione di Azure per collegare l'account di archiviazione di Azure che include i dati di input.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-330">An Azure Storage linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="6f0ea-331">Un servizio collegato di Azure SQL per collegare il database SQL di Azure che contiene i dati di output.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-331">An Azure SQL linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="6f0ea-332">Creare **set di dati**che descrivono dati di input e dati di output per le pipeline.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="6f0ea-333">Creare una **pipeline** con un'attività di copia con BlobSource come origine e SqlSink come sink.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6f0ea-334">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6f0ea-334">Next steps</span></span>
<span data-ttu-id="6f0ea-335">In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="6f0ea-336">La tabella seguente contiene un elenco degli archivi dati supportati come origini e come destinazioni dall'attività di copia:</span><span class="sxs-lookup"><span data-stu-id="6f0ea-336">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="6f0ea-337">Per informazioni su come copiare dati da/in un archivio dati, fare clic sul collegamento relativo all'archivio dati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="6f0ea-337">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>