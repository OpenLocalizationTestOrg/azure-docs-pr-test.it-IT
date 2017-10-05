---
title: Copiare dati in e da un archivio BLOB di Azure | Microsoft Docs
description: 'Informazioni su come copiare dati BLOB in Azure Data Factory. Usare l''esempio: Come copiare dati da e verso l''archivio BLOB di Azure e il database SQL di Azure.'
keywords: dati blob, copia di blob di azure
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 2cf955b52010869a4e753c441e17bdd32fd2e63d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-or-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="5f378-105">Copiare i dati da e in Archiviazione BLOB di Azure mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5f378-105">Copy data to or from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="5f378-106">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per copiare i dati da e in Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-106">This article explains how to use the Copy Activity in Azure Data Factory to copy data to and from Azure Blob Storage.</span></span> <span data-ttu-id="5f378-107">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="5f378-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="5f378-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5f378-108">Overview</span></span>
<span data-ttu-id="5f378-109">È possibile copiare i dati da qualsiasi archivio dati di origine supportato all'archivio BLOB di Azure o dall'archivio BLOB di Azure a qualsiasi archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="5f378-109">You can copy data from any supported source data store to Azure Blob Storage or from Azure Blob Storage to any supported sink data store.</span></span> <span data-ttu-id="5f378-110">La tabella seguente contiene un elenco degli archivi dati supportati come origini o sink dall'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="5f378-110">The following table provides a list of data stores supported as sources or sinks by the copy activity.</span></span> <span data-ttu-id="5f378-111">È ad esempio possibile spostare dati **da** un database di SQL Server o un database SQL di Azure **a** una risorsa di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="5f378-112">È anche possibile copiare dati **da** Archiviazione BLOB di Azure **a** un'istanza di Azure SQL Data Warehouse o una raccolta Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5f378-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="5f378-113">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="5f378-113">Supported scenarios</span></span>
<span data-ttu-id="5f378-114">È possibile copiare i dati **da un archivio BLOB di Azure** agli archivi di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="5f378-114">You can copy data **from Azure Blob Storage** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="5f378-115">È possibile copiare i dati dagli archivi dati seguenti **a un archivio BLOB di Azure**:</span><span class="sxs-lookup"><span data-stu-id="5f378-115">You can copy data from the following data stores **to Azure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="5f378-116">L'attività di copia supporta la copia dei dati da/in account di archiviazione di Azure per utilizzo generico e servizi di Archiviazione BLOB ad accesso frequente o sporadico.</span><span class="sxs-lookup"><span data-stu-id="5f378-116">Copy Activity supports copying data from/to both general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="5f378-117">L'attività supporta la **lettura da BLOB in blocchi, di aggiunta o di pagine**, ma supporta la **scrittura solo in BLOB in blocchi**.</span><span class="sxs-lookup"><span data-stu-id="5f378-117">The activity supports **reading from block, append, or page blobs**, but supports **writing to only block blobs**.</span></span> <span data-ttu-id="5f378-118">Archiviazione Premium di Azure non è supportata come sink poiché si basa sui BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="5f378-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="5f378-119">L'attività di copia non elimina i dati dall'origine dopo che i dati sono stati correttamente copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-119">Copy Activity does not delete data from the source after the data is successfully copied to the destination.</span></span> <span data-ttu-id="5f378-120">Se è necessario eliminare i dati di origine dopo una copia con esito positivo, creare un'[attività personalizzata](data-factory-use-custom-activities.md) per eliminare i dati e usare l'attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="5f378-120">If you need to delete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) to delete the data and use the activity in the pipeline.</span></span> <span data-ttu-id="5f378-121">Per un esempio, vedere l'[esempio di eliminazione di BLOB o cartella in GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="5f378-121">For an example, see the [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="5f378-122">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="5f378-122">Get started</span></span>
<span data-ttu-id="5f378-123">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un archivio BLOB di Azure usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="5f378-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="5f378-124">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="5f378-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="5f378-125">Questo articolo include una [procedura dettagliata](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage)per la creazione di una pipeline per copiare dati da un percorso di un archivio BLOB di Azure al percorso di un altro archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline to copy data from an Azure Blob Storage location  to another Azure Blob Storage location.</span></span> <span data-ttu-id="5f378-126">Per un'esercitazione sulla creazione di una pipeline per copiare dati da un archivio BLOB di Azure a un database SQL Azure, vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="5f378-126">For a tutorial on creating a pipeline to copy data from an Azure Blob Storage to Azure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="5f378-127">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="5f378-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5f378-128">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="5f378-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="5f378-129">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="5f378-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="5f378-130">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="5f378-130">Create a **data factory**.</span></span> <span data-ttu-id="5f378-131">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="5f378-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="5f378-132">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="5f378-132">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="5f378-133">Ad esempio, se si copiano i dati da un'archiviazione BLOB di Azure in un database SQL di Azure, si creano due servizi collegati per collegare l'account di archiviazione di Azure e il database SQL di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="5f378-133">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="5f378-134">Per le proprietà del servizio collegato specifiche dell'archivio BLOB di Azure, vedere la sezione sulle [proprietà del servizio collegato](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-134">For linked service properties that are specific to Azure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="5f378-135">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="5f378-135">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="5f378-136">Nell'esempio citato nel passaggio precedente, si crea un set di dati per specificare un contenitore BLOB e la cartella che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="5f378-136">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="5f378-137">Si crea anche un altro set di dati per specificare la tabella SQL nel database SQL di Azure che contiene i dati copiati dall'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="5f378-137">And, you create another dataset to specify the SQL table in the Azure SQL database that holds the data copied from the blob storage.</span></span> <span data-ttu-id="5f378-138">Per le proprietà del set di dati specifiche dell'archivio BLOB di Azure, vedere la sezione sulle [proprietà del set di dati](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-138">For dataset properties that are specific to Azure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="5f378-139">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="5f378-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="5f378-140">Nell'esempio indicato in precedenza si usa BlobSource come origine e SqlSink come sink per l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="5f378-140">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="5f378-141">Analogamente, se si effettua la copia dal database SQL di Azure nell'archivio BLOB di Azure, si usa SqlSource e BlobSink nell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="5f378-141">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="5f378-142">Per le proprietà dell'attività di copia specifiche per l'archivio BLOB di Azure, vedere la sezione sulle [proprietà dell'attività di copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-142">For copy activity properties that are specific to Azure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="5f378-143">Per informazioni dettagliate su come usare un archivio dati come origine o come sink, fare clic sul collegamento nella sezione precedente per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="5f378-143">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="5f378-144">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5f378-144">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="5f378-145">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="5f378-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="5f378-146">Per esempi con definizioni JSON per entità di data factory utilizzate per copiare i dati da e verso un'archiviazione BLOB di Azure, vedere la sezione degli [esempi JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="5f378-146">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="5f378-147">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche di un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-147">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5f378-148">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="5f378-148">Linked service properties</span></span>
<span data-ttu-id="5f378-149">Esistono due tipi di servizi collegati, che consentono di collegare un archivio di Azure a una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-149">There are two types of linked services you can use to link an Azure Storage to an Azure data factory.</span></span> <span data-ttu-id="5f378-150">I due tipi di servizi sono il servizio collegato **AzureStorage** e il servizio collegato **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="5f378-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="5f378-151">Il servizio collegato Archiviazione di Azure garantisce alla data factory l'accesso globale ad Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-151">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="5f378-152">Invece il servizio collegato Firma di accesso condiviso di Archiviazione di Azure garantisce alla data factory l'accesso limitato o a scadenza ad Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-152">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="5f378-153">Non esistono altre differenze tra questi due servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="5f378-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="5f378-154">Scegliere il servizio collegato più adatto alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="5f378-154">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="5f378-155">Le sezioni seguenti forniscono altri dettagli su questi due servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="5f378-155">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="5f378-156">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="5f378-156">Dataset properties</span></span>
<span data-ttu-id="5f378-157">Per specificare un set di dati per rappresentare i dati di input o di output in un'archiviazione BLOB di Azure, impostare la proprietà del tipo del set di dati su **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="5f378-157">To specify a dataset to represent input or output data in an Azure Blob Storage, you set the type property of the dataset to: **AzureBlob**.</span></span> <span data-ttu-id="5f378-158">Impostare la proprietà **linkedServiceName** del set di dati sul nome del servizio collegato di Archiviazione di Azure o di firma di accesso condiviso Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-158">Set the **linkedServiceName** property of the dataset to the name of the Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="5f378-159">Le proprietà del tipo del set di dati specificano il **contenitore BLOB** e la **cartella** nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="5f378-159">The type properties of the dataset specify the **blob container** and the **folder** in the blob storage.</span></span>

<span data-ttu-id="5f378-160">Per un elenco completo delle proprietà e delle sezioni JSON disponibili per la definizione dei set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="5f378-160">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5f378-161">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="5f378-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="5f378-162">Data Factory supporta i valori di tipo basati su .NET conformi a CLS per specificare informazioni sul tipo nella sezione "structure" in relazione allo schema su origini dati di lettura come BLOB di Azure: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="5f378-162">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="5f378-163">La data factory esegue automaticamente le conversioni quando si spostano dati da un archivio dati di origine a un archivio dati di sink.</span><span class="sxs-lookup"><span data-stu-id="5f378-163">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span>

<span data-ttu-id="5f378-164">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione, il formato dei dati e così via nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="5f378-164">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span></span> <span data-ttu-id="5f378-165">La sezione typeProperties per il set di dati di tipo **AzureBlob** presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="5f378-165">The typeProperties section for dataset of type **AzureBlob** dataset has the following properties:</span></span>

| <span data-ttu-id="5f378-166">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5f378-166">Property</span></span> | <span data-ttu-id="5f378-167">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5f378-167">Description</span></span> | <span data-ttu-id="5f378-168">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="5f378-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5f378-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="5f378-169">folderPath</span></span> |<span data-ttu-id="5f378-170">Percorso del contenitore e della cartella nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="5f378-170">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="5f378-171">Esempio: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="5f378-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="5f378-172">Sì</span><span class="sxs-lookup"><span data-stu-id="5f378-172">Yes</span></span> |
| <span data-ttu-id="5f378-173">fileName</span><span class="sxs-lookup"><span data-stu-id="5f378-173">fileName</span></span> |<span data-ttu-id="5f378-174">Nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="5f378-174">Name of the blob.</span></span> <span data-ttu-id="5f378-175">fileName è facoltativo e non applica la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="5f378-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="5f378-176">Se si specifica un filename, l'attività, inclusa la copia, funziona sul BLOB specifico.</span><span class="sxs-lookup"><span data-stu-id="5f378-176">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="5f378-177">Quando fileName non è specificato, la copia include tutti i BLOB in folderPath per il set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="5f378-177">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="5f378-178">Quando non è specificato **fileName** per un set di dati di output e non è specificato **preserveHierarchy** nel sink dell'attività, il nome del file generato avrà il formato seguente: Data.<Guid>.txt (ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt).</span><span class="sxs-lookup"><span data-stu-id="5f378-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="5f378-179">No</span><span class="sxs-lookup"><span data-stu-id="5f378-179">No</span></span> |
| <span data-ttu-id="5f378-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="5f378-180">partitionedBy</span></span> |<span data-ttu-id="5f378-181">partitionedBy è una proprietà facoltativa.</span><span class="sxs-lookup"><span data-stu-id="5f378-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="5f378-182">Può essere utilizzata per specificare una proprietà folderPath dinamica e un nome file per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="5f378-182">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="5f378-183">Ad esempio, è possibile includere parametri per ogni ora di dati in folderPath.</span><span class="sxs-lookup"><span data-stu-id="5f378-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="5f378-184">Per informazioni dettagliate ed esempi, vedere la sezione [Uso della proprietà partitionedBy](#using-partitionedBy-property) .</span><span class="sxs-lookup"><span data-stu-id="5f378-184">See the [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="5f378-185">No</span><span class="sxs-lookup"><span data-stu-id="5f378-185">No</span></span> |
| <span data-ttu-id="5f378-186">format</span><span class="sxs-lookup"><span data-stu-id="5f378-186">format</span></span> | <span data-ttu-id="5f378-187">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="5f378-187">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="5f378-188">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="5f378-188">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="5f378-189">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="5f378-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="5f378-190">Per **copiare i file così come sono** tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="5f378-190">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="5f378-191">No</span><span class="sxs-lookup"><span data-stu-id="5f378-191">No</span></span> |
| <span data-ttu-id="5f378-192">compressione</span><span class="sxs-lookup"><span data-stu-id="5f378-192">compression</span></span> | <span data-ttu-id="5f378-193">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="5f378-193">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="5f378-194">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="5f378-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="5f378-195">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="5f378-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="5f378-196">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="5f378-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="5f378-197">No</span><span class="sxs-lookup"><span data-stu-id="5f378-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="5f378-198">Uso della proprietà partitionedBy</span><span class="sxs-lookup"><span data-stu-id="5f378-198">Using partitionedBy property</span></span>
<span data-ttu-id="5f378-199">Come indicato nella sezione precedente, è possibile specificare valori fileName e folderPath dinamici per i dati di una serie temporale con la proprietà **partitionedBy**, le [funzioni di data factory e le variabili di sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="5f378-199">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="5f378-200">Per maggiori informazioni sui set di dati delle serie temporali, sulla pianificazione e sulle sezioni, leggere gli articoli [Creazione di set di dati](data-factory-create-datasets.md) e [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="5f378-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="5f378-201">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="5f378-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="5f378-202">In questo esempio {Slice} viene sostituito con il valore della variabile di sistema SliceStart di Data Factory nel formato (AAAAMMGGHH) specificato.</span><span class="sxs-lookup"><span data-stu-id="5f378-202">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="5f378-203">SliceStart fa riferimento all'ora di inizio della sezione.</span><span class="sxs-lookup"><span data-stu-id="5f378-203">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="5f378-204">La proprietà folderPath è diversa per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="5f378-204">The folderPath is different for each slice.</span></span> <span data-ttu-id="5f378-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="5f378-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="5f378-206">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="5f378-206">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="5f378-207">In questo esempio l'anno, il mese, il giorno e l'ora di SliceStart vengono estratti in variabili separate che vengono usate dalle proprietà folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="5f378-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="5f378-208">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="5f378-208">Copy activity properties</span></span>
<span data-ttu-id="5f378-209">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="5f378-209">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5f378-210">Proprietà quali nome, descrizione, criteri e set di dati di input e di output sono disponibili per tutti i tipi di attività.</span><span class="sxs-lookup"><span data-stu-id="5f378-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="5f378-211">Le proprietà disponibili nella sezione **typeProperties** dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="5f378-211">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="5f378-212">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="5f378-212">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="5f378-213">Se si effettua il trasferimento dei dati da un archivio BLOB di Azure, impostare il tipo di origine nell'attività di copia su **BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="5f378-213">If you are moving data from an Azure Blob Storage, you set the source type in the copy activity to **BlobSource**.</span></span> <span data-ttu-id="5f378-214">Analogamente, se si effettua il trasferimento dei dati in un archivio BLOB di Azure, impostare il tipo di sink nell'attività di copia su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="5f378-214">Similarly, if you are moving data to an Azure Blob Storage, you set the sink type in the copy activity to **BlobSink**.</span></span> <span data-ttu-id="5f378-215">Questa sezione presenta un elenco delle proprietà supportate da BlobSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="5f378-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="5f378-216">**BlobSource** supporta le seguenti proprietà della sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="5f378-216">**BlobSource** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="5f378-217">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5f378-217">Property</span></span> | <span data-ttu-id="5f378-218">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5f378-218">Description</span></span> | <span data-ttu-id="5f378-219">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="5f378-219">Allowed values</span></span> | <span data-ttu-id="5f378-220">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="5f378-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5f378-221">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="5f378-221">recursive</span></span> |<span data-ttu-id="5f378-222">Indica se i dati vengono letti in modo ricorsivo dalle cartelle secondarie o solo dalla cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="5f378-222">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="5f378-223">True (valore predefinito), False</span><span class="sxs-lookup"><span data-stu-id="5f378-223">True (default value), False</span></span> |<span data-ttu-id="5f378-224">No</span><span class="sxs-lookup"><span data-stu-id="5f378-224">No</span></span> |

<span data-ttu-id="5f378-225">**BlobSink** supporta le proprietà della sezione **typeProperties** seguenti:</span><span class="sxs-lookup"><span data-stu-id="5f378-225">**BlobSink** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="5f378-226">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5f378-226">Property</span></span> | <span data-ttu-id="5f378-227">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5f378-227">Description</span></span> | <span data-ttu-id="5f378-228">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="5f378-228">Allowed values</span></span> | <span data-ttu-id="5f378-229">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="5f378-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5f378-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="5f378-230">copyBehavior</span></span> |<span data-ttu-id="5f378-231">Definisce il comportamento di copia quando l'origine è BlobSource o FileSystem.</span><span class="sxs-lookup"><span data-stu-id="5f378-231">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="5f378-232"><b>PreserveHierarchy:</b> mantiene la gerarchia dei file nella cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-232"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="5f378-233">Il percorso relativo del file di origine nella cartella di origine è identico al percorso relativo del file di destinazione nella cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-233">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="5f378-234"><b>FlattenHierarchy</b>: tutti i file della cartella di origine si trovano nel primo livello della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-234"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="5f378-235">Il nome dei file di destinazione viene generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5f378-235">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="5f378-236"><b>MergeFiles</b>: unisce tutti i file della cartella di origine in un solo file.</span><span class="sxs-lookup"><span data-stu-id="5f378-236"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="5f378-237">Se viene specificato il nome file/BLOB, il nome file unito sarà il nome specificato. In caso contrario, sarà il nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5f378-237">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="5f378-238">No</span><span class="sxs-lookup"><span data-stu-id="5f378-238">No</span></span> |

<span data-ttu-id="5f378-239">**BlobSource** supporta anche le due proprietà seguenti per la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="5f378-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="5f378-240">**treatEmptyAsNull**: specifica se considerare una stringa vuota o Null come valore Null.</span><span class="sxs-lookup"><span data-stu-id="5f378-240">**treatEmptyAsNull**: Specifies whether to treat null or empty string as null value.</span></span>
* <span data-ttu-id="5f378-241">**skipHeaderLineCount** : specifica il numero di righe che devono essere ignorate.</span><span class="sxs-lookup"><span data-stu-id="5f378-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="5f378-242">È applicabile solo quando il set di dati di input usa TextFormat.</span><span class="sxs-lookup"><span data-stu-id="5f378-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="5f378-243">In modo analogo, **BlobSink** supporta la proprietà seguente per la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="5f378-243">Similarly, **BlobSink** supports the following property for backward compatibility.</span></span>

* <span data-ttu-id="5f378-244">**blobWriterAddHeader**: specifica se aggiungere un'intestazione di definizioni di colonna durante la scrittura di un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="5f378-244">**blobWriterAddHeader**: Specifies whether to add a header of column definitions while writing to an output dataset.</span></span>

<span data-ttu-id="5f378-245">Ora i set di dati supportano le proprietà seguenti che implementano la stessa funzionalità: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="5f378-245">Datasets now support the following properties that implement the same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="5f378-246">La tabella seguente fornisce indicazioni sull'uso delle nuove proprietà del set di dati al posto di queste proprietà del sink o dell'origine BLOB.</span><span class="sxs-lookup"><span data-stu-id="5f378-246">The following table provides guidance on using the new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="5f378-247">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="5f378-247">Copy Activity property</span></span> | <span data-ttu-id="5f378-248">Proprietà del set di dati</span><span class="sxs-lookup"><span data-stu-id="5f378-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f378-249">skipHeaderLineCount in BlobSource</span><span class="sxs-lookup"><span data-stu-id="5f378-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="5f378-250">skipLineCount e firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="5f378-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="5f378-251">Le righe vengono prima ignorate e poi la prima riga viene letta come intestazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-251">Lines are skipped first and then the first row is read as a header.</span></span> |
| <span data-ttu-id="5f378-252">treatEmptyAsNull in BlobSource</span><span class="sxs-lookup"><span data-stu-id="5f378-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="5f378-253">treatEmptyAsNull nel set di dati di input</span><span class="sxs-lookup"><span data-stu-id="5f378-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="5f378-254">blobWriterAddHeader in BlobSink</span><span class="sxs-lookup"><span data-stu-id="5f378-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="5f378-255">firstRowAsHeader nel set di dati di output</span><span class="sxs-lookup"><span data-stu-id="5f378-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="5f378-256">Per informazioni dettagliate su queste proprietà, vedere la sezione [Specifica di TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) .</span><span class="sxs-lookup"><span data-stu-id="5f378-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="5f378-257">esempi ricorsivi e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="5f378-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="5f378-258">In questa sezione viene descritto il comportamento derivante dell'operazione di copia per diverse combinazioni di valori ricorsivi e copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="5f378-258">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="5f378-259">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="5f378-259">recursive</span></span> | <span data-ttu-id="5f378-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="5f378-260">copyBehavior</span></span> | <span data-ttu-id="5f378-261">Comportamento risultante</span><span class="sxs-lookup"><span data-stu-id="5f378-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5f378-262">true</span><span class="sxs-lookup"><span data-stu-id="5f378-262">true</span></span> |<span data-ttu-id="5f378-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="5f378-263">preserveHierarchy</span></span> |<span data-ttu-id="5f378-264">Per una cartella di origine Cartella1 con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="5f378-264">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="5f378-265">Cartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-265">Folder1</span></span><br/><span data-ttu-id="5f378-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5f378-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5f378-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5f378-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5f378-268">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5f378-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5f378-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5f378-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5f378-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5f378-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5f378-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5f378-272">la cartella di destinazione Cartella1 viene creata con la stessa struttura dell'origine</span><span class="sxs-lookup"><span data-stu-id="5f378-272">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="5f378-273">Cartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-273">Folder1</span></span><br/><span data-ttu-id="5f378-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5f378-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5f378-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5f378-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5f378-276">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5f378-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5f378-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5f378-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5f378-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5f378-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="5f378-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="5f378-280">true</span><span class="sxs-lookup"><span data-stu-id="5f378-280">true</span></span> |<span data-ttu-id="5f378-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="5f378-281">flattenHierarchy</span></span> |<span data-ttu-id="5f378-282">Per una cartella di origine Cartella1 con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="5f378-282">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="5f378-283">Cartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-283">Folder1</span></span><br/><span data-ttu-id="5f378-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5f378-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5f378-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5f378-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5f378-286">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5f378-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5f378-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5f378-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5f378-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5f378-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5f378-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5f378-290">la Cartella1 di destinazione viene creata con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="5f378-290">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="5f378-291">Cartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-291">Folder1</span></span><br/><span data-ttu-id="5f378-292">&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="5f378-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="5f378-293">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2</span><span class="sxs-lookup"><span data-stu-id="5f378-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="5f378-294">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File3</span><span class="sxs-lookup"><span data-stu-id="5f378-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="5f378-295">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File4</span><span class="sxs-lookup"><span data-stu-id="5f378-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="5f378-296">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File5</span><span class="sxs-lookup"><span data-stu-id="5f378-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="5f378-297">true</span><span class="sxs-lookup"><span data-stu-id="5f378-297">true</span></span> |<span data-ttu-id="5f378-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="5f378-298">mergeFiles</span></span> |<span data-ttu-id="5f378-299">Per una cartella di origine Cartella1 con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="5f378-299">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="5f378-300">Cartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-300">Folder1</span></span><br/><span data-ttu-id="5f378-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5f378-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5f378-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5f378-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5f378-303">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5f378-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5f378-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5f378-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5f378-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5f378-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5f378-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5f378-307">la Cartella1 di destinazione viene creata con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="5f378-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="5f378-308">Cartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-308">Folder1</span></span><br/><span data-ttu-id="5f378-309">&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 + File3 + File4 + File 5 viene unito in un file con nome file generato automaticamente</span><span class="sxs-lookup"><span data-stu-id="5f378-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="5f378-310">false</span><span class="sxs-lookup"><span data-stu-id="5f378-310">false</span></span> |<span data-ttu-id="5f378-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="5f378-311">preserveHierarchy</span></span> |<span data-ttu-id="5f378-312">Per una cartella di origine Cartella1 con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="5f378-312">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="5f378-313">Cartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-313">Folder1</span></span><br/><span data-ttu-id="5f378-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5f378-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5f378-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5f378-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5f378-316">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5f378-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5f378-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5f378-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5f378-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5f378-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5f378-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5f378-320">la cartella di destinazione Cartella1 viene creata con la struttura seguente</span><span class="sxs-lookup"><span data-stu-id="5f378-320">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="5f378-321">Cartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-321">Folder1</span></span><br/><span data-ttu-id="5f378-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5f378-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5f378-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5f378-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="5f378-324">Sottocartella1 con File3, File4 e File5 non considerati.</span><span class="sxs-lookup"><span data-stu-id="5f378-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="5f378-325">false</span><span class="sxs-lookup"><span data-stu-id="5f378-325">false</span></span> |<span data-ttu-id="5f378-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="5f378-326">flattenHierarchy</span></span> |<span data-ttu-id="5f378-327">Per una cartella di origine Cartella1 con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="5f378-327">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="5f378-328">Cartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-328">Folder1</span></span><br/><span data-ttu-id="5f378-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5f378-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5f378-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5f378-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5f378-331">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5f378-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5f378-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5f378-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5f378-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5f378-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5f378-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5f378-335">la cartella di destinazione Cartella1 viene creata con la struttura seguente</span><span class="sxs-lookup"><span data-stu-id="5f378-335">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="5f378-336">Cartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-336">Folder1</span></span><br/><span data-ttu-id="5f378-337">&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="5f378-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="5f378-338">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2</span><span class="sxs-lookup"><span data-stu-id="5f378-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="5f378-339">Sottocartella1 con File3, File4 e File5 non considerati.</span><span class="sxs-lookup"><span data-stu-id="5f378-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="5f378-340">false</span><span class="sxs-lookup"><span data-stu-id="5f378-340">false</span></span> |<span data-ttu-id="5f378-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="5f378-341">mergeFiles</span></span> |<span data-ttu-id="5f378-342">Per una cartella di origine Cartella1 con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="5f378-342">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="5f378-343">Cartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-343">Folder1</span></span><br/><span data-ttu-id="5f378-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5f378-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5f378-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5f378-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5f378-346">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5f378-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5f378-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5f378-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5f378-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5f378-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5f378-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5f378-350">la cartella di destinazione Cartella1 viene creata con la struttura seguente</span><span class="sxs-lookup"><span data-stu-id="5f378-350">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="5f378-351">Cartella1</span><span class="sxs-lookup"><span data-stu-id="5f378-351">Folder1</span></span><br/><span data-ttu-id="5f378-352">&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 viene unito in un file con un nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5f378-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="5f378-353">Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="5f378-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="5f378-354">Sottocartella1 con File3, File4 e File5 non considerati.</span><span class="sxs-lookup"><span data-stu-id="5f378-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage"></a><span data-ttu-id="5f378-355">Procedura dettagliata: Usare la copia guidata per copiare i dati in/da una risorsa di archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="5f378-355">Walkthrough: Use Copy Wizard to copy data to/from Blob Storage</span></span>
<span data-ttu-id="5f378-356">Ecco come copiare rapidamente i dati in/da una risorsa di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-356">Let's look at how to quickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="5f378-357">In questa procedura dettagliata gli archivi dati sia di origine che di destinazione sono di tipo archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="5f378-358">La pipeline in questa procedura dettagliata copia i dati da una cartella a un'altra cartella nello stesso contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="5f378-358">The pipeline in this walkthrough copies data from a folder to another folder in the same blob container.</span></span> <span data-ttu-id="5f378-359">Questa procedura dettagliata è volutamente semplice perché illustra le impostazioni o le proprietà quando si usa l'archivio BLOB come origine o come sink.</span><span class="sxs-lookup"><span data-stu-id="5f378-359">This walkthrough is intentionally simple to show you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="5f378-360">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5f378-360">Prerequisites</span></span>
1. <span data-ttu-id="5f378-361">Creare un **account di archiviazione di Azure** per utilizzo generico, se necessario.</span><span class="sxs-lookup"><span data-stu-id="5f378-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="5f378-362">In questa procedura dettagliata si usa l'archivio BLOB come archivio dati sia di **origine** che di **destinazione**.</span><span class="sxs-lookup"><span data-stu-id="5f378-362">You use the blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="5f378-363">Se non si ha un account di archiviazione di Azure, vedere l'articolo [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) per informazioni su come crearne uno.</span><span class="sxs-lookup"><span data-stu-id="5f378-363">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
2. <span data-ttu-id="5f378-364">Creare un contenitore BLOB denominato **adfblobconnector** nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-364">Create a blob container named **adfblobconnector** in the storage account.</span></span> 
4. <span data-ttu-id="5f378-365">Creare una cartella denominata **input** nel contenitore **adfblobconnector**.</span><span class="sxs-lookup"><span data-stu-id="5f378-365">Create a folder named **input** in the **adfblobconnector** container.</span></span>
5. <span data-ttu-id="5f378-366">Creare un file denominato **emp.txt** con il contenuto seguente e caricarlo nella cartella **input** usando strumenti come [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="5f378-366">Create a file named **emp.txt** with the following content and upload it to the **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-the-data-factory"></a><span data-ttu-id="5f378-367">Creare la data factory</span><span class="sxs-lookup"><span data-stu-id="5f378-367">Create the data factory</span></span>
1. <span data-ttu-id="5f378-368">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f378-368">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5f378-369">Fare clic su **+ NUOVO** nell'angolo in alto a sinistra e quindi su **Intelligence e analisi** e su **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="5f378-369">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="5f378-370">Nel pannello **Nuova data factory** :</span><span class="sxs-lookup"><span data-stu-id="5f378-370">In the **New data factory** blade:</span></span>   
    1. <span data-ttu-id="5f378-371">Immettere **ADFBlobConnectorDF** come **nome**.</span><span class="sxs-lookup"><span data-stu-id="5f378-371">Enter **ADFBlobConnectorDF** for the **name**.</span></span> <span data-ttu-id="5f378-372">È necessario specificare un nome univoco globale per l'istanza di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5f378-372">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="5f378-373">Se viene visualizzato l'errore `*Data factory name “ADFBlobConnectorDF” is not available`, modificare il nome della data factory, ad esempio, nomeutenteADFBlobConnectorDF, e provare di nuovo a crearla.</span><span class="sxs-lookup"><span data-stu-id="5f378-373">If you receive the error: `*Data factory name “ADFBlobConnectorDF” is not available`, change the name of the data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="5f378-374">Per informazioni sulle regole di denominazione per gli elementi di Data Factory, vedere l'argomento [Azure Data Factory - Regole di denominazione](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="5f378-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="5f378-375">Selezionare la **sottoscrizione**di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="5f378-376">Per Gruppo di risorse, selezionare **Usa esistente** per selezionare un gruppo di risorse esistente oppure selezionare **Crea nuovo** per immettere un nome per un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5f378-376">For Resource Group, select **Use existing** to select an existing resource group (or) select **Create new** to enter a name for a resource group.</span></span>
    4. <span data-ttu-id="5f378-377">Selezionare una **località** per la data factory.</span><span class="sxs-lookup"><span data-stu-id="5f378-377">Select a **location** for the data factory.</span></span>
    5. <span data-ttu-id="5f378-378">Selezionare la casella di controllo **Aggiungi al dashboard** nella parte inferiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="5f378-378">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>
    6. <span data-ttu-id="5f378-379">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5f378-379">Click **Create**.</span></span>
3. <span data-ttu-id="5f378-380">Al termine della creazione verrà visualizzato il pannello **Data factory**, come illustrato nell'immagine seguente: ![Home page di Data factory](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-380">After the creation is complete, you see the **Data Factory** blade as shown in the following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="5f378-381">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="5f378-381">Copy Wizard</span></span>
1. <span data-ttu-id="5f378-382">Nella home page di Data Factory fare clic sul riquadro **Copia dati (ANTEPRIMA)** per avviare **Copy Data Wizard** (Copia dati guidata).</span><span class="sxs-lookup"><span data-stu-id="5f378-382">On the Data Factory home page, click the **Copy data [PREVIEW]** tile to launch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="5f378-383">Se il Web browser è bloccato su "Concessione autorizzazioni in corso...", disabilitare/deselezionare l'impostazione **Block third party cookies and site data** (Blocca cookie e dati del sito di terze parti) oppure lasciarla abilitata, creare un'eccezione per **login.microsoftonline.com** e quindi provare di nuovo ad avviare la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="5f378-383">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="5f378-384">Nella pagina **Proprietà** :</span><span class="sxs-lookup"><span data-stu-id="5f378-384">In the **Properties** page:</span></span>
    1. <span data-ttu-id="5f378-385">Immettere **CopyPipeline** in **Nome attività**.</span><span class="sxs-lookup"><span data-stu-id="5f378-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="5f378-386">Il nome dell'attività è il nome della pipeline nella data factory.</span><span class="sxs-lookup"><span data-stu-id="5f378-386">The task name is the name of the pipeline in your data factory.</span></span>
    2. <span data-ttu-id="5f378-387">Immettere una **descrizione** per l'attività (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="5f378-387">Enter a **description** for the task (optional).</span></span>
    3. <span data-ttu-id="5f378-388">In **Task cadence or Task schedule** (Cadenza attività o pianificazione attività) lasciare selezionata l'opzione **Run regularly on schedule** (Esegui periodicamente come pianificato).</span><span class="sxs-lookup"><span data-stu-id="5f378-388">For **Task cadence or Task schedule**, keep the **Run regularly on schedule** option.</span></span> <span data-ttu-id="5f378-389">Per eseguire questa attività una sola volta invece che ripetutamente in base a una pianificazione, selezionare **Run once now** (Esegui una volta ora).</span><span class="sxs-lookup"><span data-stu-id="5f378-389">If you want to run this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="5f378-390">Se si seleziona l'opzione **Run once now** (Esegui una volta ora), viene creata una [pipeline con esecuzione singola](data-factory-create-pipelines.md#onetime-pipeline).</span><span class="sxs-lookup"><span data-stu-id="5f378-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="5f378-391">Mantenere le impostazioni per **Recurring pattern** (Schema ricorrente).</span><span class="sxs-lookup"><span data-stu-id="5f378-391">Keep the settings for **Recurring pattern**.</span></span> <span data-ttu-id="5f378-392">Questa attività viene eseguita ogni giorno tra le ore di inizio e fine specificate nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="5f378-392">This task runs daily between the start and end times you specify in the next step.</span></span>
    5. <span data-ttu-id="5f378-393">Impostare **Start date time** (Data e ora di inizio) su **21/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="5f378-393">Change the **Start date time** to **04/21/2017**.</span></span> 
    6. <span data-ttu-id="5f378-394">Impostare **End date time** (Data e ora di fine) su **25/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="5f378-394">Change the **End date time** to **04/25/2017**.</span></span> <span data-ttu-id="5f378-395">È possibile digitare la data invece di cercarla nel calendario.</span><span class="sxs-lookup"><span data-stu-id="5f378-395">You may want to type the date instead of browsing through the calendar.</span></span>     
    8. <span data-ttu-id="5f378-396">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f378-396">Click **Next**.</span></span>
      <span data-ttu-id="5f378-397">![Strumento di copia - Pagina Proprietà](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="5f378-398">Nella pagina **Source data store** (Archivio dati di origine) fare clic sul riquadro **Archivio BLOB di Azure**.</span><span class="sxs-lookup"><span data-stu-id="5f378-398">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="5f378-399">Usare questa pagina per specificare l'archivio dati di origine per l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="5f378-399">You use this page to specify the source data store for the copy task.</span></span> <span data-ttu-id="5f378-400">È possibile usare un servizio collegato di archivio dati esistente oppure specificare un nuovo archivio dati.</span><span class="sxs-lookup"><span data-stu-id="5f378-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="5f378-401">Per usare un servizio collegato esistente, selezionare **FROM EXISTING LINKED SERVICES** (DA SERVIZI COLLEGATI ESISTENTI) e selezionare il servizio collegato corretto.</span><span class="sxs-lookup"><span data-stu-id="5f378-401">To use an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select the right linked service.</span></span> 
    <span data-ttu-id="5f378-402">![Strumento di copia - Pagina Archivio dati di origine](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="5f378-403">Nella pagina **Specify the Azure Blob storage account** (Specificare l'account di archiviazione BLOB di Azure):</span><span class="sxs-lookup"><span data-stu-id="5f378-403">On the **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="5f378-404">Mantenere il nome generato automaticamente per **Nome connessione**.</span><span class="sxs-lookup"><span data-stu-id="5f378-404">Keep the auto-generated name for **Connection name**.</span></span> <span data-ttu-id="5f378-405">Il nome della connessione è il nome del servizio collegato di tipo: Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-405">The connection name is the name of the linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="5f378-406">Verificare che in **Account selection method** (Metodo di selezione dell'account) sia selezionata l'opzione **From Azure subscriptions** (Da sottoscrizioni di Azure).</span><span class="sxs-lookup"><span data-stu-id="5f378-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="5f378-407">Selezionare la sottoscrizione di Azure o mantenere **Seleziona tutte** per **Sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="5f378-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="5f378-408">Selezionare un **Account di archiviazione di Azure** nell'elenco di quelli disponibili nella sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="5f378-408">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="5f378-409">È anche possibile scegliere di immettere manualmente le impostazioni dell'account di archiviazione, selezionando l'opzione **Immetti manualmente** per **Account selection method** (Metodo di selezione dell'account).</span><span class="sxs-lookup"><span data-stu-id="5f378-409">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**.</span></span>
   5. <span data-ttu-id="5f378-410">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f378-410">Click **Next**.</span></span> 
      <span data-ttu-id="5f378-411">![Strumento di copia - Specificare l'account di archiviazione BLOB di Azure](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-411">![Copy Tool - Specify the Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="5f378-412">Nella pagina **Choose the input file or folder** (Scegliere il file o la cartella di input):</span><span class="sxs-lookup"><span data-stu-id="5f378-412">On **Choose the input file or folder** page:</span></span>
   1. <span data-ttu-id="5f378-413">Fare doppio clic su **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="5f378-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="5f378-414">Selezionare **input** e fare clic su **Scegli**.</span><span class="sxs-lookup"><span data-stu-id="5f378-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="5f378-415">In questa procedura dettagliata si seleziona la cartella input.</span><span class="sxs-lookup"><span data-stu-id="5f378-415">In this walkthrough, you select the input folder.</span></span> <span data-ttu-id="5f378-416">È anche possibile scegliere invece il file emp.txt nella cartella.</span><span class="sxs-lookup"><span data-stu-id="5f378-416">You could also select the emp.txt file in the folder instead.</span></span> 
      <span data-ttu-id="5f378-417">![Strumento di copia - Scegliere il file o la cartella di input](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-417">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="5f378-418">Nella pagina **Choose the input file or folder** (Scegliere il file o la cartella di input):</span><span class="sxs-lookup"><span data-stu-id="5f378-418">On the **Choose the input file or folder** page:</span></span>
    1. <span data-ttu-id="5f378-419">Verificare che **File o cartella** sia impostato su **adfblobconnector/input**.</span><span class="sxs-lookup"><span data-stu-id="5f378-419">Confirm that the **file or folder** is set to **adfblobconnector/input**.</span></span> <span data-ttu-id="5f378-420">Se i file sono in cartelle secondarie, ad esempio 2017/04/01, 2017/04/02 e così via, immettere adfblobconnector/input/{anno}/{mese}/{giorno} per il file o la cartella.</span><span class="sxs-lookup"><span data-stu-id="5f378-420">If the files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="5f378-421">Quando si preme TAB al di fuori della casella di testo, vengono visualizzati tre elenchi a discesa per selezionare i formati per anno (yyyy), mese (MM) e giorno (dd).</span><span class="sxs-lookup"><span data-stu-id="5f378-421">When you press TAB out of the text box, you see three drop-down lists to select formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="5f378-422">Non impostare **Copy file recursively** (Copia file in modo ricorsivo).</span><span class="sxs-lookup"><span data-stu-id="5f378-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="5f378-423">Selezionare questa opzione per cercare in modo ricorsivo nelle cartelle i file da copiare nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-423">Select this option to recursively traverse through folders for files to be copied to the destination.</span></span> 
    3. <span data-ttu-id="5f378-424">Non selezionare l'opzione **binary copy** (Copia binaria).</span><span class="sxs-lookup"><span data-stu-id="5f378-424">Do not the **binary copy** option.</span></span> <span data-ttu-id="5f378-425">Selezionare questa opzione per eseguire una copia binaria del file di origine nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-425">Select this option to perform a binary copy of source file to the destination.</span></span> <span data-ttu-id="5f378-426">Non selezionarla per questa procedura dettagliata per poter visualizzare altre opzioni nelle pagine successive.</span><span class="sxs-lookup"><span data-stu-id="5f378-426">Do not select for this walkthrough so that you can see more options in the next pages.</span></span> 
    4. <span data-ttu-id="5f378-427">Verificare che **Tipo di compressione** sia impostato su **Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="5f378-427">Confirm that the **Compression type** is set to **None**.</span></span> <span data-ttu-id="5f378-428">Selezionare un valore per questa opzione se i file di origine sono compressi in uno dei formati supportati.</span><span class="sxs-lookup"><span data-stu-id="5f378-428">Select a value for this option if your source files are compressed in one of the supported formats.</span></span> 
    5. <span data-ttu-id="5f378-429">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f378-429">Click **Next**.</span></span>
    <span data-ttu-id="5f378-430">![Strumento di copia - Scegliere il file o la cartella di input](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-430">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="5f378-431">Nella pagina **File format settings** (Impostazioni di formato file) vengono visualizzati i delimitatori e lo schema rilevati automaticamente dalla procedura guidata analizzando il file.</span><span class="sxs-lookup"><span data-stu-id="5f378-431">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> 
    1. <span data-ttu-id="5f378-432">Confermare le opzioni seguenti: a.</span><span class="sxs-lookup"><span data-stu-id="5f378-432">Confirm the following options: a.</span></span> <span data-ttu-id="5f378-433">Il **formato file** è impostato su **Testo**.</span><span class="sxs-lookup"><span data-stu-id="5f378-433">The **file format** is set to **Text format**.</span></span> <span data-ttu-id="5f378-434">È possibile visualizzare tutti i formati supportati nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="5f378-434">You can see all the supported formats in the drop-down list.</span></span> <span data-ttu-id="5f378-435">Ad esempio: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="5f378-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="5f378-436">b.</span><span class="sxs-lookup"><span data-stu-id="5f378-436">b.</span></span> <span data-ttu-id="5f378-437">Il **delimitatore di colonna** è impostato su `Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="5f378-437">The **column delimiter** is set to `Comma (,)`.</span></span> <span data-ttu-id="5f378-438">È possibile visualizzare gli altri delimitatori di colonna supportati da Data Factory nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="5f378-438">You can see the other column delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="5f378-439">È anche possibile specificare un delimitatore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5f378-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="5f378-440">c.</span><span class="sxs-lookup"><span data-stu-id="5f378-440">c.</span></span> <span data-ttu-id="5f378-441">Il **delimitatore di riga** è impostato su `Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="5f378-441">The **row delimiter** is set to `Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="5f378-442">È possibile visualizzare gli altri delimitatori di riga supportati da Data Factory nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="5f378-442">You can see the other row delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="5f378-443">È anche possibile specificare un delimitatore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5f378-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="5f378-444">d.</span><span class="sxs-lookup"><span data-stu-id="5f378-444">d.</span></span> <span data-ttu-id="5f378-445">Il **numero di righe da ignorare** è impostato su **0**.</span><span class="sxs-lookup"><span data-stu-id="5f378-445">The **skip line count** is set to **0**.</span></span> <span data-ttu-id="5f378-446">Per ignorare alcune righe all'inizio del file, immettere il numero qui.</span><span class="sxs-lookup"><span data-stu-id="5f378-446">If you want a few lines to be skipped at the top of the file, enter the number here.</span></span>
        <span data-ttu-id="5f378-447">e.</span><span class="sxs-lookup"><span data-stu-id="5f378-447">e.</span></span>  <span data-ttu-id="5f378-448">L'opzione **Nomi di colonne nella prima riga di dati** non è impostata.</span><span class="sxs-lookup"><span data-stu-id="5f378-448">The **first data row contains column names** is not set.</span></span> <span data-ttu-id="5f378-449">Se i file di origine contengano nomi di colonna nella prima riga, selezionare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="5f378-449">If the source files contain column names in the first row, select this option.</span></span>
        <span data-ttu-id="5f378-450">f.</span><span class="sxs-lookup"><span data-stu-id="5f378-450">f.</span></span> <span data-ttu-id="5f378-451">L'opzione **treat empty column value as null** (Considera i valori di colonna vuoti come null) è impostata.</span><span class="sxs-lookup"><span data-stu-id="5f378-451">The **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="5f378-452">Espandere **Impostazioni avanzate** per visualizzare l'opzione avanzata disponibile.</span><span class="sxs-lookup"><span data-stu-id="5f378-452">Expand **Advanced settings** to see advanced option available.</span></span>
    3. <span data-ttu-id="5f378-453">Nella parte inferiore della pagina visualizzare l'**anteprima** dei dati del file emp.txt.</span><span class="sxs-lookup"><span data-stu-id="5f378-453">At the bottom of the page, see the **preview** of data from the emp.txt file.</span></span>
    4. <span data-ttu-id="5f378-454">Fare clic sulla scheda **SCHEMA** nella parte inferiore per visualizzate lo schema derivato dalla copia guidata esaminando i dati nel file di origine.</span><span class="sxs-lookup"><span data-stu-id="5f378-454">Click **SCHEMA** tab at the bottom to see the schema that the copy wizard inferred by looking at the data in the source file.</span></span>
    5. <span data-ttu-id="5f378-455">Dopo aver esaminato i delimitatori e i dati di anteprima, fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="5f378-455">Click **Next** after you review the delimiters and preview data.</span></span>
    <span data-ttu-id="5f378-456">![Strumento di copia - Impostazioni di formattazioni del file](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="5f378-457">Nella pagina **Destination data store** (Archivio dati di destinazione) selezionare **Archivio BLOB di Azure** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f378-457">On the **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="5f378-458">In questa procedura dettagliata si usa l'archivio BLOB di Azure come archivio dati sia di origine che di destinazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-458">You are using the Azure Blob Storage as both the source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="5f378-459">![Strumento di copia - Selezionare l'archivio dati di destinazione](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="5f378-460">Nella pagina **Specify the Azure Blob storage account** (Specificare l'account di archiviazione BLOB di Azure):</span><span class="sxs-lookup"><span data-stu-id="5f378-460">On **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="5f378-461">Immettere **AzureStorageLinkedService** nel campo **Connection name** (Nome connessione).</span><span class="sxs-lookup"><span data-stu-id="5f378-461">Enter **AzureStorageLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="5f378-462">Verificare che in **Account selection method** (Metodo di selezione dell'account) sia selezionata l'opzione **From Azure subscriptions** (Da sottoscrizioni di Azure).</span><span class="sxs-lookup"><span data-stu-id="5f378-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="5f378-463">Selezionare la **sottoscrizione**di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="5f378-464">Selezionare l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="5f378-465">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f378-465">Click **Next**.</span></span>     
10. <span data-ttu-id="5f378-466">Nella pagina **Choose the output file or folder** (Scegliere il file o la cartella di output):</span><span class="sxs-lookup"><span data-stu-id="5f378-466">On the **Choose the output file or folder** page:</span></span> 
    6. <span data-ttu-id="5f378-467">In **Percorso cartella** specificare **adfblobconnector/output/{year}/{month}/{day}** (adfblobconnector/output/{anno}/{mese}/{giorno}).</span><span class="sxs-lookup"><span data-stu-id="5f378-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="5f378-468">Premere **TAB**.</span><span class="sxs-lookup"><span data-stu-id="5f378-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="5f378-469">Per **anno**, selezionare **yyyy**.</span><span class="sxs-lookup"><span data-stu-id="5f378-469">For the **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="5f378-470">Per **mese**, verificare che sia impostato su **MM**.</span><span class="sxs-lookup"><span data-stu-id="5f378-470">For the **month**, confirm that it is set to **MM**.</span></span>
    9. <span data-ttu-id="5f378-471">Per **giorno**, verificare che sia impostato su **dd** (gg).</span><span class="sxs-lookup"><span data-stu-id="5f378-471">For the **day**, confirm that it is set to **dd**.</span></span>
    10. <span data-ttu-id="5f378-472">Verificare che **Tipo di compressione** sia impostato su **Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="5f378-472">Confirm that the **compression type** is set to **None**.</span></span>
    11. <span data-ttu-id="5f378-473">Verificare che **copy behavior** (Comportamento copia) sia impostato su **Merge files** (Unisci file).</span><span class="sxs-lookup"><span data-stu-id="5f378-473">Confirm that the **copy behavior** is set to **Merge files**.</span></span> <span data-ttu-id="5f378-474">Se esiste già un file di output con lo stesso nome, il nuovo contenuto viene aggiunto alla fine dello stesso file.</span><span class="sxs-lookup"><span data-stu-id="5f378-474">If the output file with the same name already exists, the new content is added to the same file at the end.</span></span>
    12. <span data-ttu-id="5f378-475">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f378-475">Click **Next**.</span></span>
    <span data-ttu-id="5f378-476">![Strumento di copia - Scegliere il file o la cartella di output](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="5f378-477">Nella pagina **File format settings** (Impostazioni di formato file) rivedere le impostazioni e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f378-477">On the **File format settings** page, review the settings, and click **Next**.</span></span> <span data-ttu-id="5f378-478">Una delle opzioni aggiuntive ora consiste nell'aggiungere un'intestazione al file di output.</span><span class="sxs-lookup"><span data-stu-id="5f378-478">One of the additional options here is to add a header to the output file.</span></span> <span data-ttu-id="5f378-479">Se si seleziona tale opzione, viene aggiunta una riga di intestazione con i nomi delle colonne dalla schema dell'origine.</span><span class="sxs-lookup"><span data-stu-id="5f378-479">If you select that option, a header row is added with names of the columns from the schema of the source.</span></span> <span data-ttu-id="5f378-480">È possibile rinominare i nomi di colonna predefiniti quando si visualizza lo schema per l'origine.</span><span class="sxs-lookup"><span data-stu-id="5f378-480">You can rename the default column names when viewing the schema for the source.</span></span> <span data-ttu-id="5f378-481">È ad esempio possibile impostare la prima colonna su Nome e la seconda colonna su Cognome.</span><span class="sxs-lookup"><span data-stu-id="5f378-481">For example, you could change the first column to First Name and second column to Last Name.</span></span> <span data-ttu-id="5f378-482">Viene quindi generato il file di output con un'intestazione contenente questi nomi come nomi di colonna.</span><span class="sxs-lookup"><span data-stu-id="5f378-482">Then, the output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="5f378-483">![Strumento di copia - Impostazioni di formatto file per la destinazione](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="5f378-484">Nella pagina **Performance settings** (Impostazioni prestazioni) verificare che **cloud units** (Unità cloud) e **parallel copies** (Copie parallele) siano impostati su **Auto** e fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="5f378-484">On the **Performance settings** page, confirm that **cloud units** and **parallel copies** are set to **Auto**, and click Next.</span></span> <span data-ttu-id="5f378-485">Per informazioni dettagliate su queste impostazioni, vedere [Guida alle prestazioni dell'attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="5f378-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="5f378-486">![Strumento di copia - Impostazioni relative alle prestazioni](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="5f378-487">Nella pagina **Riepilogo** rivedere tutte le impostazioni (proprietà dell'attività, impostazioni per l'origine e la destinazione e impostazioni di copia) e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f378-487">On the **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="5f378-488">![Strumento di copia - Pagina Riepilogo](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="5f378-489">Verificare le informazioni nella pagina **Riepilogo** e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="5f378-489">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="5f378-490">La procedura guidata crea due servizi collegati, due set di dati (input e output) e una pipeline nella data factory da cui è stata avviata la Copia guidata.</span><span class="sxs-lookup"><span data-stu-id="5f378-490">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span>
    <span data-ttu-id="5f378-491">![Strumento di copia - Pagina di distribuzione](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-the-pipeline-copy-task"></a><span data-ttu-id="5f378-492">Monitorare la pipeline (attività di copia)</span><span class="sxs-lookup"><span data-stu-id="5f378-492">Monitor the pipeline (copy task)</span></span>

1. <span data-ttu-id="5f378-493">Fare clic sul collegamento `Click here to monitor copy pipeline` nella pagina **Distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="5f378-493">Click the link `Click here to monitor copy pipeline` on the **Deployment** page.</span></span> 
2. <span data-ttu-id="5f378-494">L'**applicazione Monitoraggio e gestione** verrà visualizzata in una scheda separata.  ![App Monitoraggio e gestione](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="5f378-494">You should see the **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="5f378-495">Impostare l'ora di **inizio** nella parte superiore su `04/19/2017` e l'ora di **fine** su `04/27/2017` e quindi fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="5f378-495">Change the **start** time at the top to `04/19/2017` and **end** time to `04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="5f378-496">Verranno visualizzate cinque finestre attività nell'elenco **ACTIVITY WINDOWS** (FINESTRE ATTIVITÀ).</span><span class="sxs-lookup"><span data-stu-id="5f378-496">You should see five activity windows in the **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="5f378-497">Gli orari indicati da **WindowStart** (Inizio finestra) devono coprire tutti i giorni dagli orari di inizio della pipeline a quelli di fine.</span><span class="sxs-lookup"><span data-stu-id="5f378-497">The **WindowStart** times should cover all days from pipeline start to pipeline end times.</span></span> 
5. <span data-ttu-id="5f378-498">Fare clic sul pulsante **Refresh** (Aggiorna) di **ACTIVITY WINDOWS** (FINESTRE ATTIVITÀ) alcune volte finché lo stato di tutte le finestre attività non risulta impostato su Ready (Pronto).</span><span class="sxs-lookup"><span data-stu-id="5f378-498">Click **Refresh** button for the **ACTIVITY WINDOWS** list a few times until you see the status of all the activity windows is set to Ready.</span></span> 
6. <span data-ttu-id="5f378-499">Verificare ora che i file di output vengano generati nella cartella di output del contenitore adfblobconnector.</span><span class="sxs-lookup"><span data-stu-id="5f378-499">Now, verify that the output files are generated in the output folder of adfblobconnector container.</span></span> <span data-ttu-id="5f378-500">Nella cartella di output verrà visualizzata la struttura di cartelle seguente:</span><span class="sxs-lookup"><span data-stu-id="5f378-500">You should see the following folder structure in the output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="5f378-501">Per informazioni dettagliate sul monitoraggio e la gestione delle data factory, vedere l'articolo [Monitorare e gestire le pipeline di Data Factory](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="5f378-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="5f378-502">Entità di Data factory</span><span class="sxs-lookup"><span data-stu-id="5f378-502">Data Factory entities</span></span>
<span data-ttu-id="5f378-503">Tornare ora alla scheda con la home page di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5f378-503">Now, switch back to the tab with the Data Factory home page.</span></span> <span data-ttu-id="5f378-504">Si noti che ora nella data factory sono presenti due servizi collegati, due set di dati e una pipeline.</span><span class="sxs-lookup"><span data-stu-id="5f378-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Home page di Data Factory con entità](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="5f378-506">Fare clic su **Creare e distribuire** per avviare l'editor di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5f378-506">Click **Author and deploy** to launch Data Factory Editor.</span></span> 

![Editor di Data factory](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="5f378-508">Nella data factory verranno visualizzate le entità di Data Factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="5f378-508">You should see the following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="5f378-509">Due servizi collegati,</span><span class="sxs-lookup"><span data-stu-id="5f378-509">Two linked services.</span></span> <span data-ttu-id="5f378-510">uno per l'origine e l'altro per la destinazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-510">One for the source and the other one for the destination.</span></span> <span data-ttu-id="5f378-511">Entrambi i servizi collegati fanno riferimento allo stesso account di archiviazione di Azure in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="5f378-511">Both the linked services refer to the same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="5f378-512">Due set di dati,</span><span class="sxs-lookup"><span data-stu-id="5f378-512">Two datasets.</span></span> <span data-ttu-id="5f378-513">uno di input e uno di output.</span><span class="sxs-lookup"><span data-stu-id="5f378-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="5f378-514">In questa procedura dettagliata entrambi usano lo stesso contenitore BLOB, ma fanno riferimento a cartelle diverse (input e output).</span><span class="sxs-lookup"><span data-stu-id="5f378-514">In this walkthrough, both use the same blob container but refer to different folders (input and output).</span></span>
 - <span data-ttu-id="5f378-515">Una pipeline.</span><span class="sxs-lookup"><span data-stu-id="5f378-515">A pipeline.</span></span> <span data-ttu-id="5f378-516">La pipeline contiene un'attività di copia che usa un'origine BLOB e un sink BLOB per copiare i dati da una posizione del BLOB di Azure a un'altra.</span><span class="sxs-lookup"><span data-stu-id="5f378-516">The pipeline contains a copy activity that uses a blob source and a blob sink to copy data from an Azure blob location to another Azure blob location.</span></span> 

<span data-ttu-id="5f378-517">Le sezioni seguenti offrono altre informazioni su queste entità.</span><span class="sxs-lookup"><span data-stu-id="5f378-517">The following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="5f378-518">Servizi collegati</span><span class="sxs-lookup"><span data-stu-id="5f378-518">Linked services</span></span>
<span data-ttu-id="5f378-519">Verranno visualizzati due servizi collegati,</span><span class="sxs-lookup"><span data-stu-id="5f378-519">You should see two linked services.</span></span> <span data-ttu-id="5f378-520">uno per l'origine e l'altro per la destinazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-520">One for the source and the other one for the destination.</span></span> <span data-ttu-id="5f378-521">In questa procedura dettagliata entrambe le definizioni sono uguali, fatta eccezione per i nomi.</span><span class="sxs-lookup"><span data-stu-id="5f378-521">In this walkthrough, both definitions look the same except for the names.</span></span> <span data-ttu-id="5f378-522">Il **tipo** del servizio collegato è impostato su **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="5f378-522">The **type** of the linked service is set to **AzureStorage**.</span></span> <span data-ttu-id="5f378-523">La proprietà più importante della definizione di un servizio collegato è **connectionString**, usata da Data Factory per connettersi all'account di archiviazione di Azure in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5f378-523">Most important property of the linked service definition is the **connectionString**, which is used by Data Factory to connect to your Azure Storage account at runtime.</span></span> <span data-ttu-id="5f378-524">Ignorare la proprietà hubName nella definizione.</span><span class="sxs-lookup"><span data-stu-id="5f378-524">Ignore the hubName property in the definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="5f378-525">Servizio collegato di archiviazione BLOB di origine</span><span class="sxs-lookup"><span data-stu-id="5f378-525">Source blob storage linked service</span></span>
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="5f378-526">Servizio collegato di archiviazione BLOB di destinazione</span><span class="sxs-lookup"><span data-stu-id="5f378-526">Destination blob storage linked service</span></span>

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

<span data-ttu-id="5f378-527">Per altre informazioni sui servizi collegati di archiviazione di Azure, vedere la sezione [Proprietà del servizio collegato](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="5f378-528">Set di dati</span><span class="sxs-lookup"><span data-stu-id="5f378-528">Datasets</span></span>
<span data-ttu-id="5f378-529">Sono presenti due set di dati, uno di input e uno di output.</span><span class="sxs-lookup"><span data-stu-id="5f378-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="5f378-530">Il tipo di set di dati è impostato su **AzureBlob** per entrambi.</span><span class="sxs-lookup"><span data-stu-id="5f378-530">The type of the dataset is set to **AzureBlob** for both.</span></span> 

<span data-ttu-id="5f378-531">Il set di dati di input punta alla cartella **input** del contenitore BLOB **adfblobconnector**.</span><span class="sxs-lookup"><span data-stu-id="5f378-531">The input dataset points to the **input** folder of the **adfblobconnector** blob container.</span></span> <span data-ttu-id="5f378-532">La proprietà **external** è impostata su **true** per questo set di dati perché i dati non vengono generati dalla pipeline con l'attività di copia che accetta questo set di dati come input.</span><span class="sxs-lookup"><span data-stu-id="5f378-532">The **external** property is set to **true** for this dataset as the data is not produced by the pipeline with the copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="5f378-533">Il set di dati di output punta alla cartella **output** dello stesso contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="5f378-533">The output dataset points to the **output** folder of the same blob container.</span></span> <span data-ttu-id="5f378-534">Il set di dati di output usa anche l'anno, il mese e il giorno della variabile di sistema **SliceStart** per valutare in modo dinamico il percorso del file di output.</span><span class="sxs-lookup"><span data-stu-id="5f378-534">The output dataset also uses the year, month, and day of the **SliceStart** system variable to dynamically evaluate the path for the output file.</span></span> <span data-ttu-id="5f378-535">Per un elenco di funzioni e variabili di sistema supportate da Data Factory, vedere l'articolo [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="5f378-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="5f378-536">La proprietà **external** è impostata su **false** (valore predefinito) perché questo set di dati viene generato dalla pipeline.</span><span class="sxs-lookup"><span data-stu-id="5f378-536">The **external** property is set to **false** (default value) because this dataset is produced by the pipeline.</span></span> 

<span data-ttu-id="5f378-537">Per altre informazioni sulle proprietà supportate dal set di dati del BLOB di Azure, vedere la sezione [Proprietà dei set di dati](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="5f378-538">Set di dati di input</span><span class="sxs-lookup"><span data-stu-id="5f378-538">Input dataset</span></span>

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a><span data-ttu-id="5f378-539">Set di dati di output</span><span class="sxs-lookup"><span data-stu-id="5f378-539">Output dataset</span></span>

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a><span data-ttu-id="5f378-540">Pipeline</span><span class="sxs-lookup"><span data-stu-id="5f378-540">Pipeline</span></span>
<span data-ttu-id="5f378-541">La pipeline ha una sola attività.</span><span class="sxs-lookup"><span data-stu-id="5f378-541">The pipeline has just one activity.</span></span> <span data-ttu-id="5f378-542">Il **tipo** dell'attività è impostato su **Copy**.</span><span class="sxs-lookup"><span data-stu-id="5f378-542">The **type** of the activity is set to **Copy**.</span></span>  <span data-ttu-id="5f378-543">Nelle proprietà del tipo dell'attività sono presenti due sezioni, una per l'origine e l'altra per il sink.</span><span class="sxs-lookup"><span data-stu-id="5f378-543">In the type properties for the activity, there are two sections, one for source and the other one for sink.</span></span> <span data-ttu-id="5f378-544">Il tipo dell'origine è impostato su **BlobSource** perché l'attività copia i dati da un archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="5f378-544">The source type is set to **BlobSource** as the activity is copying data from a blob storage.</span></span> <span data-ttu-id="5f378-545">Il tipo del sink è impostato su **BlobSink** perché l'attività copia i dati da un archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="5f378-545">The sink type is set to **BlobSink** as the activity copying data to a blob storage.</span></span> <span data-ttu-id="5f378-546">L'attività di copia accetta InputDataset-z4y come input e OutputDataset-z4y come output.</span><span class="sxs-lookup"><span data-stu-id="5f378-546">The copy activity takes InputDataset-z4y as the input and OutputDataset-z4y as the output.</span></span> 

<span data-ttu-id="5f378-547">Per altre informazioni sulle proprietà supportate da BlobSource e BlobSink, vedere la sezione [Proprietà dell'attività di copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-to-and-from-blob-storage"></a><span data-ttu-id="5f378-548">Esempi JSON per la copia dei dati da e verso un archivio BLOB</span><span class="sxs-lookup"><span data-stu-id="5f378-548">JSON examples for copying data to and from Blob Storage</span></span>  
<span data-ttu-id="5f378-549">Gli esempi seguenti forniscono le definizioni JSON di esempio da usare per creare una pipeline con il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5f378-549">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="5f378-550">Tali esempi mostrano come copiare dati da/in Archiviazione BLOB di Azure e Database SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-550">They show how to copy data to and from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="5f378-551">Tuttavia, i dati possono essere copiati **direttamente** da una delle origini in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-551">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-to-sql-database"></a><span data-ttu-id="5f378-552">Esempio JSON: Copiare dati da un archivio BLOB al database SQL</span><span class="sxs-lookup"><span data-stu-id="5f378-552">JSON Example: Copy data from Blob Storage to SQL Database</span></span>
<span data-ttu-id="5f378-553">L'esempio seguente mostra:</span><span class="sxs-lookup"><span data-stu-id="5f378-553">The following sample shows:</span></span>

1. <span data-ttu-id="5f378-554">Un servizio collegato di tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="5f378-555">Un servizio collegato di tipo [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="5f378-556">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="5f378-557">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="5f378-558">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](#copy-activity-properties) e [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5f378-559">L'esempio copia i dati di una serie temporale da un BLOB di Azure in una tabella di Azure SQL ogni ora.</span><span class="sxs-lookup"><span data-stu-id="5f378-559">The sample copies time-series data from an Azure blob to an Azure SQL table hourly.</span></span> <span data-ttu-id="5f378-560">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="5f378-560">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="5f378-561">**Servizio collegato SQL di Azure:**</span><span class="sxs-lookup"><span data-stu-id="5f378-561">**Azure SQL linked service:**</span></span>

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="5f378-562">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="5f378-562">**Azure Storage linked service:**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="5f378-563">Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="5f378-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="5f378-564">Per il primo specificare la stringa di connessione che include la chiave dell'account e per il secondo specificare l'URI di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="5f378-564">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="5f378-565">Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="5f378-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="5f378-566">**Set di dati di input del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="5f378-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="5f378-567">I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="5f378-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="5f378-568">Il percorso della cartella e il nome del file per il BLOB vengono valutati dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-568">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="5f378-569">Il percorso della cartella usa le parti anno, mese, e giorno dell'ora di inizio e il nome del file usa la parte dell'ora di inizio relativa all'ora.</span><span class="sxs-lookup"><span data-stu-id="5f378-569">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="5f378-570">L'impostazione di "external" su "true" comunica a Data Factory che la tabella è esterna alla data factory e non è prodotta da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="5f378-570">“external”: “true” setting informs Data Factory that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="5f378-571">**Set di dati di output SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="5f378-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="5f378-572">L'esempio copia i dati in una tabella denominata "MyTable" in un database SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5f378-572">The sample copies data to a table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="5f378-573">Creare la tabella nel database SQL di Azure con lo stesso numero di colonne di quelle previste nel file CSV del BLOB.</span><span class="sxs-lookup"><span data-stu-id="5f378-573">Create the table in your Azure SQL database with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="5f378-574">Alla tabella vengono aggiunte nuove righe ogni ora.</span><span class="sxs-lookup"><span data-stu-id="5f378-574">New rows are added to the table every hour.</span></span>

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="5f378-575">**Un'attività di copia in una pipeline con un'origine BLOB e un sink SQL:**</span><span class="sxs-lookup"><span data-stu-id="5f378-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="5f378-576">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="5f378-576">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="5f378-577">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **BlobSource** e il tipo **sink** è impostato su **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="5f378-577">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
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
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
### <a name="json-example-copy-data-from-azure-sql-to-azure-blob"></a><span data-ttu-id="5f378-578">Esempio JSON: Copiare i dati da SQL Azure al BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="5f378-578">JSON Example: Copy data from Azure SQL to Azure Blob</span></span>
<span data-ttu-id="5f378-579">L'esempio seguente mostra:</span><span class="sxs-lookup"><span data-stu-id="5f378-579">The following sample shows:</span></span>

1. <span data-ttu-id="5f378-580">Un servizio collegato di tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="5f378-581">Un servizio collegato di tipo [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="5f378-582">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="5f378-583">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="5f378-584">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) e [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5f378-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="5f378-585">L'esempio copia i dati di una serie temporale da una tabella di Azure SQL in un BLOB di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="5f378-585">The sample copies time-series data from an Azure SQL table to an Azure blob hourly.</span></span> <span data-ttu-id="5f378-586">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="5f378-586">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="5f378-587">**Servizio collegato SQL di Azure:**</span><span class="sxs-lookup"><span data-stu-id="5f378-587">**Azure SQL linked service:**</span></span>

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="5f378-588">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="5f378-588">**Azure Storage linked service:**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="5f378-589">Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="5f378-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="5f378-590">Per il primo specificare la stringa di connessione che include la chiave dell'account e per il secondo specificare l'URI di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="5f378-590">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="5f378-591">Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="5f378-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="5f378-592">**Set di dati di input SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="5f378-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="5f378-593">L'esempio presuppone che sia stata creata una tabella "MyTable" in SQL Azure e che contenga una colonna denominata "timestampcolumn" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="5f378-593">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="5f378-594">Impostando "external" su "true" si comunica al servizio Data Factory che la tabella è esterna alla data factory e non è prodotta da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="5f378-594">Setting “external”: ”true” informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="5f378-595">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="5f378-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="5f378-596">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="5f378-596">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="5f378-597">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="5f378-597">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="5f378-598">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="5f378-598">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="5f378-599">**Un'attività di copia in una pipeline con un'origine SQL e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="5f378-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="5f378-600">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="5f378-600">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="5f378-601">Nella definizione JSON della pipeline, il tipo **source** è impostato su **SqlSource** e il tipo **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="5f378-601">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="5f378-602">La query SQL specificata per la proprietà **SqlReaderQuery** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="5f378-602">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

> [!NOTE]
> <span data-ttu-id="5f378-603">Per eseguire il mapping dal set di dati di origine alle colonne del set di dati sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="5f378-603">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="5f378-604">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="5f378-604">Performance and Tuning</span></span>
<span data-ttu-id="5f378-605">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="5f378-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
